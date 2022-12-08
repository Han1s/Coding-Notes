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