---
title: Use an image picker
---

import SnackInline from '~/components/plugins/SnackInline';
import Video from '~/components/plugins/Video';
import { Terminal } from '~/ui/components/Snippet';

In the previous module, you used code from React and React Native in the app. React gives a nice way to build components and React Native gives pre-built components that work on iOS, Android, and web &mdash; such as `View`, `Text`, `Pressable`. However, React Native does not provide a way to select an image from the device's media library. The app you are building requires this functionality and after the image is selected, replace the placeholder image with it.

At the same time, the app you are building needs a solution that works on all platforms and do not have to worry about supporting each platform from scratch by writing native code. For this, let's use an Expo library called [expo-image-picker](/versions/latest/sdk/imagepicker). Here is a brief description of what the library does:

> `expo-image-picker` provides access to the system's user interface (UI) for selecting images and videos from the phone's library or taking a photo with the camera.

## Step 1: Install expo-image-picker

First, install the `expo-image-picker` library in your Expo project by running the following command:

<Terminal cmd={['$ npx expo install expo-image-picker']} />

This will tell npm (or yarn) to install a version of the `expo-image-picker` library that is compatible with the Expo SDK version that your project uses.

> If you cloned the app from the GitHub repository, you do not have to install this library as it is already included in the list of dependencies.

## Step 2: Pick an image from the device's media library

After installing the library, you can use it in your project. `expo-image-picker` provides `launchImageLibraryAsync()` method that displays the system UI for choosing an image or a video from the phone's library. You can also pass an [`ImagePickerOptions` object](/versions/latest/sdk/imagepicker/#imagepickeroptions) when invoking the function to specify different options. For example, you can pass options such as `aspect` to specify the aspect ratio to maintain if the user is allowed to edit the image when picking the image.

You can also pass `mediaTypes` to specify the types of media that the user can pick. For example, the default value of this option is `ImagePicker.MediaTypeOptions.Images` which means that the user can only select images.

For our app, we will pass the following options:

- `aspect`
- `quality`
- `allowsEditing`

We will not use `mediaTypes` since we only want to pick images which is the default option.

