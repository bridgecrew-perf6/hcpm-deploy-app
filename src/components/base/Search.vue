<template>
    <div class="employee-search justify-between">
        <div class="flex">
            <button class="import border-[1px] w-[100px] h-9 pl-5 rounded font-semibold">Import</button>
            <button class="export border-[1px] w-[100px] h-9 pl-5 rounded font-semibold mr-3">Export</button>
        </div>
        <div class="flex">
            <div>
                <button @click="clickSearch" id="icon-search" class="icon-search"></button>
                <input placeholder="Tìm kiếm theo tên/mã nhân viên" type="text" class="input-search" />
            </div>

            <button class="btn-reload"></button>
        </div>
    </div>
</template>

<script>
export default {
    created() {},
    destroyed() {},
    methods: {},
    data() {
        return {
            valueSearch: "",
            employees: [],
            returnData: [],
            num: 0,
        };
    },
};
</script>

<style scoped>
.employee-search {
    width: 100%;
    height: 55px;
    background-color: #ffffff;
    align-items: center;
    display: flex;
}
.employee-search div {
    position: relative;
}

.input-search {
    width: 250px;
    height: 32px;
    border-radius: 6px;
    padding-left: 16px;
    font-size: 13px;
    color: rgb(231, 231, 231);
    border: 1px solid #babec5;
    outline: none;
}

.input-search:focus {
    color: #000;
    border-color: rgb(74, 116, 255);
}

.icon-search {
    position: absolute;
    border: none;
    width: 24px;
    height: 24px;
    background: url(../../assets/images/search.png) no-repeat;
    z-index: 2;
    top: 8px;
    right: 4px;
}

.btn-reload {
    margin-right: 16px;
    margin-left: 16px;
    width: 32px;
    height: 32px;
    background: url(../../assets/images/reload.png) no-repeat center;
    border: 1px solid rgb(201, 201, 201);
    cursor: pointer;
    background-color: rgb(255, 255, 255);
    border-radius: 4px;
}
button:hover {
    background-color: rgb(236, 236, 236);
    border-color: blue;
}
.import {
    background-image: url(../../assets/images/import.png);
    background-size: 16px 16px;
    background-repeat: no-repeat;
    background-position: 10px center;
}
.export {
    margin-left: 12px;
    background-image: url(../../assets/images/export.png);
    background-size: 16px 16px;
    background-repeat: no-repeat;
    background-position: 10px center;
}
</style>
