# Multi Containers App

This is a repo for new users getting started with Docker.

If you've already completed the How do I run a container? guide, you saw that you must start each container individually. Imagine how great it would be if a tool could start multiple containers with a single command. That tool is Docker Compose.


# Step 1 : Clone Sample Application

This is a repo for new users getting started with Docker.

Clone the repository at https://github.com/jasonMatilano/multi-container-app⁠.git

```git clone https://github.com/jasonMatilano/multi-container-app⁠.git```

# Step 2 : Understanding the sample application

This is a simple todo application built using ExpressJS and Node. All todos are saved in a MongoDB database.

# Step 3 : Digging into the compose.yaml file

If you view the code of the sample application, you will notice that it has a compose.yaml file. This file tells Docker how to run your application. Open the compose.yaml file in a text editor to explore the instructions.

# Step 4 : Running the Application

We are going to run this application with the docker compose up command in your project directory. This command builds and runs all the services listed in the compose file.

```
docker compose up -d
```

Breaking down the command
The -d flag tells docker compose to run in detached mode.
    
# Step 5 : View the frontend

In Docker Desktop, you should now have two containers running (the todo-app, and todo-database). To view the frontend, expand the app stack in Containers and select the link to localhost:3000⁠.

Add some tasks in the frontend, and then open the app in a new tab. Notice that the tasks are still visible.

And open http://localhost:3000 in your browser.

Having your configuration stored in a Compose file has another advantage, you can easily delete everything and restart.

# Step 6 : Delete and Restart

Simply select the app stack, and then select Delete on Docker Desktop. When you want to restart, run docker compose up in the project folder again. This will restart your application again. Note that when the db container is deleted, any todos created are also lost.

# Step 7 : Persist your data between containers

You just saw how to run multiple containers at the same time. However, when the db container was deleted and recreated you lost all the todos. Next you can learn how to persist data in the db container.

Docker isolates all content, code, and data in a container from your local filesystem. This means, that when you delete a container within Docker Desktop, all the content within it is deleted.

Sometimes you may want to persist data that a container generated. This is when you can use volumes.

# Step 8 : Using Volumes

If you want to persist data even after a container is deleted, you can use a volume. A volume is a location in your local filesystem, managed by Docker.

# Step 9 : Adding Volumes to Compose

To add a volume to this project, simply go to the compose.yaml file and uncomment the following lines:

```
todo-database:
    # ...
    volumes:
      - database:/data/db
                      
# ...
volumes:
  database:
```
Digging deeper

The volumes element that is nested in todo-database tells Compose to mount the volume named database to /data/db in the container for the todo-database service.

The top-level volumes element defines and configures a volume named database that can be used by any of the services in the Compose file.

Now, no matter how often you delete and restart the container, your data is persisted and accessible to any container on your system by mounting the database volume. Docker will check for a volume and create one if there is none present.