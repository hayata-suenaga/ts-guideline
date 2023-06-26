# Expensify TypeScript React Native CheatSheet

## Table of Contents

- [1.1 `props.children`](#convension-children)
- [1.2 `forwardRef`](#forwardRef)
- [1.3 Animated styles](#animated-style)
- [1.4 Style Props](#style-props)
- [1.5 Render Prop](#render-prop)
- [1.6 Type Narrowing](#type-narrowing)
- [1.7 Errors in Type Catch Clauses](#try-catch-errors)

## CheatSheet

- [1.1](#convension-children) **`props.children`**

  ```tsx
  type WrapperComponentProps = {
    children?: React.ReactNode;
  };

  function WrapperComponent({ children }: Props) {
    return <View>{children}</View>;
  }

  function App() {
    return (
      <WrapperComponent>
        <View />
      </WrapperComponent>
    );
  }
  ```

- [1.2](#forwardRef) **`forwardRef`**

  ```ts
  import { forwardRef, useRef, ReactNode } from "react";
  import { TextInput, View } from "react-native";

  export type CustomButtonProps = {
    label: string;
    children?: ReactNode;
  };

  const CustomTextInput = forwardRef<TextInput, CustomButtonProps>(
    (props, ref) => {
      return (
        <View>
          <TextInput ref={ref} />
          {props.children}
        </View>
      );
    }
  );

  function ParentComponent() {
    const ref = useRef<TextInput>;
    return <CustomTextInput ref={ref} label="Press me" />;
  }
  ```

- [1.3](#animated-style) **Animated styles**

  ```ts
  import {useRef} from 'react';
  import {Animated, StyleProp, ViewStyle} from 'react-native';

  type MyComponentProps = {
      style?: Animated.WithAnimatedValue<StyleProp<ViewStyle>>;
  };

  function MyComponent({ style }: Props) {
      return <Animated.View style={style} />;
  }

  function MyComponent() {
      const anim = useRef(new Animated.Value(0)).current;
      return <Component style={{opacity: anim.interpolate({...})}} />;
  }
  ```

- [1.4](#style-props) **Style Props**

      When converting or typing style props, use `StyleProp<T>` type where `T` is the type of styles related to the component your prop is going to apply.

  ```tsx
  import { StyleProp, ViewStyle, TextStyle, ImageStyle } from "react-native";

  type MyComponentProps = {
    containerStyle?: StyleProp<ViewStyle>;
    textStyle?: StyleProp<TextStyle>;
    imageStyle?: StyleProp<ImageStyle>;
  };

  function MyComponentProps({ containerStyle, textStyle, imageStyle }: MyComponentProps) = {
    <View style={containerStyle}>
        <Text style={textStyle}>Sample Image</Text>
        <Image style={imageStyle} src={'https://sample.com/image.png'} />
    </View>
  }
  ```

- [1.5](#render-prop) **Render Prop**

  ```tsx
  type ParentComponentProps = {
    children: (label: string) => React.ReactNode;
  };

  function ParentComponent({ children }: Props) {
    return children("String being injected");
  }

  function App() {
    return (
      <ParentComponent>
        {(label) => (
          <View>
            <Text>{label}</Text>
          </View>
        )}
      </ParentComponent>
    );
  }
  ```

- [1.6](#type-narrowing) **Type Narrowing** Narrow types down using `typeof` or custom type guards.

  ```ts
  type Manager = {
    role: "manager";
    team: string;
  };

  type Engineer = {
    role: "engineer";
    language: "ts" | "js" | "php";
  };

  function introduce(employee: Manager | Engineer) {
    console.log(employee.team); // TypeScript errors: Property 'team' does not exist on type 'Manager | Engineer'.

    if (employee.role === "manager") {
      console.log(`I manage ${employee.team}`); // employee: Manager
    } else {
      console.log(`I write ${employee.language}`); // employee: Engineer
    }
  }
  ```

  In the above code, type narrowing is used to determine whether an employee object is a Manager or an Engineer based on the role property, allowing safe access to the `team` property for managers and the `language` property for engineers.

  We can also create a custom type guard function.

  ```ts
  function isManager(employee: Manager | Engineer): employee is Manager {
    return employee.role === "manager";
  }

  function introduce(employee: Manager | Engineer) {
    if (isManager(employee)) {
      console.log(`I manage ${employee.team}`); // employee: Manager
    }
  }
  ```

  In the above code, `employee is Manager` is Type Predicate. It signifies that the return type of `isManager` is a `boolean`, indicating whether a value passed to the function is of a certain type (e.g. `Manager`).

- [1.7] **Error in Try Catch Clauses**

  Errors in try/catch clauses are typed as unknown, if the developer needs to use the error data they must conditionally check the type of the data first. Use type narrowing

  ```ts
  try {
      ....
  } catch (e) { // `e` is `unknown`.
      if (e instanceof Error) {
          // you can access properties on Error
          console.error(e.message);
      }
  }
  ```
