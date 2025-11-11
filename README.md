## Keycloak:

Keycloak is an **open-source Identity and Access Management (IAM)** solution developed by Red Hat. It provides authentication and authorization services for modern applications and services, helping developers integrate security without writing custom code.


### What Keycloak Does
- User Authentication (login, logout)
- Authorization (who can access what)
- Single Sign-On (SSO) across multiple apps
- Identity Brokering (connect to external identity providers like Google, GitHub, LDAP, etc.)
- User Federation (sync users from existing databases or directories)
- Role-Based Access Control (RBAC)



### Keycloak Architecture Overview:

```
          +---------------------+
          |   User / Browser    |
          +----------+----------+
                     |
                     v
            +--------+---------+
            |     Keycloak     |
            | (Identity Server)|
            +--------+---------+
                     |
      +--------------+---------------+
      |                              |
      v                              v
+-------------+              +----------------+
|  Application|              | External IdP   |
| (Client App)|              | (Google, LDAP) |
+-------------+              +----------------+

```



### Core Concepts:

| Term                        | Description                                                           |
| --------------------------- | --------------------------------------------------------------------- |
| **Realm**                   | Logical container for users, roles, and clients (like a tenant).      |
| **Client**                  | Any application or service that uses Keycloak for auth.               |
| **User**                    | An identity in Keycloak.                                              |
| **Role**                    | Defines permissions or access levels.                                 |
| **Group**                   | Collection of users (can have roles assigned).                        |
| **Identity Provider (IdP)** | External provider for authentication (e.g., Google).                  |
| **Token**                   | JWT issued to users upon authentication (access, refresh, ID tokens). |



### Supported Protocols
- OAuth 2.0
- OpenID Connect (OIDC)
- SAML 2.0



### Deployment Options
- Docker Container
- Kubernetes (Operator or Helm chart)
- Standalone on Linux/Windows
- Embedded in Java apps (less common)



### Example on Docker:

```
docker run --name keycloak -dit \
  -p 8080:8080 \
  -e KC_BOOTSTRAP_ADMIN_USERNAME=admin \
  -e KC_BOOTSTRAP_ADMIN_PASSWORD=admin \
  quay.io/keycloak/keycloak:26.4.2 \
  start-dev
```

> [!NOTE]
> Note Replace `start-dev` with `start` for production mode.



### Example on OpenJDK: 

#### Download Keycloak:
Download and extract `https://github.com/keycloak/keycloak/releases/download/26.4.4/keycloak-26.4.4.zip` from the Keycloak website.

```
wget https://github.com/keycloak/keycloak/releases/download/26.4.4/keycloak-26.4.4.zip
```


```
unzip keycloak-26.4.4.zip

cd keycloak-26.4.4
```


#### Start Keycloak:

```
./bin/kc.sh start-dev
```


Or,

```
## Set the password as an environment variable:

export ADMIN_PASS=admin

./bin/kc.sh bootstrap-admin user --username admin --password:env ADMIN_PASS


## Then start Keycloak:

./bin/kc.sh start-dev
```




### Web Console: 
- Open your browser to → `http://your_ip:8080`
- Login with:
    - Username: admin
    - Password: admin



#### Create a realm:

1. Open the Keycloak Admin Console: Click `Manage realms` - `Create Realm`:
    - Resource file: 
    - Realm name *: myRealm
    - Enabled: ON
    - Click Create


#### Create a user:

1. Open the Keycloak Admin Console: Click `Manage` - `Users`- `Create new user`:
    - Required user actions: N/A
    - Email verified: Off
    - Username: user1
    - Email: 
    - First name: 
    - Last name: 
    - Click Create

2. Click `Credentials` Tab at the top of the page.
    - Password: 
    - Password confirmation: 
    - Temporary: Off (so that the user does not need to update this password at the first login)
    - Save 




### Author:
- **Name:** Technbd   



### License:
This project is licensed under the **MIT** License.




### Ref:
- [Keycloak Docs](https://www.keycloak.org/guides#getting-started)









