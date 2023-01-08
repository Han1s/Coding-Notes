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
- in RN every **view** by default uses **FlexBox** and by default organizes them in **colum**n

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

## 30. Make items pressable

```jsx
        <Pressable onPress={props.onDeleteItem}>
            <View style={styles.goalItem}>
                <Text style={styles.goalText}>{props.text}</Text>
            </View>
        </Pressable>
```

## 31. Add Ripple effect

```jsx
import {Text, View} from "react-native";
import {StyleSheet} from "react-native";
import Pressable from "react-native/Libraries/Components/Pressable/Pressable";

const GoalItem = (props) => {
    return (
        <View style={styles.goalItem}>
            <Pressable
                android_ripple={{color: '#210644'}}  // Android solution, move padding to text to actually spread the entire component
                onPress={() => props.onDeleteItem(props.id)}
                // Object destruct. Ios Solution. pressed is provided via pressable
                style={({pressed}) => pressed && styles.pressedItem}> 
                <Text style={styles.goalText}>{props.text}</Text>
            </Pressable>
        </View>
    );
};

const styles = StyleSheet.create({
    goalItem: {
        margin: 8,
        borderRadius: 6,
        backgroundColor: "#5e0acc",
    },
    pressedItem: {
      opacity: 0.5
    },
    goalText: {
        padding: 8,
        color: "white",
    },
});

export default GoalItem;
```

## 33. Modal

```jsx
    <Modal visible={props.visible} animationType="slide">
      <View style={styles.inputContainer}>
        <TextInput
          value={enteredGoalText}
          style={styles.textInput}
          placeholder="Your course goal"
          onChangeText={goalInputHandler}
        />
        <Button title="Add Goal" onPress={addGoalHandler} />
      </View>
    </Modal>
```

## 35. Adding images

```jsx
        <Image
          style={styles.image}
          source={require("../assets/images/goal.png")}
        />
```

## 37. Finishing Touches

To edit **status bar:**

```jsx
return (
    <>
      <StatusBar style="light" />
      <View style={styles.appContainer}>
        <Button
          title="Add New Goal"
          color="#a065ec"
          onPress={startAddGoalHandler}
        />
        <GoalInput
          onAddGoal={addGoalHandler}
          visible={modalIsVisible}
          onCancel={endAddGoalHandler}
        />
        <View style={styles.goalsContainer}>
          <FlatList
            data={courseGoals}
            keyExtractor={(item, index) => item.id}
            renderItem={(itemData) => (
              <GoalItem
                id={itemData.item.id}
                onDeleteItem={deleteGoalHandler}
                text={itemData.item.text}
              />
            )}
          />
        </View>
      </View>
    </>
  );
```



to change background of the entire **app** go to the **/app.json**

```json
{
  "expo": {
    "name": "RNCourse",
    "slug": "RNCourse",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "backgroundColor": "#1e085a",
    "userInterfaceStyle": "light",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "updates": {
      "fallbackToCacheTimeout": 0
    },
    "assetBundlePatterns": ["**/*"],
    "ios": {
      "supportsTablet": true
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#FFFFFF"
      }
    },
    "web": {
      "favicon": "./assets/favicon.png"
    }
  }
}

```

# III. Debugging React Native Apps

- logging to the **console**
- debug **remotely**
- **react DevTools**

## 42. Debugging remotely

- if you press **?** in expo terminal, you get the list of commands
- you can open **menu** by pressing **m**
  - remote debugging then opens the special chrome tab

## 43. Use React Dev tools

- `npm install -g react-devtools`  installs devtools on the computer
- `react-devtools` runs the **devtools**
- you can then open the menu and trigger remote debugging to open the component tree

# IV. Deep Dive into Components, Layouts, Styling

## 48. Adding Shadows

```jsx
const styles = StyleSheet.create({
   inputContainer: {
       padding: 16,
       marginTop: 100,
       marginHorizontal: 24,
       borderRadius: 8,
       backgroundColor: '#72063c',
       elevation: 4, // Android
       shadowColor: 'black', // rest down is IOS
       shadowOffset: {
           width: 2,
           height:2,
       },
       shadowRadius: 6,
       shadowOpacity: 0.25
   }
});
```

## 51. Tuning the input

```jsx
import React from 'react';
import {StyleSheet, TextInput, View} from "react-native";
import PrimaryButton from "../components/PrimaryButton";

const StartGameScreen = () => {
    return (
        <View style={styles.inputContainer}>
            <TextInput
                style={styles.numberInput}
                maxLength={2}
                keyboardType="number-pad"  // only show number pad
                autoCapitalize="none"  // dont capitalize
                autoCorrect={false}  // dont autocorrect
            />
            <PrimaryButton>Reset</PrimaryButton>
            <PrimaryButton>Confirm</PrimaryButton>
        </View>
    );
};

export default StartGameScreen;

const styles = StyleSheet.create({
    inputContainer: {
        padding: 16,
        marginTop: 100,
        marginHorizontal: 24,
        borderRadius: 8,
        backgroundColor: '#72063c',
        elevation: 4,
        shadowColor: 'black',
        shadowOffset: {
            width: 2,
            height: 2,
        },
        shadowRadius: 6,
        shadowOpacity: 0.25
    },
    numberInput: {
        height: 50,
        fontSize: 32,
        borderBottomColor: '#ddb52f',
        borderBottomWidth: 2,
        color: '#ddb52f',
        marginVertical: 8,
        fontWeight: "bold",
        width: 50,
        textAlign: 'center'
    }
});
```

## 52. Styling custom button

