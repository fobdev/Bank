# dotnet-webapi-bank

This is a project made for a test related to WebAPIs.

## Main Architecture (ASP.NET MVC WebAPI)
![](APIModel.png)


# docker instructions
# 1 - run this commandline: 

```
docker network create bankapi-fobenga && docker run -d --rm --name mongo -p 27017:27017 -v mongodbdata:/data/db -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=fobenga123 --network=bankapi-fobenga mongo && docker run -it --rm -p 8080:80 -e MongoDbSettings:Host=mongo -e MongoDbSettings:Password=fobenga123 --network=bankapi-fobenga fobenga/bank:v1
```

# 2 - requests at: 
```http://localhost:8080/{endpoint}```

# healthcheck endpoints:

##### database integrity / requests available
```
http:/localhost:8080/status/ready 
```

##### server integrity / connected 
```
http:/localhost:8080/status/live
```

# usage

### get all users

    [GET] endpoint: users/

##### example response

```json
    [
        {
            "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
            "staff": false,
            "name": "string",
            "balance": 0.0
        },
    ]
```
```md
"staff" = true: staff user / false: common user
```
### get a user by id

    [GET] endpoint: users/{id}

##### example response
```json
    {
      "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "staff": false,
      "name": "string",
      "balance": 0.0
    }
```
```md
"staff" = true: staff user / false: common user
```
### create a user

     [POST] endpoint: users/

##### post model
```json
    {
      "staff": false,
      "name": "string",
      "cpf": "string",
      "email": "string",
      "password": "string"
    }
```
```md
"staff" = true: staff user / false: common user
"cpf" = string pattern: 999.999.999-99 OR 99999999999
"email" = string pattern: aaa@aaa.aaa
```

### see all transactions

      [GET] endpoint: transactions/

##### example response
```json
      [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "sender": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "receiver": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "createdAt": "2021-10-23T01:54:07.493Z",
          "amount": 0.0
        },
      ]
```

### get transaction by id

      [GET] endpoint: transactions/{id}


##### example response
```json
     [
        {
          "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "sender": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "receiver": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
          "createdAt": "2021-10-23T01:54:07.493Z",
          "amount": 0.0
        }
    ]
```
### create transaction

     [POST] endpoint: transactions/create

##### post model
```json
    {
      "sender": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "receiver": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
      "amount": 0.0
    }
```
```md
"sender" = Guid of the sender
"receiver" = Guid of the receiver
"amount" = amount of money (in double)
```

### undo transaction

    [POST] endpoint: transactions/undotransaction/{id}

##### no response
