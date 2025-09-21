# beep-arch-decisions

A repo to make decisions on Beep's new architecture, and agree on them together.

The following decisions have been taken:

- Database technologies and Search. See `search/`
- Separation into services. See `services/`
- Observability stack. See `observability/`

- IAM **has to be** Keycloak (hard requirement by the client).

The following decisions are still being decided:

- Broker tech and data format to exchange between services/broker is being taken in `broker/`
- Authz handling is being taken in `authz/`
- Infrastructure platform design in `infra-platform/`
