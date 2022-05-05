<template>
    <div class="w-full h-screen flex relative">
        <!-- <DialogAddEmployee ></DialogAddEmployee> -->
        <SideBar></SideBar> <MainContent ></MainContent>
    </div>
</template>

<script>
import SideBar from "./SideBar.vue";
import MainContent from "./MainContent.vue";
import DialogAddEmployee from "./MainContent.vue";
export default {
    components: {
        SideBar,
        MainContent,
        DialogAddEmployee
    },
};
</script>

<style></style>
