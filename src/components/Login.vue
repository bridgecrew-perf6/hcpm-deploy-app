<template>
    <div id="container" class="flex h-screen w-[1366px]">
        <div id="Login-form" class="w-1/3 min-h-[350px] mx-auto mt-[70px]">
            <div>
                <img class="mx-auto w-[160px] h-[70px] mb-3" src="../assets/images/logo.png" alt="" />
            </div>
            <div id="Login-mode" class="w-[90%] h-[50px] bg-slate-300 flex mx-auto">
                <div id="Login" class="mode w-1/2 border-r-[1px] text-center text-base font-medium pt-3" @click="LoginMode">Đăng nhập</div>
                <div id="Regis" class="mode w-1/2 text-center text-base font-medium pt-3" @click="RegisMode">Đăng ký</div>
            </div>
            <!-- //? Regis content -->

            <div v-if="isLogin" id="Login-content" class="flex flex-col justify-items-center">
                <input type="text" name="" id="" class="w-[90%] border-[2px] h-[40px] mx-auto mt-20 pl-3 rounded" placeholder="Tên đăng nhập" />
                <input type="password" name="" id="" class="w-[90%] border-[2px] h-[40px] mx-auto mt-4 pl-3 rounded" placeholder="Mật khẩu" />
                <a class="text-blue-600 text-xs text-right mt-2 mr-10 cursor-pointer">Quên mật khẩu ?</a>
                <button class="w-[90%] h-[40px] bg-blue-700 mx-auto mt-4 rounded mb-10" @click="LoginEvent">Đăng nhập</button>
            </div>
            <!-- //? Regis content -->
            <div v-if="isRegis" id="Regis-content" class="flex flex-col justify-items-center">
                <input type="text" name="" id="" class="w-[90%] border-[2px] h-[40px] mx-auto mt-20 pl-3 rounded" placeholder="Tên đăng nhập" />
                <input type="text" name="" id="" class="w-[90%] border-[2px] h-[40px] mx-auto mt-4 pl-3 rounded" placeholder="Email" />
                <input type="text" name="" id="" class="w-[90%] border-[2px] h-[40px] mx-auto mt-4 pl-3 rounded" placeholder="Số điện thoại" />
                <input type="text" name="" id="" class="w-[90%] border-[2px] h-[40px] mx-auto mt-4 pl-3 rounded" placeholder="Mật khẩu" />

                <button class="w-[90%] h-[40px] bg-blue-700 mx-auto mt-4 rounded mb-10">Đăng ký</button>
            </div>
        </div>
        <div id="right" class="w-2/3 h-full">
            <img src="../assets/images/itteam.jpg" class="w-[80%] h-[300px] mx-auto mt-[155px]" alt="" />
            <div class="">
                <p class="text-white font-normal text-4xl text-center mt-3" style="text-shadow: 1px 1px 4px white">Leading technology solutions</p>
                <p class="text-center text-white px-40 " style="text-shadow: 1px 1px 1px white"> Optimizing work processes</p>
                <p class="text-center text-white px-40 " style="text-shadow: 1px 1px 1px white"> It can be a very secure path to earn good money and make you a very successful creative entrepreneur. You can take advice from experience People and improve your startup process.</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        LoginMode() {
            this.isLogin = true;
            this.isRegis = false;
            document.getElementById("Login").style.borderBottom = "3px solid rgb(36, 204, 255) ";
            document.getElementById("Login").style.backgroundColor = "#C9D5E1";
            document.getElementById("Regis").style.borderBottom = "none";
            document.getElementById("Regis").style.backgroundColor = "#EEEEEB";
        },
        RegisMode() {
            this.isLogin = false;
            this.isRegis = true;
            document.getElementById("Regis").style.borderBottom = "3px solid rgb(36, 204, 255) ";
            document.getElementById("Regis").style.backgroundColor = "#C9D5E1";
            document.getElementById("Login").style.borderBottom = "none";
            document.getElementById("Login").style.backgroundColor = "#EEEEEB";
        },
        LoginEvent() {
            window.open("/home", "_self");
        },
    },
    data() {
        return {
            isLogin: true,
            isRegis: false,
        };
    },
};
</script>

<style scoped>
.mode:hover {
    cursor: pointer;
}
input:focus {
    outline: none;
    border: 2px solid rgb(137, 212, 241);
}
#Login {
    border-bottom: 3px solid rgb(36, 204, 255);
}
#Regis {
    background-color: #edeee8;
}
#right {
    background-image: url(../assets/images/bg.jpg);
    background-size: cover;
}
</style>
