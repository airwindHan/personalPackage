<template>
    <div class="menuBox">
        <div class="mainMenu" @click="showList=!showList">{{defaultData}}</div>
        <div class="menuList" v-show="showList">
            <ul>
                <li class="searchBox"><input type="text" v-model="searchVal"></li>
                <div class="scrollBox">
                    <li v-for="(item, index) in list" :key="item.id" v-show="searchMatch(item.value)"
                        @mouseover="setChild1(item.children, index)"
                        @mouseout="setChild1(item.children, -1)">
                        <span>{{item.value}}</span> 
                        <!-- <ul v-if="item.hasChild">
                            <li v-for="childItem in item.children" :key="childItem.id">
                                <span>{{childItem.value}}</span>
                                <ul v-if="childItem.hasChild">
                                    <li v-for="childItem1 in childItem.children" :key="childItem1.id">
                                        <span>{{childItem1.value}}</span>
                                    </li>
                                </ul>
                            </li>
                        </ul>-->
                    </li>
                </div>
            </ul>
            <ul v-show="child1Show" :style="{top:child1Top}" class="child-lv1"  @mouseover="child1Show=true;" @mouseout="child1Show=false">
                <li v-for="item in childList1" :key="item.id">{{item.value}}</li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            defaultData: '菜单',
            showList: false,
            searchVal: '',
            child1Show: false,
            child1Top: 0,
            childList1: [],
            list: [
                {
                    id: 1,
                    value: '菜单1'
                },
                {
                    id: 2,
                    value: '菜单2',
                    hasChild: true,
                    children: [
                        {
                            id:21,
                            value: '菜单21'
                        },
                        {
                            id:22,
                            value: '菜单22',
                            hasChild: true,
                            children: [
                                {
                                    id: 221,
                                    value: '菜单221'
                                },
                                {
                                    id: 222,
                                    value: '菜单222'
                                },
                                {
                                    id: 223,
                                    value: '菜单223'
                                },
                                {
                                    id: 224,
                                    value: '菜单224'
                                },
                                {
                                    id: 225,
                                    value: '菜单225'
                                },
                                {
                                    id: 226,
                                    value: '菜单226'
                                },
                                {
                                    id: 227,
                                    value: '菜单227'
                                }
                            ]
                        },
                        {
                            id:23,
                            value: '菜单23'
                        },
                        {
                            id:24,
                            value: '菜单24'
                        },
                        {
                            id:25,
                            value: '菜单25'
                        },
                        {
                            id:26,
                            value: '菜单26'
                        }
                    ]
                },
                {
                    id: 3,
                    value: '菜单3'
                },
                {
                    id: 4,
                    value: '菜单4'
                },
                {
                    id: 5,
                    value: '菜单5'
                },
                {
                    id: 6,
                    value: '菜单6'
                }
            ]
        }
    },
    methods: {
        searchMatch(val) {
            if(!this.searchVal) {
                return true;
            }
            if(val.indexOf(this.searchVal) != -1) {
                return true;
            } else {
                return false;
            }
        },
        setChild1(data, index) {
            if(!data) {
                this.child1Show = false;
                return;
            }
            if(index != -1) {
                this.childList1 = this.childList1.slice(0,0);
                this.childList1 = this.childList1.concat(data);
                this.child1Top = (index+1) *32 +'px';
                this.child1Show = true;
            }
        }
    },
    components: {
        
    }
}
</script>

<style lang="less" scoped>
    .menuBox {
        position: relative;
        cursor: pointer;
    }
    .mainMenu {
        width: 160px;
        height: 32px;
        left: 0;
        top: 0;
        background: #aaa;
        position: absolute;
    }
    .menuList {
        position: absolute;
        left: 0;
        top: 32px;
    }
    li {
        width: 160px;
        height: 32px;
        line-height: 32px;
        background: #ddd;
        position: relative;
    }
    .scrollBox {
        width: 160px;
        max-height: 160px;
        overflow: auto;
    }
    .searchBox input{
        width: 100%;
        height: 100%;
        background: transparent;
        border: none;
    }
    ul {
        position: absolute;
    }

    li:hover {
        background: #00cdcd;
    }
    .child-lv1 {
        position: absolute;
        left: 160px;
        width: 100%;
    }
</style>