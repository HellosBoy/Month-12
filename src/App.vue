<template>
    <div id="app">
        <header>
            <input type="text" v-model="url">
        </header>
        <main>
            <div class="left">
                <p :class="{active: curIndex === index}" @click="changeTab(index)" v-for="(item, index) in list" :key="index">{{item.name}}</p>
            </div>
            <RightView class="right" @changeUrl="changeUrl" :info="right" />
        </main>
    </div>
</template>

<script>
import axios from 'axios'
import RightView from './components/rightView'
export default {
    name: 'app',
    components: {
        RightView
    },
    data(){
        return {
            list: [],
            // 表示当前选中
            curIndex: 0,
            right: {},
            url: ''
        }
    },
    methods: {
        changeTab(index){
            this.curIndex = index;
            this.right = this.list[this.curIndex]
        },
        changeUrl(url){
            this.url = url
        }
    },
    created(){
        axios.get('/list').then(r => {
            this.list = r.data.values
        })
    }
}
</script>

<style lang="scss">
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
#app, html, body {
    width: 100%;
    height: 100%;
}
#app {
    display: flex;
    flex-direction: column;
}
header {
    width: 100%;
    height: 60px;
    background: #cccccc;
    input {
        width: 100%;
        height: 100%;
    }
}
main {
    flex: 1;
    overflow: hidden;
    display: flex;
}
.left {
    width: 100px;
    background: #66ccff;
    overflow-y: auto;
    p {
        line-height: 45px;
        border-bottom: 1px solid #cccccc;
        &.active {
            background: tomato;
            color: #ffffff;
        }
    }
} 
.right {
    flex: 1;
    overflow: hidden;
}
</style>
