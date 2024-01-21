# Workshop Notes

- Added Customer entity (using Lombok to save some time in the demo)
- Added CustomerRepository interface extending JpaRepository
- Can test the application with

```
./mvnw spring-boot:run
http localhost:8080/customers
http localhost:8080/customers name="John Doe" email="john.doe@email.com"
http localhost:8080/customers name="Jane Doe" email="jane.doe@email.com"
http DELETE localhost:8080/customers/1
```
- Can create the application placeholder on Azure Spring Apps with

```
az spring app create -n customer-service --assign-endpoint --cpu 1 --memory 1Gi
```

- Can deploy the application to Azure Spring Apps with 

```
az spring app deploy --name customer-service --source-path .  --build-env BP_JVM_VERSION=17
```
  - Note that Java Buildpack supports up to Java 17.

- Can test the application in `production` with

```
http https://production-customer-service.azuremicroservices.io/customers
http https://production-customer-service.azuremicroservices.io/customers name="Jill Doe" email="jill.doe@email.com"
http https://production-customer-service.azuremicroservices.io/customers
```

- You can create a new PostgreSQL flexible-server by

```
az postgres flexible-server create \
  --resource-group ${RESOURCE_GROUP} \
  --location ${REGION} \
  --name ${DATABASE_SERVER} \
  --admin-user ${DATABASE_USER} \
  --admin-password ${DATABASE_PASSWORD} \
  --sku-name Standard_B1ms \
  --tier Burstable \
  --storage-size 32 
  --yes
```

- We can create a database in PostgreSQL server by

```
az postgres flexible-server db create \
  --database-name ${DATABASE_NAME} \
  --server-name ${DATABASE_SERVER}
```

- We can create an application connection to PostgreSQL database by

```
az spring connection create postgres-flexible \
  --app customer-service \
  --server ${DATABASE_SERVER} \
  --secret name=${DATABASE_USER} secret="${DATABASE_PASSWORD}" \
  --resource-group ${RESOURCE_GROUP} \
  --service ${SPRING_APPS_SERVICE} \
  --target-resource-group ${RESOURCE_GROUP} \
  --database ${DATABASE_NAME} \
  --client-type=springBoot \
  --connection customer_database_connection \

```

- We need to restart the application by

```
az spring app stop --name customer-service
az spring app start --name customer-service
```

- We can observe the logs by

```
az spring app logs --name customer-service -f
```
