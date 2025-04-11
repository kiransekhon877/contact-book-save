<template>
    <div>
        <v-btn color="secondary" @click="$router.push('/add')" style="width: 100%;">Add New Contact</v-btn>
        <ContactList />
    </div>
</template>

<script>
import ContactList from '@/components/ContactList.vue';

export default {
    components: {
        ContactList
    }
};
</script>
