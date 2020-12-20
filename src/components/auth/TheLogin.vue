<template>
    <form>
        <div class="form-group">
            <label for="exampleInputEmail1">Email address</label>
            <input type="email" 
            class="form-control" 
            id="exampleInputEmail1" 
            aria-describedby="emailHelp"
            v-model="login.email">
            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
        </div>
        <div class="form-group">
            <label for="exampleInputPassword1">Password</label>
            <input type="password" 
            class="form-control" 
            id="exampleInputPassword1"
            v-model="login.password">
        </div>
        
        <button 
        type="submit" 
        class="btn btn-primary"
        @click.prevent="loginUser">Submit</button>

        <pre>
            {{login}}
        </pre>
    </form>
</template>

<script>
import swal from 'sweetalert';

export default {
    data(){
        return{
            login:{
                email: '',
                password: ''
            }

        }
    },
    methods: {
        async loginUser(){
            try{
                let response = await this.$http.post('/api/usuario/login', this.login);
                
                let token = response.data.tokenReturn;
                let user = response.data.user;
                //esto no sé para que es, creo que toca revisar la conosla en la página

                localStorage.setItem('jtw',token);
                //para guardarlo en el local storage se tiene que parsear como stringify
                localStorage.setItem('user', JSON.stringify(user));

                if(token){
                    swal("Login correcto", "Los datos son correctos, bienvenido!", "success");
                    this.$router.push('/home');
                    
                }
            }
            catch(error){
                swal("Oops!", "Something went wrong!", "error");
                console.log(error)
            }
        }
    }
}
</script>


<style scoped>

</style>