# Navigation

- Stack Navigator creates a stack like web with back, except the component lower in the stack will not be unmounted

### Basic Setup

```react
import * as React from 'react';
import { View, Text } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

type RootStackParamList = {
  OnboardingView: { stepIdx: number };
  StoryCategoryListView: undefined;
  StoryCategoryView: { storyCategoryId: string; storyId?: string };
};

const Stack = createNativeStackNavigator<RootStackParamList>();

function HomeScreen() {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Text>Home Screen</Text>
    </View>
  );
}

const Stack = createNativeStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={HomeScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```

### Usage

```react
import { Route, useNavigation } from '@react-navigation/native';

interface StoryCategoryViewProps {
  route: Route<'StoryCategoryView', ReactNavigation.RootParamList['StoryCategoryView']>;
}

export default function StoryCategoryView({ route }: StoryCategoryViewProps) {
  const storyCategoryId = route.params?.storyCategoryId;
  const storyId = route.params?.storyId;

  const navigation = useNavigation();
  
  const navigateToRemix = useCallback(() => {
      navigation.navigate('RemixFilterView', { filterId: filter.id });
  }, []);
```

