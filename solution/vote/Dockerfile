# Using official and latest python runtime base image based in Linux Alpine
FROM python:2.7.16-alpine3.10

# Specify a service user/group name
ENV SVC_USER=gunicorn-svc-user
ENV SVC_GROUP=gunicorn-svc-group

# Set the application directory
RUN mkdir -p /app
WORKDIR /app

# Install our python dependencies
COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt

# Copy our code from the current folder to /app inside the container
COPY . /app

# Create a service user
RUN addgroup -S ${SVC_GROUP} && \
    adduser -S ${SVC_USER} -G ${SVC_GROUP} --no-create-home --uid 1000 --shell /sbin/nologin

# Permit the service user to access the /app directory
RUN chown -R ${SVC_USER}:${SVC_GROUP} /app

# Make port 8080 available for links and/or publish
EXPOSE 8080

# Define our default command to be run when launching the container
ENTRYPOINT sh -c "gunicorn app:app -b 0.0.0.0:8080 --user ${SVC_USER} --group ${SVC_GROUP} --log-file - --access-logfile - --workers 4 --keep-alive 0"
