## What is this project?
This project was created to help me learn docker, by containerizing a full stack 'goals' application
downloaded from a udemy course.

## How can I run it?
Ideally you would run this using docker compose, which I will add support for in the near future. For
now you can clone this repository, then run each of the containers individually by executing the below commands in the root directory of the project.

### Network
<ol>
<li>Create a network for the backend and database to communicate with each other on: docker network create goals-network</li>
</ol>

### Database
<ol>
<li>Add values for DB_PASSWORD and DB_USERNAME within the .env file in the backend directory</li>
<li>Start the docker container for the database (Note: Replace username_here and password_here with the values you chose for these fields in the .env file): docker run --name goals-mongodb -v goals-mongo-volume:/data/db --network goals-network -e MONGO_INITDB_ROOT_USERNAME=username_here -e MONGO_INITDB_ROOT_PASSWORD=password_here mongo</li>
</ol>

### Backend
<ol>
<li>Build the docker image for the backend: docker build -t goals-backend ./backend</li>
<li>Start the docker container for the backend (Note: You need to replace 'absolute_path_to_project_root' with the absolute file path to your projects root): docker run -p 80:80 --name goals-backend -v "absolute_path_to_project_root/backend:/app" -v /app/node_modules -v goals-logs:/app/logs --network goals-network --env-file ./backend/.env goals-backend</li>
</ol>

### Frontend
<ol>
<li>Build the docker image for the frontend: docker build -t goals-frontend ./frontend</li>
<li>Start the docker container for the frontend (Note: You need to replace absolute path same as above): docker run -p 3000:3000 --name goals-frontend -v "absolute_path_to_project_root/frontend/src:/app/src" -v /app/node_modules goals-frontend</li>
</ol>





