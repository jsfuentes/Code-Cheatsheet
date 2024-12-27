# Notifications

## Guide to Sending Notifications

1. Get the unique expo push token for the device clientside and store in db
2. Use token on backend to trigger notifications

#### Clientside

```ts
import Constants from 'expo-constants';
import * as Device from 'expo-device';
import * as Notifications from 'expo-notifications';
import { Platform } from 'react-native';
import { IPropertyFuncArgs } from '../types';

export default function requestNotificationPermission() {

  return useCallback(async () => {
    if (Platform.OS === 'android') {
      Notifications.setNotificationChannelAsync('default', {
        name: 'default',
        importance: Notifications.AndroidImportance.MAX,
        vibrationPattern: [0, 250, 250, 250],
        lightColor: '#FF231F7C',
      });
    }

    if (Device.isDevice) {
      const { status: existingStatus } = await Notifications.getPermissionsAsync();
      let finalStatus = existingStatus;
      if (existingStatus !== 'granted') {
        const { status } = await Notifications.requestPermissionsAsync();
        finalStatus = status;
      }
      if (finalStatus !== 'granted') {
        alert('Failed to get push token for push notification!');
        return;
      }

      const token = await Notifications.getExpoPushTokenAsync({
        projectId: Constants.expoConfig.extra.eas.projectId,
      });

      console.log(token.data);
    } else {
      alert('Must use physical device for Push Notifications');
    }
  }, [setState]);
}

```

#### Backend

```ts
const ownerPushTokens = (owner?.expoPushTokenList || []).filter((token: string) =>
  Expo.isExpoPushToken(token)
);
if (ownerPushTokens.length === 0) {
  console.log('No tokens to send expo notifications');
  return;
}

const messages: ExpoPushMessage[] = ownerPushTokens.map((token: string) => ({
  to: token,
  sound: 'default',
  title: 'Your filter 🔥',
  body: `inspired ${user?.username || 'a user'} to create an Optix`,
  data: { filter_id: theme.id, type: 'inspired_optix', count: 1 },
}));

const expo = new Expo();

const ticketChunk = await expo.sendPushNotificationsAsync(messages);

for (let i = 0; i < ticketChunk.length; i++) {
  const ticket = ticketChunk[i];
  const message = messages[i];

  if (ticket.status === 'error') {
    if (ticket.details?.error === 'DeviceNotRegistered') {
      pushTokens = pushTokens.filter((token: string) => token !== message.to);
      //update user with pushToken list	
  	} else {
    console.error('Failed to send notification', ticket);
  	}	
    return;
	}
  
  console.log('Successfully queued notification', ticketChunk);
}
```

