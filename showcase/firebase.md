# Firebase - Work in Progress

### Getting Started with Firebase
#### What is Firebase?
Firebase is a Backend-as-a-Service.
 

Firebase helps developers to focus on more import stuff, like delivering good experience for the user, without worrying about the backend, sync data or scalability.
You can find all the products offered by Firebase [here]( https://firebase.google.com/products/ ).

Firebase SDK offers integration with:
* Android
* iOS
* Web (JavaScript)
* Node.js
* Java
* C++
* Python

Firebase also has an handful of libraries that help integration with different languages or frameworks ( Angular, React, Ember, etc…. ).

### Database
Firebase offers two types of databases, both NoSQL: Realtime Database and Firestore. Firestore is in beta, but is the new flagship of Google Firebase.
Firestore is a big improvement over Realtime Database. You can find a list of differences between them [ here ](https://firebase.google.com/docs/database/rtdb-vs-firestore).

**The most important feature of firebase databases is that it keeps all your data in sync automatically through WebSockets.**. This way you can sync your data to all your clients almost instanlty.

### Authentication
* Supports authentication using, email/password, phone numbers and also popular federated identity providers like Google, Facebook, Twitter…
* You can use the Firebase Authentication SDK or FirebaseUI Auth

### Cloud Storage
* is design to help you quickly and easily store and serve user-generated content, such as photos and videos

### Firebase Hosting
* its an easy to use file hosting, you files will be served from CDNs using http2


### [Pricing](https://firebase.google.com/pricing/)
* they have pretty decent free tire plan, you have the option to pay as you go or to choose a monthly subscription

### Sample Code

```html
<!DOCTYPE html>
<html>
<head>
<title>Firestore</title>
</head>
<body>
    <div id="content">Loading...</div>
    <script src="https://www.gstatic.com/firebasejs/4.6.0/firebase.js"></script>
    <script src="https://www.gstatic.com/firebasejs/4.6.0/firebase-firestore.js"></script>
    <script>
        const config= {
            //All this information can be found in your firebase console ( unique for each project )
            apiKey: "Your Api Key",
            authDomain: "Your AuthDomain",
            databaseURL: "Your DatabaseURL",
            projectId: "Your Project ID",
            storageBucket: "Your storage bucket",
            messagingSenderId: "Your ID"
        };
        firebase.initializeApp( config );
        const db = firebase.firestore( );//geting the reference to the firestore database
        const posts = db.collection( "posts" )
                  .onSnapshot( snapshot => {
                    const target =  document.querySelector( "#content" );
                    let html = "";
                    if ( snapshot ) {
                        snapshot.forEach( doc => {
                            const { title, content, addedTime } = doc.data( );
                            html += `<div>${ doc.id }</div><div>Title: ${ title }</div><div>${ content }</div><hr />`;
                        } );
                        target.innerHTML = html;
                    }
                } );
</script>
</body>
</html>
```
### Resources
* [Youtube Official Firebase Channel](https://www.youtube.com/user/Firebase)