```jsx
import React from 'react';
import {Pressable, Text, View, StyleSheet} from "react-native";

const PrimaryButton = ({children}) => {
    const pressHandler = () => {
        console.log('pressed');
    }

    return (
        <View style={styles.buttonOuterContainer}>
            <Pressable
                onPress={pressHandler}
                style={({pressed}) => pressed
                    ? [styles.buttonInnerContainer, styles.pressed]
                    : styles.buttonInnerContainer}
                android_ripple={{color: "#640233"}}>
                <Text style={styles.buttonText}>{children}</Text>
            </Pressable>
        </View>
    );
};

export default PrimaryButton;

const styles = StyleSheet.create({
    buttonOuterContainer: {
        borderRadius: 28,
        margin: 4,
        overflow: 'hidden'
    },
    buttonInnerContainer: {
        backgroundColor: '#72063c',
        paddingVertical: 8,
        paddingHorizontal: 16,
        elevation: 2,
    },
    buttonText: {
        color: 'white',
        textAlign: 'center'
    },
    pressed: {  // IOS solution
        opacity: 0.75
    }
})
```

## 55. Adding Linear Gradient

`expo install expo-linear-gradient`

```jsx
import {StyleSheet, View} from 'react-native';
import StartGameScreen from "./screens/StartGameScreen";
import {LinearGradient} from "expo-linear-gradient";

export default function App() {
  return (
    <LinearGradient colors={['#4e0329', '#ddb52f']} style={styles.rootScreen}>
      <StartGameScreen />
    </LinearGradient>
  );
}

const styles = StyleSheet.create({
  rootScreen: {
    flex: 1,
  }
});
```

## 56. Adding Image + Gradient

```jsx
import {StyleSheet, ImageBackground} from 'react-native';
import StartGameScreen from "./screens/StartGameScreen";
import {LinearGradient} from "expo-linear-gradient";

export default function App() {
    return (
        <LinearGradient colors={['#4e0329', '#ddb52f']} style={styles.rootScreen}>
            <ImageBackground
                source={require('./assets/images/background.png')}
                resizeMode={"cover"}
                style={styles.rootScreen}
                imageStyle={styles.backgroundImage}
            >
                <StartGameScreen/>
            </ImageBackground>
        </LinearGradient>
    );
}

const styles = StyleSheet.create({
    rootScreen: {
        flex: 1,
    },
    backgroundImage: {
        opacity: 0.15
    }
});
```

## 61. SafeAreaView

- to make sure the content is not under the notch.
- currently not supported on android

```jsx
    rootScreen: {
        flex: 1,
        paddingTop: StatusBar.currentHeight
    },
```

## 63. Managing Colors globally

```jsx
// /constants/colors.js
const Colors = {
  primary500: '#72063c',
  primary600: '#640233',
  primary700: '#4e0329',
  primary800: '#3b021f',
  accent500: '#ddb52f'
};

export default Colors;
```

## 69. Icons

- use **expo/vector-icons**
- already installed in expo
- **ionicons** are nice

```jsx
import React, {useEffect, useState} from "react";
import {Alert, StyleSheet, View} from "react-native";
import Title from "../components/UI/Title";
import NumberContainer from "../components/Game/NumberContainer";
import PrimaryButton from "../components/UI/PrimaryButton";
import Card from "../components/UI/Card";
import InstructionText from "../components/UI/InstructionText";
import { Ionicons } from "@expo/vector-icons";

function generateRandomBetween(min, max, exclude) {
    const rndNum = Math.floor(Math.random() * (max - min)) + min;

    if (rndNum === exclude) {
        return generateRandomBetween(min, max, exclude);
    } else {
        return rndNum;
    }
}

let minBoundary = 1;
let maxBoundary = 100;

const GameScreen = ({userNumber, onGameOver}) => {
    const initialGuess = generateRandomBetween(1, 100, userNumber)
    const [currentGuess, setCurrentGuess] = useState(initialGuess);

    useEffect(() => {
        if (currentGuess === userNumber) {
            onGameOver();
        }
    }, [currentGuess, userNumber, onGameOver]);


    const nextGuessHandler = (direction) => {
        if ((direction === 'lower' && currentGuess < userNumber) ||
        (direction === 'greater' && currentGuess > userNumber)) {
            Alert.alert(
                'Dont lie!',
                'You know that this is wrong',
                [{text: 'Sorry!', style: 'cancel'}]
            )
            return;
        }

        if (direction === 'lower') {
            maxBoundary = currentGuess;
        } else {
            minBoundary = currentGuess + 1;
        }

        const newRndNumber = generateRandomBetween(minBoundary, maxBoundary, currentGuess);
        setCurrentGuess(newRndNumber);
    }

    return (
        <View style={styles.screen}>
            <Title>Opponent's Guess</Title>
            <NumberContainer>{currentGuess}</NumberContainer>
            <Card>
                <InstructionText style={styles.instructionText}>Higher or lower?</InstructionText>
                <View style={styles.buttonsContainer}>
                    <View style={styles.buttonContainer}>
                        <PrimaryButton onPress={() => nextGuessHandler('lower')}>
                            <Ionicons name={"md-remove"} size={24} color={"white"} />
                        </PrimaryButton>
                    </View>
                    <View style={styles.buttonContainer}>
                        <PrimaryButton onPress={() => nextGuessHandler('greater')}>
                            <Ionicons name={"md-add"} size={24} color={"white"} />
                        </PrimaryButton>
                    </View>
                </View>
            </Card>
            {/*<View>LOG ROUNDS</View>*/}
        </View>
    );
};

export default GameScreen;

const styles = StyleSheet.create({
    screen: {
        flex: 1,
        paddingHorizontal: 24
    },
    instructionText: {
      marginBottom: 12
    },
    buttonsContainer: {
        flexDirection: 'row'
    },
    buttonContainer: {
        flex: 1
    }
})
```

## 70. Custom fonts

- `expo install expo-font`
  - add into **/assets/fonts** folder.
- `expo install expo-app-loading`
  - loading package

