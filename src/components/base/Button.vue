<template>
      <div class="addEmployee flex justify-between" style="background-color: #fff;">
                      <div class="name-table">NHÂN VIÊN</div>

            <button @click="emitter.emit('clickBtnAdd')" class="add-employee-btn">
                  Thêm mới nhân viên
            </button>
      </div>
</template>


<style scoped>
.addEmployee {
      width: 100%;
      height: 40px;
      display: flex;
      font-family: inherit;
}

.name-table {
      font-size: 22px;
      font-weight: 600;
      color: #111;
      padding-left: 20px;
}

.add-employee-btn {
      min-width: 100px;
      height: 35px;
      padding-left: 16px;
      padding-right: 16px;
      margin-right: 16px;
      background-color: #26a318;
      outline: none;
      border-radius: 6px;
      border: none;
      color: #fff;
}

.add-employee-btn:hover {
      background-color: #0e8800;
}
</style>


<script>

export default {
      methods: {
      },
      data(
      ) {
            return {
            };
      },
};
</script>