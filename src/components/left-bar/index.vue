<template>
    <div class="nav-container">
        <div class="nav-logo">
            <!-- <span></span> -->
        </div>
        <el-button size="small" style="width: 50%;margin-left: 25%" @click="logout()">退出登录</el-button>
        <div class="nav-menus">
            <el-menu
                    :default-active="activeIndex"
                    background-color="#545c64"
                    text-color="#fff"
                    active-text-color="#ffd04b"
            >
                <div v-for="(v,i) in navData" :key="i">
                    <el-menu-item :index="v.menuIndex" v-if="v.subMenu.length === 0" @click="linkRoute(v)">
                        <span>{{v.name}}</span>
                    </el-menu-item>
                    <el-submenu :index="v.menuIndex" v-else>
                        <template slot="title">
                            <span>{{v.name}}</span>
                        </template>
                        <el-menu-item-group>
                            <el-menu-item
                                    @click="linkRoute(subV)"
                                    v-for="(subV, subI) in v.subMenu"
                                    :index="subV.subIndex"
                                    :key="subI"
                            >{{subV.name}}
                            </el-menu-item>
                        </el-menu-item-group>
                    </el-submenu>
                </div>
            </el-menu>
        </div>

    </div>
</template>
<script>
    import "./index.scss";
    import locals from "../../lib/local_store.js"
    export default {
        name: "leftBar",
        data() {
            return {
                navData: [
                    {
                        name: "平台及商户管理",
                        menuIndex: "1",
                        subMenu: [
                            {
                                name: "平台管理",
                                subIndex: "1-1",
                                route: "/platform_manage/platform",
                            },
                            {
                                name: "商户管理",
                                subIndex: "1-2",
                                route: "/merchant_manage/merchant",
                            },
                        ]
                    },
                    {
                        name: "支付管理",
                        menuIndex: "2",
                        subMenu: [
                            {
                                name: "银行渠道管理",
                                subIndex: "2-1",
                                route: "/pay_manage/bank_list"
                            },
                            {
                                name: "支付产品管理",
                                subIndex: "2-2",
                                route: "/pay_manage/products"
                            },

                        ]
                    },
                    {
                        name: "会员管理",
                        menuIndex: "3",
                        subMenu: [
                            {
                                name: "会员列表",
                                subIndex: "3-1",
                                route: "/member_list"
                            },
                            {
                                name: "等级设置",
                                subIndex: "3-2",
                                route: "/rate_list"
                            },
                            {
                                name: "事件埋点管理",
                                subIndex: "3-3",
                                route: "/member_manage/platformevent_list"
                            },
                            {
                                name: "事件值管理",
                                subIndex: "3-4",
                                route: "/member_manage/merchantevent_list"
                            },
                            // {
                            //     name: "服务开通管理",
                            //     subIndex: "3-5",
                            //     route: "/servicemanage_list"
                            // },
                        ]
                    },
                    {
                        name: "营销管理",
                        menuIndex: "4",
                        subMenu: [
                            // {
                            //     name: "卡劵管理",
                            //     subIndex: "4-1",
                            //     route: "/card_list"
                            // },
                            {
                                name: "等级权益",
                                subIndex: "4-2",
                                route: "/ratebenefit_list"
                            },
                            {
                                name: "抢排位躺赚",
                                subIndex: "4-3",
                                route: "/rank_list"
                            },
                            {
                                name: "源头绑定分佣",
                                subIndex: "4-4",
                                route: "/firstBind_list"
                            },
                            {
                                name: "会员源头",
                                subIndex: "4-5",
                                route: "/invitationRegister_list"
                            },
                            {
                                name: "商家卖赚",
                                subIndex: "4-6",
                                route: "/merchantSalesCom_list"
                            },
                            {
                                name: "内容方分佣",
                                subIndex: "4-7",
                                route: "/contentSideCommission_list"
                            },
                            {
                                name: "专题活动",
                                subIndex: "4-8",
                                route: "/specialEvent_list"
                            },
                        ]
                    },
                    {
                        name: "收益管理",
                        menuIndex: "5",
                        subMenu: [
                            {
                                name: "支付收益",
                                subIndex: "5-1",
                                route: "/deal_manage/pay_records"
                            },
                            {
                                name: "交易订单管理",
                                subIndex: "5-2",
                                route: "/pay_manage/orders"
                            },
                        ]
                    },
                    {
                        name: "审批管理",
                        menuIndex: "6",
                        subMenu: [
                            {
                                name: "支付审批",
                                subIndex: "6-1",
                                route: "/approval_manage/pay_approve"
                            }
                        ]
                    },
                    {
                        name: "账户管理",
                        menuIndex: "7",
                        subMenu: [
                            {
                                name: "账户信息",
                                subIndex: "7-1",
                                route: "/accounts/index"
                            },
                            {
                                name: "账户历史信息",
                                subIndex: "7-2",
                                route: "/accounts/history_accounts"
                            }
                        ]
                    },
                    {
                        name: "财务管理",
                        menuIndex: "8",
                        subMenu: [
                            {
                                name: "账户列表",
                                subIndex: "8-1",
                                route: "/finance/index"
                            },
                            {
                                name: "提现列表",
                                subIndex: "8-2",
                                route: "/finance/withdraw"
                            },
                            {
                                name: "账户历史记录",
                                subIndex: "8-3",
                                route: "/finance/history"
                            }
                        ]
                    },
                    /**
                     * 侧边栏
                     *
                     * @data 2019-07-13
                     * @author sunshanshan
                     */
                    {
                        name: "创客管理",
                        menuIndex: "9",
                        subMenu: [
                            {
                                name: "创客管理",
                                subIndex: "9-1",
                                route: "/creator_manage/creator_list"
                            }
                        ]
                    },
                    /**
                     * 账号管理侧边栏
                     *
                     * @data 2019-07-15
                     * @author 刘壮
                     */
                    {
                        name: "账号管理",
                        menuIndex: "10",
                        subMenu: [
                            {
                                name: "部门管理",
                                subIndex: "10-1",
                                route: "/personnel_manage/department_list"
                            },
                            {
                                name: "人员管理",
                                subIndex: "10-2",
                                route: "/personnel_manage/personnel_list"
                            }
                        ]
                    },

                    // {
                    //   name: "权限管理",
                    //   menuIndex: "8",
                    //   subMenu: [
                    //     {
                    //       name: "管理员管理",
                    //       subIndex: "8-1",
                    //       route: "/authority_manage/admin_manage"
                    //     },
                    //     {
                    //       name: "角色管理",
                    //       subIndex: "8-2",
                    //       route: "/authority_manage/role_manage"
                    //     },
                    //     {
                    //       name: "权限管理",
                    //       subIndex: "8-3",
                    //       route: "/authority_manage/index"
                    //     }
                    //
                    //   ]
                    // },
                ],
                activeIndex: "1"
            };
        },
        mounted() {
            this.setCurrentRoute(this.$router.history.current.path)
        },
        methods: {
            linkRoute(v) {
                this.$router.push({path: v.route});
            },
            setCurrentRoute(path) {
                if (path.indexOf("/platform_manage/platform") > -1) {
                    this.activeIndex = "1-1";
                    return
                }
                if (path.indexOf("/merchant_manage/merchant") > -1) {
                    this.activeIndex = "1-2";
                    return;
                }
                if (path.indexOf("/pay_manage/bank_list") > -1) {
                    this.activeIndex = "2-1";
                    return
                }
                if (path.indexOf("/pay_manage/products") > -1) {
                    this.activeIndex = "2-2";
                    return
                }
                if (path.indexOf("/member_list") > -1) {
                    this.activeIndex = "3-1";
                    return
                }
                if (path.indexOf("/rate_list") > -1) {
                    this.activeIndex = "3-2";
                    return
                }
                if (path.indexOf("/member_manage/platformevent_list") > -1) {
                    this.activeIndex = "3-3";
                    return
                }
                if (path.indexOf("/member_manage/merchantevent_list") > -1) {
                    this.activeIndex = "3-4";
                    return
                }
                // if (path.indexOf("/servicemanage_list") > -1) {
                //     this.activeIndex = "3-5";
                //     return
                // }
                // if (path.indexOf("/card_list") > -1) {
                //     this.activeIndex = "4-1";
                //     return
                // }
                if (path.indexOf("/ratebenefit_list") > -1) {
                    this.activeIndex = "4-2";
                    return
                }
                if (path.indexOf("/rank_list") > -1) {
                    this.activeIndex = "4-3";
                    return
                }
                if (path.indexOf("/firstBind_list") > -1) {
                    this.activeIndex = "4-4";
                    return
                }
                if (path.indexOf("/invitationRegister_list") > -1) {
                    this.activeIndex = "4-5";
                    return
                }
                if (path.indexOf("/merchantSalesCom_list") > -1) {
                    this.activeIndex = "4-6";
                    return
                }
                if (path.indexOf("/contentSideCommission_list") > -1) {
                    this.activeIndex = "4-7";
                    return
                }
                if (path.indexOf("/specialEvent_list") > -1) {
                    this.activeIndex = "4-8";
                    return
                }

                if (path.indexOf("/deal_manage/pay_records") > -1) {
                    this.activeIndex = "5-1";
                    return;
                }
                if (path.indexOf("/pay_manage/orders") > -1) {
                    this.activeIndex = "5-2";
                    return
                }
                if (path.indexOf("/approval_manage/pay_approve") > -1) {
                    this.activeIndex = "6-1";
                    return;
                }
                if (path.indexOf("/deal_manage/orders") > -1) {
                    this.activeIndex = "6-1";
                    return;
                }
                if (path.indexOf("/accounts/index") > -1) {
                    this.activeIndex = "7-1";
                    return;
                }
                if (path.indexOf("/accounts/history_accounts") > -1) {
                    this.activeIndex = "7-2";
                    return;
                }
                if (path.indexOf("/finance/index") > -1) {
                    this.activeIndex = "8-1";
                    return;
                }
                if (path.indexOf("/finance/withdraw") > -1) {
                    this.activeIndex = "8-2";
                    return;
                }
                if (path.indexOf("/finance/history") > -1) {
                    this.activeIndex = "8-3";
                    return;
                }
                if (path.indexOf("/creator_manage/creator_list") > -1) {
                    this.activeIndex = "9-1";
                    return;
                }
                if (path.indexOf("/personnel_manage/department_list") > -1) {
                    this.activeIndex = "10-1";
                    return;
                }
                if (path.indexOf("/personnel_manage/personnel_list") > -1) {
                    this.activeIndex = "10-2";
                    return;
                }
            },
            logout(){
                this.$confirm("确定离开？", '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    locals.removeItem('token')
                    locals.removeItem('name')
                    this.$router.push({
                        path:'/login'
                    })
                }).catch(() => {
                    alert(1212)
                })
            }
        },
        watch: {
            $route(currentRoute) {
                this.setCurrentRoute(currentRoute.path)
            }
        }
    };
</script>