```jsx
import {StyleSheet, ImageBackground, SafeAreaView, StatusBar, View} from 'react-native';
import StartGameScreen from "./screens/StartGameScreen";
import {LinearGradient} from "expo-linear-gradient";
import {useState} from "react";
import GameScreen from "./screens/GameScreen";
import Colors from "./constants/colors";
import GameOverScreen from "./screens/GameOverSreen";
import {useFonts} from "expo-font";
import AppLoading from "expo-app-loading";

export default function App() {
    const [userNumber, setUserNumber] = useState(null);
    const [gameIsOver, setGameOver] = useState(true);

    const [fontsLoaded] = useFonts({
        'open-sans': require('./assets/fonts/OpenSans-Regular.ttf'),
        'open-sans-bold': require('./assets/fonts/OpenSans-Bold.ttf'),
    })

    if (!fontsLoaded) {
        return <AppLoading />
    }

    const pickedNumberHandler = (pickedNumber) => {
        setUserNumber(pickedNumber);
        setGameOver(false)
    }

    const gameOverHandler = () => {
        setGameOver(true);
    }

    let screen = <StartGameScreen onPickNumber={pickedNumberHandler} />;

    if (userNumber) {
        screen = (
            <GameScreen userNumber={userNumber} onGameOver={gameOverHandler}/>
        )
    }

    if (gameIsOver && userNumber) {
        screen = (
            <GameOverScreen />
        )
    }

    return (
        <LinearGradient colors={[Colors.primary700, Colors.accent500]} style={styles.rootScreen}>
            <ImageBackground
                source={require('./assets/images/background.png')}
                resizeMode={"cover"}
                style={styles.rootScreen}
                imageStyle={styles.backgroundImage}
            >
                <View style={styles.rootScreen}>
                    {screen}
                </View>
            </ImageBackground>
        </LinearGradient>
    );
}

const styles = StyleSheet.create({
    rootScreen: {
        flex: 1,
        paddingTop: StatusBar.currentHeight
    },
    backgroundImage: {
        opacity: 0.15
    },
});
```

## 71. Using and styling nested text

- just pass styles down the props and use them at the end of the array to cascade



# V. Building Adaptive User Interfaces

- use **maxWidth** - it always refers to the parent container when setting it on element

## 81. Dimensions API

```jsx
import React from 'react';
import {Text, View, StyleSheet, Dimensions} from "react-native";
import Colors from "../../constants/colors";

const NumberContainer = ({children}) => {
    return (
        <View style={styles.container}>
            <Text style={styles.numberText}>
                {children}
            </Text>
        </View>
    );
};

export default NumberContainer;

const deviceWidth = Dimensions.get('window').width

const styles = StyleSheet.create({
    container: {
        borderWidth: 4,
        borderColor: Colors.accent500,
        padding: deviceWidth < 380 ? 12 : 24,
        margin: deviceWidth < 380 ? 12 : 24,
        borderRadius: 8,
        alignItems: 'center',
        justifyContent: 'center'
    },
    numberText: {
        color: Colors.accent500,
        fontSize: deviceWidth < 380 ? 28 : 36,
        fontFamily: 'open-sans-bold'
    }
})
```

## 83. Screen Orientation

- you have to set **orientation** in **/app.json**
- **dimensions** api is only executed once, so it fails if you swithc orientation

## 84. Dynamic Dimensions

- use **useWindowDimensions**

```jsx
import React, {useState} from 'react';
import {StyleSheet, TextInput, View, Alert, Text, Dimensions, useWindowDimensions} from "react-native";
import PrimaryButton from "../components/UI/PrimaryButton";
import Colors from "../constants/colors";
import Title from "../components/UI/Title";
import Card from "../components/UI/Card";
import InstructionText from "../components/UI/InstructionText";

const StartGameScreen = ({onPickNumber}) => {
    const [enteredNumber, setEnteredNumber] = useState('');

    const { width, height } = useWindowDimensions();

    const numberInputHandler = (enteredText) => {
        setEnteredNumber(enteredText);
    }

    const resetInputHandler = () => {
        setEnteredNumber('')
    }

    const confirmInputHandler = () => {
        const chosenNumber = parseInt(enteredNumber);

        if (isNaN(chosenNumber) || chosenNumber <= 0 || chosenNumber > 99) {
            Alert.alert(
                'Invalid number!',
                'Number has to be a number between 1 and 99',
                [{text: 'Okay', style: "destructive", onPress: resetInputHandler}])
            return;
        }

        onPickNumber(chosenNumber);
    }

    const marginTopDistance = height < 400 ? 0 : 30;

    return (
        <View style={[styles.rootContainer, {marginTop: marginTopDistance}]}>
            <Title>Guess My Number</Title>
            <Card>
                <InstructionText>Enter a Number</InstructionText>
                <TextInput
                    style={styles.numberInput}
                    maxLength={2}
                    keyboardType="number-pad"
                    autoCapitalize="none"
                    autoCorrect={false}
                    onChangeText={numberInputHandler}
                    value={enteredNumber}
                />
                <View style={styles.buttonsContainer}>
                    <View style={styles.buttonContainer}>
                        <PrimaryButton onPress={resetInputHandler}>Reset</PrimaryButton>
                    </View>
                    <View style={styles.buttonContainer}>
                        <PrimaryButton onPress={confirmInputHandler}>Confirm</PrimaryButton>
                    </View>
                </View>
            </Card>
        </View>
    );
};

export default StartGameScreen;

// const deviceHeight = Dimensions.get('window').height;

const styles = StyleSheet.create({
    rootContainer: {
        flex: 1,
        // marginTop: deviceHeight < 400 ? 0 : 30
        alignItems: 'center'
    },
    numberInput: {
        height: 50,
        fontSize: 32,
        borderBottomColor: Colors.accent500,
        borderBottomWidth: 2,
        color: Colors.accent500,
        marginVertical: 8,
        fontWeight: "bold",
        width: 50,
        textAlign: 'center'
    },
    buttonsContainer: {
        flexDirection: 'row'
    },
    buttonContainer: {
        flex: 1
    }
});
```

