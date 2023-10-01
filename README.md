# munnybunny-webserver
A front end for MunnyBunny (An expense tracker) 

https://datadude.dev/wp-content/uploads/2023/10/00002-2207509569.png

Features:

@ List and Display expenses in a neat ASCII table
@ Add new expenses, and remove existing ones
@ Attach and download photos and documents to new and existing expenses inline
@ Displays expenses with existing document attachments
@ A simple API relays commands to the MunnyBunny-webServer


Docker Installation: 

Docker Compose is the preferred method of installation.  
My docker repo is private, but you can close the git repo and compile the image  
locally with the following commands: 

```
git clone https://github.com/DatadudeDev/munnybunny-webserver.git
cd ./munnybunny-webserver
docker build -t munnybunny-webserver:latest .
```

When you've built the images for both the server and the webserver, you can use  
the below docker compose template to spin up the containers in a stack (important  
for networking) 

```
version: '2'
services:
  budget:
    image: munnybunny-server:latest
    restart: unless-stopped
    volumes:
      - server:/app/
    ports:
      - 81:5050 # you can change port 81 to whatever you want
    networks:
      - my_network

  webserver:
    image: munnybunny-webserver:latest
    restart: unless-stopped
    volumes:
      - webserver:/app/
    ports:
      - 80:8050  # you can change port 80 to whatever you want
    networks:
      - my_network

networks:
  my_network:
    driver: bridge

volumes:
  server:
  webserver:

```

Navigate to your LAN IP:PORT (80 or whatever you picked) to access the web GUI. 

Enjoy! 
