<template>
    <div id="TopNav">
        <header class="main-header header">
            <div class="container">
                <div class="row">
                    <div class="col-xs-12">
                        <img src="../../../images/logo.png" alt="" class="img">
                    </div>
                </div>
            </div>
        </header>
        <nav class="main-navigation">
            <div class="container">
                <div class="row">
                    <div class="col-sm-12">
                        <div class="collapse navbar-collapse" id="main-menu">
                            <ul class="menu">
                                <li role="presentation" v-for="nav in navigation ">
                                    <a :href="nav.url" :title="nav.title" v-if="nav.title != '族谱数据'">{{ nav.title }}</a>
                                    <a :href="nav.url" :title="nav.title" v-else="" style="font-weight: bold">{{ nav.title }}</a>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </nav>
    </div>
</template>

<script>
    export default {
        data() {
          return {
              navigation: {}
          }
        },
        methods: {
            readData() {
                axios.get('http://localhost:3000/navigation').then( response => {
                    this.navigation = response.data;
                }).catch( error => {
                    console.log(error);
                    alert('网络错误，不能访问');
                })
            }
        },
        created() {
            this.readData()
        }
    }
</script>

<style scoped>
    .main-header {text-align: center;padding: 42px 0;background: #f4645f;}
    .header{padding:0px;}
    .img{float:left;}
    .home-template .main-header{padding-top:62px;padding-bottom:62px;background-repeat:no-repeat;background-position:center 20%;-webkit-background-size:cover;background-size:cover}
    .main-navigation{text-align:center;background:#fff;border-top:1px solid #ebebeb;margin-bottom:35px;border-bottom:2px solid #e1e1e1}
    .main-navigation .menu{padding:0;margin:0}
    .main-navigation .menu li{list-style:none;display:inline-block;position:relative}
    .main-navigation .menu li.nav-current{border-bottom:2px solid #f4645f;margin-bottom:-2px}
    .main-navigation .menu li.red-dot:after{content:'';display:block;background:red;border-radius:50%;width:.6em;height:.6em;top:30%;right:11px;position:absolute}
    .main-navigation .menu li a{color:#505050;line-height:4em;display:block;padding:0 21px}
    .main-navigation .menu li:hover>a{color:#f4645f;text-decoration:none}
    .main-navigation .menu li ul{visibility:hidden;background:#fff;text-align:left;padding:7px 0;margin:0;position:absolute;left:0;top:120%;width:200px;z-index:999;opacity:0;-webkit-transition:all .2s ease;-o-transition:all .2s ease;transition:all .2s ease}
</style>
