# Firebase Auth - Google Auth : Firebase For Web

VideoTutorial: https://youtube.com

### Auth with Using Google Sign-In

If you are building a web app, the easiest way to authenticate your users with Firebase using their Google Accounts is to handle the sign-in flow with the Firebase JavaScript SDK.

Follow these steps:

1.  Create an instance of the Google provider object:
    ```js
    var provider = new firebase.auth.GoogleAuthProvider();
    ```
2.  Authenticate with Firebase using the Google provider object. You can prompt your users to sign in with their Google Accounts either by opening a pop-up window or by redirecting to the sign-in page. The redirect method is preferred on mobile devices.

    To sign in with a pop-up window, call `signInWithPopup`:

    ```js
    firebase
      .auth()
      .signInWithPopup(provider)
      .then(function (result) {
        // This gives you a Google Access Token. You can use it to access the Google API.
        var token = result.credential.accessToken;
        // The signed-in user info.
        var user = result.user;
        // ...
      })
      .catch(function (error) {
        // Handle Errors here.
        var errorCode = error.code;
        var errorMessage = error.message;
        // The email of the user's account used.
        var email = error.email;
        // The firebase.auth.AuthCredential type that was used.
        var credential = error.credential;
        // ...
      });
    ```

    To sign in by redirecting to the sign-in page, call `signInWithRedirect`:

    ```js
    firebase
      .auth()
      .getRedirectResult()
      .then(function (result) {
        if (result.credential) {
          // This gives you a Google Access Token. You can use it to access the Google API.
          var token = result.credential.accessToken;
          // ...
        }
        // The signed-in user info.
        var user = result.user;
      })
      .catch(function (error) {
        // Handle Errors here.
        var errorCode = error.code;
        var errorMessage = error.message;
        // The email of the user's account used.
        var email = error.email;
        // The firebase.auth.AuthCredential type that was used.
        var credential = error.credential;
        // ...
      });
    ```

    ##### 2.2.2) Sign Out User

    To sign out a user, call `signOut`:

    ```js
    firebase
      .auth()
      .signOut()
      .then(function () {
        // Sign-out successful.
      })
      .catch(function (error) {
        // An error happened.
      });
    ```

    ##### 2.2.2) Sign Out User

    To sign out a user, call `signOut`:

    ```js
    firebase
      .auth()
      .signOut()
      .then(function () {
        // Sign-out successful.
      })
      .catch(function (error) {
        // An error happened.
      });
    ```

    ##### 2.2.3) Set an authentication state observer and get user data
    
    For each of your app's pages that need information about the signed-in user, you can call `onAuthStateChanged` method. When a user successfully signs in, you can get information about the user.

       ```js
        firebase.auth().onAuthStateChanged(function(user) {
         if (user) {
            // User is signed in.
            var displayName = user.displayName;
            var email = user.email;
            var emailVerified = user.emailVerified;
            var photoURL = user.photoURL;
            var isAnonymous = user.isAnonymous;
            var uid = user.uid;
            var providerData = user.providerData;
            // ...

         } else {
            // User is signed out.
            // ...
          }
        });
       ```
