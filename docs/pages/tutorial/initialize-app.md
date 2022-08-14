---
title: Create your first app
---

import { Terminal } from '~/ui/components/Snippet';
import { Collapsible } from '~/ui/components/Collapsible';
import ImageSpotlight from '~/components/plugins/ImageSpotlight';

In this module, let's learn how to create a new Expo project and explore the app.

## Step 0: Prerequisites

Before you get started, this tutorial assumes that you:

- Have already installed the [Expo Go](https://expo.dev/client) app on your physical device
- Have gone through the [requirements under Installation](https://docs.expo.dev/get-started/installation/#requirements) to set up your development environment

This tutorial also assumes that you have basic knowledge of JavaScript and React or React Native. If you have never written React code, go through [the official React tutorial](https://reactjs.org/tutorial/tutorial.html) first. For more resources, see [additional resources](https://docs.expo.dev/next-steps/additional-resources/).

## Step 1: Initialize a new Expo app

For this tutorial, we provide two different ways to get started:

- [Clone the repository](#clone-the-repository)
- [Manually initialize with `create-expo-app`](#manually-initialize-with-create-expo-app)

Whichever way you choose to initialize the app, open the repository in your favorite IDE. We're using Visual Studio Code for our examples.

### Clone the repository

In the directory of your choice with your preferred terminal, clone the app's starter repository:

<Terminal cmd={['$ git clone https://github.com/url-to-sticker-smash-repo']} />

The repository you are cloning comes with all the dependencies required to build and run the app pre-installed.

### Manually initialize with `create-expo-app`

In the directory of your choice with your preferred terminal, run the following command to initialize a new project:

<Terminal cmd={[
'# Create a project named StickerSmash',
'$ npx create-expo-app StickerSmash',
'',
'# Navigate to the project directory',
'$ cd StickerSmash'
]} cmdCopy="npx create-expo-app StickerSmash && cd StickerSmash" />

This command will create a new directory for the project with the name: **StickerSmash**.

## Step 2: Run the app on mobile

Whichever way you choose to initialize the app, make sure to navigate inside the project directory in your terminal window before proceeding.

After navigating inside the project directory, run the command to trigger the [development server](/guides/how-expo-works/#expo-development-server) and see the bare-bones app in action:

<Terminal cmd={['$ npx expo start']} />

After starting the development server, you can open the project in the Expo Go app on your device. Learn more on [how to open the app when developing with Expo on a physical device](/get-started/create-a-new-app/#opening-the-app-on-your-phonetablet).

Here is a little demo of the app running on an iOS simulator, and a physical Android device:

<ImageSpotlight alt="App running on an iOS simulator and a physical Android device." src="/static/images/tutorial/app-running-on-mobile-platforms.jpg" style={{maxWidth: 720}} />

The text displayed on the app's screen above can be found in the **App.js** file of the initialized project. It is the entry point of the app, and is executed when the app starts.

## Step 3: Run the app on the web

When you create a new project with `create-expo-app`, it uses the default [blank template](https://github.com/expo/expo/tree/main/templates/expo-template-blank) that comes pre-configured with necessary dependencies to run your app on mobile platforms. To support the web, you need to add a few additional dependencies to the project. In a terminal window, run the following command to install the necessary dependencies to include web support:

<Terminal cmd={['$ npx expo install react-native-web@~0.18.7 react-dom@18.0.0 @expo/webpack-config@^0.17.0']} />

Before running the above installation command, make sure to terminate `npx expo start` if it is already running the development server. After installing the dependencies, run the development server again. To see the web app in action, press <kbd>W</kbd> in the terminal window. It will open the web app in your default web browser at the URL: `http://localhost:19006/`.

<ImageSpotlight alt="App running on an all platforms" src="/static/images/tutorial/app-running-on-all-platforms.jpg" style={{maxWidth: 720}} />

## Up next

You have now set up an application in the local environment and launched it. The next step is to learn how to build a layout for your app.

If you have any trouble in this module, refer back to the [Create a new app](/get-started/create-a-new-app/). If you have trouble opening the app on the device of your choice, refer to the [Opening the app on your phone/tablet](/get-started/create-a-new-app/#opening-the-app-on-your-phonetablet) section.
