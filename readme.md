# graphql-play 

This repo for my pocs in GraphQl.

# Notes on GraphQL

## Introduction
- GraphQL is a new API standard that provides a more efficient, powerful, and flexible alternative to REST
- New API Standard created by FB -> it is just a **SPECIFICATION**
- Enables declarative data fetching
- Respond to single Endpoint 

## an Alternative to Rest
1. Increased mobile usage created need for efficient data loading
2. Variety of different fronend frameworks and platforms on the client side -> need to load different type of data
3. Fast development speed & expectation for rapid feature development

## History
- GraphQL used by fb from 2012 in their native mobile apps
- first time presented at React.js Conf
- GraphQL can be used with several languages
- Netflix and Coursera had similar Idea -> Netflix Falcor

## Core Concepts

### The Schema Definition Language (SDL)

- "!" means mandatory
- one to many example: 

type Person {
    name: String!
    age: Int!
    posts: [Post!]! 
}

One person has one or many posts

type Post {
    title: String!
    author: Person!
}

One post has one author (Person)

### Fetchin Data with Queries

- query: 
{
    allPersons {
        name
    }
}

- Response: 
  {
      "allPersons": [
          {"name": "Johnny"},
          {"name": "Sarah"},
          {"name": "Alice"},
      ]
  }
  - You can have some parameters: 
{
    allPersons (last: 2) {
        name
    }
}

### Mutatitons

- 3 kinds of mutations:
  - Creating new data
  - updating existing data
  - deleting existing data
- example:

**query:**
mutation {
    createPerson(name:"Bob", age: 36) {
        id
        name
        age
    }
} 

**response**
{
    "createPerson": {
        "id": "1",
        "name":"Bob",
        "age": 23,
    }
}

- Realtime Updates with Subscriptions

example:

subscription {
    newPerson :
    name
    age
}

Each time a client use the root newPerson, the subscribers will receive the object created.

### The GraphQL Schemq
- specify the capabilities of the API
- contract between server and client
- define the different root types
- Collection of GraphQL types with special *root types*
- example of a full schema:
- 
**Three root type:**
type Query {
    allPersons(last: Int): [Person!]!
    allPosts(last: Int): [Post!]!
}

type Mutation {
    createPerson(name: String!, age: String!): Person!
    updatePerson(id: ID!, mame: String!, age:String!): Person!
    deletePerson(id: ID!): Person!
    ...for post...
}

type Subscription {
    newPerson: Person!
    updatedPerson: Person!
    deletedPerson: Person!
    ...for post...
}

**two type:**
type Person {
    id: ID!
    name: String!
    age: Int!
    posts: [Post!]!
}

type Post { 
    title: String!
    author: Person!
}


## Architecural concepts

Here are three possible architecture: 

### GraphQl server with a connected DB
- most commin from app from scratch
- Single Web Server implementing GraphQl
- GraphQL is transport layer agnostic (TCP, Websocket or anything can work)
- Any database -> SQL or NoSQL

### GraphQL Server to integrate existing system
- useful for legacy
- And so Hide complexity to fetch data
- Doesn't care about the data sources


### A Hybrid approach with a connected DB and integration of existing system
- Combination of the two previous

## Resolver functions are the key
- One resolver per field




