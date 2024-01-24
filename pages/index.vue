<template>
<div class="wrapper">


  <div class="form_header">
            <span id="docs_header">Документы</span>
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

  <div class="search_form">
    <form action="" method="get">
      <button type="submit"><img src="/loupe.png"></button>
      <input placeholder="Поиск" type="search">
    </form>
  </div>

  <div class="accord_wrapper">
    <accordionFormVue/>

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
import accordionFormVue from '../components/accordion-form.vue'

export default {
  name: 'IndexPage',
components: {
  accordionFormVue,
}, 
data(){
  return {
    
		rows: [
			{
        id: 1,
				term: 'Term 1',
				details: 'Some text here...',
				open: false
			},
			{
        id: 2,
				term: 'Term 2',
				details: 'Some text here...',
				open: false
			},
			 {
        id: 3,
				term: 'Term 3',
				details: 'Some text here...',
				open: false
			}
		]
  }
  },
  methods: {
    
  }
}
</script>

   