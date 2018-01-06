# Firebase
### Getting Started with Firebase
#### What is Firebase?
Firebase is a Backend-as-a-Service.
 

Firebase helps developers to focus on more import stuff, like delivering good experience for users, without worrying about the backend, data synchronization or scalability.

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
Firestore is the next generation of Realtime Database, it has better queries and automatic scaling, it was build keeping in mind the drawbacks that Realtime Database had. You can find a list of differences between them [ here. ](https://firebase.google.com/docs/database/rtdb-vs-firestore)

**The most important feature of firebase databases is that it keeps all your data in sync automatically through WebSockets.**. This way you can sync your data to all your clients almost instantly. The other option would be get your data from the database only when you request it. It all depends on the type of application you wish to develop, if you need instant data syncronization or not.

**Data Model**

Firestore data model is quite simple, the information is stored in collections, the collection contain documents.
This is a usual data model for a NoSQL database, but one interesting feature of Firestore database is that documents can contain subcollections.
<ul>
 <li>Chat Rooms ( col ) </li>
   <ul>
    <li>
      General ( doc )
      <ul>
       <li>description ( info )</li>
       <li>
        messages ( subcollection )
        <ul>
         <li>message 1 ( doc )</li>
         <li>message 2 ( doc )</li>
         <li>message 3 ( doc )</li>
        </ul>
       </li>
      </ul>
    </li>
    <li>
     Random Chat ( doc )
     <ul>
      <li>description ( info )</li>
       <li>
        messages ( subcollection )
        <ul>
         <li>message 1 ( doc )</li>
         <li>message 2 ( doc )</li>
         <li>...</li>
        </ul>
       </li>
     </ul>
    </li>
   </ul>
</ul>



### Authentication
* Supports authentication using, email/password, phone numbers and also popular federated identity providers like Google, Facebook, Twitter…
* You can use the Firebase Authentication SDK or FirebaseUI Auth

### Cloud Storage
* is design to help you quickly and easily store and serve user-generated content, such as photos and videos

### Firebase Hosting
* its an easy to use file hosting, your files will be served from CDNs using http2


### Pricing
* they have pretty decent free tier plan, you have the option to pay as you go or to choose a monthly subscription
* [more about pricing](https://firebase.google.com/pricing/)


You can find all the products offered by Firebase [here]( https://firebase.google.com/products/ ).

Firebase can be added in two ways in a web project, you can add it as a script using a google CDN  or you can install it using npm( [Firebase](https://www.npmjs.com/package/firebase) ).

```
npm install --save firebase
```
One problem with firebase npm package is that is quite big and will increase your bundle size.
![alt text](https://preview.ibb.co/edVh2G/Screen_Shot_2018_01_06_at_17_38_53.png "Firebase Size")


### Sample Code
In the sample code below we:
* import firebase
* set in the config all the information to the firestore database
* we initialize firebase with the configuration info
* we save the firestore reference in db
* then we access the posts from the database and listen for any changes with onSnapshot function
* then we add each post inside the targeted div
* if any changes are done in the posts database, we get the updates almost instantly

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
        db.collection( "posts" )
          .onSnapshot( snapshot => {
            const target =  document.querySelector( "#content" );
            let html = "";
            if ( snapshot ) {
              snapshot.forEach( doc => {
                const { title, content } = doc.data( );
                   html += `<div>${ doc.id }</div><div>${ title }</div><div>${ content }</div><hr/>`;
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
* [React Native Firebase](https://github.com/invertase/react-native-firebase) - most popular React Native and Firebase implementation ( it supports Firestore as well ).


