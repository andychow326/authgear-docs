# Search for users

Authgear Admin GraphQL API supports searching user by keywords. Keywords include **email**, **phone number**, **username**, **SSO subject id** and **standard attributes**.

## Search users by email

The following example shows how to search for users by email, you can adjust the keywords and fields based on your needs.

The query has a maximum limit of 20, pagination parameters should be provided to obtain all the results. See [detail](#pagination).

### The query

```graphql
query (
  $searchKeyword: String!
) {
  users(
    searchKeyword: $searchKeyword
  ) {
    edges {
      node {
        id
        createdAt
        lastLoginAt
        isAnonymous
        isDisabled
        disableReason
        isDeactivated
        deleteAt
        standardAttributes
        identities {
          edges {
            node {
              id
              type
              claims
            }
          }
        }
        authenticators {
          edges {
            node {
              id
              type
              claims
            }
          }
        }
      }
    }
    totalCount
  }
}
```

### The variables

```json
{
  "searchKeyword": "user@example.com"
}
```

### The sample response

```json
{
  "data": {
    "users": {
      "edges": [
        {
          "node": {
            "id": "VXNlcjphZTNjMGFiZS02YjdkLTQ1ZjktOWIzZS1jMDUwYjVmY2Q3NjI",
            "createdAt": "2006-01-02T03:04:05.123456Z",
            "lastLoginAt": "2006-01-02T03:04:05.123456Z",
            "deleteAt": null,
            "isDisabled": false,
            "disableReason": null,
            "isAnonymous": false,
            "isDeactivated": false,
            "standardAttributes": {
              "email": "user@example.com",
              "email_verified": false,
              "name": "user01",
              "updated_at": 1136171045
            },
            "identities": {
              "edges": [
                {
                  "node": {
                    "claims": {
                      "email": "user@example.com",
                      "https://authgear.com/claims/login_id/key": "email",
                      "https://authgear.com/claims/login_id/original_value": "user@example.com",
                      "https://authgear.com/claims/login_id/type": "email",
                      "https://authgear.com/claims/login_id/value": "user@example.com"
                    },
                    "id": "SWRlbnRpdHk6NDNhMzZhMTEtM2VkNS00YjczLWE0ZjktMjQ1MWYyMzM5MmVj",
                    "type": "LOGIN_ID"
                  }
                }
              ]
            },
            "authenticators": {
              "edges": [
                {
                  "node": {
                    "claims": {},
                    "id": "QXV0aGVudGljYXRvcjo0YTIwMmYzMy03YmFhLTQzNWItYmE2NC02NDZkNmQ0YzRiNmE",
                    "type": "PASSWORD"
                  }
                }
              ]
            }
          }
        }
      ],
      "totalCount": 1
    }
  }
}
```

## Pagination

### The query

```graphql
query (
  $searchKeyword: String!
  $pageSize: Int!,
  $cursor: String,
  $sortBy: UserSortBy,
  $sortDirection: SortDirection
) {
  users(
    first: $pageSize
    after: $cursor
    searchKeyword: $searchKeyword
    sortBy: $sortBy
    sortDirection: $sortDirection
  ) {
    edges {
      node {
        id
      }
      cursor
    }
    totalCount
  }
}

```

### The variables

```json
{
  "searchKeyword": "",
  "pageSize": 5,
  "cursor": "b2Zmc2V0OjQ",
  "sortBy": "CREATED_AT",
  "sortDirection": "DESC"
}
```

### The sample response

```json
{
  "data": {
    "users": {
      "edges": [
        {
          "cursor": "b2Zmc2V0OjU",
          "node": {
            "id": "VXNlcjo2YTExYjkxNy0yNTg0LTRmNWEtOTkyMS0xN2E3ZmMzMWZjZWU"
          }
        },
        {
          "cursor": "b2Zmc2V0OjY",
          "node": {
            "id": "VXNlcjo0ZTFhZjZmYy0zM2VjLTQ5NjAtOGI2ZC00YTc5YjkxM2Q5N2Y"
          }
        },
        {
          "cursor": "b2Zmc2V0Ojc",
          "node": {
            "id": "VXNlcjphZDJjZWY5Ny0xYzk2LTQ4N2ItOWQzZS01NGVjMzJhYzUxYjY"
          }
        },
        {
          "cursor": "b2Zmc2V0Ojg",
          "node": {
            "id": "VXNlcjphMWIzMzVhMC1jYTdiLTRjMTItYmVmNC04NmNiZTQ4OGMxNzI"
          }
        },
        {
          "cursor": "b2Zmc2V0Ojk",
          "node": {
            "id": "VXNlcjphOWU2YTYwYy0wYTQ1LTQxMzctYTM3MC0wNWM1MjBlZWFkZmU"
          }
        }
      ],
      "totalCount": 30
    }
  }
}
```

#### Parameters

- `searchKeyword`: Search for users by specified keyword.
- `pageSize`: The page size indicates the limit on the number of items to be returned. Maximum is `20`.
- `cursor`: A cursor for use in pagination. You can pass the cursor value of the last edges item to a subsequent call to fetch the next page of results.
- `sortBy`: The field in which to order users. Supported values: `CREATED_AT` or `LAST_LOGIN_AT`.
- `sortDirection`: The direction in which to order users by the specified field. Supported values: `ASC` or `DESC`.
