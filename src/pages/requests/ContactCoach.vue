<template>
  <form @submit.prevent="submitForm">
    <div>
      <label for="email">Email</label>
      <input type="email" id="email" v-model.trim="email" />
    </div>
    <div>
      <label for="message">Message</label>
      <textarea
        name="message"
        id="message"
        rows="5"
        v-model.trim="message"
      ></textarea>
    </div>
    <p class="errors" v-if="!formIsValid">Your email or message should not be blank.</p>
    <div class="actions">
      <base-button>Send Message</base-button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      message: '',
      formIsValid: true,
    };
  },
  methods: {
    submitForm() {
      this.formIsValid = true;
      if (
        this.email === '' ||
        !this.email.includes('@') ||
        this.message === ''
      ) {
        this.formIsValid = false;
        return;
      }
      this.$store.dispatch('requests/contactCoach', {
          email: this.email,
          message: this.message,
          coachId: this.$route.id
      })
      this.$router.replace('/coaches');
    },
  },
};
</script>

<style scoped src="../../styles/contact-coach.css"></style>