## 85. Keyboard Avoiding View

```jsx
import React, {useState} from 'react';
import {Alert, KeyboardAvoidingView, ScrollView, StyleSheet, TextInput, useWindowDimensions, View} from "react-native";
import PrimaryButton from "../components/UI/PrimaryButton";
import Colors from "../constants/colors";
import Title from "../components/UI/Title";
import Card from "../components/UI/Card";
import InstructionText from "../components/UI/InstructionText";

const StartGameScreen = ({onPickNumber}) => {
    const [enteredNumber, setEnteredNumber] = useState('');

    const {width, height} = useWindowDimensions();

    const numberInputHandler = (enteredText) => {
        setEnteredNumber(enteredText);
    }

    const resetInputHandler = () => {
        setEnteredNumber('')
    }

    const confirmInputHandler = () => {
        const chosenNumber = parseInt(enteredNumber);

        if (isNaN(chosenNumber) || chosenNumber <= 0 || chosenNumber > 99) {
            Alert.alert(
                'Invalid number!',
                'Number has to be a number between 1 and 99',
                [{text: 'Okay', style: "destructive", onPress: resetInputHandler}])
            return;
        }

        onPickNumber(chosenNumber);
    }

    const marginTopDistance = height < 400 ? 0 : 30;

    return (
        <ScrollView style={styles.screen}>
            <KeyboardAvoidingView style={styles.screen} behavior={"position"}>
                <View style={[styles.rootContainer, {marginTop: marginTopDistance}]}>
                    <Title>Guess My Number</Title>
                    <Card>
                        <InstructionText>Enter a Number</InstructionText>
                        <TextInput
                            style={styles.numberInput}
                            maxLength={2}
                            keyboardType="number-pad"
                            autoCapitalize="none"
                            autoCorrect={false}
                            onChangeText={numberInputHandler}
                            value={enteredNumber}
                        />
                        <View style={styles.buttonsContainer}>
                            <View style={styles.buttonContainer}>
                                <PrimaryButton onPress={resetInputHandler}>Reset</PrimaryButton>
                            </View>
                            <View style={styles.buttonContainer}>
                                <PrimaryButton onPress={confirmInputHandler}>Confirm</PrimaryButton>
                            </View>
                        </View>
                    </Card>
                </View>
            </KeyboardAvoidingView>
        </ScrollView>
    );
};

export default StartGameScreen;

// const deviceHeight = Dimensions.get('window').height;

const styles = StyleSheet.create({
    rootContainer: {
        flex: 1,
        // marginTop: deviceHeight < 400 ? 0 : 30
        alignItems: 'center'
    },
    numberInput: {
        height: 50,
        fontSize: 32,
        borderBottomColor: Colors.accent500,
        borderBottomWidth: 2,
        color: Colors.accent500,
        marginVertical: 8,
        fontWeight: "bold",
        width: 50,
        textAlign: 'center'
    },
    buttonsContainer: {
        flexDirection: 'row'
    },
    buttonContainer: {
        flex: 1
    },
    screen: {
        flex: 1
    }
});
```

## 86. Improving the landscape mode UI

```jsx
import React, {useState} from 'react';
import {Alert, KeyboardAvoidingView, ScrollView, StyleSheet, TextInput, useWindowDimensions, View} from "react-native";
import PrimaryButton from "../components/UI/PrimaryButton";
import Colors from "../constants/colors";
import Title from "../components/UI/Title";
import Card from "../components/UI/Card";
import InstructionText from "../components/UI/InstructionText";

const StartGameScreen = ({onPickNumber}) => {
    const [enteredNumber, setEnteredNumber] = useState('');

    const {width, height} = useWindowDimensions();

    const numberInputHandler = (enteredText) => {
        setEnteredNumber(enteredText);
    }

    const resetInputHandler = () => {
        setEnteredNumber('')
    }

    const confirmInputHandler = () => {
        const chosenNumber = parseInt(enteredNumber);

        if (isNaN(chosenNumber) || chosenNumber <= 0 || chosenNumber > 99) {
            Alert.alert(
                'Invalid number!',
                'Number has to be a number between 1 and 99',
                [{text: 'Okay', style: "destructive", onPress: resetInputHandler}])
            return;
        }

        onPickNumber(chosenNumber);
    }

    const marginTopDistance = height < 400 ? 0 : 30;

    return (
        <ScrollView style={styles.screen}>
            <KeyboardAvoidingView style={styles.screen} behavior={"position"}>
                <View style={[styles.rootContainer, {marginTop: marginTopDistance}]}>
                    <Title>Guess My Number</Title>
                    <Card>
                        <InstructionText>Enter a Number</InstructionText>
                        <TextInput
                            style={styles.numberInput}
                            maxLength={2}
                            keyboardType="number-pad"
                            autoCapitalize="none"
                            autoCorrect={false}
                            onChangeText={numberInputHandler}
                            value={enteredNumber}
                        />
                        <View style={styles.buttonsContainer}>
                            <View style={styles.buttonContainer}>
                                <PrimaryButton onPress={resetInputHandler}>Reset</PrimaryButton>
                            </View>
                            <View style={styles.buttonContainer}>
                                <PrimaryButton onPress={confirmInputHandler}>Confirm</PrimaryButton>
                            </View>
                        </View>
                    </Card>
                </View>
            </KeyboardAvoidingView>
        </ScrollView>
    );
};

export default StartGameScreen;

// const deviceHeight = Dimensions.get('window').height;

const styles = StyleSheet.create({
    rootContainer: {
        flex: 1,
        // marginTop: deviceHeight < 400 ? 0 : 30
        alignItems: 'center'
    },
    numberInput: {
        height: 50,
        fontSize: 32,
        borderBottomColor: Colors.accent500,
        borderBottomWidth: 2,
        color: Colors.accent500,
        marginVertical: 8,
        fontWeight: "bold",
        width: 50,
        textAlign: 'center'
    },
    buttonsContainer: {
        flexDirection: 'row'
    },
    buttonContainer: {
        flex: 1
    },
    screen: {
        flex: 1
    }
});
```

