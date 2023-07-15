<template>
    <li><router-link to="/"> <a :style="{color: letrasColor}">Home</a></router-link></li>
    <li><router-link to="/products"><a :style="{color: letrasColor}">Registro</a></router-link></li>
    <li><router-link to="/about"><a :style="{color: letrasColor}">About</a></router-link></li>
</template>
  
<script>
export default {
    name: 'MenuPrinc',
    data() {
        return {
            letrasColor: "white"
        }

    }
}
</script>