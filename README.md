# Scaling

## Abstract: 
The idea is to create web applications, but it lacks resources on how to make your web app scalable so that it can accommodate thousands of users without having performance issues and making it fault-tolerant. 

## *Keywords* : 
Scaling , fault tolerance, server 

## Definition:
**Scalability is a feature that a web app needs to possess, it makes the app fault-tolerant, user experience smoother and the operations more efficient as the number of users grows.**

### A Simple Architecture

<div style='text-align:center'><img src="https://miro.medium.com/max/427/1*sG4nwmLYTi4-hpkDOubrsg.png" style="background-color:white"></div


- The diagram above shows a simple web architecture. It comuunication between client and database is done through a single server.

## Issues in a simple architecture

1. Single point of failure 

2. Web server overload

3. Expensive Queries

4. Distributing traffic

5. Possibility of database failure

6. Factoring out sessions


## 1. Single Point Of Failure

•	Since we are using a single server, we are unable to take any request if it goes down. This might happen due to many reasons.

•	Servers need to be stopped during maintenance

### Horizontal Scaling

<div style='text-align:center'><img src="https://miro.medium.com/max/277/1*zLAD8c2raZsTJgVurqSvaw.png" style="background-color:white"></div>

•	Horizontal scaling is cheaper in comparison to vertical scaling

•	Number of servers is increased instead of increasing the specifications.

•	Even if a few servers go down, the application will work.

## 2. Web Server Overload

- As the number of clients connecting to the server increases the load on the server increases. A server eventually runs out of resources like CPU, RAM, etc.

### Vertical Scaling

<div style='text-align:center'><img src="https://miro.medium.com/max/461/1*M-jKaJnspoL6mzsJf4Gzpw.png" style="background-color:white"></div>

•	Upgrading the server for meeting load requirements

•	Upgrading and buying high spec server is an expensive deal

•	Upgraded servers fail to meet load requirements as the number of users keeps increasing. Thus vertical scaling is a temporary fix.

## 3. Queries are expensive

•	If an application is handling millions of users then querying the database every time causes slowing down of the application.

•	We would first try to get the user from the cache, if the user exists then there is no need to query the database.

•	A Cache is used in this case.

 Sharding is another technique used to increase database efficiency



```
user = getUserFromCache(userId);
if (user == Null) {
    user = getUserFromDb(userId);
    
    setUserInCache(user);
}

```

## 4. Distributing Traffic

<div style='text-align:center'><img src="https://miro.medium.com/max/251/1*_8aMCj92o0ViI_GLH9CD4A.png" style="background-color:white"></div>

•	To evenly distribute traffic to all servers, load balancers are used.

•	2-3 load balancers are used to avoid bottlenecking or single-point failure.


## 5. Possibility of Database Failure

<div style='text-align:center'><img src="https://miro.medium.com/max/312/1*y0vFv9-dF3DL2Y4XbkDcMQ.png" style="background-color:white"></div>

•	We use multiple databases to avoid application failure due to the collapse of a single database.

•	Replication technique is used to make copies of every entry in master

•	Write, delete and edit is done in master while Read operation is handled by slaves 

•	Databases share master slave relationship


## 6. Factoring out sessions

<div style='text-align:center'><img src="https://miro.medium.com/max/632/1*r7MB6iZICOuu6o_6Zn6ujg.png" style="background-color:white"></div>

•	If a user is logged in load balancer might direct him to server 1 and a different server during his second request where the user will have to login again.

•	To solve this, the user's sessions are uncoupled to a Redis server.

  

<div style='text-align:center'><img src="https://miro.medium.com/max/461/1*M-jKaJnspoL6mzsJf4Gzpw.png" style="background-color:white"></div>

•	Upgrading the server for meeting load requirements

•	Upgrading and buying high spec server is an expensive deal

•	Upgraded servers fail to meet load requirements as the number of users keeps increasing. Thus vertical scaling is a temporary fix.


## Conclusion
Terms and technologies explained to give an idea of a better design architecture for large-scale systems.

## Reference Links

- https://www.netguru.com/blog/how-to-effectively-scale-your-web-application

- <https://medium.com/@harithjaved/scaling-your-web-application-693657ce333c>

- https://www.youtube.com/watch?v=sHPVVdITpwc&t=593s
