## 🔐 IAM (Identity & Access Management)

### 1. Choice of Technology

- **Keycloak** as IAM provider.
- **OpenID Connect (OIDC)** for authentication of clients.
- **JWT tokens** (signed) for service-to-service communication.

### 2. Core Concepts
- **Users**: accounts created and managed in Keycloak.
- **Clients**: each micro-service is registered as a client in Keycloak.


### 3. Roles & Permissions Model
- **Global RBAC** → Keycloak roles.
- **Local RBAC** → managed by the Communities Service.
- Each role has a `permissions: u64` mask.
- A member of a community can hold multiple roles → effective permissions are computed by bitwise OR of all roles.


### 4. Separation of Concerns
- **Keycloak**: authentication (who the user is)
- **Communities Service**: Authorization (what the user can do in a given context).

### 5. Integration in Services
1. The client logs in via Keycloak and receives a JWT.
2. The client calls a micro-services API (e.g., Messages).
3. The service validates the JWT (auth).
4. For authorization, the service delegates to the **Communities Service** with a request like

```bash
GET /servers/{id}/authz/check?action=SEND_MESSAGE&user{user_id}&channel={channel_id}
```

5. The Communities Services:
  - Loads the member profile in the given server.
  - Checks bans/mutes.
  - Combines all roles → bitwise permissions mask.
  - Verifies if the action is allowed.

6. Response: `{ "allow": true }` or `{ "allow": false }`
