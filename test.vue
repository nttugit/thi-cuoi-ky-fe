<template>
  <ClientOnly>
    <Vueform
      :endpoint="(x, el) => handleSubmit(x, el)"
      v-model="form"
      ref="form"
    >
      <TextareaElement name="content" label="Nội dung" :rules="['required']" />
      <TextElement name="email" label="Email" :rules="['required']" />
      <TextElement name="phone" label="Số điện thoại" :rules="['required']" />
      <ButtonElement
        name="submit"
        add-class="mt-2"
        submits
        button-label="Gửi báo cáo"
      />
    </Vueform>
  </ClientOnly>
</template>

<script>
import axios from "axios";
import { useRoute } from "vue-router";

export default {
  name: "Report",
  data() {
    return {
      form: {},
    };
  },
  mounted() {},
  methods: {
    async handleSubmit(form, el$) {
      try {
        const route = useRoute();
        const surfaceId = route.params.id;
        console.log(surfaceId);
        const formData = form;
        const submitData = {};
        formData.forEach((value, key) => {
          submitData[key] = value;
        });
        console.log("submitData:", submitData);

        // const response = await axios.post(
        //   `http://localhost:3000/reports/surface/${surfaceId}`,
        //   submitData,
        //   {
        //     headers: {
        //       "Content-Type": "application/json",
        //     },
        //   }
        // );
        // console.log(response.data);

        this.form = [];
        window.alert("Tao báo cáo thành công");
        window.location.reload();
      } catch (error) {
        console.log("error", error);
      }
    },
  },
};
</script>

<style>
.form-wrapper {
  width: 90%;
  margin: auto;
}
</style>
