# docker_aci_app_ro

# Create a directory to work in
mkdir flask-aci
cd flask-aci

# clone git repository
git clone https://github.com/smedeyinlo/aci_app_ro.git

# edit the apics list
nano aci_app_ro/apics.txt

# (Optionally) edit the flask port (default 8080)
nano aci_app_ro/oneaciapp.py
- Ctrl + W to search for 8080 or go to the bottom of the file

# create Dockerfile
nano Dockerfile

FROM ubuntu:18.04
RUN apt-get update -y
RUN apt-get install -y apt-utils
RUN apt-get install -y python-pip
RUN apt-get install -y python-dev build-essential
COPY aci_app_ro /aci_app_ro
WORKDIR /aci_app_ro
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["oneaciapp.py"]

# build the container
docker build -t aci_app_ro:latest

# run the container 
docker run -d -p 8080:8080 aci_app_ro:latest
