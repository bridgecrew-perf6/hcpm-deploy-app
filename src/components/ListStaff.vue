<template>
    <div class="w-full h-[578px]" style="border: 12px solid #ffff; border-right: none">
        <Button></Button> <Search></Search>
        <div class="employee-list scroll h-full bg-white overflow-y-scroll" id="scroll">
            <table border="0" cellspacing="0" cellpadding="0">
                <thead class="theadRow">
                    <tr>
                        <th></th>
                        <th>Mã nhân viên</th>
                        <th>Tên nhân viên</th>
                        <th>Ngày sinh</th>
                        <th>Số điện thoại</th>
                        <th>Email</th>
                        <th>Địa chỉ</th>
                        <th>Ngày vào</th>
                        <th>Tuổi</th>
                        <th>Bộ phận</th>
                        <th style="z-index: 1">Chức năng</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(employee, index) in employees" :key="employee._id" @dblclick="emitter.emit('dblClickOnRow', employee)">
                        <td>
                            <span><input @click="check(employee._id)" type="checkbox" class="checked-box" /> </span>
                        </td>
                        <td>{{ employee.Code }}</td>
                        <td>{{ employee.Name }}</td>
                        <td>{{ employee.DateOfBirth }}</td>
                        <td>{{ employee.PhoneNumber }}</td>
                        <td>{{ employee.Email }}</td>
                        <td>{{ employee.Address }}</td>
                        <td>{{ employee.StartWork }}</td>
                        <td>{{ employee.Age }}</td>
                        <td>{{ employee.Category }}</td>
                        <td style="height: 40px; position: relative">
                            <p style="text-align: left; padding-left: 12px; color: blue">Sửa</p>
                            <button  @focusout="out(index)" style="" class="btn-more-option" @click="more(index)"></button>
                            <button @click="del(employee)" class="delete" style="">Xóa</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import axios from "axios";
import Search from "./base/Search.vue";
import Button from "./base/Button.vue";
export default {
    components: {
        Search,
        Button,
    },
    created() {
        this.getData();
    },
    data() {
        return {
            employees: null,
            employees2: [],
            num: 0,
        };
    },
    methods: {
        getData() {
            var me = this;
            axios
                .get("https://nguyensynamtodolist-14-02.herokuapp.com/employee")
                .then(function (res) {
                    console.log(res.data.employees);
                    me.employees = res.data.employees;
                    console.log(me.employees);
                })
                .catch(function (res) {
                    console.log(res);
                });
        },
        check(e) {
            console.log(e);
        },
        more(e) {
            document.getElementsByClassName("delete")[e].style.display = "block";
        },
        out(e){
            document.getElementsByClassName("delete")[e].style.display = "none";
        }
    },
};
</script>

<style scoped>
.employee-list {
    width: 100%;
    height: 100%;
    position: relative;
}
th {
    background-color: #eceef1;
    border: none;
    border-right: 1px solid rgb(218, 218, 218);
    border-bottom: 1px solid rgb(218, 218, 218);
    border-top: 1px solid rgb(218, 218, 218);
    font-size: 13px;
    height: 40px;
    z-index: 30;
    text-align: center;
}
tr td {
    border: none;
    border-right: 1px solid rgb(218, 218, 218);
    text-align: center;
    height: 40px;
}
thead {
    z-index: 90;
}
thead th:nth-child(1) {
    width: 42px;
}
thead th:nth-child(2) {
    width: 100px;
}
thead th:nth-child(3) {
    width: 100px;
}
thead th:nth-child(4) {
    width: 130px;
}
thead th:nth-child(5) {
    width: 110px;
}
thead th:nth-child(6) {
    width: 210px;
}
thead th:nth-child(7) {
    width: 110px;
}
thead th:nth-child(8) {
    width: 100px;
}
thead th:nth-child(9) {
    width: 60px;
}
thead th:nth-child(10) {
    width: 100px;
}
thead th:nth-child(11) {
    width: 80px;
}
table {
    border-left: 1px solid rgb(218, 218, 218);
}
table tr td {
    border-bottom: 1px solid rgb(218, 218, 218);
}
span input {
    width: 20px;
    height: 20px;
}
tr {
    font-size: 12px;
}
tr:nth-child(2n) {
    background-color: #eceef1;
}
.theadRow {
    position: -webkit-sticky;
    position: sticky;
    top: -1px;
    z-index: 30;
}
tr td:hover {
    cursor: pointer;
}
.btn-more-option {
    width: 30px;
    height: 20px;
    background: url(../assets/images/downward-arrow.png) no-repeat;
    margin-left: 10px;
    border: none;
    z-index: 2;
    position: absolute;
    right: 8px;
    top: 8px;
}
.delete {
    width: 94px;
    height: 36px;
    background-color: rgb(255, 255, 255);
    position: absolute;
    border: 1px solid #c0c0c0;
    z-index: 3;
    bottom: -30px;
    left: -30px;
    border-radius: 4px;
    display: none;
}
</style>
