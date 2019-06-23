<template>
    <div id="main">
        <Header title="我的喵喵"/>
        <Login />
        <Navbar />
    </div>
</template>

<script>
import Header from '@/components/Header'
import Navbar from '@/components/Navbar'
import Login from '@/components/Login'

export default {
    name:'Mine',
    components:{
        Header,
        Navbar,
        Login
    }
}
</script>

<style>

</style>
