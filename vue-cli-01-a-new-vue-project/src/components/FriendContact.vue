<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(favorite)' : ''}}</h2>
    <button @click="toggleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
    <button @click="toggleFavorite">{{ isFavorite ? 'Undo' : 'Make' }} Favorite</button>

    <ul v-if="detailsAreVisible">
      <li><strong>Phone:</strong> {{ phoneNumber }}</li>
      <li><strong>Email:</strong> {{ emailAddress }}</li>
    </ul>
    <button @click="$emit('delete', this.id)">Delete Contact</button>
  </li>
</template>

<script>
export default {
  name: "FriendContact",
  props: {
    'id': {
      type: String,
      required: true,
    },
    'name': {
      type: String,
      required: true,
    },
    'phoneNumber': {
      type: String,
      required: true,
    },
    'emailAddress': {
      type: String,
      required: true,
    },
    'isFavorite': {
      type: Boolean,
      required: false,
      default: false,
      /*validator: function (value) {
        return value === '1' || value === '0';
      }*/
    },
  },
  //emits: ['toggle-favorite'],
  emits: {
    'toggle-favorite': function(id) {
      if (id) {
        return true
      } else {
        console.warn('Id is missing!')
        return false
      }

    },
    'delete': function(id){
      if (id) {
        return true
      } else {
        console.warn('Id is missing!')
        return false
      }
    },
  },
  /*
  Valid is constructor or prop types:
    String
    Number
    Boolean
    Array
    Object
    Date
    Function
    Symbol
  * */
  data(){
    return{
      detailsAreVisible: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible
    },
    toggleFavorite() {
      //this.friendIsFavorite = !this.friendIsFavorite
      this.$emit('toggle-favorite', this.id)
    },

  }
}

</script>

<style scoped>
  button {
    margin-left: 5px;
  }
</style>