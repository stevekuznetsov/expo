---
title: Introduction
---

import Highlight from '~/components/plugins/Highlight';
import SnackInline from '~/components/plugins/SnackInline';

Welcome to the beginner Expo tutorial. This is a complete tutorial to start your journey toward building universal applications with Expo. A universal app is simply an app that shares one code base and runs on multiple platforms such as iOS, Android, and the web.

## What are we building

In this tutorial, you are going to build an app for iOS, Android, and the web. This app will allow the user to add an emoji sticker to a background image. The user will have the option to pick the image from the platform's media library or use the placeholder image that will come with the app. After adding the sticker, the app user is allowed to download the image in the device's media library. You will use two third-party libraries to allow downloading of the image on different platforms (mobile and web). During the process, you will also use native gesture handlers to implement pan and tap gestures to add interactive functionalities. This complete set of functionality is common in various social media applications.

Here is a little demo of the app working on an iOS simulator, an Android device and the web browser:

<!-- TODO: Add a little demo video/gif of the app running on all platforms -->

Each module of this tutorial contains the code for that specific part, so feel free to follow along either by creating your own app from scratch or use Expo Snack examples that are provided in each module for references.

## About this tutorial

In a nutshell here are the features that we will cover in this tutorial:

- Initializing an Expo App
- Breaking down app layout and implementing it
- Use native image picker user interface (UI) to select an image from the platform's media library
- Create a sticker modal using Modal and FlatList components
- Add and handle gestures
- Use third-party libraries to capture a screenshot and save that image on the platform
- Handle any platform differences between mobile and web
- Finally, go through the process of adding a splash screen and an icon to complete the app
<!-- TODO: Add a list of features and functionalities covered by the tutorial -->

From the topic list above, the objective of this tutorial is to get you started with Expo and to get you familiar with the Expo SDK. You are going to use different Expo modules such as `expo-image-picker`, and `expo-media-library`. Some of these functionalities are picking an image from the platform's media library, saving the image back to the media library and so on. In the Expo SDK ecosystem, these modules are available to you, as an app developer, to seamlessly use native functionalities across different platforms without worrying about handling the differences on the mobile platforms.

Further in the tutorial, we will also use libraries like [React Native Gesture Handler](https://docs.swmansion.com/react-native-gesture-handler/) and [Reanimated](https://docs.swmansion.com/react-native-reanimated/) to add interactivity and provide a touch-based user experience in your app.

We will also dive into using third-party libraries and what are some of the ways you can find which third-party library to use with your app. Using these third-party libraries, you will also learn how to create functionalities by handling platform differences across the web and mobile platforms.

If you're already familiar with Expo, feel free to jump ahead to certain modules you want to learn more aboutit. If you're completely new, let's spend some time together building an application from scratch.

## How to use this tutorial

We believe in "learning by doing" and so this tutorial emphasizes doing over-explaining. You can follow along the journey of building the app in the following ways:

- Create a new Expo project and start building the app from scratch
- Clone the starter project and start building the app from scratch
- Follow along by trying out examples in [Snack](/workflow/snack/)

We will provide code snippets at various points of building the app. If you find yourself typing code that you do not understand, do not worry — we will link you to appropriate resources to help you get a deeper understanding at the end of the tutorial.

Throughout the tutorial, any important code or code that has changed between examples will be <Highlight>highlighted in yellow</Highlight>. You can hover over the highlights (on desktop) or tap them (on mobile) to see more context on the change. For example, the code highlighted in the snippet below explains what it does:

<SnackInline label="Hello world">

<!-- prettier-ignore -->
```js
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>    
      /* @info This used to say "Open up App.js to start working on your app!". Now it's "Hello world!". */<Text>Hello world!</Text>/* @end */      
    </View>
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

</SnackInline>

> **Wait, what is this "Try this example on Snack" button?**
>
> Snack is a web-based editor that works similar to a managed Expo project. It's a great way to share code snippets with people and try things out without needing to get a project running on your own computer with `npx expo`. Go ahead, press the button. You will see the above code running in it. Switch between iOS, Android, or web. Open it on your device in the Expo Go app by pressing the **Run** button.
>
> You can also use Snack to copy and paste the code into your own project on your computer. We will continue to provide Snacks for each module in this tutorial.

## Next steps

Now you are ready to go to the next step in which you are going to learn [how to initialize an app with Expo](/tutorial/initialize-app/).