## 88. Platform-specific Code with Platform API

```jsx
import React from 'react';
import {Platform, StyleSheet, Text} from "react-native";
import Colors from "../../constants/colors";

const Title = ({children}) => {
    return (
        <Text style={styles.title}>{children}</Text>
    );
};

const styles = StyleSheet.create({
    title: {
        fontFamily: 'open-sans-bold',
        fontSize: 24,
        color: 'white',
        width: '80%',
        textAlign: 'center',
        // borderWidth: Platform.OS === 'android' ? 0 : 2,
        borderWidth: Platform.select({  // as well
            ios: 2,
            android: 0
        }),
        borderColor: 'white',
        padding: 12,
        maxWidth: '80%'
    }
})

export default Title;

```

- You can also name file **[component].ios.js** or **[component].android.js** and RN will import it according to the platform
- you can do the same with **colors** as well

## 89. StatusBar

```jsx
import {ImageBackground, StatusBar, StyleSheet, View} from 'react-native';
import StartGameScreen from "./screens/StartGameScreen";
import {LinearGradient} from "expo-linear-gradient";
import {useState} from "react";
import GameScreen from "./screens/GameScreen";
import Colors from "./constants/colors";
import GameOverScreen from "./screens/GameOverSreen";
import {useFonts} from "expo-font";
import AppLoading from "expo-app-loading";

export default function App() {
    const [userNumber, setUserNumber] = useState(null);
    const [gameIsOver, setGameOver] = useState(true);
    const [guessRounds, setGuessRounds] = useState(0);

    const [fontsLoaded] = useFonts({
        'open-sans': require('./assets/fonts/OpenSans-Regular.ttf'),
        'open-sans-bold': require('./assets/fonts/OpenSans-Bold.ttf'),
    })

    if (!fontsLoaded) {
        return <AppLoading/>
    }

    const pickedNumberHandler = (pickedNumber) => {
        setUserNumber(pickedNumber);
        setGameOver(false)
    }

    const gameOverHandler = (numberOfRounds) => {
        setGameOver(true);
        setGuessRounds(numberOfRounds);
    }

    const startNewGameHandler = () => {
        setUserNumber(null);
        setGuessRounds(0);
    }

    let screen = <StartGameScreen onPickNumber={pickedNumberHandler}/>;

    if (userNumber) {
        screen = (
            <GameScreen userNumber={userNumber} onGameOver={gameOverHandler}/>
        )
    }

    if (gameIsOver && userNumber) {
        screen = (
            <GameOverScreen
                userNumber={userNumber}
                roundsNumber={guessRounds}
                onStartNewGame={startNewGameHandler}
            />
        )
    }

    return (
        <>
            <StatusBar style={'light'} />
            <LinearGradient colors={[Colors.primary700, Colors.accent500]} style={styles.rootScreen}>
                <ImageBackground
                    source={require('./assets/images/background.png')}
                    resizeMode={"cover"}
                    style={styles.rootScreen}
                    imageStyle={styles.backgroundImage}
                >
                    <View style={styles.rootScreen}>
                        {screen}
                    </View>
                </ImageBackground>
            </LinearGradient>
        </>
    );
}

const styles = StyleSheet.create({
    rootScreen: {
        flex: 1,
        paddingTop: StatusBar.currentHeight
    },
    backgroundImage: {
        opacity: 0.15
    },
});
```

# VI. Navigation

## 93. Displaying items in a grid

- use **numColumns** property in a **FlatList** component

## 94. Navigation Package

- **react navigation** package

  ```bash
  npm install @react-navigation/native
  ```

  ```bash
  npx expo install react-native-screens react-native-safe-area-context
  ```

- choose one of the navigators (**stack**, **native stack**, etc.)
  ```bash
  expo install @react-navigation/native-stack
  ```
  
  - the first child is used as the home page by default

```jsx
import {StatusBar} from 'expo-status-bar';
import {StyleSheet} from 'react-native';
import CategoriesScreen from "./screens/CategoriesScreen";
import {NavigationContainer} from '@react-navigation/native';
import { createNativeStackNavigator} from "@react-navigation/native-stack";

const Stack = createNativeStackNavigator();

export default function App() {
    return (
        <>
            <StatusBar style={'dark'}/>
            <NavigationContainer>
                <Stack.Navigator>
                    <Stack.Screen name="MealsCategories" component={CategoriesScreen}/>
                </Stack.Navigator>
            </NavigationContainer>
        </>
    );
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#fff',
        alignItems: 'center',
        justifyContent: 'center',
    },
});
```



## 95. Implementing Navigation Between Two Screens

```jsx
import React from 'react';

import {CATEGORIES} from "../data/dummy-data";
import {FlatList} from "react-native";
import CategoryGridTile from "../components/CategoryGridTile";

const CategoriesScreen = ({navigation}) => {

    const renderCategoryItem = (itemData) => {
        return (
            <CategoryGridTile title={itemData.item.title} color={itemData.item.color} onPress={() => {
                navigation.navigate('MealsOverview')
            }}/>
        )
    }

    return (
        <FlatList
            data={CATEGORIES}
            renderItem={renderCategoryItem}
            numColumns={2}
            keyExtractor={(item) => item.id}/>
    );
};

export default CategoriesScreen;
```



## 97. Using useNavigation Hook

- with **stack navigation** you push the page on top of the stack and then you can go back.
- **native stack** uses native elements for this, and it should be the preference
  - in case of problem you can fall back to **stack** navigation

