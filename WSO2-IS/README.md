# WSO2 Identity Server
https://github.com/wso2/product-is

## 🐋 Docker install
> On windows I recommend [setting up docker in WSL2](https://www.hanselman.com/blog/HowToSetUpDockerWithinWindowsSystemForLinuxWSL2OnWindows10.aspx).

https://github.com/wso2/docker-is
https://hub.docker.com/r/wso2/wso2is

Start WSO2 IS instance in docker and map port 9443.

```bash
docker run -it -p 9443:9443 --name wso2-is wso2/wso2is:5.10.0
```

## 👨‍✈️ Accessing management console
Once the container is started, access the management console with the following URL on your favorite web browser using the credentials username: **admin** and password: **admin**.
https://localhost:9443/carbon

## Some of the many REST APIs available
All REST APIs can be found [here](https://is.docs.wso2.com/en/latest/develop/rest-apis/).
> Tip: The main tenant name for WSO2 IS is 'carbon.super'. e.g. `https://localhost:9443/t/carbon.super`

### SCIM 2.0 (Users, Groups, Me)
The SCIM API can be called in order to perform various tasks in the WSO2 Identity Server on Users, Me, and Groups (Roles). For simplicity, cURL commands are used in this example to send CRUD requests to the REST endpoints of Identity Server.
>System for Cross-domain Identity Management (SCIM) is a standard for automating the exchange of user identity information between identity domains, or IT systems.

All available SCIM 2.0 API definitions are found [here](https://is.docs.wso2.com/en/latest/develop/scim2-rest-apis/).

[Here (SCIM README.md)](.\SCIM%20README.md) are some SCIM 2.0 examples.



## References and material
### WSO IS Docs
https://is.docs.wso2.com/en/latest/develop/rest-apis/
### SCIM 2.0
https://github.com/wso2/charon
http://www.simplecloud.info/#Implementations2
https://is.docs.wso2.com/en/5.10.0/develop/scim-1.1-apis/
https://is.docs.wso2.com/en/5.10.0/develop/scim2-rest-apis/

### Other
https://en.wikipedia.org/wiki/CURL
https://en.wikipedia.org/wiki/Basic_access_authentication


