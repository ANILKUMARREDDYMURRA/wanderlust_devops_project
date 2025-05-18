#Building frontend image using multi-stage docker build

# Stage 1: Using the original base image to install dependencies

FROM node:21 AS frontend-builder

#set the working directory

WORKDIR /app

#copy the package.json and package-lock.json files to the working directory

COPY package*.json .

#install the dependencies
RUN npm i

#copy the rest of the application code to the working directory
COPY . .

#Stage 2: Build the application

FROM node:21-slim 

#Set the working directory

WORKDIR /app

#Copy the build files from the previous stage
COPY --from=frontend-builder /app .

#Copy the .env.docker file to .env

COPY .env.docker .env

#Expose the port on which the application will run
EXPOSE 5173

#Define the command to run the application in Development mode
CMD ["npm", "run", "dev", "--", "--host"]