<template>
    <Header></Header>
    <h1>Hello, User! <br> Welcome on Add Restaurant Page of 60630 and 59974 </h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Name" v-model="restaurant.name"/>
        <input type="text" name="address" placeholder="Enter address" v-model="restaurant.address"/>
        <input type="text" name="contact" placeholder="Enter contact" v-model="restaurant.contact"/>
        <button type="button" v-on:click="addRestaurant">Add new Restaurant</button>
    </form>
</template>
<script>
import Header from './Header.vue';
import axios from 'axios';
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Add',
    components: {
        Header
    },
    data()
    {
        return {
            restaurant : {
                name: '',
                address: '',
                contact: ''
            }
        }
    },
    methods: {
        async addRestaurant()
        {
            console.warn(this.restaurant)
            const result = await axios.post("http://localhost:3000/restsurant", {
                name:this.restaurant.name,
                address:this.restaurant.address,
                contact:this.restaurant.contact
            });
            if(result.status==201)
            {
                this.$router.push({name:'Home'});
            }
            console.warn("result", result)
        }
    },
    mounted()
    {
        let user = localStorage.getItem('user-info');
        this.name = JSON.parse(user).name;
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }
    }
}
</script>
