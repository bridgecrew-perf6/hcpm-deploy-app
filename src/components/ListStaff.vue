<template>
    <div class="w-full h-[578px]" style="border: 12px solid #ffff; border-right: none">
        <Button></Button> <Search></Search>
        <div class="employee-list scroll h-full bg-white overflow-y-scroll" id="scroll" style="width: 1153px">
            <table border="0" cellspacing="0" cellpadding="0" id="table" style="width: 1125px">
                <thead class="theadRow" id="thead1" style="width: 1137px">
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
                            <p class="leading-[40px]" style="text-align: left; padding-left: 12px; color: blue; margin-bottom: 0px">Sửa</p>
                            <button  style="" class="btn-more-option" @click="more(index)"></button>
                            <button @focusout="out(index)" @click="del(employee._id)" class="delete" style="">Xóa</button>
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
        this.emitter.on("clickTogle", () => {
            if (this.num2 % 2 == 0) {
                document.getElementById("scroll").style.width = "1366px";
                document.getElementById("table").style.width = "1338px";
                document.getElementById("thead1").style.width = "1338px";
                this.num2++;
            } else {
                document.getElementById("scroll").style.width = "1366px";
                document.getElementById("table").style.width = "1115px";
                document.getElementById("thead1").style.width = "1115px";
                this.num2++;
            }
        });
    },
    data() {
        return {
            employees: null,
            employees2: [],
            num: 0,
            num2: 0,
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
            if (this.num % 2 == 0) {
                document.getElementsByClassName("delete")[e].style.display = "block";
                this.num++;
            } else {
                document.getElementsByClassName("delete")[e].style.display = "none";
                this.num++;
            }
        },
        out(e) {
            document.getElementsByClassName("delete")[e].style.display = "none";
        },
        del(e) {
            var url = "https://nguyensynamtodolist-14-02.herokuapp.com/employee/" + e
            axios
                .delete(url)
                .then(function (res) {
                    console.log(res)
                })
                .catch(function (res) {
                    console.log(res);
                });
        },
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
    width: 4%;
}
thead th:nth-child(2) {
    width: 8%;
}
thead th:nth-child(3) {
    width: 13%;
}
thead th:nth-child(4) {
    width: 10%;
}
thead th:nth-child(5) {
    width: 10%;
}
thead th:nth-child(6) {
    width: 16%;
}
thead th:nth-child(7) {
    width: 10%;
}
thead th:nth-child(8) {
    width: 8%;
}
thead th:nth-child(9) {
    width: 5%;
}
thead th:nth-child(10) {
    width: 9%;
}
thead th:nth-child(11) {
    width: 7%;
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
    top: 12px;
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
