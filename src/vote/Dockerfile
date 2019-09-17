# Using official python runtime base image
# TODO: Find the latest official Python 2.7 Docker image (based on Linux Alpine 3.10) tag and use it in your FROM instruction. Format: FROM <imagename>:<tagname>
...

# Allow to specify the service user/group during the Docker image build
# Use "gunicorn-svc-*" as default if build ARG is used.
ARG SVC_USER
ENV SVC_USER=${SVC_USER:-gunicorn-svc-user}
ARG SVC_GROUP
ENV SVC_GROUP=${SVC_GROUP:-gunicorn-svc-group}

# Set the application directory
# TODO: Create an working directory ("/app") inside the image where the applicaiton files can be copied to. In Linux you can create a directory by using "mkdir -p /diectory/to/create".
...
# TODO: Switch the context to the WORKDIR /app.
...

# Install our python dependencies
# TODO: Python projects usually store dependency libraries inside an "requirements.txt" file. Thats also the case in this project. Copy this file to "/app/requirements.txt".
...
# TODO: Install the Python dependencies by running "pip install -r requirements.txt".
...

# Copy our code from the current folder to /app inside the container
COPY . /app

# Create a service user
# TODO: Do not allow this service user to login. Usually this can be achieved by assigning the user the shell "/sbin/nologin".
RUN addgroup -S $SVC_GROUP && \
    adduser -S $SVC_USER -G SVC_GROUP --no-create-home --uid 1000 --shell

# Permit the service user to access the /app directory
RUN chown -R $SVC_USER:$SVC_GROUP /app

# Make port 80 available for links and/or publish
# TODO: Expose port 80 so other persons know on this port this Docker service listens on.
...

# Define our default command to be run when launching the container
ENTRYPOINT [ "gunicorn" ]
CMD [ "app:app", "-b", "0.0.0.0:80", "--user", "${SVC_USER}", "--group", "${SVC_GROUP}", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0" ]