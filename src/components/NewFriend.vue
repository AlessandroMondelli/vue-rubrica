<template>
    <form @submit.prevent="submitData"> <!--Evito alla pagina di ricaricarsi e richiamo una funzione -->
        <div class="form-group">
            <label>Nome</label>
            <input type="text" placeholder="Nome" v-model="enteredName" />
        </div>
       <div class="form-group">
            <label>Telefono</label>
            <input type="tel" placeholder="Telefono" v-model="enteredPhone"/>
        </div>
        <div class="form-group">
            <label>Email</label>
            <input type="email" placeholder="Email" v-model="enteredEmail"/>
        </div>
        <div class="form-group">
            <button>Aggiungi Contatto</button>
        </div>
    </form>
</template>

<script>
export default {
    emits: ['add-contact'],
    data() {
        return {
            enteredName: '',
            enteredPhone: '',
            enteredEmail: '',
        }
    },
    methods: {
        submitData() {
            if( ( this.enteredName.length != 0 ) && ( this.enteredPhone.length != 0 ) && ( this.enteredEmail.length != 0 )  ) {
                this.$emit('add-contact', this.enteredName, this.enteredPhone, this.enteredEmail) //Invio dati presi dal form ad App.vue

                this.enteredName = '';
                this.enteredPhone = '';
                this.enteredEmail = '';
            } else {
                alert("All fields are required!");
            }
        }
    }
}
</script>

<style>
    .form-group {
        margin-bottom: 20px;     
    }

    .form-group label {
        margin-right: 10px;
        text-align: left;
    }
</style>