``` jsx
import React from 'react';
import {Platform, Pressable, StyleSheet, Text, View} from "react-native";
import { useNavigation } from "@react-navigation/native";

const CategoryGridTile = ({title, color, onPress}) => {
    const navigation = useNavigation(); // gives you the access to navigation if you wanna navigate from the component that is not registered as a screen

    return (
        <View style={[styles.gridItem]}>
            <Pressable
                onPress={onPress}
                android_ripple={{color: '#ccc'}}
                style={({pressed}) => [styles.button, pressed ? styles.buttonPressed : null]}>
                <View style={[styles.innerContainer, {backgroundColor: color}]}>
                    <Text style={styles.title}>
                        {title}
                    </Text>
                </View>
            </Pressable>
        </View>
    );
};

export default CategoryGridTile;

const styles = StyleSheet.create({
    gridItem: {
        flex: 1,
        margin: 16,
        height: 150,
        borderRadius: 8,
        elevation: 4,
        shadowColor: 'black',
        shadowOpacity: 0.25,
        backgroundColor: 'white',
        shadowOffset: {
            width: 0,
            height: 2
        },
        shadowRadius: 8,
        overflow: Platform.OS === 'android' ? 'hidden' : 'visible',
    },
    button: {
        flex: 1
    },
    buttonPressed: {
        opacity: 0.5
    },
    innerContainer: {
        flex: 1,
        borderRadius: 8,
        padding: 16,
        justifyContent: "center",
        alignItems: 'center'
    },
    title: {
        fontWeight: 'bold',
        fontSize: 18
    }
});
```



## 98. pass data between screens

```jsx
    const renderCategoryItem = (itemData) => {
        return (
            <CategoryGridTile title={itemData.item.title} color={itemData.item.color} onPress={() => {
                navigation.navigate('MealsOverview', {
                    categoryId: itemData.item.id,
                })
            }}/>
        )
    }
```

```jsx
import React from 'react';
import { MEALS } from "../data/dummy-data";
import {Text, View, StyleSheet} from "react-native";

const MealsOverviewScreen = ({ route }) => {
    const { categoryId } = route.params;

    return (
        <View style={styles.container}>
            <Text>Meals Overview Screen = {categoryId}</Text>
        </View>
    );
};

export default MealsOverviewScreen;

const styles = StyleSheet.create({
    container: {
        flex: 1,
        padding: 16
    }
})

```

- alternatively use **useRoute** hook

## 101. Styling Screen Headers and backgrounds

```jsx
export default function App() {
    return (
        <>
            <StatusBar style={'dark'}/>
            <NavigationContainer>
                <Stack.Navigator screenOptions={{ // GLOBAL
                    headerStyle: {backgroundColor: '#351401'},
                    headerTintColor: 'white',
                    contentStyle: {
                        backgroundColor: '#351401'
                    }
                }}>
                    <Stack.Screen
                        options={{
                            title: 'All Categories',
                            // headerStyle: {backgroundColor: '#351401'}, // INDIVIDUAL
                            // headerTintColor: 'white',
                            // contentStyle: {
                            //     backgroundColor: '#351401'
                            // }
                        }}
                        name="MealsCategories"
                        component={CategoriesScreen}/>
                    <Stack.Screen name="MealsOverview" component={MealsOverviewScreen}/>
                </Stack.Navigator>
            </NavigationContainer>
        </>
    );
}
```

## 102. Setting navigation options dynamically

```jsx
<Stack.Screen
    name="MealsOverview"
    component={MealsOverviewScreen}
    // options={({navigation, route}) => {
    //     const catId = route.params.categoryId;
    //     return {
    //         title: catId
    //     }}}
    />
```

Option 2:

```jsx
import React, {useLayoutEffect} from 'react';
import {CATEGORIES, MEALS} from "../data/dummy-data";
import {FlatList, StyleSheet, View} from "react-native";
import MealItem from "../components/MealItem";

const MealsOverviewScreen = ({route, navigation}) => {
    const {categoryId} = route.params;

    useLayoutEffect(() => { // HERE
        const categoryTitle = CATEGORIES.find((category) => category.id === categoryId).title;

        navigation.setOptions({
            title: categoryTitle
        })
    }, [categoryId, navigation])

    const displayedMeals = MEALS.filter((mealItem) => {
        return mealItem.categoryIds.includes(categoryId)
    })

    const renderMealItem = (itemData) => {
        const item = itemData.item
        const mealItemProps = {
            title: item.title,
            imageUrl: item.imageUrl,
            affordability: item.affordability,
            complexity: item.complexity,
            duration: item.duration
        }

        return (
            <MealItem {...mealItemProps} />
        )
    }

    return (
        <View style={styles.container}>
            <FlatList
                keyExtractor={(item) => item.id}
                data={displayedMeals}
                renderItem={renderMealItem}
            />
        </View>
    );
};

export default MealsOverviewScreen;

const styles = StyleSheet.create({
    container: {
        flex: 1,
        padding: 16
    }
})
```

## 106. Adding buttons to the header

- **option 1**: Good when you dont need to access the state cause it will be in the root component

```jsx
                    <Stack.Screen name={'MealDetail'}
                                  component={MealDetailScreen}
                                  // options={{
                                  //     headerRight: () => {
                                  //         return (
                                  //             <Button title={'Tap me!'} onPress={}/>
                                  //         )
                                  //     }
                                  // }}
                    />
```

- **option 2**:

```jsx
const MealDetailScreen = ({route, navigation}) => {
    const mealId = route.params.mealId;

    const selectedMeal = MEALS.find((meal) => meal.id === mealId);

    const headerButtonpresshandler = () => {
        console.log('pressed');
    }

    // add button
    useLayoutEffect(() => {
        navigation.setOptions({
            headerRight: () => (
                <Button title={'tap'} onPress={headerButtonpresshandler}/>
            )
        })
    }, [headerButtonpresshandler, navigation])

    return (
        <ScrollView style={styles.root}>
            <Image source={{uri: selectedMeal.imageUrl}} style={styles.image}/>
            <Text style={styles.title}>{selectedMeal.title}</Text>
            <MealDetails
                affordability={selectedMeal.affordability}
                complexity={selectedMeal.complexity}
                duration={selectedMeal.duration}
                textStyle={styles.detailText}/>
            <View style={styles.listOuterContainer}>
                <View style={styles.listContainer}>
                    <Subtitle>Ingredients</Subtitle>
                    <List data={selectedMeal.ingredients}/>
                    <Subtitle>Steps</Subtitle>
                    <List data={selectedMeal.steps}/>
                </View>
            </View>
        </ScrollView>
    );
};
```



