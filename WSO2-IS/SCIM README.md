# Some SCIM examples
The following requests use [Basic Auth](https://en.wikipedia.org/wiki/Basic_access_authentication) authentication to demonstrate sending requests to the REST endpoints of WSO2 Identity Server as a quick start. **In a production environment, we recommend that you use OAuth Authentication instead**.
> The `--insecure` option is added to cURL commands to allow insecure server connections when using SSL to our docker instance

## 👨‍💼 User
Get: Filter Users. This API returns users according to the filter, sort and pagination parameters.
*Request*
```bash
curl -v --location --request GET 'https://localhost:9443/scim2/Users?attributes=name,emails,groups,userName&filter=userName%20Eq%20admin' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' --insecure
```
*Response*
```json 
{"totalResults":1,"startIndex":1,"itemsPerPage":1,"schemas":["urn:ietf:params:scim:api:messages:2.0:ListResponse"],"Resources":[{"emails":["admin@wso2.com"],"name":{"familyName":"Administrator"},"groups":[{"display":"Application/User Portal","value":"ac180429-d83f-4e3d-a031-4915335aacea","$ref":"https://localhost:9443/scim2/Groups/ac180429-d83f-4e3d-a031-4915335aacea"},{"display":"admin","value":"506b29ac-5d6c-4ada-8d1d-510c177c30c0","$ref":"https://localhost:9443/scim2/Groups/506b29ac-5d6c-4ada-8d1d-510c177c30c0"}],"id":"189acf7b-73de-441f-b72d-e7c0f29178b4","userName":"admin"}]}
```

Get all users:
*Request*
```bash
curl -v --location --request GET 'https://localhost:9443/scim2/Users' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' --insecure
```

Create user:
*Request*
```bash
curl -v --location --request POST 'https://localhost:9443/scim2/Users' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' \
--header 'Content-Type: application/json' \
--data-raw '{
    "schemas": [],
    "name": {
        "firstName": "Nicolas",
        "lastName": "Cage"
    },
    "userName": "nicolas.cage",
    "password": "password",
    "emails": [
        {
            "type": "home",
            "value": "nicolas.cage@example.com",
            "primary": true
        },
        {
            "type": "work",
            "value": "nicolas.cage@wso2,com"
        }
    ],
    "EnterpriseUser": {
        "employeeNumber": "1234A",
        "manager": {
            "value": "Benjamin Franklin Gates"
        }
    }
}' --insecure
```
*Response*
```json
{"emails":[{"type":"work","value":"nicolas.cage@wso2,com"},{"type":"home","value":"nicolas.cage@example.com"}],"meta":{"created":"2020-05-19T03:44:45.775501Z","location":"https://localhost:9443/scim2/Users/a677f949-dbc5-4879-80f2-c02fdaa510ae","lastModified":"2020-05-19T03:44:45.775501Z","resourceType":"User"},"schemas":["urn:ietf:params:scim:schemas:core:2.0:User","urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"],"roles":[{"type":"default","value":"Internal/everyone"}],"name":{"familyName":"nicolas.cage"},"id":"a677f949-dbc5-4879-80f2-c02fdaa510ae","userName":"nicolas.cage"}
```

Delete user:
*Request*
```bash
curl -v --location --request DELETE 'https://localhost:9443/scim2/Users/a677f949-dbc5-4879-80f2-c02fdaa510ae' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' --insecure
```
*Response*
```
< HTTP/1.1 204
```

## 👫 Groups (Roles)
Get Roles:
*Request*
```bash
curl --location --request GET 'https://localhost:9443/scim2/Groups' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' --insecure
```
*Response*
```json
{"totalResults":3,"startIndex":1,"itemsPerPage":3,"schemas":["urn:ietf:params:scim:api:messages:2.0:ListResponse"],"Resources":[{"displayName":"Application/User Portal","meta":{"created":"2020-05-18T20:50:11.060Z","location":"https://localhost:9443/scim2/Groups/ac180429-d83f-4e3d-a031-4915335aacea","lastModified":"2020-05-18T20:50:11.060Z"},"members":[{"display":"admin","value":"189acf7b-73de-441f-b72d-e7c0f29178b4","$ref":"https://localhost:9443/scim2/Users/189acf7b-73de-441f-b72d-e7c0f29178b4"}],"id":"ac180429-d83f-4e3d-a031-4915335aacea"},{"displayName":"Internal/system","meta":{"created":"2020-05-19T03:51:25.652Z","location":"https://localhost:9443/scim2/Groups/08272e47-aa14-4577-8154-e92323edc403","lastModified":"2020-05-19T03:51:25.652Z"},"id":"08272e47-aa14-4577-8154-e92323edc403"},{"displayName":"admin","meta":{"created":"2020-05-18T19:50:49.885Z","location":"https://localhost:9443/scim2/Groups/506b29ac-5d6c-4ada-8d1d-510c177c30c0","lastModified":"2020-05-18T19:50:49.885Z"},"members":[{"display":"admin","value":"189acf7b-73de-441f-b72d-e7c0f29178b4","$ref":"https://localhost:9443/scim2/Users/189acf7b-73de-441f-b72d-e7c0f29178b4"}],"id":"506b29ac-5d6c-4ada-8d1d-510c177c30c0"}]}
```

Create Role:
*Request*
```bash
curl -v --location --request POST 'https://localhost:9443/scim2/Groups' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' \
--header 'Content-Type: application/json' \
--data-raw '{
    "schemas": [
        "urn:ietf:params:scim:schemas:core:2.0:Group"
    ],
    "displayName": "Treasure_Hunter",
    "members": [
        {
            "value": "189acf7b-73de-441f-b72d-e7c0f29178b4",
            "display": "admin"
        }
    ]
}' --insecure
```
*Response*
```json
{"displayName":"PRIMARY/Treasure_Hunter","meta":{"created":"2020-05-19T04:19:26.903832Z","location":"https://localhost:9443/scim2/Groups/74211a8d-7a70-4afd-9e73-5951803d93a5","lastModified":"2020-05-19T04:19:26.903832Z","resourceType":"Group"},"schemas":["urn:ietf:params:scim:schemas:core:2.0:Group"],"members":[{"display":"admin","value":"189acf7b-73de-441f-b72d-e7c0f29178b4"}],"id":"74211a8d-7a70-4afd-9e73-5951803d93a5"}
```

Delete Role:
*Request*
```bash
curl -v --location --request DELETE 'https://localhost:9443/scim2/Groups/74211a8d-7a70-4afd-9e73-5951803d93a5' \
--header 'Authorization: Basic YWRtaW46YWRtaW4=' --insecure
```
*Response*
```
< HTTP/1.1 204
```

## References and material
### SCIM 2.0
https://github.com/wso2/charon
http://www.simplecloud.info/#Implementations2
https://is.docs.wso2.com/en/5.10.0/develop/scim-1.1-apis/
https://is.docs.wso2.com/en/5.10.0/develop/scim2-rest-apis/

### Other
https://en.wikipedia.org/wiki/CURL
https://en.wikipedia.org/wiki/Basic_access_authentication
