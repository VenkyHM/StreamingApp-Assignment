# I completed only 50-60 % of this assignment , still working on it and i will update the complete asssignment and remove this notification line . Since due date is over hence i am submitting the task. Later i will do some t/s and finish the task.


# StreamingApp

Stream premium video content, host live watch parties, and manage your catalogue with a modern microservice architecture. The platform now ships with a production-ready admin portal, real-time chat, S3-backed adaptive streaming, and a redesigned cinematic frontend experience.

## Architecture

----
<img width="982" height="657" alt="image" src="https://github.com/user-attachments/assets/ca6b9229-9402-40bb-8328-3c3b8938092a" />

----

## Environment Configuration

Create an `.env` for each service (or export variables before running). All services accept the standard AWS credentials for S3 access.

### Auth Service (`backend/authService/.env`)
```ini
PORT=3001
MONGO_URI=mongodb://localhost:27017/streamingapp
JWT_SECRET=changeme
CLIENT_URLS=http://localhost:3000
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=ap-south-1
AWS_S3_BUCKET=
```

### Streaming Service (`backend/streamingService/.env`)
```ini
PORT=3002
MONGO_URI=mongodb://localhost:27017/streamingapp
JWT_SECRET=changeme
CLIENT_URLS=http://localhost:3000
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=ap-south-1
AWS_S3_BUCKET=
AWS_CDN_URL=
STREAMING_PUBLIC_URL=http://localhost:3002
```

### Admin Service (`backend/adminService/.env`)
```ini
PORT=3003
MONGO_URI=mongodb://localhost:27017/streamingapp
JWT_SECRET=changeme
CLIENT_URLS=http://localhost:3000
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=ap-south-1
AWS_S3_BUCKET=
```

### Chat Service (`backend/chatService/.env`)
```ini
PORT=3004
MONGO_URI=mongodb://localhost:27017/streamingapp
JWT_SECRET=changeme
CLIENT_URLS=http://localhost:3000
```

### Frontend build variables (`frontend/.env` or Docker build args)
```ini
REACT_APP_AUTH_API_URL=http://localhost:3001/api
REACT_APP_STREAMING_API_URL=http://localhost:3002/api
REACT_APP_STREAMING_PUBLIC_URL=http://localhost:3002
REACT_APP_ADMIN_API_URL=http://localhost:3003/api/admin
REACT_APP_CHAT_API_URL=http://localhost:3004/api/chat
REACT_APP_CHAT_SOCKET_URL=http://localhost:3004
```

| Service | Port | Description |
| --- | --- | --- |
| `authService` | 3001 | User authentication, registration, JWT issuance |
| `streamingService` | 3002 | Video catalogue, S3 playback endpoints, public APIs |
| `adminService` | 3003 | Dedicated admin microservice for asset management and uploads |
| `chatService` | 3004 | Websocket + REST chat for live watch parties |
| `frontend` | 3000 | React SPA with revamped UI and integrated chat |
| `mongo` | 27017 | Shared MongoDB instance |

All backend services share common database models and utilities through `backend/common`.

## Testing on local 

##Frontend 
---
<img width="1906" height="984" alt="image" src="https://github.com/user-attachments/assets/7a4cb0b8-5da5-4571-b6d6-1c7bd4a7f113" />

----
## Backend services built steps

```bash
docker build -t admin-service .
docker build -t auth-service .
docker build -t chat-service .
docker build -t streaming-service .

docker run -d -p 3003:3003 --name admin-container admin-service
docker run -d -p 3001:3001 --name auth-container auth-service
docker run -d -p 3002:3002 --name streaming-container streaming-service
docker run -d -p 3004:3004 --name chat-container chat-service

````
-----

## Dockers Images 
---
<img width="834" height="278" alt="image" src="https://github.com/user-attachments/assets/793d42a7-2e32-4929-8cf5-9749f07906c4" />

----

## Docker Images pushed to ECR successfully

---
<img width="1914" height="904" alt="image" src="https://github.com/user-attachments/assets/bd1cb31c-7bfb-4815-8e85-f172ad6623e5" />

----
<img width="1308" height="413" alt="image" src="https://github.com/user-attachments/assets/4a90036b-3fb5-4615-9d42-ba18fdbffdaa" />

----

## All services are deployed successfully in kubernetes

---
<img width="1885" height="693" alt="image" src="https://github.com/user-attachments/assets/26fa757d-3a4c-47ff-9cca-c36a0ca2e92f" />


---
## Helm list

---
<img width="1466" height="118" alt="image" src="https://github.com/user-attachments/assets/4530410f-7aa6-48ea-92eb-7a8d964dba81" />

---














