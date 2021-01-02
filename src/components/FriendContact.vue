<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(Favorito)' : ''}}</h2>
    <button @click="toggleFavorite">Inserisci/Togli preferito</button>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Dettagli</button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Telefono:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
    <button @click="$emit('delete', id)">Elimina contatto</button>
  </li>
</template>

<script>
export default {
  // props: ['name', 'phoneNumber', 'emailAddress', 'isFavorite'],
  props: { //Props con validazione
    id: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true
    },
    emailAddress: {
      type: String,
      required: true
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
    },
  },
  emits: ['toggle-favorite', 'delete'],
  // emits: { //emits con validazione
  //   'toggle-favorite': function(id) {
  //     if (id) {
  //       return true;
  //     } else {
  //       console.warn('Id is missing!');
  //       return false;
  //     }
  //   } 
  // },
  data() {
    return {
      detailsAreVisible: false
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      this.$emit('toggle-favorite', this.id);
    },
  },
};
</script>