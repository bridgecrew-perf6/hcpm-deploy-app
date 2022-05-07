<template>
    <div class="dialogAdd z-40 w-screen h-screen left-[-201px]" id="dialogAdd" v-if="isOpen">
        <div class="dialog-content">
            <div class="header">
                <div class="name">Thông tin nhân viên</div>
                <input type="checkbox" class="checkEmploy1" /> Là khách hàng <input type="checkbox" class="checkEmploy2" /> Là nhà cung cấp
                <div class="info-and-close absolute top-3 right-3">
                    <button id="btn-close" class="btn-close" @click="emitter.emit('closeForm')"></button>
                </div>
            </div>
            <img class="w-[80px] h-[80px] rounded-[100%] mx-auto mb-3" src="../assets/images/avatar.png" alt="" />
            <div class="content" style="height: 366px">
                <div class="top-content" style="height: 120px">
                    <div class="left-content">
                        <div style="display: flex; justify-content: space-between">
                            <div>
                                <div>
                                    Mã nhân viên
                                    <span style="color: red; margin-top: 3px">*</span>
                                </div>
                                <input v-model="employee.Code" type="text" style="width: 150px" class="employeeCode" />
                            </div>
                            <div>
                                <div>
                                    Tên nhân viên
                                    <span style="color: red; margin-top: 3px">*</span>
                                </div>
                                <input v-model="employee.Name" type="text" style="width: 220px" />
                            </div>
                        </div>

                        <div style="height: 50px; margin-top: 0">
                            <div>Chức danh</div>
                            <input v-model="employee.Category" type="text" style="width: 100%" />
                        </div>
                    </div>
                    <div class="right-content">
                        <div class="top" style="display: flex">
                            <div>
                                <div>Ngày sinh</div>
                                <input v-model="employee.DateOfBirth" type="text" style="width: 150px" />
                            </div>
                            <div style="margin-left: 40px">
                                <div>Giới tính</div>
                                <form style="display: flex; align-items: center">
                                    <input @change="onChange($event)" value="Nam" type="radio" name="gender" id="female" />
                                    <div style="margin-left: 6px; margin-right: 10px">Nam</div>
                                    <input @change="onChange($event)" type="radio" name="gender" value="Nữ" id="male" />
                                    <div style="margin-left: 6px; margin-right: 10px">Nữ</div>
                                    <input @change="onChange($event)" type="radio" name="gender" value="other" id="other" />
                                    <div style="margin-left: 6px; margin-right: 10px">Khác</div>
                                </form>
                            </div>
                        </div>
                        <div class="mid" style="display: flex; justify-content: space-between">
                            <div>
                                <div>Số CMND</div>
                                <input v-model="employee.Cccd" type="text" style="width: 220px" />
                            </div>
                        </div>
                    </div>
                </div>
                <div class="bottom-content">
                    <div class="top">
                        <div style="height: 50px; margin-top: 25px">
                            <div>Địa chỉ</div>
                            <input v-model="employee.Address" type="text" style="width: 100%" />
                        </div>
                    </div>
                    <div class="mid" style="display: flex; margin-top: 32px">
                        <div>
                            <div>ĐT di động</div>
                            <input v-model="employee.PhoneNumber" type="text" style="width: 190px" />
                        </div>
                        <div style="margin-left: 16px">
                            <div>ĐT cố định</div>
                            <input type="text" style="width: 190px" />
                        </div>
                        <div style="margin-left: 16px">
                            <div>Email</div>
                            <input v-model="employee.Email" type="text" style="width: 190px" />
                        </div>
                    </div>
                </div>
            </div>
            <div class="bottom" style="display: flex; align-content: center">
                <button class="cancel" id="cancel" @click="closeForm">Hủy</button>
                <div>
                    <button class="save">Cất</button>
                    <button @click="emitter.emit('addEmployee',employee)" class="save-add">Thêm</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    created() {
        this.emitter.on("clickBtnAdd", () => {
            this.employee = {};
            this.isOpen = true;
            this.isAdd = true;
            this.isFix = false;
        });
        this.emitter.on("closeForm", () => {
            this.isOpen = false;
        });
        this.emitter.on("dblClickOnRow", (staff) => {
            // console.log(staff);
            this.isFix = true;
            this.isAdd = false;
            this.employee = staff;
            console.log(this.employee);
            this.isOpen = true;
        });
        this.emitter.on("addEmployee", (employee) => {
            console.log(employee);
            if (this.isAdd) {
                console.log(this.employee);
                var me = this;
                axios
                    .post(`https://nguyensynamtodolist-14-02.herokuapp.com/createemployee`, me.employee)
                    .then(function (res) {
                        console.log(res);
                    })
                    .catch(function (res) {
                        console.log(res);
                    });
            } else {
                var me = this;
                var url = `https://nguyensynamtodolist-14-02.herokuapp.com/employee/` + employee._id
                axios
                    .put(url, employee)
                    .then(function (res) {
                        console.log(res);
                    })
                    .catch(function (res) {
                        console.log(res);
                    });
            }

        });
    },
    data() {
        return {
            employee: {},
            isOpen: false,
            isFix: false,
            isAdd: false,
        };
    },
};
</script>

<style scoped>
.dialogAdd {
    background-color: rgba(143, 143, 143, 0.445);
    position: absolute;
    z-index: 50;
    box-sizing: border-box;
    font-family: inherit;
}

.dialog-content {
    width: 890px;
    height: 600px;
    background-color: #fff;
    margin: 30px auto;
    border-radius: 4px;
    position: relative;
}

.top-content {
    justify-content: space-between;
    height: 220px;
    width: 100%;
    background-color: rgb(255, 255, 255);
    display: flex;
}

.left-content {
    width: 48%;
    background-color: rgb(255, 255, 255);
}

.right-content {
    width: 48%;
    background-color: rgb(255, 255, 255);
}

.content input {
    height: 30px;
    border: 1px solid black;
    border-radius: 4px;
    padding-left: 16px;
    outline: none;
}

.content div {
    margin-bottom: 5px;
}

.header {
    width: 100%;
    height: 70px;
    background-color: rgb(255, 255, 255);
    display: flex;
    align-items: center;
}

.name {
    font-size: 22px;
    font-weight: bold;
    margin-left: 35px;
}

.checkEmploy1,
.checkEmploy2 {
    width: 17px;
    height: 17px;
    margin-left: 12px;
    margin-right: 3px;
}

.info {
    background: url(../assets/images/question.png) no-repeat;
}

.btn-close {
    background: url(../assets/images/close.png) no-repeat;
}

.content {
    width: 100%;
    height: 480px;
    background-color: rgb(255, 255, 255);
    padding-left: 35px;
    padding-right: 35px;
}

.bottom {
    justify-content: space-between;
    width: 100%;
    height: 60px;
    background-color: rgb(255, 255, 255);
    align-items: center;
    border-top: 1px solid gray;
}

.bottom button {
    height: 36px;
    padding-left: 16px;
    padding-right: 16px;
    border-radius: 4px;
    outline: none;
    border: 1px solid gray;
}

.cancel {
    margin-left: 35px;
}

.save-add {
    margin-right: 35px;
    margin-left: 8px;
    background-color: #2c9f1c;
}
</style>
