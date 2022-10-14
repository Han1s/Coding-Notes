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

- download **Expo** apk on your phone
- `npm start`
- scan the QR code

