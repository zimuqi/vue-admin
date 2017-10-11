<template>
	<div class="app-container">
		<header class="app-header">
			<div class="header-bar">
				<div class="header-left">
					<i class="el-icon-menu hidden-btn" v-show="ismobile" @click="toggleSidebar"></i>
				</div>
				<nav class="header-center"></nav>
				<div class="header-right">
					<el-dropdown>
					  	<span class="el-dropdown-link">
						刘诗诗
						</span>
						<el-dropdown-menu slot="dropdown">
							<el-dropdown-item>我的资料</el-dropdown-item>
							<el-dropdown-item>我的消息</el-dropdown-item>
							<el-dropdown-item>退出系统</el-dropdown-item>
						</el-dropdown-menu>
					</el-dropdown>
					<div class="user-avatar">
						<img src="../../static/avatar.png" alt="">
					</div>
				</div>
			</div>
		</header>
		<transition name="fade" mode="out-in" appear :duration="1000">
			<aside class="app-sidebar" v-show="showSidebar">
			<div class="menu-label">General</div>
			<el-menu default-active="2" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose">
				<el-submenu index="1">
					<template slot="title"><i class="el-icon-message"></i>导航一</template>
					<el-menu-item-group>
						<template slot="title">分组一</template>
						<el-menu-item index="1-1">选项1</el-menu-item>
						<el-menu-item index="1-2">选项2</el-menu-item>
					</el-menu-item-group>
					<el-menu-item-group>
						<template slot="title">分组一</template>
						<el-menu-item index="1-1">选项1</el-menu-item>
						<el-menu-item index="1-2">选项2</el-menu-item>
					</el-menu-item-group>
					<el-submenu index="1-4">
						<template slot="title">选项4</template>
						<el-menu-item index="1-4-1">选项1</el-menu-item>
					</el-submenu>
				</el-submenu>
				<el-submenu index="2">
					<template slot="title"><i class="el-icon-message"></i>导航二</template>
					<el-menu-item-group>
						<template slot="title">分组一</template>
						<el-menu-item index="1-1">选项1</el-menu-item>
						<el-menu-item index="1-2">选项2</el-menu-item>
					</el-menu-item-group>
					<el-menu-item-group>
						<template slot="title">分组一</template>
						<el-menu-item index="1-1">选项1</el-menu-item>
						<el-menu-item index="1-2">选项2</el-menu-item>
					</el-menu-item-group>
					<el-submenu index="1-4">
						<template slot="title">选项4</template>
						<el-menu-item index="1-4-1">选项1</el-menu-item>
					</el-submenu>
				</el-submenu>
				<el-submenu index="3">
					<template slot="title"><i class="el-icon-message"></i>导航三</template>
					<el-menu-item-group>
						<template slot="title">分组一</template>
						<el-menu-item index="1-1">选项1</el-menu-item>
						<el-menu-item index="1-2">选项2</el-menu-item>
					</el-menu-item-group>
					<el-menu-item-group>
						<template slot="title">分组一</template>
						<el-menu-item index="1-1">选项1</el-menu-item>
						<el-menu-item index="1-2">选项2</el-menu-item>
					</el-menu-item-group>
					<el-submenu index="1-4">
						<template slot="title">选项4</template>
						<el-menu-item index="1-4-1">选项1</el-menu-item>
					</el-submenu>
				</el-submenu>
				<el-menu-item index="4"><i class="el-icon-menu"></i>导航四</el-menu-item>
				<el-menu-item index="5"><i class="el-icon-setting"></i>导航五</el-menu-item>
			</el-menu>
		</aside>
		</transition>
		<section class="app-main" :class="{ismobile:ismobile}">
			<div class="container">
				<router-view></router-view>
			</div>
		</section>
	</div>
</template>

<script>
    export default {
        data(){
            return{
          		"ismobile":false,
				"showSidebar":true,
			}
		},
        beforeMount () {
            const { body } = document;
            const WIDTH = 768;
            const RATIO = 3;

            const handler = () => {
                if (!document.hidden) {
                    let rect = body.getBoundingClientRect();
                    this.ismobile = rect.width - RATIO < WIDTH;
                    if(!this.ismobile){
                        this.showSidebar=true;
					}else{
                        this.showSidebar=false;
					}
                }
            }

            document.addEventListener('visibilitychange', handler);
            window.addEventListener('DOMContentLoaded', handler);
            window.addEventListener('resize', handler);
        },
        methods: {
            handleOpen(key, keyPath) {
                console.log(key, keyPath);
            },
            handleClose(key, keyPath) {
                console.log(key, keyPath);
            },
            toggleSidebar(){
                this.showSidebar=!this.showSidebar;
			}
        }
    }
</script>

<style scoped lang="less">
	.app-header{
		position: fixed;
		min-width: 100%;
		z-index: 1024;
		background-color: #ffffff;
		box-shadow: 0 2px 3px hsla(0,0%,7%,.1), 0 0 0 1px hsla(0,0%,7%,.1);
		overflow-x: auto;
		.header-bar{
			display: flex;
			min-height: 50px;
			background: none;
			.header-left{
				min-width: 50px;
				.hidden-btn{
					display: block;
					padding: 15px;
					font-size: 20px;
				}
				i{
					color: #666666;
				}
			}
			.header-center{
				flex: 1;
			}
			.header-right{
				min-width: 300px;
				display: flex;
				flex-direction:row-reverse;
				.user-avatar{
					height: 30px;
					width: 30px;
					padding: 10px;
					img{
						width: 100%;
						height: 100%;
						border-radius: 15px;
					}
				}
				.el-dropdown{
					line-height: 50px;
					margin-right: 30px;
				}
			}
		}
	}
	.app-sidebar{
		position: fixed;
		top: 50px;
		left: 0;
		bottom: 0;
		padding: 20px 0 50px 0;
		width: 180px;
		min-width: 45px;
		max-height: 100vh;
		z-index: 1023;
		background: #fff;
		box-shadow:1px 0 0 hsla(0,0%,7%,.1);
		overflow-y: auto;
		overflow-x: hidden;
		.menu-label {
			color: #7a7a7a;
			font-size: 11px;
			letter-spacing: 1px;
			margin-bottom: 5px;
			text-transform: uppercase;
			padding-left: 20px;
			line-height: 1;
		}
		.el-menu{
			background-color: #ffffff;
		}
	}
	.app-main{
		padding-top: 50px;
		margin-left: 180px;
		transform: translateZ(0);
		.container{
			padding: 20px;
			position: relative;
		}
	}
	.ismobile{
		margin-left: 0;
	}
</style>