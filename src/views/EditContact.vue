<template>
    <div>
        <h1>Edit Contact</h1>
        <ContactForm :contactId="$route.params.id" />
    </div>
</template>

<script>
import ContactForm from '@/components/ContactForm.vue';

export default {
    components: {
        ContactForm
    }
};
</script>
