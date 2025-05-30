## **Key Concepts in Keycloak**

---

### 1. **Realm**

A **realm** is the **highest-level container** in Keycloak.

* It **isolates everything** inside it: users, roles, clients, groups, configurations.
* Realms are like **tenants**—each can have its own identity management setup.

You can have:

* `master` realm (admin only)
* Custom realms like `myapp-realm`, `client-xyz`, etc.

> Think of a realm as a *namespace* for your identity and access configuration.

---

### 2. **Client**

A **client** is any application or service that **wants to use Keycloak** to authenticate users or obtain access tokens.

#### Examples:

* A frontend SPA
* A backend API (Spring Boot service)
* A third-party app like Grafana

Clients can be:

* **Confidential**: Backend apps (have a secret)
* **Public**: Frontend or mobile apps (no secret)
* **Bearer-only**: Services that accept tokens but don’t initiate login (e.g., microservices)

---

### 3. **User**

A **user** represents a person (or machine) that can authenticate.

* Has credentials (password, OTP)
* Can belong to groups
* Can be assigned roles and attributes

> Users can be local (stored in Keycloak) or come from **User Federation** (e.g., LDAP).

---

### 4. **Role**

A **role** defines a set of permissions.

* Can be assigned to users or clients.
* Used for **role-based access control (RBAC)**.

Types:

* **Realm Roles**: Global roles within a realm.
* **Client Roles**: Specific to a client (e.g., `reader` for `service-a`).

---

### 5. **Group**

A **group** is a way to organize users and apply roles in bulk.

* Assign roles to a group, and all users in that group inherit those roles.

> Great for managing large teams or organizations.

---

### 6. **Identity Provider (IdP)**

Allows Keycloak to delegate authentication to **external identity providers**, like:

* Google
* GitHub
* Another Keycloak realm
* SAML provider

> Enables **social login** or **cross-realm federation**.

---

### 7. **Client Scope**

Defines **protocol-level settings** (like what claims go into tokens).

* Helps customize what info is included in the **Access Token**, **ID Token**, etc.
* Can be **default** or **optional** for a client.

---

### 8. **Token**

Keycloak issues several types of tokens (typically JWTs):

| Token Type        | Purpose                                              |
| ----------------- | ---------------------------------------------------- |
| **Access Token**  | Used to access APIs (contains roles, permissions)    |
| **ID Token**      | Contains user profile info (mainly for frontend use) |
| **Refresh Token** | Used to get new access tokens without re-login       |

---

### 9. **Authorization Services**

Advanced feature to define fine-grained access policies, resources, and permissions:

* Used for **Attribute-Based Access Control (ABAC)** or **Policy-Based Access Control (PBAC)**.
* You can define rules based on roles, time, user attributes, etc.

---

## Example Scenario

Let’s say you’re building a Spring Boot app with Keycloak:

| Component                           | Keycloak Term                         |
| ----------------------------------- | ------------------------------------- |
| Your app's auth system              | **Realm**                             |
| Your Spring Boot backend            | **Confidential Client**               |
| Your Angular frontend               | **Public Client**                     |
| Admins & users                      | **Users**                             |
| `admin`, `viewer`                   | **Realm Roles**                       |
| Departmental access group           | **Groups**                            |
| Google login                        | **Identity Provider**                 |
| Permissions like `can_view_reports` | **Authorization Services / Policies** |

