# Oracle Database Docker Image Setup Guide

This guide explains how to build and run Oracle Database 19c in Docker.

## Option 1: Using Pre-built Image

Pull the pre-built Oracle 19.3.0 Enterprise Edition x64 image:
```bash
docker pull khushaalan/oracle-19.3.0-ee-x64
```

## Option 2: Building from Scratch

### Prerequisites
1. Download Oracle Database zip files from:
   - [Oracle Database Software Downloads](https://www.oracle.com/my/database/technologies/oracle-database-software-downloads.html)
   - Or use existing zip files from the repository's zips folder (x64 or ARM architecture)

### Build Steps
1. Clone the repository:
```bash
git clone https://github.com/khushaalan/docker-images
```

2. Navigate to the dockerfiles directory:
```bash
cd OracleDatabase/SingleInstance/dockerfiles
```

3. Copy the downloaded zip file to the appropriate version directory (e.g., 19.3.0)

4. Build the container image:
```bash
./buildContainerImage.sh -v 19.3.0 -e
```

### Push to Docker Hub (Optional)
```bash
docker login
docker tag oracle/database <username>/oracle-19.3.0-ee-x64
docker push <username>/oracle-19.3.0-ee-x64
```

## Running the Container

Start the container (using port 1521):
```bash
docker run -d --name oracle19 -e ORACLE_PWD=OracleHomeUser1 -p 1521:1521 oracle/database:19.3.0-ee
```

Alternative port (if 1521 is in use):
```bash
docker run -d --name oracle19 -e ORACLE_PWD=OracleHomeUser1 -p 1522:1521 oracle/database:19.3.0-ee
```

Check container status:
```bash
docker ps
```

## Database Connection Details

Use these credentials in SQL Developer or VS Code:
- Host: localhost
- Service name/SID: orclcdb
- Port: 1521
- Username: SYSTEM
- Password: OracleHomeUser1
- Role: Default
