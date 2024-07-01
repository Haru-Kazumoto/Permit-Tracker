<template>
    <div class="wrapper">
        <div class="top-section">
            <n-flex>
                <div class="left-component">
                        <div class="greetings">
                            <p>Good Day, Haru Kazumoto!</p>
                        </div>
                </div>
                <div class="right-component">
                    <n-flex>
                        <div class="notification">
                            <n-float-button position="relative" @click="drawerActivate()">
                                <n-badge v-if="checkNewNotification() > 0" :value="checkNewNotification()" :offset="[6, -8]">
                                    <n-icon>
                                        <md-notifications-outline />
                                    </n-icon>
                                </n-badge>
                                <n-icon v-else>
                                    <md-notifications-outline />
                                </n-icon>
                            </n-float-button>
                            <n-drawer v-model:show="drawerActive" :width="502">
                                <n-drawer-content>
                                    <template #header>
                                        <div class="drawer-head">
                                            <n-flex>
                                                Notification
                                                <n-button text @click="readAllNotifications()">
                                                    Read all
                                                </n-button>
                                            </n-flex>
                                        </div>
                                    </template>
                                    <div class="wrapper-notification-content">
                                        <n-collapse v-model:expanded-names="expandedNames">
                                            <n-collapse-item 
                                                v-for="(notification, index) in notifications"
                                                :key="index"
                                                :name="index + 1"
                                            >
                                                <template #header>
                                                    <div 
                                                    class="notification-content-header" 
                                                    :class="{ 
                                                        unread: !notification.hasRead, 
                                                        read: notification.hasRead 
                                                    }"
                                                >
                                                    {{ notification.title }}
                                                </div>
                                                </template>
                                                <div class="notification-content">
                                                    <span>{{ notification.content }}</span>
                                                </div>
                                            </n-collapse-item>
                                        </n-collapse>
                                    </div>
                                </n-drawer-content>
                            </n-drawer>
                        </div>
                        <n-dropdown :options="profileDropdownOptions">
                            <div class="profile">
                                <n-flex>
                                    <n-avatar
                                        round
                                        size="large"
                                        src="https://07akioni.oss-cn-beijing.aliyuncs.com/07akioni.jpeg"
                                    />
                                    <div class="profile-info">
                                        <p style="font-weight: 700;">Haru Kazumoto</p>
                                        <span style="font-size: smaller;">Admin Approval</span>
                                    </div>
                                </n-flex>
                            </div>
                        </n-dropdown>
                    </n-flex>
                </div>
            </n-flex>
        </div>
        <div class="content-wrapper">
            <n-flex>
                <div class="card-info">
                    <div class="card-info-title">
                        <p>Today's dashboard</p>
                    </div>
                    <div class="card-info-content">
                        <div v-for="(info, index) in dashboardInfo" :key="index">
                            <CardInfo 
                                :icon="info.icon"
                                :count-data="info.countData"
                                :info-text="info.infoText"
                                :sub-text="info.subText"
                                style="width: 350px;"
                            />
                        </div>
                    </div>
                </div>
            </n-flex>
        </div>
    </div>
</template>

<script setup lang="ts">
import {
    MdNotificationsOutline,
    IosTime as Waiting,
    IosHourglass as WaitToBack
} from "@vicons/ionicons4";
import {
  PersonCircleOutline as UserIcon,
  LogOutOutline as LogoutIcon,
  Book as BookIcon
} from '@vicons/ionicons5'
import { NIcon } from 'naive-ui'
import { useMessage } from "naive-ui";

definePageMeta({
    layout: "admin-layout"
});

const drawerActive = ref(false);
const expandedNames = ref([]);
const message = useMessage();
const drawerActivate = () => { drawerActive.value = true };

const dashboardInfo = [
  {
    icon: BookIcon,
    countData: 10,
    subText: "Today's permit created",
    infoText: "Most major leaving today : AKL"
  },
  {
    icon: Waiting,
    countData: 5,
    subText: "Waiting to approve",
    infoText: "Today more than yasterday"
  },
  {
    icon: WaitToBack,
    countData: 8,
    subText: "Wait to return",
    infoText: "Today less than yasterday"
  }
];

const notifications = ref([
    { title: 'Notification 1', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Cumque, culpa excepturi? Doloribus aspernatur autem maxime, facilis at culpa eaque voluptatem? Ratione maiores sunt amet debitis dicta reiciendis, at architecto facere.', hasRead: false },
    { title: 'Notification 2', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Cumque, culpa excepturi? Doloribus aspernatur autem maxime, facilis at culpa eaque voluptatem? Ratione maiores sunt amet debitis dicta reiciendis, at architecto facere.', hasRead: true },
    { title: 'Notification 3', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Cumque, culpa excepturi? Doloribus aspernatur autem maxime, facilis at culpa eaque voluptatem? Ratione maiores sunt amet debitis dicta reiciendis, at architecto facere.', hasRead: false },
    { title: 'Notification 4', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Cumque, culpa excepturi? Doloribus aspernatur autem maxime, facilis at culpa eaque voluptatem? Ratione maiores sunt amet debitis dicta reiciendis, at architecto facere.', hasRead: false },
    { title: 'Notification 5', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Cumque, culpa excepturi? Doloribus aspernatur autem maxime, facilis at culpa eaque voluptatem? Ratione maiores sunt amet debitis dicta reiciendis, at architecto facere.', hasRead: false }
]);

function checkNewNotification(): number {
    return notifications.value.filter(data => data.hasRead).length;
}

computed(() => {
    return notifications.value.filter(notification => notification.hasRead).length;
});

function readAllNotifications() {
    notifications.value.forEach((data) => {
        data.hasRead = false;
    });
    
    message.success("Read all notification", {closable: true, duration: 1500});
}

const renderIcon = (icon: Component) => {
  return () => {
    return h(NIcon, null, {
      default: () => h(icon)
    })
  }
}

const profileDropdownOptions = ref([
    {
        label: 'Profile',
        key: 'profile',
        icon: renderIcon(UserIcon)
    },
    {
        label: 'Logout',
        key: 'logout',
        icon: renderIcon(LogoutIcon)
    }
])
</script>

<style scoped>
.card-info {
  display: flex;
  flex-direction: column;
  background-color: white;
  padding: 20px 30px;
  border-radius: 10px;
}

.card-info-title {
    font-size: 20px;
    font-weight: 600;
}

.card-info-content {
    display: flex;
    flex-wrap: wrap;
    gap: 25px;
    justify-content: space-between;
    width: 100%;
    margin: 20px 0px;
}

.wrapper {
    display: flex;
    flex-direction: column;
}

.notification-content {
    padding: 10px 10px;
    border-radius: 5px;
}

.notification-content-header {
    font-weight: 600;
}

.unread {
    color: black;
}

.read {
    color: red;
}

.wrapper-notification-content {
    padding: 10px 20px;
}

.drawer-head {
    display: flex;
    align-items: center;
}

.top-section {
    width: 100%;
    margin-bottom: 40px;
}

.profile {
    display: flex;
    padding: 0px 20px;
    margin-left: auto;
}

.notification {
    display: flex;
    margin-left: auto;
}

.profile-info {
    display: flex;
    flex-direction: column;
}

.right-component {
    display: flex;
    margin-left: auto;
}

.left-component {
    display: flex;
    align-items: center;
    flex-grow: 1;
}

.greetings {
    display: flex;
    font-size: larger;
    font-weight: 500;
    align-items: center;
}
</style>