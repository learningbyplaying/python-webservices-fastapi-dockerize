

# Dockerized FastApi Hello World Application

```
.
├── Dockerfile
├── docker-compose.yml
├── main.py
└── requirements.txt
```

# Requirements.txt

The requirements.txt file is used to specify the Python packages that are required for the application to run. This file is used by the Dockerfile to install the necessary packages when the container is built.

The following packages are required for the FastAPI Hello World application:

```
fastapi
uvicorn
```

These packages can be installed using the pip package manager. The following command can be used to install the packages:

```
pip install -r requirements.txt
```

The requirements.txt file should be placed in the same directory as the main.py file. This will ensure that the packages are installed when the container is built.

### main.py

This file contains the code for the FastAPI application. It is responsible for creating the API endpoints and handling the requests.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}
```

The code above creates a FastAPI application and adds a single endpoint to it. The endpoint is accessible at the root URL (`/`) and returns a JSON object with the message `{"Hello": "World"}`.

### Dockerfile

The Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. It is used to create a Docker image, which is a snapshot of a container.

The Dockerfile for this FastApi Hello World application is as follows:

```
FROM python:3.7

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 80

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]
```

This Dockerfile will create an image based on the Python 3.7 image. It will then copy the requirements.txt file into the image, install the dependencies, copy the application files, expose port 80, and then run the application.

### docker-compose.yml

The docker-compose.yml file is used to define and run multi-container Docker applications. This file is used to define the services that make up the application, the networks they belong to, and the volumes they use.

The following code is an example of a docker-compose.yml file for a FastApi Hello World application:

```
version: '3'

services:
  web:
    build: .
    ports:
      - "8080:8080"
    volumes:
      - .:/app
    environment:
      - PORT=8080
```

In this example, the `web` service is defined. This service will build the application from the current directory, map port 8080 on the host to port 8080 on the container, mount the current directory to the `/app` directory in the container, and set the `PORT` environment variable to `8080`.