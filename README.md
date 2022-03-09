# React Native Developer questions

### 1. State vs Props
What is the difference between React components props and state ?<br />
What are their purposes ?

### 2. OS specific implementation
Name all possible methods to implement OS specific code in React Native

### 3. useCallback
What is `useCallback` hook used for ? Explain how it works

### 4. Components rendering
Name all possible ways to re-render component

### 5. Functional components lifecycle

### 6. Navigation
`screen.tsx`
```tsx
import React, { useCallback } from 'react'
import { StackScreenProps } from '@react-navigation/stack'

import { Button, Container } from './styles'

type Props = StackScreenProps<Record<string, any | undefined>, string> & {
  isFirstStep?: boolean
}

function TestScreen({ isFirstStep, navigation }: Props) {
  const handleButtonPress = useCallback(() => {
    if (isFirstStep) {
      navigation.navigate('Route.SecondStep')
    } else {
      navigation.navigate('Route.TestStepsFinish')
    }
  }, [isFirstStep])

  return (
    <Container>
      <Button onPress={handleButtonPress} />
    </Container>
  )
}

export default TestScreen
```
`navigator.tsx`
```tsx
import React from 'react'
import { createStackNavigator } from '@react-navigation/stack'

import TestScreen from 'screens/Test'
import TestFinishScreen from 'screens/TestFinish'

const Stack = createStackNavigator()

function TestNavigator() {
  return (
    <Stack.Navigator headerMode="none">
      <Stack.Screen name="Route.FirstStep">
        {(props) => <TestScreen {...props} isFirstStep />}
      </Stack.Screen>
      <Stack.Screen name="Route.SecondStep">
        {(props) => <TestScreen {...props} />}
      </Stack.Screen>
      <Stack.Screen name="Route.TestStepsFinish">
        {(props) => <TestFinishScreen {...props} />}
      </Stack.Screen>
    </Stack.Navigator>
  )
}

export default TestNavigator
```

### 7. Styling
`styles.ts`
```ts
import styled from 'styled-components/native'

export const Container = styled.View`
  margin-top: 16px;
`
```
`index.tsx`
```tsx
import React from 'react'
import { Text } from 'react-native'

import { Container } from './styles'

function TestComponent() {
  return (
    <Container>
      <Text>Something</Text>
    </Container>
  )
}

export default TestComponent
```
