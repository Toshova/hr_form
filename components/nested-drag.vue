<template>
  <div>

    <div class="search_form" >
    <form action="" method="get" >
      <button type="submit"><img src="/loupe.png"></button>
      <input 
      placeholder="Поиск" 
      type="search" 
      v-model="query">
    </form>
  </div>

    <draggable 
      :list="docs" 
      :group="{ name: 'g1', put: [] }" 
      ghost-class="moving-item"
      >

      <dl class="acc_items item" v-for="(doc, idx) in queryDocs" :key="doc.id">

        <div class="category term" >

          <button class="arrow arrow-up" v-if="doc.open && doc.type === 'Category'" @click="doc.open = !doc.open"></button>
          <button class="arrow arrow-down" v-if="!doc.open && doc.type === 'Category'" @click="doc.open = !doc.open" ></button>

          <p > {{ doc.name }}</p>

          <div class="btns">
            <button><img src="/pen.png"></button>         
            <button class="del_btn" @click= "$emit('delete-doc', docs, idx )"><img src="/delete.png"></button>          
            <button class="arrowDbl handle"></button>
          </div>

        </div>


      <draggable 
        v-if="doc.type === 'Category'" 
        :list="doc.childs"
        :group="{ name: 'g2', put: ['g2','g3']}"
        ghost-class="moving-item"
        >

        <div class="term nested"  v-for="el in doc.childs" :key="el.id" v-show="doc.open">
          <p>{{ el.name }}</p>
          <div class="btns">
            <button><img src="/pen.png"></button>         
            <button class="del_btn" @click= "$emit('delete-doc', doc.childs, idx )"><img src="/delete.png"></button>        
            <button class="arrowDbl handle"></button>
          </div>
        </div>
      </draggable>

      </dl>

    </draggable>

    <draggable 
      class="docs2"
      :list="docs2" 
      :group="{ name: 'g3', put: ['g2']  }"
      ghost-class="moving-item"
      >

      <div class='term' v-for="doc in queryDocs2" :key="doc.id">
        <p> {{ doc.name }}</p>
        <div class="btns">
          <button><img src="/pen.png"></button>         
          <button class="del_btn" @click= "$emit('delete-doc', docs2, idx )"><img src="/delete.png"></button>        
          <button class="arrowDbl handle"></button>
        </div>
      </div>
    </draggable>

  </div>
  
</template>


<script>
import { ref } from "vue";
import draggable from "vuedraggable"


export default {
  data(){
    return{
      query: ref(''),
    }
  },
  computed: {
   
     

      
queryDocs(){
  const q= this.query.toLowerCase()
  return this.docs.filter(doc => {
    if (doc.name.toLowerCase().includes(q)) {
      return true ||
     doc.childs.filter((doc => doc.name.toLowerCase().includes(q)));
    }
    return false
  }
  
  )
  },


  queryDocs2(){
     return this.docs2.filter(doc => doc.name.toLowerCase().includes(this.query.toLowerCase()))
  
},
  },

  props: {
    docs: {
      required: true,
      type: Array
    },
    docs2: {
      required: true,
      type: Array
    },  
  },
  components: {
    draggable
  },
  
 
   
  
};
</script>
<style scoped>
.del_btn:hover{
  opacity: 0.5;  
}

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

.moving-item {
  border: 3px solid blue !important;
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