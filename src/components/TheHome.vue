<template>
    <div>
        <nav class="navbar navbar-light bg-light">
            <a class="navbar-brand">Navbar</a>
            <form class="form-inline">
                <button class="btn btn-outline-success my-2 my-sm-0" 
                type="submit"
                @click.prevent="LogoutUser">Logout</button>
            </form>
        </nav>
        <ul class="list-group">
            <li class="list-group-item"><span>Usuario: </span>{{user.nombre}}</li>
            <li class="list-group-item"><span>E-mail: </span> {{user.email}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    data(){
        return{
            user : {}
        }
    },
    methods:{
        LogoutUser(){
            localStorage.removeItem('jwt');
            localStorage.removeItem('user');
            this.$router.push('/');
        },
        getUserData(){
            let token = localStorage.getItem('jwt');
            let user = localStorage.getItem('user');
            //verificar la diferencia entre guardarlo como solo user
            console.log(user);
            this.user = JSON.parse(user);
            //aca lo vuelve .json para visualizarlo mejor
            console.log(this.user);
        }
    },
    //se ejecuta cuando el elemento es creado
    created(){
        this.getUserData();

    }
    
}
</script>

<style lang="stylus" scoped>

</style>