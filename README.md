# React Native Developer questions

## Navigation

`screen.tsx`

```ts
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

```ts
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
      <Stack.Screen name="Route.SecondStep">{(props) => <TestScreen {...props} />}</Stack.Screen>
      <Stack.Screen name="Route.TestStepsFinish">
        {(props) => <TestFinishScreen {...props} />}
      </Stack.Screen>
    </Stack.Navigator>
  )
}

export default TestNavigator

```

## styling
`styles.ts`
```ts
import styled from 'styled-components/native'

export const Content = styled.View`
  margin-top: 16px;
`
```
`index.tsx`
```ts
import React from 'react'
import { Text } from 'react-native'

import { Content } from './styles'

function TestComponent() {
  return (
    <Content>
      <Text>Something</Text>
    </Content>
  )
}

export default TestComponent
```