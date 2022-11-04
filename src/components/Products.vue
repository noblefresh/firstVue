<template>
    <div>
        <div class="py-28">
    <div class="max-w-6xl mx-auto py-4 space-y-5">
        <div class="flex">
            <div class="flex-grow text-4xl font-extrabold">Special Menu For You</div>
        </div>
        <div class="grid gap-20 grid-cols-1 md:grid-cols-2 lg:grid-cols-3 px-3">
            <div v-for="(products, i) in fetchData" :key="i" class="rounded-lg shadow-xl" style="">
                <router-link :to="{ name: 'single-product', params: { id: products.id }}">
                <div class=" bg-white w-full flex justify-center items-center">
                    <img :src="products.thumbnail" alt="" srcset="">
                </div>
                <div class="bg-gray-100 py-16 relative font-bold text-xl w-full flex flex-col justify-center px-6">
                    <div class="">{{ products.title}}</div>
                    <div class="">
                        &#8358; 2040
                    </div>
                    <button @click="getProductID(products.id)" class="absolute bg-btn-color text-sm cursor-pointer rounded-lg px-10 right-6 top-20 font-light text-white" style="padding:10px 45px 10px">
                        Order
                    </button>
                </div>
                </router-link>
            </div>
        </div>
    </div>
</div>
    </div>
</template>

<script>
// import { defineComponent } from '@vue/composition-api'
import axios from 'axios'
import { RouterLink } from 'vue-router';

export default ({
    data(){
        return{
            fetchData:[],
            productId:''
        }
    },
    mounted(){
        axios.get('http://localhost:9000/store/products')
        .then((data) => {
                this.fetchData = data.data.products
                // console.log(this.fetchData);
            }).catch(err => console.log(err.products));
    },
    methods:{
        getProductID(id){
            axios.get(`http://localhost:9000/store/products/${id}`)
            .then((productData) => {
                this.$router.push({ name: 'single-product', params: {productData} })
                    // console.log(data);
                }).catch(err => console.log(err));
            // this.$router.push({ name: 'single-product', params: {id} })

            // let data = {
            //     id: id,
            //     description: "pass data through params"
            // };
            // this.$router.push({
            //     name: "single-product", //use name for router push
            //     params: { data }
            // });
            // console.log(this.data);
        }
    }
})
</script>

