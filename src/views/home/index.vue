<template>
    <div class="page-home">
        <cube-button @click="goConsolePage">{{ msg }}</cube-button>
        <cube-input v-model='searchInputValue' ></cube-input>
        <input type="search" v-focus :value="searchVal | toFixed" title=""/>
        基础路径：{{publicPath}}
        demo：{{blogTitle}}
    </div>
</template>

<script>
    export default {
        name: 'home',
        data () {
            return {
                msg: '首页-阿卡迪亚',
                searchInputValue: '搜索厂家/生产编号',
                publicPath: process.env.BASE_URL,
                blogTitle: '你好',
                searchVal: 1
            }
        },
        watch: {
            // 用于搜索联想
            searchInputValue: {
                handler: 'searchSuggest', // 使用函数字面量方法调用，化简watchers
                immediate: true // 创建数组时立马执行一次
            }
        },
        mounted () {
            console.log(this.$el)
        },
        methods: {
            searchSuggest () {
                console.log('使用函数字面量方法调用，化简watchers')
            },
            goConsolePage () {
                // 跳转到console页面 没有路由
                window.location.href = location.href + 'console.html'
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
    @import "../../stylus/base/base.styl"
</style>
