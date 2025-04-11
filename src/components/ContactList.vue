<template>
    <div>
        <v-text-field v-model="searchQuery" label="Search by name" class="mb-4 my-3" clearable />
        <v-list>
            <v-list-item-group v-if="filteredContacts.length">
                <v-list-item v-for="contact in filteredContacts" :key="contact.id">
                    <v-list-item-content class="card">
                        <v-list-item-title>{{ contact.firstName }} {{ contact.lastName }}</v-list-item-title>
                        <v-list-item-actions>
                            <v-btn @click="editContact(contact.id)" small>Edit</v-btn>
                            <v-btn @click="deleteContact(contact.id)" small color="red"
                                style="margin-left: 20px;">Delete</v-btn>
                        </v-list-item-actions>
                    </v-list-item-content>
                </v-list-item>
            </v-list-item-group>

            <v-list-item v-else>
                <v-list-item-content>No contacts found</v-list-item-content>
            </v-list-item>
        </v-list>
    </div>
</template>


<script>
export default {
    data() {
        return {
            contacts: [],
            searchQuery: ''
        };
    },
    computed: {
        filteredContacts() {
            const query = this.searchQuery.toLowerCase();
            return this.contacts.filter(contact =>
                contact.firstName.toLowerCase().includes(query) ||
                contact.lastName.toLowerCase().includes(query)
            );
        }
    },
    created() {
        const storedContacts = JSON.parse(localStorage.getItem('contacts')) || [];

        storedContacts.sort((a, b) =>
            a.lastName.toLowerCase().localeCompare(b.lastName.toLowerCase())
        );

        this.contacts = storedContacts;
    },
    methods: {
        editContact(id) {
            this.$router.push(`/edit/${id}`);
        },
        deleteContact(id) {
            let contacts = JSON.parse(localStorage.getItem('contacts'));
            contacts = contacts.filter(contact => contact.id !== id);

            contacts.sort((a, b) =>
                a.lastName.toLowerCase().localeCompare(b.lastName.toLowerCase())
            );

            localStorage.setItem('contacts', JSON.stringify(contacts));
            this.contacts = contacts;
        }
    }
};
</script>