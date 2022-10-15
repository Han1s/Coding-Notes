# I. Getting Started

## 2. What is React native

- its an alternative to **react-DOM**
- its a collection of special **react components** that are compiled to native UI elements for other platforms
- it also exposes certain **APIs** like using the device camera etc.
- It is like **react-dom** but targets IOS and Android instead of Web browser



## 3. Join Online Learning Community

- https://academind.com/community/ - Discord



## 4. A look under the hood

- a normal react component will be compiled to **react native app**

```jsx
const App = props => {
    return (
    	<View>
            <Text>Hello there!</Text>
        </View>
    )
}
```

- components are compiled to elements for appropriate platforms

- the logic is run run by **JavaScript** thread hosted by **React Native** and its **Not compiled!**



## 5. Creating React Native projects - Expo CLI vs React Native CLI

- **EXPO CLI**
  - **Recommended**
  - 3rd party service
  - you get **managed app development** workflow
  - makes the process more convenient
  - you can leave the Expo whenever you need to
- **React native CLI**
  - Provided by React Native team
  - Bare-bone development setup (you need to do more setup)
  - Less convenience features
  - Easier to integrate with native source code

## 6. Create a new React Native Project

1. Download **NodeJS**
2. `npm install -g expo-cli`
   1. `expo` - try if its installed
   2. www.expo.dev contains documentation
3. `expo init AwesomeProject`

## 8. Running First App on the Real Device

- download **Expo** apk
- to install a simulator download **Android Studio** for an emulator on your local machine



# II. React Native Basics (Course Goals App)

## 13. Core Components & Components Styling

- Native elements like **h2** wont work in the native
  - **div** is **VIew** for examples
  - https://reactnative.dev/docs/components-and-apis
- Styling React Native Apps
  - There is no **css**
  - you can apply **inline styles** or with help of **StyleSheet Objects**.
    - Styling is therefore written in **JS**

## 14. Working With Core Components

- stricter than normal html
- Views are usually meant to hold boxes that form a component. Its a container



## 15. Styling React Native Apps

- **inline styles** or **StyleSheet Objects**
  - **SS object** provides validation and autocompletion
- written in JS
- based on CSS
- we use the **style** prop that is supported on some elements
- **The official styling documentation**: https://reactnative.dev/docs/style
- **The official article about colors**: https://reactnative.dev/docs/colors
- **The official API reference for different core components**: https://reactnative.dev/docs/view

```jsx
import { StyleSheet, Button, Text, View } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <View>
        <Text style={styles.dummyText}>Another piece of text</Text>
      </View>
      <Text style={styles.dummyText}>Hello world!</Text>
      <Button title="tap me!" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
  dummyText: {
    margin: 16,
    borderWidth: 2,
    borderColor: "red",
    padding: 16,
  },
});

```



## 18. Flexbox

- Layouts are typically created with Flexbox
- Very similar to css Flexbox
- Elements are positioned inside of containers
- Positioning is controlled via style setting applied to the containers

## 19. Using Flexbox to create layout

- cheatsheet: https://reactnative.dev/docs/flexbox
- in RN every **view** by default uses **FlexBox** and by default organizes them in **colum**

## 24. Differences between iOS and Android Styling

- native elements differ
- e.g. text elements might not have border radius in iOS
  - you can also wrap the element in a View to avoid it
- **The styles do not cascade!**

## 25. Making content Scrollable

- **by default the views are not scrollable!**
- good to check the component API with this one

## 26. Optimizing Lists with FlatList

- scrollView allways renders all the child elements, no matter how long of a list it is.
- A better solution is **FlatList**
  - the items are rendered as needed
  - flat list works well if youre putting a list of objects that have a key property

```jsx
import {
  StyleSheet,
  Button,
  Text,
  View,
  TextInput,
  ScrollView,
  FlatList,
} from "react-native";
import { useState } from "react";

export default function App() {
  const [enteredGoalText, setEnteredGoalText] = useState("");
  const [courseGoals, setCourseGoals] = useState([]);

  const goalInputHandler = (enteredText) => {
    setEnteredGoalText(enteredText);
  };

  const addGoalHandler = () => {
    setCourseGoals((prevCourseGoals) => [
      ...prevCourseGoals,
      {
        text: enteredGoalText,
        id: Math.random().toString(),
      },
    ]);
  };

  return (
    <View style={styles.appContainer}>
      <View style={styles.inputContainer}>
        <TextInput
          style={styles.textInput}
          placeholder="Your course goal"
          onChangeText={goalInputHandler}
        />
        <Button title="Add Goal" onPress={addGoalHandler} />
      </View>
      <View style={styles.goalsContainer}>
        <FlatList
          data={courseGoals}
          keyExtractor={(item, index) => item.id}
          renderItem={(itemData) => (
            <View style={styles.goalItem}>
              <Text style={styles.goalText}>{itemData.item.text}</Text>
            </View>
          )}
        />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  appContainer: {
    paddingTop: 50,
    paddingHorizontal: 16,
    flex: 1,
  },
  inputContainer: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
    marginBottom: 24,
    borderBottomWidth: 1,
    borderBottomColor: "grey",
  },
  textInput: {
    borderWidth: 1,
    borderColor: "#cccccc",
    width: "70%",
    marginRight: 8,
    padding: 8,
  },
  goalsContainer: {
    flex: 5,
  },
  goalItem: {
    margin: 8,
    padding: 8,
    borderRadius: 6,
    backgroundColor: "#5e0acc",
  },
  goalText: {
    color: "white",
  },
});

```

