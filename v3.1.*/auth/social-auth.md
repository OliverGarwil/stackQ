# Social Auth

A common misconception is that RNFirebase provides social login out of the box. This is somewhat true, it leaves the implementation of the login provider up to the user and only signs the user in once the provider data has been returned.

Firebase allows a number of social providers to be used out of the box; Facebook, Google, Twitter and Github. You can however choose any provider you wish assuming they have an oAuth API.

## Facebook

Facebook provide a wrapper around their Android & iOS SDKs called [react-native-fbsdk](https://github.com/facebook/react-native-fbsdk). This module handles the flow of logging in a user and obtaining their `accessToken`. The main benefit of using the native SDK is that it detects whether the user is has the Facebook app installed and falls back to the web if not.

The `react-native-fbsdk` library allows us to first login (using `LoginManager`) and then obtain the users `accessToken` (using `AccessToken`). Once we have the access token we need to create a credential using [ref auth.FacebookAuthProvider#credential] and then sign in with that credential using [ref auth#signInWithCredential]:

```js
import { AccessToken, LoginManager } from 'react-native-fbsdk';
import firebase from 'react-native-firebase'

// Calling the following function will open the FB login dialogue:
const facebookLogin = () => {
  return LoginManager
    .logInWithReadPermissions(['public_profile', 'email'])
    .then((result) => {
      if (!result.isCancelled) {
        console.log(`Login success with permissions: ${result.grantedPermissions.toString()}`)
        // get the access token
        return AccessToken.getCurrentAccessToken()
      }
    })
    .then(data => {
      if (data) {
        // create a new firebase credential with the token
        const credential = firebase.auth.FacebookAuthProvider.credential(data.accessToken)
        // login with credential
        return firebase.auth().signInWithCredential(credential)
      }
    })
    .then((currentUser) => {
      if (currentUser) {
        console.info(JSON.stringify(currentUser.toJSON()))
      }
    })
    .catch((error) => {
      console.log(`Login fail with error: ${error}`)
    })
}
```

## Google

We recommend using [react-native-google-signin](https://github.com/devfd/react-native-google-signin) for Google authentication.  This module handles the flow of logging in a user and obtaining their `accessToken` and `idToken` by wrapping around the offical Google login library. This means you get a much smoother experience than using a standard OAuth library, particularly on Android.

The `react-native-google-sign` library allows us to login (using `GoogleSignin`) which returns an optional `accessToken` and `idToken`. Once we have the two tokens we need to create a credential using [ref auth.GoogleAuthProvider#credential] and then sign in with that credential using [ref auth#signInWithCredential]:

```js
import { GoogleSignin } from 'react-native-google-signin';

// ... somewhere in your login screen component
GoogleSignin
  .signIn()
  .then((data) => {
    // create a new firebase credential with the token
    const credential = firebase.auth.GoogleAuthProvider.credential(data.idToken, data.accessToken);
    
    // login with credential
    return firebase.auth().signInWithCredential(credential);
  })
  .then((currentUser) => {
    console.warn(JSON.stringify(currentUser.toJSON()));
  })
  .catch((error) => {
    console.log(`Login fail with error: ${error}`);
  });

```

## Twitter

## Github

## Custom Provider

