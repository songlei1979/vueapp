

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
    import Parents from "./parents.vue";
     const StackNavigator = createStackNavigator(
        {
            Home: MainScreen,
            Another: AnotherScreen,
            Parents: Parents,
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

