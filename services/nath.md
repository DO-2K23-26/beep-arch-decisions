# 🧩 Services

## Users Service

### Responsibilities
- Manage user profiles (username, avatar, bio, status).
- Handle friendships and online presence.

### Data
- PostgreSQL (users, friendships).
- Redis for presence cache.

### APIs
- REST API for user management.

### Events emitted
- `UserCreated`
- `UserStatusChanged`


## Communities Service

### Responsibilities
- Manage servers
- Manage channels
- Manage roles with bitwise permissions.

### Data
- PostgreSQL (servers, channels, role, memberships, bans, mutes)

### Events emitted
- `ServerCreated`
- `ChannelCreated`
- `RoleUpdated`
- `MemberBanned` / `MemberMuted`

## Messages Service

### Responsibilities
- Store and deliver text messages.
- Support threads and reactions.


### Data
- PostgreSQL (messages, threads, reactions)

### APIs
- REST API for message operations.

### Events emitted
- `MessageCreated`
- `MessageDeleted`
