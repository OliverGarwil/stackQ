# User

A user account.

## Methods

### delete
[method]delete() returns Promise containing void;[/method]

Adds an observer for changes to the user's sign-in state.

Returns an unsubscriber function.

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/requires-recent-login  | Thrown if the user's last sign-in time does not meet the security threshold. Use [firebase.User#reauthenticateWithCredential](#reauthenticatewithcredential) to resolve. This does not apply if the user is anonymous. |

### getIdToken
[method]getIdToken(forceRefresh) returns Promise containing string;[/method]

Returns a JWT token used to identify the user to a Firebase service.

Returns the current token if it has not expired, otherwise this will refresh the token and return a new one.

| Parameter |         |
| --------- | ------- |
| forceRefresh   | **boolean** (option) <br /> Force refresh regardless of token expiration. |

### linkAndRetrieveDataWithCredential
[method]linkAndRetrieveDataWithCredential(credential) returns Promise containing [UserCredential](#);[/method]

Links the user account with the given credentials, and returns any available additional user information, such as user name.

| Parameter |         |
| --------- | ------- |
| credential   | **[AuthCredential](#)** (option) <br /> The auth credential. <br /> Value must not be null. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/provider-already-linked  | Thrown if the provider has already been linked to the user. This error is thrown even if this is not the same provider's account that is currently linked to the user. |
| auth/invalid-credential  | Thrown if the provider's credential is not valid. This can happen if it has already expired when calling link, or if it used invalid token(s). See the Firebase documentation for your provider, and make sure you pass in the correct parameters to the credential method. |
| auth/credential-already-in-use  | Thrown if the account corresponding to the credential already exists among your users, or is already linked to a Firebase User. For example, this error could be thrown if you are upgrading an anonymous user to a Google user by linking a Google credential to it and the Google credential used is already associated with an existing Firebase Google user. The fields error.email, error.phoneNumber, and error.credential ([firebase.auth.AuthCredential](#)) may be provided, depending on the type of credential. You can recover from this error by signing in with error.credential directly via [firebase.auth.Auth#signInWithCredential](version /auth/reference#signinwithcredential). |
| auth/email-already-in-use  | Thrown if the email corresponding to the credential already exists among your users. When thrown while linking a credential to an existing user, an error.email and error.credential ([firebase.auth.AuthCredential](#)) fields are also provided. You have to link the credential to the existing user with that email if you wish to continue signing in with that credential. To do so, call [firebase.auth.Auth#fetchProvidersForEmail](version /auth/reference#fetchprovidersforemail), sign in to error.email via one of the providers returned and then [firebase.User#linkWithCredential](#linkwithcredential) the original credential to that newly signed in user |
| auth/operation-not-allowed  | Thrown if you have not enabled the provider in the Firebase Console. Go to the Firebase Console for your project, in the Auth section and the **Sign in Method** tab and configure the provider. |
| auth/invalid-email  | Thrown if the email used in a [firebase.auth.EmailAuthProvider#credential](#) is invalid. |
| auth/wrong-password  | Thrown if the password used in a [firebase.auth.EmailAuthProvider#credential](#) is not correct or when the user associated with the email does not have a password. |
| auth/invalid-verification-code  | Thrown if the credential is a [firebase.auth.PhoneAuthProvider#credential](#) and the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the credential is a [firebase.auth.PhoneAuthProvider#credential](#) and the verification ID of the credential is not valid. |

### linkWithCredential
[method]linkWithCredential(credential) returns Promise containing [UserCredential](#);[/method]

Links the user account with the given credentials, and returns any available additional user information, such as user name.

| Parameter |         |
| --------- | ------- |
| credential   | **[AuthCredential](#)** (option) <br /> The auth credential. <br /> Value must not be null. |

#### Error Codes

| Code | Message |
| --------- | ------- |
| auth/provider-already-linked  | Thrown if the provider has already been linked to the user. This error is thrown even if this is not the same provider's account that is currently linked to the user. |
| auth/invalid-credential  | Thrown if the provider's credential is not valid. This can happen if it has already expired when calling link, or if it used invalid token(s). See the Firebase documentation for your provider, and make sure you pass in the correct parameters to the credential method. |
| auth/credential-already-in-use  | Thrown if the account corresponding to the credential already exists among your users, or is already linked to a Firebase User. For example, this error could be thrown if you are upgrading an anonymous user to a Google user by linking a Google credential to it and the Google credential used is already associated with an existing Firebase Google user. The fields error.email, error.phoneNumber, and error.credential ([firebase.auth.AuthCredential](#)) may be provided, depending on the type of credential. You can recover from this error by signing in with error.credential directly via [firebase.auth.Auth#signInWithCredential](version /auth/reference#signinwithcredential). |
| auth/email-already-in-use  | Thrown if the email corresponding to the credential already exists among your users. When thrown while linking a credential to an existing user, an error.email and error.credential ([firebase.auth.AuthCredential](#)) fields are also provided. You have to link the credential to the existing user with that email if you wish to continue signing in with that credential. To do so, call [firebase.auth.Auth#fetchProvidersForEmail](version /auth/reference#fetchprovidersforemail), sign in to error.email via one of the providers returned and then [firebase.User#linkWithCredential](#linkwithcredential) the original credential to that newly signed in user |
| auth/operation-not-allowed  | Thrown if you have not enabled the provider in the Firebase Console. Go to the Firebase Console for your project, in the Auth section and the **Sign in Method** tab and configure the provider. |
| auth/invalid-email  | Thrown if the email used in a [firebase.auth.EmailAuthProvider#credential](#) is invalid. |
| auth/wrong-password  | Thrown if the password used in a [firebase.auth.EmailAuthProvider#credential](#) is not correct or when the user associated with the email does not have a password. |
| auth/invalid-verification-code  | Thrown if the credential is a [firebase.auth.PhoneAuthProvider#credential](#) and the verification code of the credential is not valid. |
| auth/invalid-verification-id  | Thrown if the credential is a [firebase.auth.PhoneAuthProvider#credential](#) and the verification ID of the credential is not valid. |

### linkWithPhoneNumber
### reauthenticateAndRetrieveDataWithCredential
### reauthenticateWithCredential
### reauthenticateWithPhoneNumber
### 
TODO

### reload
[method]reload() returns Promise containing void;[/method]

Refreshes the current user, if signed in.

### sendEmailVerification
TODO

### toJSON
[method]reload() returns Object;[/method]

Returns a JSON-serializable representation of this object.

### unlink
[method]unlink(providerId) returns [User](#methods);[/method]

## Properties

### displayName
[method]displayName returns string or null;[/method]

The user's display name (if available).

### email
[method]email returns string or null;[/method]

The user's email address (if available).

### emailVerified
[method]emailVerified returns boolean;[/method]

Returns `true` if the user's email address has been verified.

### isAnonymous
[method]isAnonymous returns boolean;[/method]

Returns `true` if the user is anonymous.

### photoURL
[method]photoURL returns string or null;[/method]

The URL of the user's profile picture (if available).

### providerData
[method]providerData returns Array of [UserInfo](#);[/method]

Additional provider-specific information about the user.

### providerId
[method]providerId returns string;[/method]

The authentication provider ID for the current user. For example, 'facebook.com', or 'google.com'.

### refreshToken
[method]refreshToken returns string;[/method]

A refresh token for the user account. Use only for advanced scenarios that require explicitly refreshing tokens.

### uid
[method]uid returns string;[/method]

The user's unique ID.
