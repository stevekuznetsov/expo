---
title: Create an emoji picker modal
---

import SnackInline from '~/components/plugins/SnackInline';
import ImageSpotlight from '~/components/plugins/ImageSpotlight'

React Native provides a [`Modal` component](https://reactnative.dev/docs/modal) that is used to present the content above an underlying view. In general, Modals are used to draw a user's attention toward some critical information or guide them to take an action to trigger the next step in an ongoing process.

A modal can be the new view that disables the previous or the underlying view and covers up the whole screen or a certain amount percentage of the screen. In this module, let's create a modal that shows an emoji picker. The contents of this component are only going to take 25% of the screen.

## Step 1: Declare a state variable to show buttons

Before implementing the modal, you have to direct the app screen to display the button to trigger the modal. This button is only visible when the user has picked an image from the media library or they have decided to use the placeholder image. So, let's implement a circle button that will be visible when the user has decided which image they want to use.

Start by declaring a state variable called `showAppOptions` in the `App` component. This variable will be used to show or hide buttons to open the modal and a few other options. The value of this variable is a boolean and by default, when the app screen loads, it is set to `false` so that the options are not shown before picking an image.

```js
export default function App() {
  const [showAppOptions, setShowAppOptions] = useState(false);
  // ...
}
```

The value of this variable will be set to true when the user has picked an image from the media library or they have decided to use the placeholder image.

Next, modify the `pickImageHandler()` method to set the value of `showAppOptions` to `true` after the user has picked an image.

<!-- prettier-ignore -->
```js
const pickImageHandler = async () => {
  // ...

  if (!result.cancelled) {
    setSelectedImage(result.uri);
    /* @info */ setShowAppOptions(true); /* @end */

  } else {
    // ...
  }
};
```

Then, update the borderless button by adding an `onPressHandler` prop with the following value:

```js
<Button label="Use this photo" isBorderLess onPressHandler={() => setShowOptions(true)} />
```

Don't forget to remove the `alert` on the `Button` component and update the `onPress` prop when rendering the borderless button in **components/Button.js**:

<!-- prettier-ignore -->
```js
function Button({ label, isBorderLess, onPressHandler }) {
  if (isBorderLess) {
    return (
      <View style={styles.buttonContainer}>
        /* @info */
        <Pressable style={styles.button} onPress={onPressHandler}>
        /* @end */
          <Text style={styles.buttonLabel}>{label}</Text>
        </Pressable>
      </View>
    );
  }

  // ...
}
```

Next, update the JSX of the `App` component to conditionally render the `Button` component based on the value of `showAppOptions`.

<!-- prettier-ignore -->
```js
export default function App() {
  // ...
  return (
    <View style={styles.container}>
      /* ... */ 
      /* @info */
      {showAppOptions ? (
        <View />
      ) : (
        <View style={styles.footerContainer}>
          <Button label="Choose a photo" onPressHandler={pickImageHandler} />
          <Button
            label="Use this photo"
            isBorderLess
            onPressHandler={() => setShowAppOptions(true)}
          />
        </View>
      )}
      /* @end */
      <StatusBar style="auto" />
    </View>
  );
}
```

For now, an empty `View` component is rendered when the value of `showAppOptions` is `true`. This value is handled in the next step.

## Step 2: Add buttons

The layout of the option buttons you are going to implement in this section looks like this:

<ImageSpotlight alt="Break down of the layout of the buttons row." src="/static/images/tutorial/buttons-layout.jpg" style={{ maxWidth: 480 }} containerStyle={{ marginBottom: 0 }} />

It contains a parent `View` that contains three buttons aligned in a row. The button in middle with the plus icon (+) will be used to open the model and is styled differently than the other two buttons.

Inside the `components` folder, start by creating a new file called **CircleButton.js** with the following code snippet:

```js
import { View, Pressable, StyleSheet } from 'react-native';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';

export default function CircleButton({ onPressHandler }) {
  return (
    <View style={styles.circleButtonContainer}>
      <Pressable style={styles.circleButton} onPress={onPressHandler}>
        <MaterialIcons name="add" size={38} color="#25292e" />
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  circleButtonContainer: {
    width: 84,
    height: 84,
    marginHorizontal: 60,
    borderWidth: 4,
    borderColor: '#ffd33d',
    borderRadius: 42,
    alignItems: 'center',
    justifyContent: 'center',
    padding: 3,
  },
  circleButton: {
    justifyContent: 'center',
    alignItems: 'center',
    width: '100%',
    height: '100%',
    borderRadius: 42,
    backgroundColor: '#fff',
  },
});
```

It uses the `MaterialIcons` icon set from `@expo/vector-icons` library to render the plus icon.

The other two buttons only show a text label and an icon aligned vertically. Let's create a reusable function component for them inside **components/IconButton.js**. This component accepts three props:

- `icon`: the name of the icon to be displayed that corresponds to the icon name in `MaterialIcons` library.
- `label`: the text label to be displayed on the button.
- `onPressHandler`: the function to be called when the button is pressed.

```js
function IconButton({ icon, label, onPressHandler }) {
  return (
    <Pressable style={styles.iconButton} onPress={onPressHandler}>
      <MaterialIcons name={icon} size={24} color="#fff" />
      <Text style={styles.iconButtonLabel}>{label}</Text>
    </Pressable>
  );
}
```

To display these buttons, import them in **App.js** and replace the empty `View` component from the previous step. Let's also create the handler methods for these buttons.

<SnackInline
label="Add Button options"
templateId="tutorial/module-modal/App"
dependencies={['expo-image-picker', '@expo/vector-icons/FontAwesome', '@expo/vector-icons', 'expo-status-bar', '@expo/vector-icons/MaterialIcons']}
files={{
  'assets/images/background-image.png': 'https://snack-code-uploads.s3.us-west-1.amazonaws.com/~asset/503001f14bb7b8fe48a4e318ad07e910',
  'components/ImageViewer.js': 'tutorial/module-image-picker/ImageViewer.js',
  'components/Button.js': 'tutorial/module-modal/Button.js',
  'components/CircleButton.js': 'tutorial/module-modal/CircleButton.js',
  'components/IconButton.js': 'tutorial/module-modal/IconButton.js',
}}>

<!-- prettier-ignore -->
```js
// ... rest of the import statements

import CircleButton from './components/CircleButton';
import IconButton from './components/IconButton';

export default function App() {
  // ...
  const resetHandler = () => {
    setShowAppOptions(false);
  };

  const modalVisibilityHandler = () => {
    // we will implement this later
  };

  const saveImageHandler = () => {
    // we will implement this later
  };

   return (
    <View style={styles.container}>
      /* ... */
      {showAppOptions ? (        
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton
              icon="refresh"
              label="Reset"
              onPressHandler={resetHandler}
            />
            <CircleButton onPressHandler={modalVisibilityHandler} />
            <IconButton
              icon="save-alt"
              label="Save"
              onPressHandler={saveImageHandler}
            />
          </View>
        </View>
      ) : (
        /* ... */
      )}
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  // ...previous styles remain unchanged
  optionsContainer: {
    flex: 1 / 4,
  },
  optionsRow: {
    alignItems: 'center',
    flexDirection: 'row',
  },
})
```

</SnackInline>

In the above snippet, the `resetHandler()` method is called when the user presses the reset button. When this button is pressed, the user is shown the image picker button again.
