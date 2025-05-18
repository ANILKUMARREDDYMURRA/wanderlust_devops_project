#Building the backend image by multi-stage docker builds


#Stage1

#Using the original base image to install the dependencies
FROM node:21 AS backend-builder

#setting up the working directory in the container
WORKDIR /app

#Copying the all the files from the current local directory to the working directory in the container
COPY . .

#Installing the dependencies which are mentioned in the package.json and package-lock.json file
RUN npm i

#Runs the tests to ensure that the code is working as expected
RUN npm run test



#Stage2

#Using the base image that takes less resources to run the application

FROM node:21-slim

#setting up the working directory in the container
WORKDIR /app

#Copying the files from the previous stage to the current stage
COPY --from=backend-builder /app .

#Copying the .env file to the current stage

COPY .env.docker .env

EXPOSE 8080

CMD ["npm","start"]
