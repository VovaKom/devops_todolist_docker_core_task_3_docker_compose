# Django-Todolist (instructions)

Here are the instructions on how to run and stop containers with docker-compose.

## Requirments
Before running the project, make sure you have installed:
- Docker (version 20+)
- Docker Compose (v1: docker-compose or v2: docker compose)

Check installation:
```bash
docker --version
docker compose version
```

or
```bash
docker-compose --version
```

## Clone the repository
```bash
git clone https://github.com/mate-academy/devops_todolist_docker_core_task_3_docker_compose.git
cd devops_todolist_docker_core_task_3_docker_compose
```

## Run the project
Build and start containers:
```bash
docker-compose up --build
```

or (Compose v2):
```bash
docker compose up --build
```

Run in detached mode:
```bash
docker-compose up -d --build
```

## Stop the project
Stop containers:
```bash
docker-compose down
```

Stop containers and remove volumes (full DB reset):
```bash
docker-compose down -v
```

## Access the application
After startup, the application is available at:
> Web UI:
> http://localhost:8081

> Admin panel:
> http://localhost:8081/admin

> API:
> http://localhost:8081/api/

## View containers and access them
List running containers:
```bash
docker ps
```
You should see:
- app
- mysql

## Enter the app container
```bash
docker-compose exec app sh
```

## Connect to MySQL database
Connect to MySQL container:
```bash
docker-compose exec db mysql -u app_user -p

Password:
1234
```

Or connect as root:
```bash
docker-compose exec db mysql -u root -p

Password:
root_1234
```

## Check database structure
After connecting to MySQL:
```sql
USE app_db;
```

Show tables:
```sql
SHOW TABLES;
```

View records:
```sql
SELECT * FROM <your_table_name>;
```

## Create a test record via SQL
Example (replace table name if needed):
```sql
INSERT INTO <your_table_name> (title, description, is_completed)
VALUES ('Test task', 'Created manually from MySQL', 0);
```

## Create superuser (for Django admin)
Enter app container:
```bash
docker-compose exec app sh
```

Create admin user:
```bash
python manage.py createsuperuser
```

Then login at:
> http://localhost:8081/admin

## View logs
All logs:
```bash
docker-compose logs
```

Logs for specific service:
```bash
docker-compose logs app
docker-compose logs db
```

## Full cleanup
```bash
docker-compose down -v
docker system prune -f
```

(This removes containers, volumes and unused Docker resources)