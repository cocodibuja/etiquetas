<template>
  <div>
    <form @submit.prevent="procesarFormulario" >
      <div class="input-nombre">
        <div>
        <label for="nombre">Nombre etiqueta:</label>
        <!-- <div class="error" > Error </div> -->
        </div>
        <input type="text" name="nombre" id="" placeholder="ingrese nombre" autocomplete="off" v-model.trim="etiqueta.nombre" maxlength="20">
      </div>

      <br>
      <hr>
      <input type="radio" name="tipo" value="frecuencia" v-model="etiqueta.tipo"> Frecuencia
      <input type="radio" name="tipo" value="tiempo" v-model="etiqueta.tipo"> Tiempo
      <br>
      <span>Picked: {{etiqueta.tipo }}</span>
      <hr>
      <br>
      <p>{{etiqueta.tipo ==='tiempo'?'ingrese teclas':'ingrese tecla'}} </p>
      <input type="text"  id="inputKey01" placeholder="ingrese tecla 1" autocomplete="off" v-on:keyup="almacenaTecla1" >
      <input v-if="etiqueta.tipo === 'tiempo'" type="text"  id="inputKey02" placeholder="ingrese tecla 2" autocomplete="off" v-model="etiqueta.key02" v-on:keyup="almacenaTecla2">
      <hr>
      <br>
      <select v-model="etiqueta.color">
        <option disabled value="null">Seleccione un color:</option>
        <option>Rojo</option>
        <option>Azul</option>
        <option>Violeta</option>
      </select>
      <span>Color seleccionado: {{ etiqueta.color }}</span>
      <hr> 
      <button type="submit" :disabled="bloquear"> Procesar </button>  
    </form>
    <p>{{etiqueta}}</p>
  </div>
</template>

<script>
// @ is an alias to /src


export default {
  name: 'Home',
  components: {
    
  },
  data() {
    return {
      etiqueta:{
        nombre:'',
        tipo:'',
        key01:null,
        keycode01:null,
        key02:null,
        keycode02:null,
        color:null
      },
      colores:["red","blue","celeste"]
    }
  },
  methods: {
    almacenaTecla1(event) {
      console.log("hola Nico: " +event.key+" " +event.keyCode)
      this.etiqueta.key01 = event.key
      this.etiqueta.keycode01 = event.keyCode
      document.getElementById('inputKey01').value = this.etiqueta.key01
      if (this.etiqueta.tipo === 'tiempo') {
        if (this.etiqueta.keycode01 === this.etiqueta.keycode02) {
          console.log('ya estas usando esta tecla en key 2')
        }
      }
    },
    almacenaTecla2(event) {
      console.log("hola Nico: " +event.key+" " +event.keyCode)
      this.etiqueta.key02 = event.key
      this.etiqueta.keycode02 = event.keyCode
      document.getElementById('inputKey02').value = this.etiqueta.key02
      if (this.etiqueta.tipo === 'tiempo') {
        if (this.etiqueta.keycode01 === this.etiqueta.keycode02) {
          console.log('ya estas usando esta tecla en key 1')
        }
      }
     
    },
    procesarFormulario(){
      console.log(this.etiqueta)

      this.etiqueta = {
        nombre:'',
        tipo:'',
        key01:null,
        keycode01:null,
        key02:null,
        keycode02:null,
        color:null
      }
    }
    },
    computed: {
      bloquear() {
        return  this.etiqueta.nombre === ''
      }
    },
}
</script>

<style scoped>
  .div{
    display:flex;
    flex-direction: column;
  }
</style>
