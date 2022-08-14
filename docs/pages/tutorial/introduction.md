---
title: Introduction
---

import Highlight from '~/components/plugins/Highlight';

Welcome to the beginner Expo tutorial. This is a complete tutorial to start your journey toward building universal applications with Expo. A universal app is simply an app that shares one code base and runs on multiple platforms such as iOS, Android, and web.

## What are we building

In this tutorial, we are going to build an app for iOS, Android, and the web. The app we are going to build is to add an emoji sticker on a background image that can be picked from the platform's media library. It is a common functionality in various social media applications. After adding the sticker, you or your app users are allowed to download the image in the device's media library.

Here is a little demo of the app working on an iOS simulator, an Android device and the web browser:

<!-- TODO: Add a little demo video/gif of the app running on all platforms -->

Each module of this tutorial contains the code for that specific part, so feel free to follow along either by creating your own app from scratch or use Expo Snack examples that are provided in each module for references.

## About this tutorial

In a nutshell here are the features that we will cover in this tutorial:

- Initializing an Expo App
- Creating your first button component
<!-- TODO: Add a list of features and functionalities covered by the tutorial -->

From the topic list above, the objective of this tutorial is to get you started with Expo and to get you familiar with the Expo SDK. You are going to use different Expo modules such as `expo-image-picker`, and `expo-media-library`. Some of these functionalities are picking an image from the platform's media library, saving the image back to the media library and so on. In the Expo SDK ecosystem, these modules are available to you, as an app developer, to seamlessly use native functionalities across different platforms without worrying about handling the differences on the mobile platforms.

Further in the tutorial, we will also use libraries like React Native Gesture Handler and Reanimated to add interactivity and provide a touch-based user experience in your app.

We will also dive into using third-party libraries and what are some of the ways you can find which third-party library to use with your app. Using these third-party libraries, you will also learn how to create functionalities by handling platform differences across the web and mobile platforms.

If you're already familiar with Expo, feel free to jump ahead past certain modules. If you're completely new, let's spend some time together building an application from scratch.

## How to use this tutorial

We believe in "learning by doing" and so this tutorial emphasizes doing over explaining. You can follow along the journey of the building the app in the following ways:

- Create a new Expo project and start building the app from scratch
- Clone the starter project and start building the app from scratch
- Follow along by trying out examples in [Snack](/workflow/snack/)

We will provide code snippets at various points of building the app. If you find yourself typing code that you do not understand, do not worry — we will link you to appropriate resources to help you get a deeper understanding at the end of the tutorial.

Throughout the tutorial, any important code or code that has changed between examples will be <Highlight>highlighted in yellow</Highlight>. You can hover over the highlights (on desktop) or tap them (on mobile) to see more context on the change. For example, the code highlighted in the snippet below explains what it does:

<!-- prettier-ignore -->
```js

import React from 'react';
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

## Up next

Now you are ready to go to the next step in which you are going to learn how to initialize an app with Expo.
