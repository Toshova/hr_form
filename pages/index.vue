<template>
  <div class="wrapper">

    <div class="form_header">
      <span id="docs_header" >Документы</span>
        <div class="btn_wrapper">
        <div>
          <button ><img id="bookmark" src="/bookmark.png"></button>
        </div>
        <div class="btn">
          <button  @click="toggleModal"> Новый тип</button>
        </div>
        <div class="btn">
          <button>Новый документ</button>
        </div>
      </div>           
  </div>

  <div class="search_form" >
    <form action="" method="get" >
      <button type="submit"><img src="/loupe.png"></button>
      <input 
      placeholder="Поиск" 
      type="search" 
      v-model="query">
    </form>
  </div>





  <div class="accord_wrapper">
    <nestedDrag :docs="docs" :docs2="docs2" @delete-doc="deleteDoc"/>
 
  </div>


<modalWindow  
v-show="isShowModal" 
@close="toggleModal"
@addDoc="addDoc"
/>

<ul>
  <div v-for="doc of queryDocs" :key="doc">{{ doc.name }}
    <div v-for="el of doc.childs" :key="el">{{ el.name}}</div>
  </div>
</ul>

{{ query }}
</div>
  

</template>




<script>
import { ref } from "vue";
import nestedDrag from "../components/nested-drag.vue";
import modalWindow from "../components/modal-window.vue";


export default {
  name: 'IndexPage',
components: {
 nestedDrag, modalWindow
}, 

data(){
  return {
    display: "Nested",   
    isShowModal: false,
    query: ref(''),
    
		docs: [
        {
          id: 1,
          name: "Обязательные для всех",
          type: "Category",
          open: false,
          childs: [
            {
              id: 2,
              name: "Паспорт",
              type: "Document",
              
            },
            {
              id: 3,
              name: "Тестовое задание кандидата",
              type: "Document",
              
            },
            {
              id: 4,
              name: "Трудовой договор",
              type: "Document",
            },
            {
              id: 5,
              name:  "ИНН",
              type: "Document",
            },
            {
            id: 6,
            name: 'Мед. книжка',
            type: "Document",
            },
          ]
        },
        {
          id: 7,
          name: 'Обязательные для трудоустройства',
          type: "Category",
          open: false,
          childs: [
            {
              id: 8,
              name: 'Мед. книжка',
              type: "Document",
             
            }
          ]
        },
        {
          id: 9,
          name: 'Специальные',
          type: "Category",
          open: false, 
          childs: []
          
        }
      ],
      docs2:[
      {
              id: 8,
              name: 'Мед. книжка',
              type: "Document",
             
            }
      ]
  }
  },
  methods: {
  deleteDoc(arr, idx){
    arr.splice(idx, 1);     
  },
  toggleModal() {
      this.isShowModal = !this.isShowModal;
    },
  changeInputValue(event){
    console.log(event.target.value)
  },
  addDoc(data){
    this.docs.push(data)
  }
},

}
</script>

<style>
.red {
  border: 3px solid red;
  margin-top: 30px;
}
body{
  width: 100%;
}
.wrapper{
  display: flex;
  flex-direction:column;
  margin:38px 30px ;
  font-family: "Fira Sans";
}

.form_header {
  display: flex;
  justify-content: space-between;
  margin-top: 29px;
  
}

.form_header span {
  font-size: 20px;
  font-weight: 600;
}

.search_form{
  width: 564px;
  height: 30px;
  border-bottom: 0.5px solid grey;
  margin-top: 20px;
  margin-bottom: 19px;
}

.btn_wrapper{
  display: flex; 
  margin-top: 8px; 
}

.btn {
  display: flex;
  flex-direction: row;
  height: 30px;
  border: 1px solid #D3D8DF;
  border-radius: 50px;
  font-size: 12px;
  font-weight: 500;
  line-height: 13px;
  background-image: url("/cross.png");
  background-repeat: no-repeat;
  background-position: 10px 50%;
  padding: 8px 20px 9px 30px;
  margin-left: 10px;
}
 .accord_wrapper{
  width: 100%;
 }

#docs_header{
  font-size: 22px;
  font-weight: 500;
  line-height: 23.76px;
  margin-top: 8px;
}

.docs2{
  margin-top: 20px;
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

.moving-card {
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