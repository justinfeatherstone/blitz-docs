
How to Structure Your React Native Project: A Guide to Best Practices 

React Native is an un-opinionated framework, which means that it doesn’t dictate how you should structure your code. As a beginner, this can be both a blessing and a curse. While it’s easy to start writing code all over the place, it can quickly become difficult to manage as your project grows. A proper folder structure can provide better separation of concerns, make it easier to manage different modules, enforce coding standards, and make your project look more professional.

In this article, we’ll take a look at a version folder structure for React Native projects I personally use in my projects. This structure is based on best practices and can be modified to suit the specific needs of your project.

# ==*The Directory Structure==*

Here is a bird’s eye view of the recommended directory structure:

```
AwesomeProject  
  -src  
    |--- assets  
    |--- screens  
    |--- navigation  
    |--- services  
    |--- components  
    |--- hooks  
    |--- types  
    |--- redux  
    |--- utils
```

Let’s go through each directory and its purpose in more detail.

## **1. assets**

The `assets` directory is where you should put all your static assets, such as fonts and images. It's a good idea to organize these assets into separate subdirectories for each asset type. For example:

```
assets  
  |--- fonts  
  |--- images
```

## **2. screens**

The `screens` directory is where you should put all your application screens or pages. Each screen should have its own directory with the following files:

- `index.js`: This will export default screenName to shortened import path
- `styles.ts`: The styles for the screen.
- `helper.ts`: Utility function like any business or state management fuction can be put here. For example, function which returns `buttonColor` based on status. Ideally, you should try to write as little as possible logic into your component file. This will make your code more abstract and testable
- `screenName.tsx`: The TypeScript file for the screen. In this file you will define your UI.
- `screenName.test.tsx`: The test file for the screen.

**Pro tip:** Use ChatGPT to alteast have basic test cases even if timeline don’t allow you to maintain testing code.

- `useAnimated.ts` (optional): All animation-related code goes here. As the animation code gets very messy and is completely unrelated to component logic, try to avoid any animation-related logic in the component file


```typescript

import { interpolate, SharedValue, useSharedValue, useAnimatedStyle } from 'react-native-reanimated';  
  
import colors from '../../constants/colors';  
  
export default function useAnimated() {  
  
  const animated: SharedValue<number> = useSharedValue(0);  
  
    const animatedStyle = useAnimatedStyle(() => {  
        return {  
            opacity: interpolate(animated?.value ?? 0, [0, 1], [0, 0.5]),  
            backgroundColor: colors.black,  
        };  
    }, [animated]);  
  
    return {  
        animated,  
        animatedStyle,  
    };  
}
```


- `components` (optional): Any reusable components used by the screen.

## **3. navigation**

The `navigation` directory is where you should put all your navigation-related code. This includes:

- `NavigationContainer`: The top-level component that wraps all the screens.
- `Route`: The folder where you define your application routes like stack, tab bar and drawers
- `NavigationService`: This file will contain ref of your route and will help in navigation from outside components, like deep links or notification

```typescript

import { createNavigationContainerRef } from '@react-navigation/native';  
  
export const navigationRef = createNavigationContainerRef();  
  
export function goBack() {  
    return navigationRef?.goBack();  
}  
  
export function navigate(name: string, params?: Record<string, any>) {  
    if (navigationRef.isReady()) {  
        navigationRef.navigate(name, params);  
    }  
}  
  
  
function push(routeName: string, params?: Record<string, any>) {  
    throw new Error('Missing implementation of push');  
}  
  
function reset(routeName: string) {  
    throw new Error('Missing implementation of reset');  
}  
  
function getCurrentRoute() {  
    throw new Error('Missing implementation of getCurrentRoute');  
}  
  
const getRouteName = () => {  
    return navigationRef.getCurrentRoute()?.name ?? '';  
};  
  
const NavigationService = {  
    navigate,  
    push,  
    goBack,  
    reset,  
    getCurrentRoute,  
    getRouteName,  
};  
  
export default NavigationService;
```


- `linking`: The configuration for deep linking.

## **4. services**

###### The `services` directory is where you should put all your code related to external services, such as APIs. It's a good idea to organize these services into separate subdirectories for each service type. For example:

###### ```
###### services  
  ###### |--- apiclient  
  ###### |--- requestInterceptor  
  ###### |--- responseInterceptor  
  ###### |--- urls  
  ###### |--- UserApi
###### ```

## **5. components**

###### The `components` directory is where you should put all your reusable components. Each component should have its own directory with the following files (it is similar to the screen folder structure)

###### - `index.ts`: The main component file.
###### - `ComponentName.tsx`: The TypeScript file for the component.
###### - `styles.ts`: The styles for the component.
###### - `helper.ts`: Any helper functions related to the component.
###### - `useAnimated.ts` (optional): Any animation-related hooks for the component.

## 6. hooks

###### The `hooks` directory is where you should put all your custom hooks. Each hook should have its own file. For example:

###### ```
###### hooks  
  ###### |--- useBackHandler.ts  
  ###### |--- useKeyboard.ts
