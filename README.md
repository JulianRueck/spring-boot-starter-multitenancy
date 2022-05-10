# Introduction
This starter provides an application with multitenancy.
It currently provides a database per tenant / schema per tenant solution.
A Shared Schema solution is currently under development.

# Installation
### Add the following dependency to the pom.xml file
```
<dependency>
    <groupId>io.github.julianrueck</groupId>
    <artifactId>spring-boot-starter-multitenancy</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>
```
# Settings
The starter is to be configured in the application.yml file (or application.properties if preferred).
All settings are found under the "multitenancy" prefix. "implementation" denotes the type of multitenancy required.
Currently only DATABASE_PER_TENANT is supported. 'interceptor' denotes the type of interceptor to be used.
Currently the manner in which to idintify a tenant is by adding a tenantId to the header of a request.
Thus the HEADER interceptor. An interceptor using JWT Tokens is currently under development.<br><br>
All tenants are to be provided in the "tenantList" prefix. The id field is required to uniquely identify a tenant.
Use this same id in in the value field of the request header with the key 'tenantId'.
```
Request Headers

Key: tenantId   Value: tenantId1  
```
The dataSource generates a concrete DataSource object for said tenant to be used in the multitenancy logic.

### application.yml
```
multitenancy:
  implementation: DATABASE_PER_TENANT
  interceptor: HEADER

  tenantList:
    - id: tenantId1
      dataSource:
        driverClassName: org.postgresql.Driver
        url: jdbc:postgresql:db1
        username: postgres
        password: password
    - id: tenantId2
      dataSource:
        driverClassName: org.postgresql.Driver
        url: jdbc:postgresql:db2
        username: postgres
        password: password
```
