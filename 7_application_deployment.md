# Build and Deploy the Artifact

Beanstalk Health Status is showing Severe because we changed the health check to /login and not able to load yet the application at that path.

After deploying the artifact, it will change back to normal.


1. On the local machine, clone the source code repository.


```
mkdir /f/aws-refactor


git clone https://github.com/hkhcoder/vprofile-project


vprofile-project/src/main/resources/application.properties
```


Inside the artifact, there is application.properties


```
Q#JDBC Configutation for Database Connection
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://RDS_ENDPOINT:3306/accounts?useUnicode=true&characterEncoding=UTF-8&zeroDateTimeBehavior=convertToNull
jdbc.username=admin
jdbc.password=Auto_Generated_Password

#Memcached Configuration For Active and StandBy Host
#For Active Host
memcached.active.host=Active_MQ_ENDPOINT
memcached.active.port=11211
#For StandBy Host
memcached.standBy.host=127.0.0.2
memcached.standBy.port=11211

#RabbitMq Configuration
rabbitmq.address=Rabbit_MQ_ENDPOINT
rabbitmq.port=5671
rabbitmq.username=rabbit
rabbitmq.password=Auto_Generated_Password

```


2. Get the endponits for RDS, Memcached and ActiveMQ and replace with the place holders (RDS_ENDPOING, Auto_generated_Password, Active_MQ_ENDPOINT, Rabbit_MQ_ENDPOINT) respectively

3. Build the artifact in the git clone directory.
```
mvn -version
mvn install
```
4. After that, the artifact file is created in the target directory

5. Upload the artifact file to Beanstalk

	**Beanstalk>Environments > Upload and Deploy> Choose the artifact file**

	Version Label: vprofile-app-v2.5

	image

6. After deploying, check Beanstalk events

7. Load Beanstalk URL and Web App page will show up, but it will still show insecure.

   The reason for this that SSL cerfificate is only configured for vprofile.minpyae.xyz
   
   Let's configure DNS in the next step.
   
   