###### ```

###### **Networking**

###### Next up is the `networking` folder. This folder should contain all the files related to network requests and responses. In general, the `networking` folder should contain the following files:

###### - apiclient: This file should contain a class or a function responsible for sending network requests to your API.
###### - requestInterceptor: This file is optional, but it is useful for intercepting requests before they are sent. In the case of Axios, this is done with an interceptor.
###### - responseInterceptor: Similar to the `requestInterceptor`, this file is also optional and can be used for intercepting responses before they are returned.
###### - urls: This file should contain all the URLs for your API calls. This is useful for centralizing URLs, so if they ever change, you only have to update one file.
###### - API files: These files can contain a group of related API calls. For example, if you have a user module in your app, you can create a `UserApi.ts` file to contain all the API calls related to the user module. These file will parse/format request and response into proper format and can be used to apply any logic before sending response to caller.

###### **Types**

###### The `types` folder should contain all the TypeScript interfaces and types in your app. It's important to use TypeScript in your React Native app because it can catch errors at compile-time instead of run-time.

###### The `types` folder should contain a separate file for each interface or type. For example, `UserInterface.ts` can contain all the interfaces related to users in your app.

###### **Redux**

###### If you’re using Redux in your app, you should create a separate folder for Redux files. The `redux` folder should contain the following files:

###### - store.ts: This file should create the Redux store and configure it with any middleware or enhancers required for your app.
###### - slices: This folder should contain all the Redux slices in your app. A Redux slice is a piece of the Redux store that can be updated independently of the rest of the store. Each slice should be in a separate file with a descriptive name. For example, `UserSlice.ts`.

## 7. Utils

###### The `utils` folder contains various utility functions that are not related to a specific feature or module of the app. Here are some examples of files that might be included in this folder:

###### ```
###### utils  
    ###### |--- Analytics.ts  
    ###### |--- CommonUtils.ts  
    ###### |--- Logger.ts  
    ###### |--- ErrorManager.ts  
    ###### |--- DateTimeUtils.ts  
    ###### |--- EncryptedStore.ts  
    ###### |--- string.ts  
    ###### |--- constants.ts  
    ###### |--- enums.ts
###### ```


## Overview **(src/)**
Here is the complete picture for you

```
AwesomeProject  
  -src  
    |--- assets  
    |      |--- fonts  
    |            |--- <<Your Fonts>>  
    |      |--- images  
    |            |--- << Your Images>>  
    |  
    |  
    |--- route  
    |      |--- screenName  
    |      |      |--- index.js  
    |      |      |--- styles.ts  
    |      |      |--- helper.ts  
    |      |      |--- screenName.tsx  
    |      |      |--- screenName.test.tsx  
    |      |      |--- useAnimated.ts (Optional)  
    |      |      |--- components (Optional)  
    |      |  
    |      |--- screenName2  
    |              |--- index.js  
    |              |--- styles.ts  
    |              |--- helper.ts  
    |              |--- screenName.tsx  
    |              |--- screenName.test.tsx  
    |              |--- useAnimated.ts (Optional)  
    |              |--- components (Optional)  
    |    
    |--- navigation  
    |      |--- NavigationContainer  
    |      |--- Route  
    |      |--- NavigationService  
    |      |--- linking  
    |  
    |--- networking  
    |      |--- apiclient  
    |      |--- requestInterceptor (Assuming axios)  
    |      |--- responseInterceptor (Assuming axios)  
    |      |--- urls  
    |      |--- UserApi (You can create a file for a group of related api calls)  
    |  
    |--- components  
    |      |---Button (This is will have same structure as the screen)  
    |      |      |--- index.ts  
    |      |      |--- Button.tsx  
    |      |      |--- styles.ts  
    |      |      |--- helper.ts  
    |      |      |--- useAnimated.ts (Optional)  
    |      |  
    |      |--- <<Any other component>>  
    |  
    |--- hooks  
    |      |--- useBackHandler.ts  
    |      |--- useKeyboard.ts  
    |      |--- useUploadImage.ts  
    |      |--- useCamera.ts  
    |      |--- <<Any other hook>>  
    |  
    |--- types   
    |      |--- UserInterface  
    |      |--- MediaInterface  
    |      |--- AppConfigInterface  
    |  
    |--- redux  
    |      |--- store.ts  
    |      |--- slices  
    |            |--- UserSlice  
    |            |--- IntermittentSlice  
    |            |--- ToastSlice  
    |  
    |--- utils  
    |      |--- Analytics.ts  
    |      |--- CommonUtils.ts  
    |      |--- Logger.ts  
    |      |--- ErrorManager.ts  
    |      |--- DateTimeUtils.ts  
    |      |--- EncryptedStore.ts  
    |      |--- string.ts  
    |      |--- constants.ts  
    |      |--- enums.ts  
    |       
---------------------------- << MULTIPLE MODULE APP >> ----------------  
    |--- Module_Name  
          |--- routes  
          |--- components  
          |--- hooks

```