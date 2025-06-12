## 1. `grant_type=password` — **Resource Owner Password Credentials**

Used when a trusted application collects the user's credentials (username/password) and exchanges them directly for a token.

```bash
curl -X POST http://localhost:8080/realms/spring-jwt/protocol/openid-connect/token \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "client_id=java-jwt-hello-world" \
  -d "client_secret=fPv7HPZIztJOO8clry53YUMAP4KDErak" \
  -d "username=admin" \
  -d "password=admin" \
  -d "grant_type=password" \
  -d "scope=openid"
```

#### Response (partial):

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR...",
  "expires_in": 300,
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR...",
  "id_token": "eyJhbGciOiJSUzI1NiIsInR...",
  "refresh_expires_in": 1800,
  "token_type": "Bearer"
  "not-before-policy": 0,
  "session_state": "6d92ab2a-bd35-42ee-aea7-55d2fc195b5b"
}
```

---

## 2. `grant_type=client_credentials` — **Machine-to-Machine Authentication**

Used when a backend service (client) wants to authenticate itself without any user context (e.g., service-to-service).

```bash
curl -X POST "http://localhost:8080/realms/spring-jwt/protocol/openid-connect/token" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  --data-urlencode "client_id=java-jwt-hello-world" \
  --data-urlencode "client_secret=fPv7HPZIztJOO8clry53YUMAP4KDErak" \
  --data-urlencode "grant_type=client_credentials"
```

#### Response (partial):

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR...",
  "expires_in": 300,
  "token_type": "Bearer",
  "scope": "profile email"
}
```

---

## 3. `grant_type=refresh_token` — **Get New Token Without Re-login**

Used to obtain a new access token when the current one expires, without requiring the user to log in again.

```bash
curl -X POST "http://localhost:8080/realms/spring-jwt/protocol/openid-connect/token" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  --data-urlencode "client_id=java-jwt-hello-world" \
  --data-urlencode "client_secret=fPv7HPZIztJOO8clry53YUMAP4KDErak" \
  --data-urlencode "grant_type=refresh_token" \
  --data-urlencode "refresh_token=<your-refresh-token-here>"
```

#### Response (partial):

```json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsInR...",
  "expires_in": 300,
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR...",
  "id_token": "eyJhbGciOiJSUzI1NiIsInR...",
  "refresh_expires_in": 1800,
  "token_type": "Bearer"
  "not-before-policy": 0,
  "session_state": "6d92ab2a-bd35-42ee-aea7-55d2fc195b5b"
}
```
