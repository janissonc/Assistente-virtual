<template>

  <site-template>

    <span slot="menuesquerdo">
      <img :src="usuario.imagem" class="responsive-img">
    </span>

    <span slot="principal">

      <h2>Perfil</h2>

      <input type="text" placeholder="Nome" v-model="name">
      <input type="text" placeholder="E-mail" v-model="email">
      <input type="file" v-on:change="uploadImagem">
      <input type="password" placeholder="Senha" v-model="password">
      <input type="password" placeholder="Confirme sua Senha" v-model="password_confirmation">
      <button class="btn" v-on:click="perfil()">Atualizar</button>



    </span>



  </site-template>



</template>

<script>
import SiteTemplate from '@/templates/SiteTemplate'
import axios from 'axios';

export default {
  name: 'Perfil',
  data () {
    return {
      name:'',
      email:'',
      imagem:'',
      password:'',
      password_confirmation:'',
      usuario:false
    }
  },
  created(){

    let usuarioAux = sessionStorage.getItem('usuario');
    if(usuarioAux){
      this.usuario = JSON.parse(usuarioAux);
      this.name = this.usuario.name;
      this.email = this.usuario.email;
    }
  },
  components:{
    SiteTemplate
  },
  methods:{
    uploadImagem(e){
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length)
        return;
      this.createImage(files[0]);

    },
    createImage(file) {
      var reader = new FileReader();
      reader.onload = (e) => {
        this.imagem = e.target.result;
      };
      reader.readAsDataURL(file);
    },
    removeImage: function (e) {
      this.imagem = '';
    },
    perfil(){

      axios.put(`http://127.0.0.1:8000/api/perfil`, {
        name: this.name,
        email: this.email,
        imagem: this.imagem,
        password:this.password,
        password_confirmation:this.password_confirmation
      },{"headers": {"authorization": "Bearer "+this.usuario.token}})
      .then(response => {
        //console.log(response)
        if(response.data.token){
          // login com sucesso
          console.log(response.data)
          this.usuario = response.data;
          sessionStorage.setItem('usuario',JSON.stringify(this.usuario));
        }else{
          // erros de validação
          console.log('erros de validação')
          let erros = '';
          for(let erro of Object.values(response.data)){
            erros += erro +" ";
          }
          alert(erros);
        }
      })
      .catch(e => {
        console.log(e)
        alert("Erro! Tente novamente mais tarde!");
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
