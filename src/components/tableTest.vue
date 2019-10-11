<template>
    <div >
        <div class="flex-container" >
            <div class="flex-item item4" v-for="item in viewList">
                <div style="display: flex;" >
                    <div class="flex-item item1" >
                        <div v-for="(title,index) in item.titleList">{{title}}</div>
                    </div>
                    <div class="flex-item item1" >
                        <div v-for="(content,index) in item.contentList">{{content}}</div>
                    </div>
                </div>
        </div>
        </div>
<!--        <div class="box2">-->
<!--            box2:多行多列-->
<!--            <ul>-->
<!--                <li v-for="i in data">-->
<!--                    <div class="com" >-->
<!--                        <div >{{i}}</div>-->
<!--                    </div>-->
<!--                </li>-->
<!--            </ul>-->
<!--        </div>-->
<!--            </div>-->
<!--        </div>-->

<!--        <ul class="flexcontainer">-->
<!--            <li>Something</li>-->
<!--            <li>Fox Example</li>-->
<!--            <li>All About Web</li>-->
<!--            <li>Fox Example</li>-->
<!--            <li>Something</li>-->
<!--            <li>Fox Example</li>-->
<!--            <li>Something</li>-->
<!--            <li>Fox Example</li>-->
<!--        </ul>-->

<!--        <div class="box1">-->
<!--            box1:实现两列多行布局-->
<!--            <ul>-->
<!--                <li>111</li>-->
<!--                <li>222</li>-->
<!--                <li>333</li>-->
<!--                <li>111</li>-->
<!--                <li>222</li>-->
<!--                <li>333</li>-->
<!--                <li>111</li>-->
<!--                <li>222</li>-->
<!--                <li>333</li>-->
<!--                <li>111</li>-->
<!--                <li>222</li>-->
<!--                <li>333</li>-->
<!--                <li>111</li>-->
<!--                <li>222</li>-->
<!--                <li>333</li>-->

<!--            </ul>-->
<!--        </div>-->




    </div>
</template>

<script>
  export default {
    name: 'tableTest',
    data() {
      return{
        data: [
          '刘涛为胡歌庆生',
          '高雷雷炮轰足协',
          '刘涛为胡歌庆生',
          '高雷雷炮轰足协',
        ],
        list: [
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
          '高雷雷炮轰足协',
        ],
        viewList: [
          {
            titleList: [
              'Carrier',
              'Departure Airport code',
              'Arrival City code',
              'Arrival day',
              'Intermeditate Airports',
              'General Aircraft type code',
              'Freight',
              'Passenger Classs 4',
              'Passenger Classs 8',
              'Restriction',
              'Full Routing',
              'Multi Carrier Designator',
              'Ghost Flight',
              'Duplicate Carrier 2',
              'Duplicate Carrier 4',
              'Duplicate Carrier 6',
              'Duplicate Carrier 8',
              'Duplicate Carrier 10',
              'Duplicate Carrier 12',
              'Duplicate Carrier 14'
            ],
            contentList: [
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎'
            ]
          },
          {
            titleList: [
              'Flight No.',
              'Departure City code',
              'Arrival Country code',
              'Elapsed journey time',
              'Aircraft Change',
              'Specific Aircraft type code',
              'Passenger Class 1',
              'Passenger Class 5',
              'Passenger Class 9',
              'Domestic/International marker',
              'Longest Sector',
              'Flight Duplication',
              'Duplicate',
              'Duplicate Flight 2',
              'Duplicate Flight 4',
              'Duplicate Flight 6',
              'Duplicate Flight 8',
              'Duplicate Flight 10',
              'Duplicate Flight 12',
              'Duplicate Flight 14'
            ],
            contentList: [
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎'
            ]
          },
          {
            titleList: [
              'Carrier 2',
              'Departure Airport code',
              'Departure time',
              'Days of Operation',
              'Government Approval',
              'Service type',
              'Passenger Class 2',
              'Passenger Class 6',
              'Passenger Class 10',
              'Effective from date',
              'Distance',
              'Aircraft Owner',
              'Duplicate Carrier 1',
              'Duplicate Carrier 3',
              'Duplicate Carrier 5',
              'Duplicate Carrier 7',
              'Duplicate Carrier 9',
              'Duplicate Carrier 11',
              'Duplicate Carrier 13',
              'Duplicate Carrier 15'
            ],
            contentList: [
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎'
            ]
          },
          {
            titleList: [
              'Flight No.2',
              'Arrival Airport code',
              'Arrival time',
              'Stops',
              'Comment 010/050',
              'Available seats',
              'Passenger Class 3',
              'Passenger Class 7',
              'Freight Classes',
              'Effective to date',
              'Shared Airline Designator',
              'Operating/Non Operating marker',
              'Duplicate Flight 1',
              'Duplicate Flight 3',
              'Duplicate Flight 5',
              'Duplicate Flight 7',
              'Duplicate Flight 9',
              'Duplicate Flight 11',
              'Duplicate Flight 13',
              'Duplicate Flight 15'
            ],
            contentList: [
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎',
              '王小虎'
            ]
          }
        ]
      }
    },
    methods: {

    }
  }
</script>

<style>
    .flex-container {
        display: -webkit-flex;
        display: flex;
        width: 100%;
        background-color: lightgrey;
    }

    .flex-item {
        background-color: cornflowerblue;
        margin: 10px;
    }
    .flex-item1 {
        background-color: palegreen;
        margin: 10px;
        display: -webkit-flex;
        display: flex;
    }

    .item1 {
        flex: 1;
    }

    .item4 {
        flex: 1;
    }
    .flexcontainer {
        width: 600px;
        display: flex;
        flex-flow: row wrap;
    }
    .flexcontainer li {
        width: 25%;
        background-color: pink;
    }
    .box1 {
        width: 500px;
        background: #EEEEEE;
    }
    .box1 ul {
        clear: both;
        overflow: hidden;
    }
    .box1 ul li {
        width: 48%;
        height: 100px;
        margin-bottom: 10px;
        background: skyblue;
        float: left;
    }
    .box1 ul li:nth-child(even) {
        margin-left: 4%;
    }
    .box2 {
        background: #EEEEEE;
        margin-top: 20px;
        width: 500px;
    }
    .box2 ul {
        overflow: hidden;
        margin-left: -10px;
        background: #EEEEEE;
    }
    .box2 ul li {
        width: 25%;
        height: 50px;
        float: left;
        padding-left: 10px;
        box-sizing: border-box;
        margin-bottom: 10px;
    }
    .box2 ul li .com {
        height: inherit;
        background: skyblue;
    }
</style>
