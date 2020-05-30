<template>
    <view class="container">
        <text class="text-color-primary">Myyy Vue Native App</text>
        <text>{{ message }}</text>
        <image
                :style="{width: 50, height: 50}"
                :source="{uri: 'https://facebook.github.io/react-native/docs/assets/favicon.png'}"
        />
        <text-input
                :style="{height: 40, width: 100, borderColor: 'gray', borderWidth: 1}"
                v-model="myInput"
        />
        <!--    <button-->
        <!--            :on-press="handleButton"-->
        <!--            title="My Button"-->
        <!--            color="#841584"-->
        <!--            accessibility-label="Learn more about this purple button"-->
        <!--            :style="{backgroundColor:'red'}"-->
        <!--    />-->
        <touchable-opacity
                :on-press="handleButton"
                :style="{backgroundColor:'red',padding:10}"
        >
            <text :style="{color: 'white'}">My Button</text>
        </touchable-opacity>

        <!--    <flat-list-->
        <!--            :data="countries"-->
        <!--            :render-item="({item}) => renderList(item)"-->
        <!--    />-->
      <scroll-view :style="{width: '100%'}">
<!--        <view class="border" v-for="(country, index) in countries" :key="index">-->
<!--          <view class="flex-container">-->
<!--            <image-->
<!--            :style="{width:40, height:40, borderRadius:25, marginRight:8}"-->
<!--            :source="{uri: country.imageSrc}"-->
<!--            />-->
<!--            <text>{{country.name}}</text>-->
<!--          </view>-->

<!--        </view>-->


        <view class="border" v-for="(post, index) in posts" :key="index">
          <touchable-opacity class="flex-container" :on-press="() => handleListTap(post)">
            <image
                    :style="{width:40, height:40, borderRadius:25, marginRight:8}"
                    :source="{uri: post.data.thumbnail}"
            />
            <text>{{post.data.title}}</text>
          </touchable-opacity>

        </view>
      </scroll-view>

    </view>
</template>

<script>
    import React from 'react';
    import {Text} from 'react-native';

    export default {
        props: {
            navigation: {
                type: Object
            }
        },
        mounted(){
            fetch('https://reddit.com/r/aww.json')
            .then(response => response.json())
            .then(data => {
                this.posts = data.data.children
            })
        },
        data() {
            return {
                message: "Hello world",
                myInput: '',
                posts:[],
                // countries: [
                //     {name: "Australia", imageSrc: "https://play.nativescript.org/dist/assets/img/flags/au.png"},
                //     {name: "Belgium", imageSrc: "https://play.nativescript.org/dist/assets/img/flags/be.png"},
                //
                // ]
            }
        },
        methods: {
            handleButton() {
                // this.myInput = 'Button clicked'
                this.navigation.navigate("Another");
            },
            // renderList: function (item) {
            //     return ( < Text > {item.name} < /Text>)
            // },
          handleListTap(post){
              this.navigation.navigate("Another", {
                  title: post.data.title, imageSrc: post.data.preview.images[0].source.url
              });
          }
        }
    }
</script>

<style>
    .container {
        background-color: white;
        align-items: center;
        justify-content: center;
        flex: 1;
    }

    .text-color-primary {
        color: green;
        font-size: 20px;
    }

    .border {
      border-bottom-width: 1;
      border-color: gray;
      width: 100%;
      padding: 15;
    }

  .flex-container{
    flex-direction: row;
    align-items: center;
  }
</style>
