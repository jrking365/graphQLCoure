# graphQLCourse

starter graphQL simple app

* Basic nodeJS app
Installing express, body-parser and nodemon

```bash
npm install --save express body-parser
npm install --save-dev nodemon
```

Creating a basic app, in app.js

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const app = express();
app.use(bodyParser.json())

app.get('/',(req,res,next)=>{
    res.send("Hello World");
})

app.listen(3000);
```

* Installeing graphql-express and graphql

```bash
npm install --save graphql-express graphql
```

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
```
