<script setup>
import Preview from './components/Preview.vue';
import { ref } from 'vue';

const descPlaceholder =
  " Describe your discount, this will be shown as a badge (eg '25% off' or 'free shipping')";
const imagePlaceholder = '538x138, 3.9 aspect ratio, no WEBP or GIF';

let data = ref({
  subject: '',
  description: '',
  discCode: '',
  logo: 'https://picsum.photos/100',
  image: 'https://picsum.photos/600/200',
  startDate: null,
  endDate: null,
  timezone: '+1000',
});
let scriptTag = ref(`
[{
  "@context": "http://schema.org/",
  "@type": "Organization",

  // WARNING: Before sending email, either point the logo
  // at your own image or delete the logo annotation.
  //
  // If showing a logo, we recommend using an https URL.
  // It's not a requirement today, but may be in the future.
  "logo": "${data.logo}"
},{
  "@context": "http://schema.org/",
  "@type": "EmailMessage",

  // Use this optional alternative subject line to avoid duplicate text
  // between the subject, deal badge, and discount code.
  "subjectLine": "[Important] Please add subject line in annotation"
},{
  "@context": "http://schema.org/",
  "@type": "DiscountOffer",

  // Describe your discount, this will be shown as a badge (eg "25% off" or "free shipping")
  "description": "${data.description}",

  "discountCode": "${data.discCode}",
  "availabilityStarts": "${data.startDate}",
  "availabilityEnds": "${data.endDate}"
},{
  // Promotion card with single image.
  // We recommend using an https URL.  It's not a requirement today, but may be in the future.
  // Any image size will work and will just be cropped automatically.
  // GIF & WEBP images are not supported and will be filtered out.
  // Sample image is 538x138, 3.9 aspect ratio
  "@context": "http://schema.org/",
  "@type": "PromotionCard",
  "image": "${data.image}"
}]
`);
</script>
<template>
  <h1>Google Promotions Schema Editor</h1>
  <main>
    <section class="schema-editor">
      <h2>Edit</h2>
      <div class="inputs">
        <div class="input-wrapper">
          <label for="">Subject</label>
          <input type="text" v-model="data.subject" />
        </div>
        <div class="input-wrapper">
          <label for="">Description</label>
          <input
            type="text"
            :placeholder="descPlaceholder"
            v-model="data.description"
          />
        </div>
        <div class="input-wrapper">
          <label for="">Discount Code</label>
          <input type="text" v-model="data.discCode" />
        </div>
        <div class="input-wrapper">
          <label for="">Logo URL</label>
          <input type="text" v-model="data.logo" />
        </div>
        <div class="input-wrapper">
          <label for="">Image URL</label>
          <input
            type="text"
            v-model="data.image"
            :placeholder="imagePlaceholder"
          />
        </div>
        <div class="input-wrapper date">
          <label for="">Start Date, Time</label>
          <input type="datetime-local" v-model="data.startDate" />
        </div>
        <div class="input-wrapper date">
          <label for="">End Date, Time</label>
          <input type="datetime-local" v-model="data.endDate" />
        </div>
      </div>
      <div class="output">
        <p>{{ data.startDate }}{{ data.timezone }}</p>
        <p>2022-11-22T20:18:37-08:00</p>
        <hr />
        <p>{{ data.endDate }}{{ data.timezone }}</p>
        <p>2022-11-25T20:18:37-08:00</p>
      </div>
    </section>
    <section>
      <article>
        <h2>Preview</h2>
        <Preview :data="data" />
      </article>
      <div class="copy-section">
        <h2>Copy</h2>
        <textarea
          v-model="scriptTag"
          name=""
          id=""
          cols="30"
          rows="10"
        ></textarea>
      </div>
    </section>
  </main>
  <div>
    {{ scriptTag }}
  </div>
</template>
<style scoped>
main * {
  box-sizing: border-box;
}
main {
  display: flex;
  min-height: 70vh;
}
section {
  box-sizing: border-box;
  width: 50%;
  height: 100%;
  margin: 0.2rem;
  padding: 1rem;
}
section > article {
  width: 100%;
  box-sizing: border-box;
  background: lightblue;
  margin-bottom: 0.4rem;
  padding: 1rem;
  border-radius: 10px;
}
section > .copy-section {
  width: 100%;
  box-sizing: border-box;
  background: lightblue;
  padding: 1rem;
  border-radius: 10px;
}
.schema-editor {
  box-sizing: border-box;
  width: 50%;
  background: lightblue;
  margin: 0.2rem;
  padding: 1rem;
  border-radius: 10px;
}
section .input-wrapper {
  border: 1px solid gray;
  background: lightgray;
  border-radius: 8px;
  padding: 0.4rem;
  margin-top: 0.1rem;
}
section .input-wrapper .date {
  width: 50%;
}
section input {
  min-width: 100%;
  height: 100%;
  border: none;
  border-radius: 4px;
  padding: 0.5rem 0.5rem;
}
section textarea {
  width: 100%;
  padding: 0.5rem 0.5rem;
  border-radius: 8px;
}
</style>

<!--     <script type="application/ld+json">
[{
  "@context": "http://schema.org/",
  "@type": "Organization",

  // WARNING: Before sending email, either point the logo
  // at your own image or delete the logo annotation.
  //
  // If showing a logo, we recommend using an https URL.
  // It's not a requirement today, but may be in the future.
  "logo": "https://www.gstatic.com/images/branding/product/1x/googleg_48dp.png"
},{
  "@context": "http://schema.org/",
  "@type": "EmailMessage",

  // Use this optional alternative subject line to avoid duplicate text
  // between the subject, deal badge, and discount code.
  "subjectLine": "[Important] Please add subject line in annotation"
},{
  "@context": "http://schema.org/",
  "@type": "DiscountOffer",

  // Describe your discount, this will be shown as a badge (eg "25% off" or "free shipping")
  "description": "20% off",

  "discountCode": "PROMO",
  "availabilityStarts": "2022-11-22T20:18:37-08:00",
  "availabilityEnds": "2022-11-25T20:18:37-08:00"
},{
  // Promotion card with single image.
  // We recommend using an https URL.  It's not a requirement today, but may be in the future.
  // Any image size will work and will just be cropped automatically.
  // GIF & WEBP images are not supported and will be filtered out.
  // Sample image is 538x138, 3.9 aspect ratio
  "@context": "http://schema.org/",
  "@type": "PromotionCard",
  "image": "https://www.google.com/gmail-for-marketers/promo-tab/markup-tool/sample.png"
}]
    </script> -->
