/**
* 左边菜单
*/ 
<template>
  <el-menu default-active="2" :collapse="collapsed" collapse-transition router :default-active="$route.path" unique-opened class="el-menu-vertical-demo" background-color="#334157" text-color="#fff" active-text-color="#ffd04b">
    <div class="logobox">
      <img class="logoimg" src="../assets/img/logo.png" alt="">
    </div>
    <el-submenu v-for="menu in allmenu" :key="menu.menuid" :index="menu.menuname">
      <template slot="title">
        <i class="iconfont" :class="menu.icon"></i>
        <span>{{menu.menuname}}</span>
      </template>
      <el-menu-item-group>
        <el-menu-item v-for="chmenu in menu.menus" :index="'/'+chmenu.url" :key="chmenu.menuid">
          <i class="iconfont" :class="chmenu.icon"></i>
          <span>{{chmenu.menuname}}</span>
        </el-menu-item>
      </el-menu-item-group>
    </el-submenu>
  </el-menu>
</template>
<script>
import { menu } from '../api/userMG'
export default {
  name: 'leftnav',
  data() {
    return {
      collapsed: false,
      allmenu: []
    }
  },
  // 创建完毕状态(里面是操作)
  created() {
    // 获取图形验证码
    let res = {
      success: true,
      data: [
        // {
        //   menuid: 1,
        //   icon: 'li-icon-xiangmuguanli',
        //   menuname: '登录管理',
        //   hasThird: null,
        //   url: null,
        //   menus: [
        //     {
        //       menuid: 11,
        //       icon: 'icon-cms-manage',
        //       menuname: '登录列表',
        //       hasThird: 'N',
        //       url: 'masterData/masterData',
        //       menus: null
        //     },
        //   ]
        // },
        {
          menuid: 1,
          icon: 'li-icon-xiangmuguanli',
          menuname: '用户管理',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 11,
              icon: 'icon-order-manage',
              menuname: '用户列表',
              hasThird: 'N',
              url: 'userManage/index',
              menus: null
            },
          ]
        },
        {
          menuid: 2,
          icon: 'li-icon-xiangmuguanli',
          menuname: 'FTP管理',
          hasThird: null,
          url: null,
          menus: [
            // {
            //   menuid: 21,
            //   icon: 'icon-cms-manage',
            //   menuname: 'FTP列表',
            //   hasThird: 'N',
            //   url: 'interface/Interface',
            //   menus: null
            // },
            {
              menuid: 21,
              icon: 'icon-order-manage',
              menuname: '分发方管理',
              hasThird: 'N',
              url: 'distributor/index',
              menus: null
            },
            {
              menuid: 22,
              icon: 'icon-order-manage',
              menuname: '接收方管理',
              hasThird: 'N',
              url: 'recipient/index',
              menus: null
            },
            {
              menuid: 23,
              icon: 'icon-order-manage',
              menuname: '接收邮件管理',
              hasThird: 'N',
              url: 'email/index',
              menus: null
            },
            // {
            //   menuid: 23,
            //   icon: 'icon-cms-manage',
            //   menuname: '接口调用规则设置',
            //   hasThird: 'N',
            //   url: 'interfaceSet/InterfaceSet',
            //   menus: null
            // }
          ]
        },
        {
          menuid: 3,
          icon: 'li-icon-xiangmuguanli',
          menuname: '任务管理',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 31,
              icon: 'icon-order-manage',
              menuname: '任务列表',
              hasThird: 'N',
              url: 'task/index',
              menus: null
            },
          ]
        },
        {
          menuid: 4,
          icon: 'li-icon-xiangmuguanli',
          menuname: '日志管理',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 41,
              icon: 'icon-order-manage',
              menuname: '日志列表',
              hasThird: 'N',
              url: 'log/index',
              menus: null
            },
          ]
        },
        {
          menuid: 5,
          icon: 'li-icon-xiangmuguanli',
          menuname: '监控管理',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 51,
              icon: 'icon-order-manage',
              menuname: '监控列表',
              hasThird: 'N',
              url: 'monitorDir/index',
              menus: null
            },
          ]
        },
        {
          menuid: 6,
          icon: 'li-icon-xiangmuguanli',
          menuname: '系统配置',
          hasThird: null,
          url: null,
          menus: [
            {
              menuid: 61,
              icon: 'icon-order-manage',
              menuname: '系统配置列表',
              hasThird: 'N',
              url: 'sysConfig/index',
              menus: null
            },
          ]
        },
        // {
        //   menuid: 1,
        //   icon: 'li-icon-xiangmuguanli',
        //   menuname: '基础管理',
        //   hasThird: null,
        //   url: null,
        //   menus: [
        //     {
        //       menuid: 2,
        //       icon: 'icon-cat-skuQuery',
        //       menuname: '接口管理',
        //       hasThird: 'N',
        //       url: 'interface/Interface',
        //       menus: null
        //     }
        //   ]
        // },
        // {
        //   menuid: 33,
        //   icon: 'li-icon-dingdanguanli',
        //   menuname: '订单管理',
        //   hasThird: null,
        //   url: null,
        //   menus: [
        //     {
        //       menuid: 34,
        //       icon: 'icon-order-manage',
        //       menuname: '交易订单',
        //       hasThird: 'N',
        //       url: 'pay/Order',
        //       menus: null
        //     }
        //   ]
        // },
        // {
        //   menuid: 71,
        //   icon: 'li-icon-xitongguanli',
        //   menuname: '系统管理',
        //   hasThird: null,
        //   url: null,
        //   menus: [
        //     {
        //       menuid: 72,
        //       icon: 'icon-cus-manage',
        //       menuname: '用户管理',
        //       hasThird: 'N',
        //       url: 'system/user',
        //       menus: null
        //     },
        //     {
        //       menuid: 174,
        //       icon: 'icon-cms-manage',
        //       menuname: '菜单管理',
        //       hasThird: 'N',
        //       url: 'system/Module',
        //       menus: null
        //     },
        //     {
        //       menuid: 73,
        //       icon: 'icon-news-manage',
        //       menuname: '角色管理',
        //       hasThird: 'N',
        //       url: 'system/Role',
        //       menus: null
        //     },
        //     {
        //       menuid: 74,
        //       icon: 'icon-cs-manage',
        //       menuname: '公司管理',
        //       hasThird: 'N',
        //       url: 'system/Dept',
        //       menus: null
        //     },
        //     {
        //       menuid: 75,
        //       icon: 'icon-promotion-manage',
        //       menuname: '系统环境变量',
        //       hasThird: 'N',
        //       url: 'system/Variable',
        //       menus: null
        //     },
        //     {
        //       menuid: 76,
        //       icon: 'icon-cms-manage',
        //       menuname: '权限管理',
        //       hasThird: 'N',
        //       url: 'system/Permission',
        //       menus: null
        //     }
        //   ]
        // },
        // {
        //   menuid: 128,
        //   icon: 'li-icon-shangchengxitongtubiaozitihuayuanwenjian91',
        //   menuname: '支付管理',
        //   hasThird: null,
        //   url: null,
        //   menus: [
        //     {
        //       menuid: 129,
        //       icon: 'icon-provider-manage',
        //       menuname: '支付配置信息',
        //       hasThird: 'N',
        //       url: 'machine/MachineConfig',
        //       menus: null
        //     },
        //     {
        //       menuid: 175,
        //       icon: 'icon-provider-manage',
        //       menuname: '支付配置',
        //       hasThird: 'N',
        //       url: 'pay/Config',
        //       menus: null
        //     }
        //   ]
        // },
        // {
        //   menuid: 150,
        //   icon: 'li-icon-shangchengxitongtubiaozitihuayuanwenjian91',
        //   menuname: '图表',
        //   hasThird: null,
        //   url: null,
        //   menus: [
        //     {
        //       menuid: 159,
        //       icon: 'icon-provider-manage',
        //       menuname: '数据可视化',
        //       hasThird: 'N',
        //       url: 'charts/statistics',
        //       menus: null
        //     }
        //   ]
        // }
      ],
      msg: 'success'
    }
          this.allmenu = res.data
    
    // menu(localStorage.getItem('logintoken'))
    //   .then(res => {
    //     console.log(JSON.stringify(res))
    //     if (res.success) {
    //       this.allmenu = res.data
    //     } else {
    //       this.$message.error(res.msg)
    //       return false
    //     }
    //   })
    //   .catch(err => {
    //     this.$message.error('菜单加载失败，请稍后再试！')
    //   })
    // 监听
    this.$root.Bus.$on('toggle', value => {
      this.collapsed = !value
    })
  }
}
</script>
<style>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 210px;
  min-height: 400px;
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
  border: none;
  text-align: left;
}
.el-menu-item-group__title {
  padding: 0px;
}
.el-menu-bg {
  background-color: #1f2d3d !important;
}
.el-menu {
  border: none;
}
.logobox {
  height: 40px;
  line-height: 40px;
  color: #9d9d9d;
  font-size: 20px;
  text-align: center;
  padding: 20px 0px;
}
.logoimg {
  width:160px;
  height: 20px;
}
</style>