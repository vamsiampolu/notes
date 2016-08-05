Protip: Use throttle and debounce functions from 'lodash' to avoid continously performing expensive operations.

Protip: When using localStorage, wrap your code in try-catch to avoid errors

Protip: When using react-router, wrap your param in parenthesis to tell react-router that it is optional

Protip: Only have a single source of truth per each part of the application. For anything from the url, rely heavily
on react-router. For any state within the application, use redux.

Protip: Use withRouter to get the state from react-router wherever it is needed without having to pass it down from
the route handling component.

> To use withRouter and connect together, use atleast react-router 3.0

Protip: When colocating reducers and state selectors, use a named export starting with `get` for each selector.

Protip: Have a selector within the root reducer which forwards to selectors within nested reducer.

> This means that when you use a selector from the outside, you make no assumptions about the state of the reducer.

Protip: Treat your state as a lookup table and a list of valid ids that can be used with the lookup table.
Use multiple reducers for this, one to compute the state of each individual item, one to compute the state of the lookup table
and one to compute the list of all valid ids that can be used with the lookup table.

Nest combineReducers, let multiple reducers handle the same action.

Protip: Middleware just wraps dispatch, you can create middleware by wrapping dispatch without affecting it adversely.

Protip: When you need to fetch data when props change, use both componentDidMount and componentDidUpdat
