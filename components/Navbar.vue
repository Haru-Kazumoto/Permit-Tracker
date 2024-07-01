<template>
    <n-flex vertical>
      <aside class="side-wrapper">
        <div class="logo">
          <p>Permit Track</p>
        </div>
        <div class="divider" />
        <n-menu 
          :options="menuOptions" 
          :default-expanded-keys="defaultExpandedKeys" 
          accordion 
          :theme-overrides="menuThemeOverrides"
        />
        <div class="wrapper">
          <div class="profile">
              <p class="avatar-profile">
                  <n-avatar
                      round
                      size="huge"
                      src="https://07akioni.oss-cn-beijing.aliyuncs.com/07akioni.jpeg"
                  />
              </p>
          </div>
        </div>
      </aside>
    </n-flex>
  </template>
  
  <script setup lang="ts">
import { h, ref, type Component } from 'vue'
import { NIcon } from 'naive-ui'
import type { MenuOption, MenuProps } from 'naive-ui'
import {
  StatsChartOutline as DashboardIcon,
  PeopleOutline as UsersIcon,
  WalletOutline as PaymentsIcon,
  LogOutOutline as LogoutIcon,
  PersonOutline as StudentsIcon,
  SchoolOutline as ClassOfStudentsIcon,
  CloudUploadOutline as UploadPaymentIcon,
  SearchOutline as FindPaymentIcon
} from '@vicons/ionicons5'
import { RouterLink } from 'vue-router';

  type MenuThemeOverrides = NonNullable<MenuProps['themeOverrides']>; 
  
  const menuThemeOverrides: MenuThemeOverrides = {
      arrowColor: "white",
      arrowColorChildActiveHover: "black",
      arrowColorChildActive: "white",
      itemColorActive: "#dff348",
      itemColorActiveHover: "#dff348",
      itemColorActiveInverted: "white",
      itemColorActiveHoverInverted: "#dff348",
      itemIconColor: "white",
      itemIconColorActive: "black",
      itemIconColorActiveHover: "black",
      itemIconColorChildActive: "white",
      itemIconColorActiveInverted: "black",
      itemIconColorChildActiveHover: "black",
      itemIconColorActiveHoverInverted: "black",
      itemTextColor: "white",
      itemTextColorHover: "black",
      itemTextColorActive: "black",
      itemTextColorActiveHover: "black",
      itemTextColorActiveInverted: "black",
      itemTextColorActiveHoverInverted: "black",
      itemTextColorChildActive: "white",
      itemTextColorChildActiveHover: "black",
      borderRadius: "40px",
  }
  
  function renderIcon(icon: Component) {
    return () => h(NIcon, null, { default: () => h(icon) })
  }
  
  const menuOptions = ref<MenuOption[]>([
    {
      label: () =>
        h(
          RouterLink,
          {
            to: {
              path: '/admin/dashboard',
            }
          },
          {
              default: () => "Dashboard"
          }
        ),
      key: 'dashboard',
      icon: renderIcon(DashboardIcon)
    },
    {
      label: 'Users',
      key: 'users',
      icon: renderIcon(UsersIcon),
      children: [
        {
          label: 'Students',
          key: 'students',
          icon: renderIcon(StudentsIcon)
        },
        {
          label: 'Class of Students',
          key: 'class-of-students',
          icon: renderIcon(ClassOfStudentsIcon)
        }
      ]
    },
    {
      label: 'Payments',
      key: 'payments',
      icon: renderIcon(PaymentsIcon),
      children: [
        {
          label: 'Upload Payment',
          key: 'upload-payment',
          icon: renderIcon(UploadPaymentIcon)
        },
        {
          label: 'Find Payment',
          key: 'find-payment',
          icon: renderIcon(FindPaymentIcon)
        }
      ]
    },
    {
      label: 'Logout',
      key: 'logout',
      icon: renderIcon(LogoutIcon)
    }
  ])
  
  const defaultExpandedKeys = ref(['users', 'payments'])
  </script>
  
  <style scoped>
  .divider {
    border: 0.5px solid rgb(224, 222, 222);
    margin: 0px 10px 20px;

  }

  .wrapper {
      display: flex;
      margin-top: auto;
      padding: 10px;
  }
  
  .profile {
      display: flex;
      border: 1px solid white;
      border-radius: 10px;
      width: 100%;
      padding: 10px 20px;
      margin-bottom: 10px;
  }
  
  .avatar-profile {
      margin-right: 20px;
  }
  
  .profile-role {
      color: white;   
  }
  
  .profile-role p {
      font-weight: bold;
  }
  
  .profile-info p {
      font-size: 15px;
      font-weight: bold;
      color: white;
  }
  
  .side-wrapper {
    background-color: black;
    width: 300px;
    height: 100vh;
    display: flex;
    flex-direction: column;
  }
  
  .logo {    
    padding: 20px 10px;
  }
  
  .logo p {
    font-size: 30px;
    font-weight: 600;
    color: white;
  }
  
  .n-menu {
      color: white;
  }
  </style>