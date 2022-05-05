<template>
    <div class="w-full bg-gray-100 relative" id="main">
        <DialogAddEmployee></DialogAddEmployee>

        <Header></Header>
        <div class="w-full h-[50px] border-t-[1px] border-b-[1px] bg-white pl-3 font-medium text-base leading-[50px]">
            {{ namePage }}
        </div>
        <Project v-if="isProject"></Project>
        <Staff v-if="isStaff" />
        <ListStaff v-if="isListStaff" />
        <HomeContent v-if="isHomeContent" />
    </div>
</template>

<script>
import Header from "./Header.vue";
import ListStaff from "./ListStaff.vue";
import Project from "./Project.vue";
import Staff from "./Staff.vue";
import DialogAddEmployee from "./DialogAddEmployee.vue";
import HomeContent from "./HomeContent.vue";
export default {
    components: {
        Header,
        Project,
        Staff,
        ListStaff,
        HomeContent,
        DialogAddEmployee,
    },
    created() {
        this.emitter.on("clickProject", () => {
            this.isProject = true;
            this.isStaff = false;
            this.isListStaff = false;
            this.isHomeContent = false;
        });
        this.emitter.on("clickList", () => {
            this.isListStaff = true;
            this.isProject = false;
            this.isStaff = false;
            this.isHomeContent = false;
        });
        this.emitter.on("clickStaff", () => {
            this.isStaff = true;
            this.isListStaff = false;
            this.isProject = false;
            this.isHomeContent = false;
        });
        this.emitter.on("clickTogle", () => {
            if (this.num % 2 == 0) {
                document.getElementById("main").style.width = "1366px";
                this.num++;
            } else{
                document.getElementById("main").style.width = "1141px";
                this.num++;
            }
        });
    },
    data() {
        return {
            isProject: false,
            isListStaff: false,
            isStaff: false,
            isHomeContent: true,
            namePage: "Khách hàng",
            num: 0,
        };
    },
};
</script>

<style></style>
