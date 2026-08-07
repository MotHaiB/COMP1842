<template>
  <div>
    <h1>Edit Word</h1>
    <word-form @createOrUpdate="createOrUpdate" :word="word"></word-form>
  </div>
</template>

<script>
import WordForm from '../components/WordForm.vue';
import { api } from '../helpers/helpers';

export default {
  name: 'edit',
  components: {
    'word-form': WordForm
  },
  data() {
    return {
      word: {}
    };
  },
  async mounted() {
    const res = await api.getWord(this.$route.params.id);
    if (res) {
      this.word = res;
    }
  },
  methods: { 
    createOrUpdate: async function(word) {
    await api.updateWord(word);
    this.flash('Word updated successfully!', 'success');
    this.$router.push(`/words/${word._id}`);
    
    }
  }
};
</script>