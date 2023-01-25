# Dockerfile walkthrough

[Creating your docker image](https://docs.docker.com/build/building/packaging/)

Create an empty directory 

Create the dockerfile and name it ```Dockerfile``` with no extension

```dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:22.04

# install app dependencies
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip install flask==2.1.*

# install app
COPY hello.py /

# final configuration
ENV FLASK_APP=hello
EXPOSE 8000
CMD flask run --host 0.0.0.0 --port 8000
```

Create ```hello.py``` in the directory created above

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"
```

Now, build your Docker image with the following:

```dockerfile
docker build -t test:latest .
```

You should now see your new imaged named ```test``` appear under images in **Docker desktop** or by running ```docker images```

Test the image by running

```docker run -p 8000:8000 test:latest```
