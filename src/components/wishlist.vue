<template>
  <div class="wishlist">
    <input v-model="newItem" placeholder="Add new wish" @keyup.enter="addItem" />
    <button @click="addItem">Add</button>

    <ul>
      <li v-for="(item, index) in wishlist" :key="index">
        <div v-if="editIndex === index">
          <input v-model="editItem" @keyup.enter="saveEdit(index)" />
          <button @click="saveEdit(index)">Save</button>
          <button @click="cancelEdit">Cancel</button>
        </div>
        <div v-else>
          {{ item }}
          <button @click="startEdit(index, item)">Edit</button>
          <button @click="removeItem(index)">Remove</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: '',
      wishlist: [],
      editIndex: null,
      editItem: '',
    }
  },
  mounted() {
    const saved = localStorage.getItem('wishlist')
    if (saved) {
      this.wishlist = JSON.parse(saved)
    }
  },
  methods: {
    addItem() {
      if (this.newItem.trim()) {
        this.wishlist.push(this.newItem.trim())
        this.newItem = ''
        this.saveWishlist()
      }
    },
    removeItem(index) {
      this.wishlist.splice(index, 1)
      this.saveWishlist()
    },
    startEdit(index, value) {
      this.editIndex = index
      this.editItem = value
    },
    saveEdit(index) {
      if (this.editItem.trim()) {
        this.wishlist[index] = this.editItem.trim()
        this.editIndex = null
        this.editItem = ''
        this.saveWishlist()
      }
    },
    cancelEdit() {
      this.editIndex = null
      this.editItem = ''
    },
    saveWishlist() {
      localStorage.setItem('wishlist', JSON.stringify(this.wishlist))
    },
  },
}
</script>

<style scoped>
.wishlist {
  max-width: 500px;
  margin: auto;
}
input {
  margin: 5px;
  padding: 5px;
}
button {
  margin-left: 5px;
}
</style>
