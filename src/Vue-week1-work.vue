<template>
    <div class="container">
        <h3>VUE - 2024 - Week1</h3>    
        <table class="table table-striped text-center align-middle">
            <thead>
                <tr style="border-bottom:2px solid #adb5bd;border-top: 1px solid #adb5bd;">
                    <th scope="col">品項</th>
                    <th scope="col">描述</th>
                    <th scope="col">價格</th>
                    <th scope="col">庫存</th>
                    <th scope="col">功能</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="drinks in drinkTea" :key="drinks.id">
                    <td>{{ drinks.title }}</td>
                    <td><small>{{ drinks.description }}</small></td>
                    <td>{{ drinks.price }}</td>
                    <td>
                        <button type="button" class="btn-sm" @click="drinks.stock--" :disabled="drinks.stock < 1">－</button>
                        {{ drinks.stock }}
                        <button type="button" class="btn-sm" @click="drinks.stock++">＋</button>
                    </td>
                    <td>
                        <button type="button" class="btn btn-secondary" @click="editDrink(drinks)">內容編輯</button>
                    </td>
                </tr>
            </tbody>
        </table>
        <!-- 編輯 -->
        <div v-if="isShow" class="edit-box">
        <h5>編輯內容</h5>
        <div class="mb-3">
            <label class="form-label">品項名稱</label>
            <input type="text" class="form-control" v-model="tempBox.title">
        </div>
        <div class="mb-3">
            <label class="form-label">描述</label>
            <input type="text" class="form-control" v-model="tempBox.description">
        </div>
        <div class="mb-3">
            <label class="form-label">價格</label>
            <input type="number" class="form-control" v-model="tempBox.price">
        </div>
        <div class="mb-3">
            <label class="form-label">庫存</label>
            <input type="number" class="form-control" v-model="tempBox.stock">
        </div>
        <button type="submit" class="btn btn-primary me-2" @click="tempBox= {} ; isShow = false">取消</button>
        <button type="submit" class="btn btn-primary" @click="saveChanges">儲存變更</button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const drinkTea = ref([
    {id: 1, title: "珍珠奶茶", description: "香濃奶茶搭配QQ珍珠", price: 50, stock: 20},
    {id: 2, title: "冬瓜檸檬", description: "清新冬瓜配上新鮮檸檬", price: 45, stock: 18},
    {id: 3, title: "翡翠檸檬", description: "綠茶與檸檬的完美結合", price: 55, stock: 34},
    {id: 4, title: "四季春茶", description: "香醇四季春茶，回甘無比", price: 45, stock: 10},
    {id: 5, title: "阿薩姆奶茶", description: "阿薩姆紅茶搭配香醇鮮奶", price: 50, stock: 25},
    {id: 6, title: "檸檬冰茶", description: "檸檬與冰茶的清新組合", price: 45, stock: 20},
    {id: 7, title: "芒果綠茶", description: "芒果與綠茶的獨特風味", price: 55, stock: 18},
    {id: 8, title: "抹茶拿鐵", description: "抹茶與鮮奶的絕配", price: 60, stock: 20},
])

const isShow = ref(false);
const tempBox = ref({});
const editDrink = (item) => {
    tempBox.value = { ...item }; // 複製一個新的物件來編輯
    console.log(tempBox);
    isShow.value = true;
};

const saveChanges = () => {
    if (!tempBox.value.title || !tempBox.value.description || !tempBox.value.price || tempBox.value.stock === undefined) {
        alert('欄位不可空白唷！');
        return;
    }else if (tempBox.value.price < 0 || tempBox.value.stock < 0) {
        alert('價格和庫存不能是負數！');
        return;
    }
    
    isShow.value = false;
    const index = drinkTea.value.findIndex(item => item.id === tempBox.value.id);
    if (index !== -1) {
        drinkTea.value[index] = tempBox.value;
    }
    tempBox.value = {};
}
</script>