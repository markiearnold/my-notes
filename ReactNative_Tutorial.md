# React Tutorial

[Turbo 360 | Learn Node, React, Redux with Real World Project Tutorials.](https://www.turbo360.co/tutorial/react-native---instagram)

## Setup

`react-native init AwesomeProject`

`cd AwesomeProject`

`react-native run-ios`


## Build Initial view
1. Scaffold View
Add folder `src/components/screens`

Add View1
```
import React, { Component } from 'react'
import {
  View,
  Text,
  StyleSheet,
} from 'react-native'

class ViewOne extends Component {

  constructor(props) {
    super(props);
    this.state = {
      example: false,
    };
  }

  render() {
    return (
      <View style={ styles.container }>
        <Text>Hello</Text>
      </View>
    )
  }

}

const styles = StyleSheet.create({
  container: {
    backgroundColor: "pink",
  },
})

export default ViewOne
```

add index.js
```
import ViewOne from './ViewOne';

export {
  ViewOne,
};
```


2. Show on main view

Update App.js
`import { ViewOne } from "./src/components/screens";`

update render
```
      <View style={styles.container}>
        <ViewOne />
      </View>
```

3. Add image

4. Add button
add `TouchableOpacity`

update render
```
        <TouchableOpacity
        onPress={() => alert('hi')}
      >
          <Text>Hello</Text>
        </TouchableOpacity>
```




## Build Second view
1. Duplicate ViewOne

Change references from `ViewOne` to `ViewTwo`

add `ViewTwo` to `index.js`

2. Switch Main to target view

`import { ViewOne, ViewTwo } from "./src/components/screens";`

update render
`<ViewTwo />`

4. Add text
5. Add image
6. Add button

## Add Navigation
1. Install

Visit [Getting started · React Navigation](https://reactnavigation.org/docs/en/getting-started.html)

Stop server and install
```
yarn add react-navigation
yarn add react-native-gesture-handler
react-native link react-native-gesture-handler
```

2. Create stack navigator

`import { createAppContainer, createStackNavigator } from 'react-navigation';`


3. Create routes
```
const RootStack = createStackNavigator(
  {
    ViewOne: {
      screen: ViewOne,
      navigationOptions: {
      },
    },
    ViewTwo: {
      screen: ViewTwo,
      navigationOptions: {
      },
    },
  }, {
    initialRouteName: 'ViewOne',
  }
);

const AppContainer = createAppContainer(RootStack);
```


4. Update render
`<AppContainer />`

5. Bring in withNavigation to ViewOne

`import { withNavigation } from 'react-navigation';`

& update the export

`export default withNavigation(ViewOne);`

Update our onPress

`this.props.navigation.push('ViewTwo', { data: 'Hello' })`			
