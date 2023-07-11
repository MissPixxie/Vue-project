<template>
  <header>
    <headerComponent /> 
  </header> 
  <main>
    <router-view/>  
  </main>
  <footer>
    <div>
      <ul>
        <li><h3>Rubrik</h3></li>
        <li>Lite text</li>
        <li>Lite mer text</li>
      </ul>
    </div>
    <div>
      <ul>
        <li><h3>Rubrik</h3></li>
        <li>Lite text</li>
        <li>Lite mer text</li>
      </ul>
    </div>
    <div>
      <ul>
        <li><h3>Rubrik</h3></li>
        <li>Lite text</li>
        <li>Lite mer text</li>
      </ul>
    </div>
  </footer>
</template>

<script>
  import headerComponent from './components/headerComponent.vue';

  export default {
    components: { headerComponent }
  }
</script>
<style>
#app {
  font-family: 'Shadows Into Light Two', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(224, 224, 224);
}

body {
  margin: 0%;
  background-color: rgb(26, 26, 26);
}

footer {
  background-color: rgb(12, 12, 12);
  display: flex;
  font-size: 1.1em;
  font-family: 'Taviraj', serif;
  padding: 1%;
  justify-content: space-evenly;
  box-shadow: 0px -3px 20px 2px rgba(0, 0, 0, 0.589);
}

footer h3 {
  text-transform: uppercase;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
