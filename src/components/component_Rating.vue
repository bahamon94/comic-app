<template>
<div class="rating">
    <ul class="list">
      <li @click="votar(cantidad)" v-for="cantidad in maximaCalificacion" :class="{ 'active': cantidad <= calificacion }" :key="cantidad.calificacion" class="star">
      <i :class="cantidad <= calificacion ? 'fas fa-star' : 'far fa-star'"></i> 
      </li>
    </ul>
  </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
  export default {
    props: {
      calificacion: { type: Number, required: true , default: 0 },
      maximaCalificacion: { type: Number, required: false, default: 5 }
    },
    setup(props, context){
      const data =  reactive({ 
        stars: props.calificacion
      })
      

      function votar(cantidad) {
        context.emit('seleccionCalificar', {cantidad: cantidad, max:props.maximaCalificacion})
      }

    return { votar, ...toRefs(data) }
    }

    
  }
</script>

<style lang="scss" scoped>
.rating {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 10px;
    color: #b7b7b7;
    background: #fff;
    border-radius: 8px;
    .list {
        padding: 0;
        margin: 0 20px 0 0;
        &:hover {
            .star {
                color: #ffe100;
            }
        }
        .star {
            display: inline-block;
            font-size: 42px;
            transition: all .2s ease-in-out; 
            cursor: pointer;
            &:hover {
                ~ .star:not(.active) {
                    color: inherit;
                }
            }
            &:first-child {
                margin-left: 0;
            }
            &.active {
                color: #ffe100;
            }
        }
    }
    .info {
        margin-top: 15px;
        font-size: 40px;
        text-align: center;
        display: table;
        .divider {
            margin: 0 5px;
            font-size: 30px;
        }
        .score-max {
            font-size: 30px;
            vertical-align: sub;
        }
    }
}
</style>