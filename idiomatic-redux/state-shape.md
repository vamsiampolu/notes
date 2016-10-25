Tracking the shape of the application state in idiomatic redux course.

+ At the beginning of the course, the state of the app looks like this:

```
{
  todos:[{
    id:Number,
    text:String,
    completed:Boolean
  }],
  visibilityFilter:'SHOW_ALL'
}
```

+ using a unique key to ensure that initial state can be loaded from localStorage:

```
{
  todos:[
    {
      id:UUID,
      text: String,
      completed: Boolean
    }
  ]
}
```

+ visibiltyFilter is now available as a param on the url, so we can remove the piece of state

```
{
  todos:[
    {
      id:UUID,
      text:String,
      completed:Boolean
    }
  ]
}
```

+ normalize the state of the todo reducer to a map of ids to todos:

```
{
  todos: {
    allIds:[UUID]
    byId:{
      [id]:{
        id:UUID,
        text:String,
        completed:Boolean
      }
    }
  }
  }
```

+ when fetching data from the server, instead of maintaining a list of all ids as a single array, have a list of ids for each filter

> allIds is replaced with idsByFilter

> all the lists live in idsByFilter which means that we can add or remove filters easily. as we fetch data for each filter, the corresponding list
gets updated



```
{
  todos:{
    {
      idsByFilter:{
        all:[UUID],
        active:[UUID],
        completed:[UUID]
      },
        allIds:{
          [id]:{
            id:UUID,
            text:String,
            completed:Boolean
          }
        }
      }
    }
  }
}
```

Interestingly, while getting to this state


+ something like this is used:

```
function byId(state = {},action) {
  switch(action.type) {
    case RECIEVE_TODOS:{
      let nextState = {...state}
      action.response.forEach(todo => (
          {
            [todo.id]:todo
          }
        )
      )
    }
  }
}
```


+ to mean something like this:

```
const recievedTodo = ({
  id,
  text,
  completed
}) => (
  {
    [id]:{
      id,
      text,
      completed
    }
  }
)


const recievedTodos = ({
  response:todos
}) => todos.reduce(state,todo => (
      {
        ...state,
        ...recievedTodo(todo)
      }),
  {}
)

function byId(state = {},action) {
  switch(action.type) {
    case RECIEVE_TODOS: {
      const recievedState = recievedTodos(action)

      const nextState = {
        ...state,
        ...recievedState
      }
      return nextState;

    }
  }
}
```

except that Dan Abramov's version is simple, concise and easy to read.

This means that any todos that change are replaced and any new todos are added. The todos that are not affected are already there.

+ Remove `todos` and flatten the state shape:

```
{
  byId:{
    [id]:{
      id:UUID,
      text:String,
      completed:Boolean
    }
  },
  listByFilter:{
    ids:[UUID],
    isFetching:Boolean
  }
}
```
