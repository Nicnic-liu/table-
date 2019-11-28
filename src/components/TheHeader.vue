<template>
    <section>
        <nav class="header-bar">
            <div class="header-bar-container">
                <img src="../../assets/images/logo.png" alt="" class="logo">
            </div>
        </nav>
        <Hamburger></Hamburger>
        <div class="f-fr g-logout">
            <el-link type="success" class="g-user-name" @click="goUserDetail()">{{username}}</el-link>
            <el-button type="danger" @click="logout()">退出</el-button>
        </div>
    </section>
</template>
<script>
    /**
     * 头部组件
     *
     *@date 2019-04-30
     *@author chenyongzheng
     */
    // 引入侧边栏导航开关
    import Hamburger from '@/components/hamburger/Hamburger.vue'
    // 引入Vuex
    import {mapState, mapGetters, mapActions} from 'vuex'

    export default {
        name: 'TheHeader',
        components: {
            Hamburger
        },
        computed: {
            username() {
                return this.$localStorage.getItem('user_name');
            }
        },
        data() {
            return {}
        },
        methods: {
            /**
             * 登出
             */
            logout() {

                this.$confirm('此操作将退出系统, 是否继续?', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {

                    this.$localStorage.clear();
                    window.location.href = '/';
                    this.clearView();
                }).catch(() => {
                    this.$message({
                        type: 'info',
                        message: '已取消'
                    });
                });
            },

            /**
             * 去用户详情
             */
            goUserDetail() {

                this.addView({
                    index: 'managerDetail',
                    title: '管理员详情',
                    barFlag: false
                })

                this.$router.push({
                    path: '/managerDetail'
                });
            },

            /**
             * 引用vuex中操作路由模块
             */
            ...mapActions('tagView', ['addView', 'clearView'])
        },
        mounted() {
        }
    }
</script>
<style scoped lang="scss">
    .header-bar {
        width: 200px;
        display: inline;
        z-index: 1030;
        height: 60px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, .08);

        .header-bar-container {
            position: relative;
            float: left;
            width: 200px;
            height: 50px;
            overflow: hidden;

            .logo {
                width: 180px;
                height: 60px;
                margin-left: 10px;
            }
        }
    }

    .g-logout {
        margin-right: 30px;

        .g-user-name {
            margin-right: 30px;
        }
    }

</style>
