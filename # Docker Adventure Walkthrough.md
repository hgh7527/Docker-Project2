# Docker Adventure Walkthrough
## In terminal 
### ssh into 10.10.1.116
### I chose Wordpress
Open your operating system’s preferred command line interface and check the Docker Compose Installation version:
```bash
docker compose -version
```
This will confirm that the Compose module is working correctly.
Create a new project directory for WordPress application with the following command:
```bash
mkdir wordpress
```
Navigate to the new directory:
```bash
cd wordpress
```
Create a new ***docker-compose.yml file***, and add the contents below:
```bash 
version: "3" 
# Defines which compose version to use
services:
# Services line define which Docker images to run. In this case, it will be MySQL server and WordPress image.
  db:
    image: mysql:5.7
# image: mysql:5.7 indicates the MySQL database container image from Docker Hub used in this installation.
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: MyR00tMySQLPa$$5w0rD
      MYSQL_DATABASE: MyWordPressDatabaseName
      MYSQL_USER: MyWordPressUser
      MYSQL_PASSWORD: Pa$$5w0rD
# Previous four lines define the main variables needed for the MySQL container to work: database, database username, database user password, and the MySQL root password.
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    restart: always
# Restart line controls the restart mode, meaning if the container stops running for any reason, it will restart the process immediately.
    ports:
      - "8000:80"
# The previous line defines the port that the WordPress container will use. After successful installation, the full path will look like this: http://localhost:8000
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: MyWordPressUser
      WORDPRESS_DB_PASSWORD: Pa$$5w0rD
      WORDPRESS_DB_NAME: MyWordPressDatabaseName
# Similar to MySQL image variables, the last four lines define the main variables needed for the WordPress container to work properly with the MySQL container.
    volumes:
      ["./:/var/www/html"]
volumes:
  mysql: {}
```
Then run the file, to start the containers:
```bash
docker compose up -d
```
## You Are Done
Screen shots on github linked below.
Guide that helped me:
    https://www.hostinger.com/tutorials/run-docker-wordpress