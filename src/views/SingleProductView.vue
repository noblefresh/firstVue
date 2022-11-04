<script setup>
import FooterCom from '../components/FooterComponent.vue'
</script>

<template>
    <main>
        <div class='py-20 px-4'>
            <div class='text-white max-w-6xl mx-auto py-2'>
                <div class='grid md:grid-cols-2 gap-20 grid-cols-1'>
                
                    <div class=''>
                        <div class="relative">
                            <img src="/src/images/black_hoodie_front.webp" alt="no image" />
                            <div class="absolute overflow-x-scroll w-full bottom-0 right-0 p-4 flex flex-nowrap gap-4">
                                <!-- <divclass="w-24 h-32 bg-red-300 py-2"></div> -->
                                <div  v-for="(er,i) in 12" :key="i" class="flex w-full flex-nowrap gap-4 rounded-lg">
                                    <div class="w-24 flex-none">
                                        <div class="p-4 w-full rounded-lg">01</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>


  


                    <div class=''>
                        <div class='flex md:flex-col flex-col space-y-7 justify-center'>
                            <div class='text-black space-y-3'>
                                <h2 class='font-bold text-xl text-black'>{{product.title}}</h2>
                                <p class='text-sm'>{{product.description}}</p>
                            </div>

                            <div class='space-y-3'>
                            <div class='font-bold text-md text-black'>Select Size</div>
                            <div class='flex flex-row gap-4'>
                                <div v-for="(size,i) in sizes" :key="i" class="">
                                    <div @click="currentSize = size ; currentPrice = priceList[i]" :class="currentSize == size ? 'border-purple-300 bg-purple-100':'border-gray-100' " contenteditable="false" class='border-2 rounded-md cursor-pointer flex justify-center py-3 px-5'>
                                        <span class=' text-black text-sm'>{{size}}</span>
                                    </div>
                                </div>
                            </div>
                            </div>


                            <div>
                            <div class='flex flex-col space-y-3'>
                                <div>
                                <span class='text-gray-700 text-2xl font-san'>&euro; {{ currentPrice }}</span>
                                </div>

                                <div class='bg-gray-900 text-white w-full text-sm font-semibold py-3 flex justify-center cursor pointer hover:bg-white hover:border hover:border-gray-900 hover:text-black '>
                                    ADD TO CART
                                </div>
                            </div>
                            </div>

                            <div class='space-y-4'>
                            <div class='flex flex-row gap-4'>
                                <div class='text-black text-sm border-b border-black cursor-pointer'>
                                PRODUCT INFORMATION
                                </div>
                                <div class='text-black text-sm  cursor-pointer'>
                                SHIPPING & RETURNS
                                </div>
                            </div>

                            <div class='grid grid-cols-2 gap-8 text-black'>
                                <div class='flex flex-col space-y-3'>
                                <div class='space-y-1'>
                                    <h3 class='text-sm text-black'>Material</h3>
                                    <p class='text-sm'>--</p>
                                </div>

                                <div class='space-y-1'>
                                    <h3 class='text-sm text-black'>Country of Origin</h3>
                                    <p class='text-sm'>--</p>
                                </div>

                                <div class='space-y-1'>
                                    <h3 class='text-sm text-black'>Type</h3>
                                    <p class='text-sm'>--</p>
                                </div>
                                </div>

                                <div class='flex flex-col space-y-3'>
                                <div class='space-y-1'>
                                    <h3 class='text-sm text-black'>Weight</h3>
                                    <p class='text-sm'>450 g</p>
                                </div>

                                <div class='space-y-1'>
                                    <h3 class='text-sm text-black'>Dimension</h3>
                                    <p>--</p>
                                </div>
                                </div>

                            </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <footer-com/>
    </main>
</template>

<script>
import axios from 'axios'

export default {
    // props:['data'],
    data(){
        return{
            productData:[],
            product:[],
            productId:'',
            sizes:[],
            currentSize:'S',
            priceList:[],
            currentPrice: ''
        }
    },
    mounted(){
        this.productId = this.$route.params.id
        axios.get(`http://localhost:9000/store/products/${this.productId}`)
        .then((productData) => {
                this.product = productData.data.product;
                console.log(this.product);
                this.currentPrice = this.product.variants[0].prices[0].amount
                this.product.variants.forEach(data => {
                    this.sizes.push(data.title)                    
                    this.priceList.push(data.prices[0].amount)                    
                });
                // this.data = this.$route.params.id
            }).catch(err => console.log(err));
    }
}
</script>