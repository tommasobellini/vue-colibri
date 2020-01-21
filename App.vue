<template>
  <app-navigator></app-navigator>
</template>

<script>
import {
  createAppContainer,
  createBottomTabNavigator,
  createMaterialTopTabNavigator,
  createStackNavigator
} from "vue-native-router";
import React, { Component } from 'react';
import HomeScreen from "./screens/HomeScreen.vue";
import DetailsScreen from "./screens/DetailsScreen.vue";
import Hand3dScreen from "./screens/Hand3dScreen.vue";
import Icon from 'react-native-vector-icons/FontAwesome5';

import { Ionicons } from "@expo/vector-icons";
import Vue from "vue-native-core";
Vue.component("ionicons", Ionicons);
// An iOS style bottom tab-bar navigator
const BottomTabNavigator = createBottomTabNavigator(
  {
    Home: {
      screen: HomeScreen,
      navigationOptions: ({ navigation }) => ({
        tabBarIcon: ({ focused, tintColor }) => {
          return <Icon name="home" size={35} color="#4286f4" />;
        },
      })
    },
    Hand3d: Hand3dScreen,
    Settings: DetailsScreen
  }
);

// // An Android style top tab-bar navigator
// const MaterialTopTabNavigator = createMaterialTopTabNavigator(
//   {
//     Details: DetailsScreen,
//     Settings: SettingsScreen
//   }
// );

// // The navigators can be used as regular screens in any other navigator
// const StackNavigator = createStackNavigator(
//   {
//     Home: HomeScreen,
//     IOSTabs: BottomTabNavigator,
//     AndroidTabs: MaterialTopTabNavigator
//   }
// );

const AppNavigator = createAppContainer(BottomTabNavigator);

// const StackNavigator = createStackNavigator(
//   {
//     Home: HomeScreen,
//     Details: DetailsScreen,
//   },
//   {
//     initialRouteName: 'Home',
//   }
// );

// const AppNavigator = createAppContainer(StackNavigator);

export default {
  components: { AppNavigator,Icon },
}
</script>