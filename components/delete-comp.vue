<template>  
    <div>
        <button
        @click="$emit('remove-doc', doc.id)"><img src="/delete.png">
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
   
    </style>