<template>  
    <div>
        <button
        class="del_btn"
        @click="$emit('delete-doc', doc.id)"><img src="/delete.png">
        </button>
    </div>
    </template>
    
    <script>
    export default {
        props: {
        doc: {
            type: Object,
            required: true     
        },
        
    },
        
    }
    </script>
    
    <style scoped>
   
    .del_btn:hover{
       opacity: 0.5;  
    }
   
    </style>