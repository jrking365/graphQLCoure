# graphQLCouse

starter graphQL simple app

* Installed express, body parser, nodemon

* created a simple app.js file with a get that returns hello world

* Installed graphql-express and graphql

* Import graphQlHttp and create a basic example

```javascript
...
const { graphqlHTTP } = require('express-graphql');
const { buildSchema } = require('graphql');
...
//Note: resolver functions need to match our schema endpoint by name
app.use(
    '/graphql',
    graphqlHTTP({
        schema: buildSchema(`
        type RootQuery {
            events: [String!]!
        }

        type RootMutation {
            createEvent(name:String):String
        }

        schema {
            query: RootQuery
            mutation: RootMutation
        }
    `),
        rootValue: { //resolvers
            events: () => {
                return ['mock', 'test', 'cooking', 'coding']
            },
            createEvent: (args) => {
                const eventName = args.name;

                return eventName;
            }
        },
        graphiql: true //graphq query interface
    }));
const graphQlHttp = require('express-graphql');
...
```
