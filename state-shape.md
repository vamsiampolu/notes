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
  allIds:[UUID]
  byId:{
    [id]:{
      id:UUID,
      text:String,
      completed:Boolean
    }
  }
}
```
