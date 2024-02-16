<template>
    <div class="simple-modal">
      <div class="simple-modal-backdrop"  >
        <div class="simple-modal-container">
          <div class="simple-modal-content"  @click.stop>
            <header class="simple-modal-header">
              Modal title
            </header>
            <section class="simple-modal-body">
              <form>
                <input class="input" 
                type="text" 
                placeholder="Введите документ"
                v-model="inputValue"
                >
              </form>
              
            </section>
            <footer class="simple-modal-footer">
              <button class="btn" type="button" @click="addDoc"> Add </button>
              <button class="btn" type="button" @click="closeModal">Close</button>
            </footer>
          </div>
        </div>
      </div>
    </div>
  </template>

<script>
export default {
  name: 'modalWindow2',
  data(){
    return {
        inputValue: '',
    }
  },
  props: {
   
  },
  methods: {
    closeModal() {
      this.$emit('close');
    },
   
    addDoc() {
        if (this.inputValue.trim()){
            this.$emit('addDoc', {
                id: Date.now(),
                name: this.inputValue,
                type: "Document", 
            })
        }
        this.inputValue=''
    },
  },
};
</script>
  
  <style scoped>
    
    .simple-modal-backdrop {
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.8);
        transition: opacity 0.3s ease;
        z-index: 9999;
      }
  
      .simple-modal-container {
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        width: auto;
        margin: 16px;
      }
  
      .simple-modal-content {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        width: 100%;
        max-width: 500px;
        margin: 1.75rem auto;
        padding: 20px 30px;
        border-radius: 5px;
        color: #000;
        background-color: #fff;
        transform: translate(0, 0);
        transition: all 0.3s ease;
        box-sizing: border-box;
      }
  
      .simple-modal-header {
        padding-bottom: 16px;
        font-size: 25px;
        text-align: center;
      }
  
      .simple-modal-footer {
        display: flex;
        flex-direction: row;
        justify-content: start;
        align-items: center;
        height: 80px;
        text-align: center;
      }
    
  </style>