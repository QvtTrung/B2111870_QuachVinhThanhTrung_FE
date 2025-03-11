<template>
  <div class="page">
    <h4>Thêm mới Liên hệ</h4>
    <ContactForm
      :contact="{
        name: '',
        email: '',
        address: '',
        phone: '',
        favorite: false,
      }"
      @submit:contact="createContact"
    />
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
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      try {
        await ContactService.create(data); // Gọi API để tạo contact mới
        this.message = "Liên hệ được tạo thành công.";
        this.$router.push({ name: "contactbook" }); // Quay lại trang danh bạ sau khi thêm
      } catch (error) {
        console.log(error);
        this.message = "Có lỗi xảy ra khi tạo liên hệ.";
      }
    },
  },
};
</script>

<style scoped>
.page {
  text-align: left;
  max-width: 750px;
}
</style>
