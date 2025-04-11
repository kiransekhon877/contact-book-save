<template>
    <v-card v-if="contact" style="padding: 24px;">
        <v-card-title>{{ contact.firstName }} {{ contact.lastName }}</v-card-title>
        <v-card-title>Phone:</v-card-title>
        <v-card-subtitle style="font-size: 15px;">
            {{ contact.phone }}
        </v-card-subtitle>
        <v-card-title>Email: </v-card-title>
        <v-card-subtitle style="font-size: 15px;">
            {{ contact.email }}
        </v-card-subtitle>
        <v-btn color="red" @click="backDetail" style="margin-top: 20px;">Back</v-btn>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            contact: null
        };
    },
    created() {
        const contactId = this.$route.params.id;
        let contacts = JSON.parse(localStorage.getItem('contacts'));
        this.contact = contacts.find(contact => contact.id == contactId);
    },
    methods: {
        backDetail() {
            this.$router.push('/');
        }
    }
};
</script>
