# LAB - Introduction to Containers

If running on Linux, you may need to run the docker commands as root:

``` bash
sudo -i
```

> **_NOTE:_** Ensure that the local ports mapped to containers are not already in use.

### Exercise 1:

``` bash
docker pull tutum/wordpress
docker images
docker run -d -p 80:80 tutum/wordpress
docker ps
docker run -d -p 8080:80 tutum/wordpress
docker run -d -p 9090:80 tutum/wordpress 
docker ps
docker run --name mycontainer1 -d -p 8081:80 tutum/wordpress
docker ps
```

### Exercise 2:

``` bash
docker ps
docker stop <<CONTAINER-ID>>
docker ps -a
docker start <<CONTAINER-ID>>
docker ps
docker rm -f <<CONTAINER-ID>>
docker stop $(docker ps -aq)
docker images
docker rmi <<IMAGE ID>> -f
docker images
```

### Exercise 3:

1. nodejs

``` bash
cd nodejs
ls
code Dockerfile
docker build -t mynodejs .
docker images
docker run -d -p 8080:8080 mynodejs
```

2. nginx

``` bash
cd nginx
code Dockerfile
docker build -t mynginx .
docker history mynginx
docker images
docker run -d -p 80:80 mynginx
```

3. ASP.NET Core 3.x

``` bash
cd aspnetcore
code Dockerfile
dotnet publish -o published
docker build -t myaspcoreapp:3.1 . 
docker run -d -p 8090:80 myaspcoreapp:3.1
```

### Exercise 4:

``` bash
docker ps 
docker exec -it <<CONTAINER ID OR NAME>> bash
ls
apt-get update
apt-get install code
code server.js
exit
docker stop <<CONTAINER ID>> 
docker start <<CONTAINER ID>>
docker commit <<CONTAINER ID>> mynodejsv2
docker images
docker run -d -p 8081:8080 mynodejsv2
```

### Exercise 5:

``` bash
docker tag <<IMAGE ID or IMAGE NAME>> mynodejs:v1
docker images
cd nginx
docker build -t nginxsample:v1 .
docker images
```

### Exercise 6:

``` bash
cd sqlserver2017
docker rm $(docker ps -aq) -f
cat Dockerfile
docker build -t mysqlserver .
docker run -e ACCEPT_EULA=Y -e SA_PASSWORD=AAAbbb12345!@#$% -d -p 1433:1433 --name mydb mysqlserver
docker logs mydb -f
docker exec -it mydb /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P AAAbbb12345!@#$%
SELECT name FROM master.dbo.sysdatabases
GO
USE LabData
SELECT * FROM Users
GO
exit
```

``` bash
cd aspnetcorewithsqlserver
docker inspect mydb
code Startup.cs # update the connection string to use the SQL container IP Address 
dotnet build  
dotnet publish -o published  
docker build -t myaspcoreapp:3.1-withsql .  
docker run -d -p 8082:80 --name myapp myaspcoreapp:3.1-withsql
docker logs myapp -f
# navigate to http://localhost:8082
docker rm $(docker ps -aq) -f
```



