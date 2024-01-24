<template>
	<div class="accordions">

		<dl class="acc_items" v-for="doc in docs" :key="doc.id" @click="doc.open = !doc.open" >
      <div class="acc_item">
        <button class="arrow arrow-up" v-if="doc.open && doc.term" ></button>
        <button class="arrow arrow-down" v-if="!doc.open && doc.term" ></button>
        <div class="term" v-text="doc.term"></div>
        <span class="term" v-if="!doc.term" v-text="doc.type"></span>
        <span class="def" v-text="doc.def"></span>
        <deleteComp 
        :doc="doc"
        @remove-doc="removeDoc"
        />
      </div>
      <div>
        <span class="docs" v-show="doc.open">   
          <div class="doc_type doc_in" v-for="item in doc.items" :key="item.id">
            <span  v-text="item.type"></span> 
            <deleteComp 
            :doc="doc"
        @remove-doc="removeDoc"
        />     
          </div>  
          
        </span>
      </div>
     
      </dl> 


</div>
   
    

</template>


<style scoped>

.term {
  display: flex;
  flex-direction: column;
  font-size: 15px;
  font-weight: 500;
  line-height: 16px;
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
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  min-height: 48px;
  
}
.acc_item{
  display: flex;
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

.docs{
  display: flex;
  flex-direction: column;
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


</style>

<script>
import deleteComp from './delete-comp.vue'; 

export default {
  components: {
  deleteComp
  },
data() {
  return{
    docs: [
      {
        id:1,
				term: 'Обязательные для всех',
        def: 'Документы, обязательные для всех сотрудников без исключения',
				items: [
          {
            id: 7,
            type: "Паспорт",
            def: ''
          },
          {
            id: 8,
            type:  "ИНН",
            def: ''
        }

    ],
				open: false
			},
			{
        id: 2,
				term: 'Обязательные для трудоустройства',
        def: 'Документы, без которых невозможно трудоустройство человека на какую бы то ни было должность в компании вне зависимости от гражданства',
				items: [
        {
            id: 9,
            type:  "item 1",
        },
          {
            id: 10,
            type:   "item 2",
        }
    ],
				open: false
			},
			{
       id: 3,
				term: 'Специальные',
        def: '',
				items: '',
				open: false
			},
      {
        id: 4,
        type: 'Тестовое задание кандидата',
        def: 'Россия, Белоруссия, Украина, администратор филиала, повар-сушист, повар-пиццмейкер, повар горячего цеха'
      },
      {
        id: 5,
        type: 'Трудовой договор',
        def: ''
      },
      {
        id: 6,
        type: 'Мед. книжка',
        def: ''
      },

    ],
      
    } 
  },

methods: {
  removeDoc(id){
   this.docs=this.docs.filter(x => x.id !== id);   
      
  },
}
}

</script>