## 108. Adding drawer navigation

- returns a drawer method of navigation

```jsx
import 'react-native-gesture-handler';
import {NavigationContainer} from "@react-navigation/native";
import {createDrawerNavigator} from "@react-navigation/drawer";
import WelcomeScreen from "./screens/WelcomeScreen";
import UserScreen from "./screens/UserScreen";

const Drawer = createDrawerNavigator();

export default function App() {
  return (
      <NavigationContainer>
          <Drawer.Navigator>
              <Drawer.Screen name={'Welcome'} component={WelcomeScreen} />
              <Drawer.Screen name={'User'} component={UserScreen} />
          </Drawer.Navigator>
      </NavigationContainer>
  );
}
```



## 109. Configuring the drawer navigator and the drawer

```jsx
import 'react-native-gesture-handler';
import {NavigationContainer} from "@react-navigation/native";
import {createDrawerNavigator} from "@react-navigation/drawer";
import WelcomeScreen from "./screens/WelcomeScreen";
import UserScreen from "./screens/UserScreen";
import {Ionicons} from '@expo/vector-icons';

const Drawer = createDrawerNavigator();

export default function App() {
    return (
        <NavigationContainer>
            <Drawer.Navigator screenOptions={{
                headerStyle: {backgroundColor: '#3c0a6b'},
                headerTintColor: 'white',
                drawerActiveBackgroundColor: '#f0e1ff',
                drawerActiveTintColor: '#3c0a6b',
            }}>
                <Drawer.Screen
                    name={'Welcome'}
                    component={WelcomeScreen}
                    options={{
                        drawerLabel: "Welcome Screen",
                        drawerIcon: ({color, size}) => <Ionicons name={'home'} color={color} size={size}/>
                    }}
                />
                <Drawer.Screen
                    name={'User'}
                    component={UserScreen}
                    options={{
                        drawerIcon: ({color, size}) => <Ionicons name='person' color={color} size={size}/>
                    }}
                />
            </Drawer.Navigator>
        </NavigationContainer>
    );
}
```



- to open the drawer without the navigation

```jsx
function UserScreen({navigation}) {
  const openDrawerHandler = () => {
    navigation.toggleDrawer();
  }

  return (
    <View style={styles.rootContainer}>
      <Text>
        This is the <Text style={styles.highlight}>"User"</Text> screen!
      </Text>
      <Button title={'Open Drawer'} onPress={openDrawerHandler} />
    </View>
  );
}
```

## 110. Adding Bottom Tabs

```bash
npm install @react-navigation/bottom-tabs
```

```jsx
import 'react-native-gesture-handler';
import {NavigationContainer} from "@react-navigation/native";
import WelcomeScreen from "./screens/WelcomeScreen";
import UserScreen from "./screens/UserScreen";
import {Ionicons} from '@expo/vector-icons';
import CreateBottomTabNavigator from "@react-navigation/bottom-tabs/src/navigators/createBottomTabNavigator";

const BottomTab = CreateBottomTabNavigator();

export default function App() {
    return (
        <NavigationContainer>
            <BottomTab.Navigator
                screenOptions={{
                    headerStyle: {backgroundColor: '#3c0a6b'},
                    headerTintColor: 'white',
                    tabBarActiveTintColor: '#3c0a6b'
                }}>
                <BottomTab.Screen
                    name={'Welcome'}
                    component={WelcomeScreen}
                    options={{
                        tabBarIcon: ({color, size}) => <Ionicons name={'home'} color={color} size={size} />
                    }}
                />
                <BottomTab.Screen
                    name={'User'}
                    component={UserScreen}
                    options={{
                        tabBarIcon: ({color, size}) => <Ionicons name={'person'} color={color} size={size} />
                    }}
                />
            </BottomTab.Navigator>
        </NavigationContainer>
    );
}
```



# VII. App-wide state management with context and redux

## 116. Defining context

```jsx
// store/context/favorites-context.js

import { createContext, useState } from "react";

export const FavoritesContext = createContext({
  ids: [],
  addFavorite: () => {},
  removeFavorite: () => {},
});

const FavoritesContextProvider = ({ children }) => {
  const [favoriteMealIds, setFavoriteMealIds] = useState([]);

  const addFavorite = (id) => {
    setFavoriteMealIds((currentIds) => [...currentIds, id]);
  };

  const removeFavorite = (id) => {
    setFavoriteMealIds((currentIds) =>
      currentIds.filter((mealId) => mealId !== id)
    );
  };

  const value = {
    ids: favoriteMealIds,
    addFavorite: addFavorite,
    removeFavorite: removeFavorite,
  };

  return (
    <FavoritesContext.Provider value={value}>
      {children}
    </FavoritesContext.Provider>
  );
};

export default FavoritesContextProvider;

```

## 117. Using the created context

