<template>
  <div id="app" class="appContainer p-5">
    <div class="p-5 text-center">
      <h1>Crea tu contenido personalizado</h1>
    </div>
    
    <div class="container p-5">
    <div class="containerForm">
      <div>
        <label class="p-2" for="colorFondo">Color de fondo </label>
        <input type="color" id="colorFondo" name="colorFondo" v-model="colorFondo">
        </div>
        <div>
        <label class="p-2" for="colorTexto">Color de texto </label>
        <input type="color" id="colorTexto" name="colorTexto" v-model="colorTexto">
        </div>
        <div>
          <label class="p-2" for="colorTexto">Mostrar texto </label><input type="checkbox" v-model="texto">
        </div>
        <div>
          <label class="p-2" for="rangeBorder">Borde </label>
          <input type="range" id="rangeBorder" name="rangeBorder" min="0" max="50" step="1" v-model="radiusElement"> <span>{{ radiusElement + "%" }}</span>
        </div>
        <div>
          <label class="p-2" for="textArea">Contenido textual</label>
          <textarea class="form-control" placeholder="Escriba su comentario" id="textArea" v-model="textArea"></textarea>
        </div>
        <div>
          <label class="p-2" for="tipografia">Tipografía</label>
          <select name="tipografia" id="tipografia" v-model="tipografiaSeleccionada">
            <option v-for="tipografia in tipografias" :key="tipografia.id" :value="tipografia.font">
            {{ tipografia.font }}</option>
          </select>
        </div>
        <div>
          <label class="p-2" for="opacidad">Opaco</label>
          <input type="checkbox" name="opacidad" id="opacidad" v-model="opacity">
        </div>
        <div>
        <label class="p-2" for="fontWeight">Tamaño de letras</label>
        <br>
        <input class="mx-2"  type="radio"  value="pequeño" v-model="tamañoLetra">Pequeño
        <input class="mx-2" type="radio"  value="mediano" v-model="tamañoLetra">Mediano
        <input class="mx-2" type="radio"  value="grande" v-model="tamañoLetra">Grande
      </div>
    </div>

    <div class="containerElement">
      <div class="element" :style="{backgroundColor:color2(), borderRadius:radiusElement +'%'}">
        <!-- <p v-show="texto === true" :style="{color:colorTexto, fontFamily:tipografiaSeleccionada}"> {{ textArea }} </p> -->
        <div v-show="texto === true">
          <p v-if="tamañoLetra == 'pequeño'"
          :style="{fontFamily: tipografiaSeleccionada, fontSize:'1.5em', color: colorTexto, opacity:1 }">{{ textArea }}</p>
          <p v-else-if="tamañoLetra == 'mediano'"
          :style="{fontFamily: tipografiaSeleccionada, fontSize:'2.5em', color: colorTexto }">{{ textArea }}</p>
          <p v-else
          :style="{fontFamily: tipografiaSeleccionada, fontSize:'3.5em', color: colorTexto }">{{ textArea }}</p>
        </div>
      </div>
    </div>
    </div>


  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      colorFondo: "",
      colorTexto: "",
      texto: "",
      radiusElement: 0,
      textArea: "",
      opacity: false,
      tamañoLetra:"",
      tipografias: [
      {id: 1, name: "Arial", font: "Arial"},
      {id: 2, name: "Lucida sans", font: "Lucida sans"},
      {id: 3, name: "Georgia", font: "Georgia"},
      ],
      tipografiaSeleccionada: "",
     
    }
  },
  methods:{
    color2: function(){
      console.log(this.colorFondo)
      let red = parseInt(this.colorFondo.slice(1,3),16) 
      let green = parseInt(this.colorFondo.slice(3,5),16) 
      let blue = parseInt(this.colorFondo.slice(5,7),16) 
      let transparencia = 0.7
      if(this.opacity){
        transparencia = 1
      }
      console.log(red)
      return `rgba(${red},${green},${blue},${transparencia})`
    }
  },
  components: {
  
  }
}
</script>

<style>
.appContainer{
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}

.container{
  display: flex;
  justify-content: space-evenly;
  background-color: aqua;
  border-radius: 15px;
}

.element{
  width: 300px;
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
