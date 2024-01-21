# Notes

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

