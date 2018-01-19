<template>
    <!-- App -->
    <div id="app">

        <!-- Statusbar -->
        <f7-statusbar></f7-statusbar>

        <!-- Left Panel -->
        <f7-panel left reveal layout="dark">
            <f7-view id="left-panel-view" navbar-through :dynamic-navbar="true">
                <f7-navbar v-if="$theme.ios" title="Left Panel" sliding></f7-navbar>
                <f7-pages>
                    <f7-page>
                        <f7-navbar v-if="$theme.material" title="Left Panel" sliding></f7-navbar>
                        <f7-block inner>
                            <p>Left panel content goes here</p>
                        </f7-block>
                        <f7-block-title>Load page in panel</f7-block-title>
                        <f7-list>
                            <f7-list-item link="/about/" title="About"></f7-list-item>
                            <f7-list-item link="/form/" title="Form"></f7-list-item>
                        </f7-list>
                        <f7-block-title>Load page in main view</f7-block-title>
                        <f7-list>
                            <f7-list-item link="/about/" title="About" link-view="#main-view"
                                          link-close-panel></f7-list-item>
                            <f7-list-item link="/form/" title="Form" link-view="#main-view"
                                          link-close-panel></f7-list-item>
                        </f7-list>
                    </f7-page>
                </f7-pages>
            </f7-view>
        </f7-panel>

        <!-- Right Panel -->
        <f7-panel right cover layout="dark">
            <f7-view id="right-panel-view" navbar-through :dynamic-navbar="true">
                <f7-navbar v-if="$theme.ios" title="Right Panel" sliding></f7-navbar>
                <f7-pages>
                    <f7-page>
                        <f7-navbar v-if="$theme.material" title="Right Panel" sliding></f7-navbar>
                        <f7-block>
                            <p>Right panel content goes here</p>
                        </f7-block>
                        <f7-block-title>Load page in panel</f7-block-title>
                        <f7-list>
                            <f7-list-item link="/about/" title="About"></f7-list-item>
                            <f7-list-item link="/form/" title="Form"></f7-list-item>
                        </f7-list>
                        <f7-block-title>Load page in main view</f7-block-title>
                        <f7-list>
                            <f7-list-item link="/about/" title="About" link-view="#main-view"
                                          link-close-panel></f7-list-item>
                            <f7-list-item link="/form/" title="Form" link-view="#main-view"
                                          link-close-panel></f7-list-item>
                        </f7-list>
                    </f7-page>
                </f7-pages>
            </f7-view>
        </f7-panel>

        <!-- Main Views -->
        <f7-views>
            <f7-view id="main-view" navbar-through :dynamic-navbar="true" main>
                <!-- iOS Theme Navbar -->
                <f7-navbar v-if="$theme.ios">


                    <f7-nav-left>
                        <f7-link icon="icon-bars" open-panel="left"></f7-link>
                    </f7-nav-left>
                    <f7-nav-center sliding>{{shipName}}</f7-nav-center>
                    <f7-nav-right>
                        <f7-link icon="icon-bars" open-panel="right"></f7-link>
                    </f7-nav-right>

                </f7-navbar>

                <!-- Pages -->
                <f7-pages>

                    <f7-page>
                        <!-- Simple Chip -->
                        <f7-chip v-text="'地址：'+address"></f7-chip>
                        <!-- Colored Chip -->
                        <f7-chip v-text="'phone:'+phone" color="white"></f7-chip>
                        <!-- Media Chip -->
                        <f7-chip text="Jared73" media='<img src="http://lorempixel.com/100/100/people/9/">'></f7-chip>


                        <div class="content-block">
                            <div class="row no-gutter">
                                <div class="col-30">菜品类别</div>
                                <div class="col-70">菜品详情</div>
                            </div>
                            <div class="row no-gutter">
                                <div class="col-30">
                                    <ul v-for="mType in fmenuTypes" style="list-style-type:none">
                                        <li class="list-group-item" @click="getMenus(shipNo,mType.menuTypeId)">
                                            {{mType.menuType}}
                                        </li>
                                    </ul>
                                </div>
                                <div class="col-70">


                                    <ul v-for="menu in menuList" style="list-style-type:none">


                                        <li type="button" class="list-group-item">
                                            <img :src="menu.bmenuPic" height="50" width="50">
                                            {{menu.bmenuName}} &nbsp;&nbsp;&nbsp; 原价：{{menu.bprice}}元
                                            &nbsp;&nbsp;&nbsp;
                                            <template>
                                                <button class="cut" @click="cuts(menu)">-</button>
                                                <span :id="menu.bmenuId">{{getNo(menu)}}</span>
                                                <button class="add" @click="add(menu)">+</button>
                                            </template>

                                        </li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </f7-page>

                </f7-pages>
                <f7-toolbar tabbar>
                    <f7-link tab-link="#tab1">查看订单</f7-link>
                    <!--<f7-link tab-link="#tab2">Tab 2</f7-link>-->
                </f7-toolbar>
            </f7-view>
        </f7-views>

        <!-- Popup -->
        <f7-popup id="popup">
            <f7-view navbar-fixed>
                <f7-pages>
                    <f7-page>
                        <f7-navbar title="Popup">
                            <f7-nav-right>
                                <f7-link close-popup>Close</f7-link>
                            </f7-nav-right>
                        </f7-navbar>
                        <f7-block>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Neque, architecto.
                            Cupiditate laudantium rem nesciunt numquam, ipsam. Voluptates omnis, a inventore atque
                            ratione aliquam. Omnis iusto nemo quos ullam obcaecati, quod.
                        </f7-block>
                    </f7-page>
                </f7-pages>
            </f7-view>
        </f7-popup>

        <!-- Login Screen -->
        <f7-login-screen id="login-screen">
            <f7-view>
                <f7-pages>
                    <f7-page login-screen>
                        <f7-login-screen-title>Login</f7-login-screen-title>
                        <f7-list form>
                            <f7-list-item>
                                <f7-label>Username</f7-label>
                                <f7-input name="username" placeholder="Username" type="text"></f7-input>
                            </f7-list-item>
                            <f7-list-item>
                                <f7-label>Password</f7-label>
                                <f7-input name="password" type="password" placeholder="Password"></f7-input>
                            </f7-list-item>
                        </f7-list>
                        <f7-list>
                            <f7-list-button title="Sign In" close-login-screen></f7-list-button>
                            <f7-list-label>
                                <p>Click Sign In to close Login Screen</p>
                            </f7-list-label>
                        </f7-list>
                    </f7-page>
                </f7-pages>
            </f7-view>
        </f7-login-screen>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                isLoging: false,
                shipName: '',
                shipNo: '',
                address: '',
                menuType: '',
                fmenuTypes: '',
                menuList: '',
                phone: '',
                myurl: '',
                currentMenuPage: 0,
                order: {
                    shipNo: '',
                    menuList: []
                },
                menuOrder: {
                    menuId: '',
                    bnum: '',
                },
                mOrder: '',
                pnum:''
            }
        },
        created() {
            var formData = JSON.stringify(this.user);
            var url = "http://localhost:8001/getShipInfo?shipNo=S001";
            this.axios.post(url, formData, {
                headers: {
                    "Content-Type": "application/json;charset=utf-8",
                }
            }).then(function (response) {
                this.shipName = response.data.shipName;
                this.shipNo = response.data.shipNo;
                this.address = response.data.address;
                this.phone = response.data.phone;
                this.fmenuTypes = response.data.fmenuTypes;
                this.menuList = response.data.fmenuTypes[0].menuList;
                //这两个回调函数都有各自独立的作用域，如果直接在里面访问 this，无法访问到 Vue 实例,这时只要添加一个 .bind(this) 就能解决这个问题
            }.bind(this)).catch(function (response) {
                // 这里是处理错误的回调
                console.log(response)
            });
        },
        computed: {
            data: function () {
                var menuOrder = {};
                menuOrder = JSON.parse(JSON.stringify(this.templateData)); //this.templateData是父组件传递的对象
                return menuOrder;
            }
        },
        methods: {
            getMenus: function (shipNo, menuTypeId) {

                ///getMenuType?shipNo=S001&menuTypeId=1
                var url = "http://localhost:8001/getMenuType";
                this.axios.post(url, $.param({menuTypeId: menuTypeId, shipNo: shipNo}), {}).then(function (response) {
                    this.menuList = response.data.menuList;
                    //这两个回调函数都有各自独立的作用域，如果直接在里面访问 this，无法访问到 Vue 实例,这时只要添加一个 .bind(this) 就能解决这个问题

                    this.menuList

                }.bind(this)).catch(function (response) {
                    // 这里是处理错误的回调
                    console.log(response)
                });
            },
            getNo: function (menu) {
                var menuId = menu.bmenuId;
                var index = this.order.menuList.findIndex(function (item) {
                    return item.menuId == menuId;
                });
                var num = 0;
                if (index != -1) {
                    num = this.order.menuList[index].bnum;
                }

                return num;
            },
            cuts: function (menu) {
                var menuId = menu.bmenuId;
                var oindex = this.order.menuList.findIndex(function (item) {
                    //根据item中的id属性来判断这个item是否是上面id中
                    //对应的数据，如果是返回一个true ,否返回false,继续下面的一条数据的遍历，以此类推
                    return item.menuId == menuId;//如果返回true，那么findIndex方法会将这个item对应的id返回到外面接受
                });

                oindex == -1 ? this.pnum=0:this.pnum = this.order.menuList[oindex].bnum;
                if (this.pnum > 0) {
                    this.pnum=this.pnum-1;

                    this.menuOrder.menuId = menuId;
                    this.menuOrder.bnum = this.pnum ;

                    this.mOrder = {menuId: menuId, bnum: this.pnum};
                    oindex == -1 ? this.order.menuList.push(this.mOrder)
                        : Object.assign(this.order.menuList[oindex], this.menuOrder);

                }


            },
            add: function (menu) {
                var menuId = menu.bmenuId;
                var oindex = this.order.menuList.findIndex(function (item) {
                    //根据item中的id属性来判断这个item是否是上面id中
                    //对应的数据，如果是返回一个true ,否返回false,继续下面的一条数据的遍历，以此类推
                    return item.menuId == menuId;//如果返回true，那么findIndex方法会将这个item对应的id返回到外面接受
                });

                oindex == -1 ? this.pnum=0:this.pnum = this.order.menuList[oindex].bnum;
                this.pnum=this.pnum+1;
                // var pnum=this.menuList[index].bnum+1;
                this.menuOrder.menuId = menuId;
                this.menuOrder.bnum = this.pnum ;

                this.mOrder = {menuId: menuId, bnum: this.pnum};
                oindex == -1 ? this.order.menuList.push(this.mOrder)
                    : Object.assign(this.order.menuList[oindex], this.menuOrder);
                // this.menuList[index].bnum = this.pnum;
            }

        }
    }
</script>