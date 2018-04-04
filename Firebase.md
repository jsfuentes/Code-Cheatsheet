# Firebase

## Making App
Go to firebase console and copy pasta the code they give you to setup connection.

## Using Database/Firestore

Firestore allows you to live update data on as many devices as you want on the frontend. Add listeners to data.

- For testing go to db setting, rules, and set read and write to true(allowing all users to read and write no auth)
- Then you can add data
- the DbRef gets the key value pair from text and on change changes the val of snap
```js
  var bigOne = document.getElementById('bigOne');
  var dbRef = firebase.database().ref().child('text');
  dbRef.on('value', snap => bigOne.innerText = snap.val());
```

## Firebase Authenication

Allows ease console setup of Facebook auth, twitter, github, etc where all the user objects look the same
```js
const auth = firebase.auth();
auth.signInWithEmailAndPassoword(email, pass);
//return a promise where you can resolve that user
auth.createUserWithEmailAndPassword(email, pass);
 //another promise
auth.onAuthStateChanged(firebaseUser => { });
//fires callback on changes, firebaseUser = null when logout
```

Using the promise
```js
const promise = auth.signInWithEmailAndPassoword(email, pass);
promise.catch(e => console.log(e, message));
```

Signup event
```js
function signUp(email, pass)) {
  const promise = auth.createUserWithEmailAndPassword(email, pass);
  promise.catch(e => console.log(e.message));
  //catch errors but dont do anything on state change just make request
  //using promise then would not allow auth changes
}

//SIGNOUT
firebase.auth().signOut();

//handle the auth state changes here
firebase.auth().onAuthStateChanged(firebaseUser => {
  if(firebaseUser) {
    //logged in
  } else {
    //not logged in
  }
})
```

## Ref Objects
In the cloud, event.data.ref

- .child('specificChild')
- .set(value) //returns promise

## Delta Snapshot
- .ref //to get about ref
- .changed() //boolean if changed
- .val() //to get the actual value there

Getting val
```js
ref.once('value')
  .then(function(dataSnapshot) {
    // handle read data.
  });
  ```

## Adding Backend APIS / Cloud Functions

Could do clientside, but like secrets on client?? and write for every platform??
Require the APIS apparently @google-cloud/speech can be require(nodejs right). Then you add listener to upload file and then use api then write to translationed file. So you handle the conversion clientside. Then deploy these


### Setup
Need firebase CLI
`npm install -g firebase-tools`
`firebase login`

Start Project
`firebase init functions`
`firebase deploy`

Return the promise from the set method to allow it to wait or null/

### Basic Usage

functions.database/firestore.ref('/somepath/1')
Can do:
- onWrite(), created, updated, or deleted
- onCreate(), created
- onUpdate(), updated
- onDelete(), deleted

Return a null or a promise to be waited for b4 cleaning up

```js
exports.test = functions.database
.ref('/games/1')
  .onUpdate(event => {
    const game = event.data.val() //game object
    return null
  }
```

### Get specific changes
Use .params.[key] to get the wildcard routes
```js
exports.locationChange = functions.database
  .ref('/games/1/players/{playerId}/location')
  .onUpdate(event => {
    const location = event.data.val();
    console.log("LOC change");
    console.log(location);
    console.log(event.params.playerId)
```

### Promises

Can use the promises as promises with then chains and all and such
```js
const p1Update = event.data.ref.child(pId).child("potentialHacks").set(curPotentialHacks);
const p2Update = event.data.ref.child(changedPId).child("potentialHacks").set(changedPotentialHacks);
return Promise.all([p1Update, p2Update]);
```

### Modularize Files

Nodejs style simply require i.e `const location = require('./location.js');`
