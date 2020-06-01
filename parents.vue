<template>
    <view>
        <scroll-view :style="{width: '100%'}">
            <view class="border" v-for="parent in parents">
                <touchable-opacity class="flex-container" :on-press="() => showParent(parent)">
                    <text>{{parent.FirstName}}, {{parent.LastName}}</text>
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
            fetch('https://abckindergarten.herokuapp.com/api/ParentView/')
                .then(response => response.json())
                .then(data => {
                    console.log(data)
                    this.parents = data
                })
        },
        data() {
            return {
                parents:[],
            }
        },
        methods: {
            showParent(parent){
                // this.navigation.navigate("Another", {
                //     title: post.data.title, imageSrc: post.data.preview.images[0].source.url
                // });
                console.log(parent)
            }
        }
    }
</script>
