# Using official and latest dotnet/core/sdk base image based on Linux Alpine
FROM mcr.microsoft.com/dotnet/core/sdk:2.2.402-alpine3.9

# Set the application directory
RUN mkdir -p /code
WORKDIR /code

# Copy our code from the current src folder to /code/src/Worker inside the container
COPY src/Worker /code/src/Worker

# Install our dotnet dependencies
RUN dotnet restore -v minimal src/Worker \
    && dotnet publish -c Release -o "./" "src/Worker/" 

# Define our default command to be run when launching the container
ENTRYPOINT [ "dotnet" ]
CMD [ "src/Worker/Worker.dll" ]