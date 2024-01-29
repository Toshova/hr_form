<template>
  <draggable 
  tag="ul" 
  :list="docs" 
  :group="{ name: 'g1' }"
  ghost-class="moving-card"
  :options="{handle:'.handle'}"
  >
    <dl class="acc_items item" v-for="doc in docs" :key="doc.id">
      <div class="category_wrap">
        <div class="category" v-if="doc.type === 'Category'">

          <button class="arrow arrow-up" v-if="doc.open && doc.type === 'Category'" @click="doc.open = !doc.open"></button>
          <button class="arrow arrow-down" v-if="!doc.open && doc.type === 'Category'" @click="doc.open = !doc.open" ></button>

          <span v-text="doc.name "></span>

          <div class="btns">
            <button><img src="/pen.png"></button>         
              <deleteDoc :doc="doc" @delete-doc="deleteDoc"/>            
            <button class="arrowDbl handle"></button>
          </div>

        </div>
        
        <div class="term" v-if="doc.type !== 'Category'">
          <span  v-text="doc.name "></span>

           <div class="btns">
            <button ><img src="/pen.png"></button>  
            <deleteDoc :doc="doc" @delete-doc="deleteDoc"/>        
            <button class="arrowDbl handle"></button>
          </div>

        </div>

        <div class="nested" v-if="doc.type === 'Category'" >
            <nested-draggable :docs="doc.docs" v-show="doc.open" />        
        </div>

      </div>
         
    </dl>


  </draggable>
</template>
<script>
import draggable from "vuedraggable"
import deleteDoc from "./delete-doc.vue";

export default {
  props: {
    docs: {
      required: true,
      type: Array
    },
    el: {
      required: true,
      type: Array
    },
  },
  components: {
    draggable, deleteDoc
  },
  name: "nested-draggable",
  methods: {
    deleteDoc(id){
      this.$emit('delete-doc', id)      
  },
}
};
</script>
<style scoped>


.nested{
  margin-left: 16px;
}
.category{
  display: flex;
  align-items: center;
  font-size: 15px;
  font-weight: 500;
  line-height: 16px;
  border: #DFE4EF solid 1px;
}
.arrowDbl {
  width: 22px;
  height: 22px;
  background-image: url("/arrowDblGrey.png");
  background-repeat: no-repeat;
  background-position: center center;

}
.arrowDbl:hover {
  background-image: url("/arrowDbl.png");
}

.moving-card {
  border: 3px solid blue;
}

.term {
  display: flex;
  align-items: center;
  font-size: 15px;
  font-weight: 500;
  line-height: 16px;
  
  height: 48px;
  border: #DFE4EF solid 1px;
  padding-left: 15px;
}

.def {
font-size: 11px;
font-weight: 400;
line-height: 12px;
color: #8E9CBB;
margin-left: 15px;
}
.accordions {
width: 100%;
margin-top: 20px; 
}

.acc_items{
justify-content: center;
width: 100%;
min-height: 48px;
}

.acc_item{
  width: 100%;
  min-height: 48px;
  border: #DFE4EF solid 1px;
  align-items: center;

}

.arrow {
  width: 22px;
  height: 22px;
  padding: 8px;
  border: 1px solid #D3D8DF;
  border-radius: 50%;
  margin: 14px
}

.arrow-up  {
background-image: url("/arrowUp.png");
background-repeat: no-repeat;
background-position: center center;
}

.arrow-down{
background-image: url("/arrowDown.png");
background-repeat: no-repeat;
background-position: center center;
}


.doc_type {
display: flex;
flex-direction: column;
justify-content: center;
border: 1px solid #DFE4EF;
min-height: 34px;
padding-left: 15px;
}
.doc_in {
margin-left: 12px;
}

.doc_out {
display: flex;
flex-direction: column;
}

.btns {
  width: 100px;
  display: flex;
  justify-content: space-around;
 
  align-items: center;
}





</style>