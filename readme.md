## **REST**HEART
## The Web API for MongoDB

This is a premade stack designed to reduce friction on adopt MongoDB with **REST**Heart.

### Stack Services
* MongoDB (without authentication)
* **REST**Heart

### Configuration
```
--git@github.com:docker-gallery/RESTheart.git
 |--docker-compose.yml (1)
 |--readme.md
 |--restheart 
    |--config
       |--restheart.yml (2)
       |--security.yml (3)
```

#### 1 - docker-compose.yml
Docker Compose file used do declare configurations about both services (restheart and mongodb).

#### 2 - restheart.yml
Used to configure **REST**Heart.

Take a look at line 69: `mongo-uri: mongodb://mongodb` defines a connectionstring to worj with mongodb.

#### 3 - security.yml
Used to configure authentication and authorization on **REST**Heart, by default i've produced some rules, like:
* Anonymus Uses can only read the `publicdb` database data (only if you create the database with name `publicdb`).
* User `admin` user has password `admin`, they has `admins` role and can do everything.
* User `user` user has password `user`, they has `users` role and can do everything only on `publicdb`.


# Get Started

* On any docker environment
* There we go! Run `docker-compose up`. Just it. 


# Using API by Example

### Create appdb database
#### Request
```
curl -i -X PUT \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
   -H "Content-Type:application/json" \
   -d \
'{
  "desc" :"Application Database"
}' \
 'http://localhost:10080/appdb'
```
#### Response
```
201 - Created
```








### Create **person** collection on **appdb** database
#### Request
```
curl -i -X PUT \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
   -H "Content-Type:application/json" \
   -d \
'{
  "desc" :"Persons in my app"
}' \
 'http://localhost:10080/appdb/person'
```
#### Response
```
201 - Created
```







### Insert one document on person collection of appdb database
#### Request
```
curl -i -X POST \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
   -H "Content-Type:application/json" \
   -d \
'{      
  "name": "Luiz Carlos Faria"
  "email": "luizcarlosfaria@gmail.com", 
  "pin": "123",
  "roles": [ "role1" ]
}' \
 'http://localhost:10080/appdb/person'
```
#### Response
```
201 - Created
```


### Update one document on person collection of appdb database
#### Request
```
curl -i -X PUT \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
   -H "Content-Type:application/json" \
   -d \
'{      
  "name": "Luiz Carlos Faria"
  "email": "luizcarlosfaria@gmail.com", 
  "pin": "456",
  "roles": [ "role2", "role3" ]
}' \
 'http://localhost:10080/appdb/person/5aa739ab7ec55efe83deee22'
```
#### Response
```
200 - Ok
```



### List Databases

#### Request
```
curl -i -X GET \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
 'http://localhost:10080/'

```
#### Response
```
{
    "_embedded": [
        {
            "_id": "appdb",
            "_etag": {
                "$oid": "5aa737f7857aba0007504e3f"
            }
        }
    ],
    "_size": 1,
    "_total_pages": 1,
    "_returned": 1
}
```



### List collections on appdb

#### Request
```
curl -i -X GET \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
 'http://localhost:10080/appdb/'

```
#### Response
```
{
    "_embedded": [
        {
            "_id": "person",
            "_etag": {
                "$oid": "5aa7383a857aba0007504e40"
            },
            "desc": "Persons in my app"
        }
    ],
    "_id": "appdb",
    "_etag": {
        "$oid": "5aa737f7857aba0007504e3f"
    },
    "_size": 1,
    "_total_pages": 1,
    "_returned": 1
}
```




### List documents on person collection

#### Request
```
curl -i -X GET \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
 'http://localhost:10080/appdb/person'
```
#### Response
```
{
    "_embedded": [
        {
            "_id": {
                "$oid": "5aa739ab7ec55efe83deee22"
            },
            "_etag": {
                "$oid": "5aa73a34857aba0007504e46"
            },
            "email": "luizcarlosfaria@gmail.com",
            "name": "Luiz Carlos Faria",
            "pin": "456",
            "roles": [
                "role2",
                "role3"
            ]
        }
    ],
    "_id": "person",
    "_etag": {
        "$oid": "5aa7383a857aba0007504e40"
    },
    "desc": "Persons in my app",
    "_returned": 1
}
```


### Query documents on person collection

#### Request
```
curl -i -X GET \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
 'http://localhost:10080/appdb/person?filter=%7B+'pin'%3A+%22456%22+%7D'
```
#### Response
```
{
    "_embedded": [
        {
            "_id": {
                "$oid": "5aa739ab7ec55efe83deee22"
            },
            "_etag": {
                "$oid": "5aa73a34857aba0007504e46"
            },
            "email": "luizcarlosfaria@gmail.com",
            "name": "Luiz Carlos Faria",
            "pin": "456",
            "roles": [
                "role2",
                "role3"
            ]
        }
    ],
    "_id": "person",
    "_etag": {
        "$oid": "5aa7383a857aba0007504e40"
    },
    "desc": "Persons in my app",
    "_returned": 1
}
```


### Delete document on person collection

#### Request
```
curl -i -X DELETE \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
 'http://localhost:10080/appdb/person/5aa739ab7ec55efe83deee22'
```
#### Response
```
204 - No Content
```


### Drop person collection

#### Request
```
curl -i -X DELETE \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
   -H "If-Match:5aa7383a857aba0007504e40" \
 'http://localhost:10080/appdb/person/'
```
#### Response
```
204 - No Content
```


### Drop appdb database

#### Request
```
curl -i -X DELETE \
   -H "Authorization:Basic YWRtaW46YWRtaW4=" \
   -H "If-Match:5aa737f7857aba0007504e3f" \
 'http://localhost:10080/appdb/'
```
#### Response
```
204 - No Content
```

