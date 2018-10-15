# GoStrest
My attempt at recreating https://github.com/eykrehbein/strest/

It mostly works as expected.

usage 

`strest -script req.yml`

### TODO

example configuratation

```
version: 1
requests:
  userRequest:
    failOnError: true
    url: 'http://localhost:8080/user'
    #may need to take consideration for additional method types
    method: POST | GET 
    data:
        params: 
            name: testUser
        headers: 
            Authentication: Bearer
            SomemoreHeader: "asfsdfds"
# data types supported for post requests JSON/FORM/RAW    

        form: 
            username: kingwill101
            password: somepassword
        json: 
            username: kingwill101
            password: somepassword
        raw: 
            username: kingwill101
            password: somepassword
    log: true
    validation:
        body: "Hello, World!"
        statusCode: 200
    repeat: 3
    delay: 500
```

## Template function calls

All template functions are golang based so you may need to have a look at 
https://golang.org/pkg/text/template/ for better basic understanding. 

`using tempalte functions within JSON fields are not supported at this time`

### Default template functions

`ENV` 
### fake data
`MaleFirstName`

`FemaleFirstName`

`FirstName`

`MaleLastName`

`FemaleLastName`

`LastName`

`MalePatronymic`

`FemalePatronymic`

`Patronymic`

`MaleFullNameWithPrefix`

`FemaleFullNameWithPrefix`

`FullNameWithPrefix`

`MaleFullNameWithSuffix`

`FemaleFullNameWithSuffix`

`FullNameWithSuffix`

`MaleFullName`

`FemaleFullName`

`FullName`

```
version: 1
requests:
  userRequest:
    ...
    url: "http://{{ ENV `ADDRESS` }}:8080/test/user"
    data:
        params: 
            name: '{{ FullName }}'
    ...
```
debug output
```
[GIN] 2018/10/15 - 10:07:43 | 200 |      61.065µs |       127.0.0.1 | POST     /test/user?name=Walter+Sanchez

```


# TODO

1. Allow the specifying of types