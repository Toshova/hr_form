<template>
<div class="wrapper">

  <div class="form_header">
    <span id="docs_header" >Документы</span>
      <div class="btn_wrapper">
        <div >
          <button ><img id="bookmark" src="/bookmark.png"></button>
        </div>
        <div class="btn">
          <button> Новый тип</button>
        </div>
        <div class="btn">
          <button>Новый документ</button>
        </div>
      </div>           
  </div>

  <div class="search_form" >
    <form action="" method="get" >
      <button type="submit"><img src="/loupe.png"></button>
      <input placeholder="Поиск" type="search" v-model="searchQuery">
    </form>
  </div>

  <div class="accord_wrapper">
    <nested-drag :docs="list" @delete-doc="deleteDoc"/>
  </div>
  </div>
  

</template>

<style>
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



</style>


<script>
import nestedDrag from '../components/nested-drag.vue';

export default {
  name: 'IndexPage',
components: {
  nestedDrag
}, 

data(){
  return {
    display: "Nested",
		list: [
        {
          id: 1,
          name: "Обязательные для всех",
          type: "Category",
          open: false,
          docs: [
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
          docs: [
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
          docs: []
          
        }
      ]
  }
  },
  methods: {
  deleteDoc(id){
   this.list=this.list.filter(x => x.id !== id);        
  }
},
 
}
</script>

   