# Navigating without the navigation prop within [@react-navigation/native](https://github.com/react-navigation/react-navigation)

You can navigate with different screens from places where you do not have access to the `navigation` prop using the following method.

Create a Ref for accessing the navigation and attach it to the `NavigationContainer` element:

```javascript
import * as React from "react";
import { NavigationContainer } from "@react-navigation/native";

export const navigationRef = React.createRef();

export function navigate(name, params) {
  navigationRef.current?.navigate(name, params);
}

export default function App() {
  return (
    <NavigationContainer ref={navigationRef}>{/* ... */}</NavigationContainer>
  );
}
```

Now you can access this from anywhere, such as an `axios` interceptor or the likes:

```javascript
// any js module
import * as RootNavigation from "./path/to/RootNavigation.js";

// ...

RootNavigation.navigate("ChatScreen", { userName: "Lucy" });
```
