<template>
  <v-form v-model="valid" ref="form" lazy-validation>
    <v-text-field v-model="contact.firstName" label="First Name" :rules="[rules.required]" required></v-text-field>

    <v-text-field v-model="contact.lastName" label="Last Name" :rules="[rules.required]" required></v-text-field>

    <v-text-field v-model="contact.phone" label="Phone" :rules="[rules.required, rules.phone]" required></v-text-field>

    <v-text-field v-model="contact.email" label="Email" :rules="[rules.required, rules.email]" required></v-text-field>

    <v-btn :disabled="!valid" color="primary" @click="submitForm">Save</v-btn>

    <v-btn color="red" @click="cancelEdit" style="margin-left: 20px;">Cancel</v-btn>
  </v-form>
</template>

<script>
export default {
  props: ['contactId'],
  data() {
    return {
      valid: true,
      contact: {
        firstName: '',
        lastName: '',
        phone: '',
        email: ''
      },
      rules: {
        required: value => !!value || 'This field is required',
        email: value =>
          /.+@.+\..+/.test(value) || 'E-mail must be valid',
        phone: value =>
          /^[0-9]{10}$/.test(value) || 'Phone must be 10 digits'
      }
    };
  },
  methods: {
    submitForm() {
      if (this.$refs.form.validate()) {
        this.saveContact();
      }
    },
    saveContact() {
      if (this.contactId) {
        this.updateContact();
      } else {
        this.addContact();
      }
    },
    addContact() {
      const id = new Date().getTime();
      let contacts = JSON.parse(localStorage.getItem('contacts')) || [];
      contacts.push({ ...this.contact, id });
      localStorage.setItem('contacts', JSON.stringify(contacts));
      this.$router.push(`/details/${id}`);
    },
    updateContact() {
      let contacts = JSON.parse(localStorage.getItem('contacts')) || [];
      let contactIndex = contacts.findIndex(contact => contact.id === Number(this.contactId));
      if (contactIndex !== -1) {
        contacts[contactIndex] = { ...this.contact, id: Number(this.contactId) };
        localStorage.setItem('contacts', JSON.stringify(contacts));
        this.$router.push(`/details/${this.contactId}`);
      }
    },

    cancelEdit() {
      this.$router.push('/');
    }
  },
  created() {
    if (this.contactId) {
      const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
      const contact = contacts.find(contact => contact.id === Number(this.contactId));
      if (contact) {
        this.contact = { ...contact };
      }
    }
  },
};
</script>
