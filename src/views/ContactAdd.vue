<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="onAddContact" />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            // Khởi tạo một đối tượng contact rỗng, không có _id để ContactForm hiểu là chế độ 'add'
            contact: {
                name: "",
                email: "",
                address: "",
                phone: "",
                favorite: false,
            },
            message: "",
        };
    },
    methods: {
        async onAddContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được thêm thành công.";
                // Quay về trang danh bạ sau khi thêm thành công (tùy chọn)
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
                this.message = "Đã xảy ra lỗi khi thêm liên hệ.";
            }
        },
    },
};
</script>