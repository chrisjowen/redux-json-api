Redux ❤️ JSON API
----------------

Redux actions, action creators and reducers to make life with [JSON API](http://jsonapi.org)s a breeze.

# Features

- Automatically maintains a state of all loaded entities
- Provides actions for
  - Creating entity
  - Reading endpoint
  - Updating entity
  - Deleting entity
- Automatically keeps relationships up to date on related entities when creating, updating and deleting entities

# Usage

1. `npm install redux-json-api`
1. Enable JSON API reducer (examples assume that you've connected it to `state.api`)
1. Dispatch actions
1. Connect your view to `state.api.${entityType}`

# State structure

```json
{
  "api": {
    "users": {
      "data": [
        {
          "type": "users",
          "id": 1,
          "attributes": { }
        }
      ],
      "isInvalidating": "IS_DELETING"
    },
    "isCreating": 0,
    "isReading": 0,
    "isUpdating": 0,
    "isDeleting": 0
  }
}
```

Entity objects are 1-to-1 with the API response.

# API

## Options

Each function accepts an options object with two callbacks: `onSuccess`, `onError`.

## Create entity

`createEntity(entity, options)`

Pass a full resource object to `createEntity`. It will trigger a request to `POST /${entity.type}`.

Expects the API to return `200 OK` with the newly created resource object in response body.

## Read endpoint

`readEndpoint(endpoint, options)`

Provide the endpoint from where to read. E.g. `users/1/roles`. The module will read each entity and map them from their type specified.

## Update entity

`updateEntity(entity, options)`

Pass your resource object to `updateEntity`. It will trigger a request to `PATCH /${entity.type}/${entity.id}`.

Expects the API to return `200 OK` with the updated resource object in response body.

## Delete entity

`deleteEntity(entity.options)`

Accept a resource object and triggers a request to `DELETE /${entity.type}/${entity.id}`.

Expects the API to return `204 No content`.