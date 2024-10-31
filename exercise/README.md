<h1>
  <span class="headline">Building a Node.js Docker Container Lab</span>
  <span class="subhead">Exercise</span>
</h1>

# Building and Dockerizing a Node.js API

In this lab, you will create a simple Node.js API using Express, test it locally, and then package it in a Docker container for easy deployment. By the end, you will have a Docker image of your application that can be deployed on any machine.

## Step 1: Set Up the Project Directory

1. **Create a directory** for the project:

   - Open a terminal, navigate to your Desktop, and run the following command to create a new folder called `hello-node`:

     ```bash
     mkdir hello-node
     cd hello-node
     ```

## Step 2: Initialize the Project with `package.json`

1. **Generate a `package.json` file**:

   - Inside the `hello-node` directory, initialize your project with npm:

     ```bash
     npm init -y
     ```

   - This command creates a `package.json` file, which tracks the dependencies and scripts for your Node.js project.

## Step 3: Install Express.js

1. **Install Express**:

   - Express is a Node.js framework for handling HTTP requests and responses, ideal for building APIs.
   - Install it as a dependency by running:

     ```bash
     npm install express
     ```

2. **Check `package.json`**:

   - After installation, your `package.json` file should look similar to this:

     ```json
     {
       "name": "hello-node",
       "version": "1.0.0",
       "description": "",
       "main": "index.js",
       "scripts": {
         "test": "echo \"Error: no test specified\" && exit 1"
       },
       "author": "",
       "license": "ISC",
       "dependencies": {
         "express": "^4.17.1"
       }
     }
     ```

   - The `dependencies` section now includes Express.

## Step 4: Create a Basic Server with Express

1. **Create an `index.js` file**:

   - In the `hello-node` directory, create a file named `index.js` and open it in your code editor.

2. **Add a basic Express server**:

   - Copy the following code into `index.js` to create a simple server that responds to requests on the root URL `'/'`:

     ```js
     const express = require('express');
     const app = express();
     const port = 3000;

     app.get('/', (req, res) => {
       res.send('Hello World!');
     });

     app.listen(port, () => {
       console.log(`Example app listening at http://localhost:${port}`);
     });
     ```

3. **Add a Start Script**:

   - To make it easy to run the server, add a `"start": "node index.js"` script to the `package.json` file under `"scripts"`. Your full `package.json` should now look like this:

     ```json
     {
       "name": "hello-node",
       "version": "1.0.0",
       "description": "",
       "main": "index.js",
       "scripts": {
         "test": "echo \"Error: no test specified\" && exit 1",
         "start": "node index.js"
       },
       "author": "",
       "license": "ISC",
       "dependencies": {
         "express": "^4.17.1"
       }
     }
     ```

4. **Run the Application Locally**:

   - In the terminal, run the server:

     ```bash
     npm start
     ```

   - You should see a message indicating the server is listening on port **3000**.
   - Open your browser and go to [`http://localhost:3000`](http://localhost:3000). You should see the message "Hello World!"

## Step 5: Dockerize the Application

Now that we have a working application, let’s package it into a Docker container.

1. **Create a `Dockerfile`**:

   - In the `hello-node` directory, create a file named `Dockerfile`.

2. **Define the Dockerfile Instructions**:

   - Add the following content to the `Dockerfile` to specify how to build and run the application in Docker:

     ```yml
     FROM node:16-alpine # Use a lightweight Node.js image
     COPY . . # Copy project files into the container
     RUN npm install # Install project dependencies
     CMD ["node", "index.js"] # Start the application
     ```

3. **Clean Up Local Dependencies**:

   - Since Docker will install the dependencies inside the container, delete the `node_modules` folder on your machine to ensure the app only relies on Docker for dependencies:

     ```bash
     rm -rf node_modules
     ```

4. **Build the Docker Image**:

   - In the terminal, build the Docker image. The `-t` flag lets you name the image (in this case, `hello-node`):

     ```bash
     docker build -t hello-node .
     ```

5. **Verify the Docker Image**:

   - Run `docker images` to confirm that the `hello-node` image was created.

     ```bash
     docker images
     ```

6. **Run the Docker Container**:

   - Start the container with the following command, mapping port 3000 on your machine to port 3000 in the container:

     ```bash
     docker run -dp 3000:3000 hello-node
     ```

   - Open your browser again and go to [`http://localhost:3000`](http://localhost:3000). You should see **"Hello World!"** served from the containerized application.

## Step 6 (Optional): Push the Docker Image to Docker Hub

To share your Docker image, you can push it to Docker Hub.

1. **Log in to Docker Hub**:

   - Make sure you have a Docker Hub account. Log in through the terminal:

     ```bash
     docker login
     ```

2. **Tag the Image for Docker Hub**:

   - Rebuild the image with a tag that includes your Docker Hub username. Replace `<dockerid>` with your Docker Hub username:

     ```bash
     docker build -t <dockerid>/hello-node .
     ```

3. **Push the Image**:

   - Push the image to Docker Hub:

     ```bash
     docker image push <dockerid>/hello-node
     ```

   - Your Docker image is now available on Docker Hub and can be pulled by others.

## Conclusion

Congratulations! You have created a Node.js application, dockerized it, and shared it using Docker. Now, the app is ready to run on any machine with Docker installed.
