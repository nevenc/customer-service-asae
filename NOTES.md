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

