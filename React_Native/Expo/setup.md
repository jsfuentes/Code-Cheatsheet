# Setup

## etup

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

## Install Packages

Use

```
npx expo install
```

instead of `npm install` so it installs the latest version of the package that is compatable with current version of expo sdk

## Building

```bash
npm install -g eas-cli
```

Need expo account and to login, can then build projects

```bash
eas build --platform ios #login and follow prompts
eas submit --platform ios #can submit build id from the uuid in the previous step at the end of the link
```

