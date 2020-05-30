

<template>
    <app-navigator></app-navigator>
</template>

<script>
    import {
        createAppContainer,
        createStackNavigator
    } from "vue-native-router";
    import MainScreen from "./Main.vue";
    import AnotherScreen from "./Another.vue";
     const StackNavigator = createStackNavigator(
        {
            Home: MainScreen,
            Another: AnotherScreen,
        },
        {
            initialRouteName: 'Home'
        }
    );
    const AppNavigator = createAppContainer(StackNavigator);
    export default {
        components: { AppNavigator }
    }
</script>

