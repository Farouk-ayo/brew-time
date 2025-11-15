<template>
  <div class="contact-page">
    <div class="container">
      <h1 class="page-title">Get In Touch</h1>

      <div class="contact-content">
        <div class="contact-info">
          <h2>Visit Us</h2>
          <p>123 Coffee Street</p>
          <p>Brew City, BC 12345</p>
          <p>Phone: (555) 123-4567</p>
          <p>Email: hello@brewtime.com</p>
        </div>

        <div class="contact-form">
          <h2>Send a Message</h2>
          <form @submit.prevent="handleSubmit">
            <div class="form-group">
              <input type="text" placeholder="Your Name" v-model="formData.name" required />
            </div>

            <div class="form-group">
              <input type="email" placeholder="Your Email" v-model="formData.email" required />
            </div>

            <div class="form-group">
              <textarea
                placeholder="Your Message"
                v-model="formData.message"
                rows="5"
                required
              ></textarea>
            </div>

            <button type="submit" class="submit-btn">Send Message</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive } from 'vue'

const formData = reactive({
  name: '',
  email: '',
  message: '',
})

const handleSubmit = () => {
  console.log('Form submitted:', formData)
  alert('Message sent! (This is a demo)')
  // Reset form
  formData.name = ''
  formData.email = ''
  formData.message = ''
}
</script>