> **Tip**: You can read more about what each option does in the [ImagePickerOptions](/versions/latest/sdk/imagepicker/#imagepickeroptions) table.

### Step 2.1: Create a handler method to pick the image

The styled button created in the previous module will be used to pick an image from the device's media library. When this button is pressed, you have to invoke a custom handler method to pick the image. Start by creating a handler method called `pickImageHandler()` inside the `App` component:

<!-- prettier-ignore -->
```js
/* @info Import the ImagePicker. */ import * as ImagePicker from 'expo-image-picker'; /* @end */

// ... other import statements

export default function App() {
  const pickImageHandler = async () => {
    /* @info Pass image picker options to launchImageLibraryAsync() */
    let result = await ImagePicker.launchImageLibraryAsync({
      allowsEditing: true,
      aspect: [4, 3],
      quality: 1,
    });
    /* @end */

    if (!result.cancelled) {
      /* @info If the image is picked, print its information in terminal window. */
      console.log(result);
      /* @end */
    } else {
      /* @info If the user does not picks an image, show an alert. */
      alert('You did not select any image.');
      /* @end */
    }
  };

  // ...rest of the code remains same
}
```

### Step 2.2: Update the button component

The handler method must trigger when the styled button is pressed. To do this, you have to update the `onPress` property of the `Button` component in **components/Button.js**:

<!-- prettier-ignore -->
```js
export default function Button({ label, isBorderLess = false, /* @info Pass this prop to trigger the handler method from the parent component. */ onPressHandler/* @end */}) {
  // ..rest of the code remains same

  return (
    <View>
      /* ... rest of the code remains unchanged */
      <Pressable
        style={[styles.button, { backgroundColor: '#fff' }]}
        /* @info */ onPress={onPressHandler} /* @end */
      >        
    </View>
  );
}
```

The `onPress` prop on the `Button` component will trigger the `pickImageHandler` when it is passed to the `Button` component in the `App` component:

<!-- prettier-ignore -->
```js
export default function App() {
  // ...rest of the code remains same

  return (
    <View style={styles.container}>
      /* ...rest of the code remains same */
      <Button label="Choose a photo" /* @info */ onPressHandler={pickImageHandler} /* @end */ />
    </View>
  );
}
```

The `pickImageHandler` handler method is responsible for invoking `ImagePicker.launchImageLibraryAsync()` and then handling the result. The `launchImageLibraryAsync()` method returns an object that contains the information about the selected image. Right now, the `result` object that contains the information is printed in the logs of the terminal window:

```json
{
  "assetId": "ED7AC36B-A150-4C38-BB8C-B6D696F4F2ED/L0/001",
  "cancelled": false,
  "fileName": "IMG_0005.JPG",
  "fileSize": 3423356,
  "height": 2002,
  "type": "image",
  "uri": "file:///Users/your-mac-os-username/Library/Developer/CoreSimulator/Devices/7C9DD290-834F-426D-A774-EBD583305F84/data/Containers/Data/Application/C5EC31DB-A654-48DF-9F42-5864DF16257B/Library/Caches/ExponentExperienceData/%2540anonymous%252FStickerSmash-a004aacc-74c3-4374-a6a9-1748f56f6b8e/ImagePicker/C1AE11EF-C8B6-4BE8-8EE3-E1779A43653A.jpg"
}
```

## Step 3: Use the selected image

The `result` object provides the local `uri` of the selected image. Let's take this value from the image picker and use it to show the selected image in the app.

Modify the **App.js** file in following steps:

- Declare a state variable called `selectedImage` using [`React.useState`](https://reactjs.org/docs/hooks-state.html). This state variable is used to hold the URI of the selected image.
- Updating the `pickImageHandler` method to save the image URI in the `selectedImage` state variable.
- Then, pass the `selectedImage` as a prop to the ImageViewer component.

<!-- prettier-ignore -->
```js
/* @info Import useState hook from React. */ import { useState } from 'react'; /* @end */

// ... rest of the import statements remain unchanged

export default function App() {
  /* @info Create a state variable that will hold the value of selected image. */
  const [selectedImage, setSelectedImage] = useState(null);
  /* @end */
  
  const pickImageHandler = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      allowsEditing: true,
      aspect: [4, 3],
      quality: 1,
    });

    if (!result.cancelled) {
      /* @info */
      setSelectedImage(result.uri);
      /* @end */
    } else {
      alert('You did not select any image.');
    }
  };


  return (
    <View style={styles.container}>
      /* @info Pass the selected image URI to the ImageViewer component. */<ImageViewer placeholderImageSource={PlaceholderImage} selectedImage={selectedImage} />/* @end */            
    </View>
  );
}
```

Now, modify the **components/ImageViewer.js** file. Inside it, the `Image` component will now use the conditional operator to load the source of the image. This is because the image picked from the image picker is a [`uri` string](https://reactnative.dev/docs/images#network-images) and not a local asset like the placeholder image. For this reason, you cannot use the `require` syntax to load the image from the device.

<SnackInline
label="Image picker"
templateId="tutorial/module-image-picker/App"
dependencies={['expo-image-picker', 'expo-status-bar', '@expo/vector-icons', '@expo/vector-icons/FontAwesome']}
files={{
'assets/images/background-image.png': 'https://snack-code-uploads.s3.us-west-1.amazonaws.com/~asset/503001f14bb7b8fe48a4e318ad07e910',
'components/ImageViewer.js': 'tutorial/module-image-picker/ImageViewer.js',
'components/Button.js': 'tutorial/module-image-picker/Button.js'
}}>

<!-- prettier-ignore -->
```js
export default function ImageViewer({ placeholderImageSource, selectedImage }) {
  return (
    <View style={styles.imageContainer}>
      /* @info If the selected image is not null, show the image, otherwise, show the placeholder image */
      <Image
        source={selectedImage !== null ? { uri: selectedImage } : placeholderImageSource}
        style={styles.image}
      />
      /* @end */
    </View>
  );
}
```

</SnackInline>

Here is the demo of the image picker working on all platforms after this step:

<Video file="tutorial/picker-show.mp4" />

> **Note**: The images used for demo in this tutorial are picked from [Unsplash](https://unsplash.com/photos/hpTH5b6mo2s).

## Up next

You have now added the functionality to pick an image from the device's media library. This is great progress! In the next module, let's learn how to create an emoji sticker picker component.
