---
title: ReactNativeNavigation
date: 2020-07-06 14:27:12
tags: React-Native
---

npm install @react-navigation/native



npm install react-native-reanimated react-native-gesture-handler react-native-screens react-native-safe-area-context @react-native-community/masked-view(React-native-cli)



expo install react-native-gesture-handler react-native-reanimated react-native-screens react-native-safe-area-context @react-native-community/masked-view(Expo-cli)



Bare example:

*// In App.js in a new project*



import * as React from 'react';

import { View, Text } from 'react-native';

import { NavigationContainer } from '@react-navigation/native';

import { createStackNavigator } from '@react-navigation/stack';



function HomeScreen() {

  return (

​    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>

​      <Text>Home Screen</Text>

​    </View>

  );

}



const Stack = createStackNavigator();



function App() {

  return (

​    <NavigationContainer>

​      <Stack.Navigator>

​        <Stack.Screen name="Home" component={HomeScreen} />

​      </Stack.Navigator>

​    </NavigationContainer>

  );

}



export default App;





- React Native doesn't have a built-in API for navigation like a web browser does. React Navigation provides this for you, along with the iOS and Android gestures and animations to transition between screens.
- `Stack.Navigator` is a component that takes route configuration as its children with additional props for configuration and renders our content.
- Each `Stack.Screen` component take a `name` prop which refers to the name of the route and `component` prop which specifies the component to render for the route. These are the 2 required props.
- To specify what the initial route in a stack is, provide an `initialRouteName` as the prop for the navigator.
- To specify screen-specific options, we can pass an `options` prop to `Stack.Screen`, and for common options, we can pass `screenOptions` to `Stack.Navigator`







- `navigation.navigate('RouteName')` pushes a new route to the stack navigator if it's not already in the stack, otherwise it jumps to that screen.
- We can call `navigation.push('RouteName')` as many times as we like and it will continue pushing routes.
- The header bar will automatically show a back button, but you can programmatically go back by calling `navigation.goBack()`. On Android, the hardware back button just works as expected.
- You can go back to an existing screen in the stack with `navigation.navigate('RouteName')`, and you can go back to the first screen in the stack with `navigation.popToTop()`.
- The `navigation` prop is available to all screen components (components defined as screens in route configuration and rendered by React Navigation as a route).

