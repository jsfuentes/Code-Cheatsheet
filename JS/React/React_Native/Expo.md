# Expo

Start a project without Xcode/Android Studio

Quickly deploy changes to your phone over ngrok, hot reloading

Expo SDK gives ez access to underlying native APIS

[Limitations](https://docs.expo.io/versions/latest/introduction/why-not-expo/) => can always eject though

**Managed** workflow has only JS and Expo does rest

**Bare** workflow give full control over native project with Expo SDK, *ejection* to regular react native project

## Setup

```sh
npm install -g expo-cli
```

Then run the following commands to create a new React Native project called "AwesomeProject":

```bash
expo init AwesomeProject

cd AwesomeProject
npm start
```

## Running

1. Download Expo app on your phone and run project 
2. Scan QR code on phone and make sure you are connected on the same Wifi

*Change to tunnel if needed*