```jsx
import { useContext, useLayoutEffect } from "react";
import { View, Text, Image, StyleSheet, ScrollView } from "react-native";

import IconButton from "../components/IconButton";
import List from "../components/MealDetail/List";
import Subtitle from "../components/MealDetail/Subtitle";
import MealDetails from "../components/MealDetails";
import { MEALS } from "../data/dummy-data";
import { FavoritesContext } from "../store/context/favorites-context";

function MealDetailScreen({ route, navigation }) {
  const favoriteMealsCtx = useContext(FavoritesContext);

  const mealId = route.params.mealId;

  const selectedMeal = MEALS.find((meal) => meal.id === mealId);

  const mealIsFavorite = favoriteMealsCtx.ids.includes(mealId);

  function changeFavoriteStatusHandler() {
    if (mealIsFavorite) {
      favoriteMealsCtx.removeFavorite(mealId);
    } else {
      favoriteMealsCtx.addFavorite(mealId);
    }
  }

  useLayoutEffect(() => {
    navigation.setOptions({
      headerRight: () => {
        return (
          <IconButton
            icon={mealIsFavorite ? "star" : "star-outline"}
            color="white"
            onPress={changeFavoriteStatusHandler}
          />
        );
      },
    });
  }, [navigation, changeFavoriteStatusHandler]);

  return (
    <ScrollView style={styles.rootContainer}>
      <Image style={styles.image} source={{ uri: selectedMeal.imageUrl }} />
      <Text style={styles.title}>{selectedMeal.title}</Text>
      <MealDetails
        duration={selectedMeal.duration}
        complexity={selectedMeal.complexity}
        affordability={selectedMeal.affordability}
        textStyle={styles.detailText}
      />
      <View style={styles.listOuterContainer}>
        <View style={styles.listContainer}>
          <Subtitle>Ingredients</Subtitle>
          <List data={selectedMeal.ingredients} />
          <Subtitle>Steps</Subtitle>
          <List data={selectedMeal.steps} />
        </View>
      </View>
    </ScrollView>
  );
}

export default MealDetailScreen;

const styles = StyleSheet.create({
  rootContainer: {
    marginBottom: 32,
  },
  image: {
    width: "100%",
    height: 350,
  },
  title: {
    fontWeight: "bold",
    fontSize: 24,
    margin: 8,
    textAlign: "center",
    color: "white",
  },
  detailText: {
    color: "white",
  },
  listOuterContainer: {
    alignItems: "center",
  },
  listContainer: {
    width: "80%",
  },
});
```

## 119. Redux

```bash
npm install @reduxjs/toolkit
npm install react-redux
```

**Creating**

```jsx
// /store/redux/store.js
import { configureStore } from "@reduxjs/toolkit";

export const store = configureStore({
  reducer: {},
});
```

**Providing**

```jsx
// App.js
<Provider store={store}>
    ...App
</Provider>
```

**Working with slices**

- creating a slice:

```jsx
// /store/redux/favorites.js
import { createSlice } from "@reduxjs/toolkit";

const favoritesSlice = createSlice({
  name: "favorites",
  initialState: {
    ids: [],
  },
  reducers: {
    addFavorite: (state, action) => {
      state.ids.push(action.payload.id);
    },
    removeFavorite: (state, action) => {
      state.ids.splice(state.ids.indexOf(action.payload.id), 1);
    },
  },
});

export const addFavorite = favoritesSlice.actions.addFavorite;
export const removeFavorite = favoritesSlice.actions.removeFavorite;
export default favoritesSlice.reducer;
```

- merging a slice

```jsx
// /store/redux/store.js
import { configureStore } from "@reduxjs/toolkit";
import favoritesReducer from "./favorites";

export const store = configureStore({
  reducer: {
    favoriteMeals: favoritesReducer,
  },
});
```

**Using redux state**

```jsx
import { useLayoutEffect } from "react";
import { Image, ScrollView, StyleSheet, Text, View } from "react-native";

import IconButton from "../components/IconButton";
import List from "../components/MealDetail/List";
import Subtitle from "../components/MealDetail/Subtitle";
import MealDetails from "../components/MealDetails";
import { MEALS } from "../data/dummy-data";
import { useDispatch, useSelector } from "react-redux";
import { addFavorite, removeFavorite } from "../store/redux/favorites";

function MealDetailScreen({ route, navigation }) {
  const favoriteMealIds = useSelector((state) => state.favoriteMeals.ids);
  const dispatch = useDispatch();

  const mealId = route.params.mealId;

  const selectedMeal = MEALS.find((meal) => meal.id === mealId);

  const mealIsFavorite = favoriteMealIds.includes(mealId);

  function changeFavoriteStatusHandler() {
    if (mealIsFavorite) {
      dispatch(removeFavorite({ id: mealId }));
    } else {
      dispatch(addFavorite({ id: mealId }));
    }
  }

  useLayoutEffect(() => {
    navigation.setOptions({
      headerRight: () => {
        return (
          <IconButton
            icon={mealIsFavorite ? "star" : "star-outline"}
            color="white"
            onPress={changeFavoriteStatusHandler}
          />
        );
      },
    });
  }, [navigation, changeFavoriteStatusHandler]);

  return (
    <ScrollView style={styles.rootContainer}>
      <Image style={styles.image} source={{ uri: selectedMeal.imageUrl }} />
      <Text style={styles.title}>{selectedMeal.title}</Text>
      <MealDetails
        duration={selectedMeal.duration}
        complexity={selectedMeal.complexity}
        affordability={selectedMeal.affordability}
        textStyle={styles.detailText}
      />
      <View style={styles.listOuterContainer}>
        <View style={styles.listContainer}>
          <Subtitle>Ingredients</Subtitle>
          <List data={selectedMeal.ingredients} />
          <Subtitle>Steps</Subtitle>
          <List data={selectedMeal.steps} />
        </View>
      </View>
    </ScrollView>
  );
}

export default MealDetailScreen;

const styles = StyleSheet.create({
  rootContainer: {
    marginBottom: 32,
  },
  image: {
    width: "100%",
    height: 350,
  },
  title: {
    fontWeight: "bold",
    fontSize: 24,
    margin: 8,
    textAlign: "center",
    color: "white",
  },
  detailText: {
    color: "white",
  },
  listOuterContainer: {
    alignItems: "center",
  },
  listContainer: {
    width: "80%",
  },
});
```



# VIII. Expense Tracker App

- good idea to first create screens and the navigation logic and go from there

