<template>
  <div>
      <label for="title">Photo Title:</label><br>
      <input type="text" name="title" id="title" />
      <br><br>
      <label for="image">Upload Photos</label><br>
      <input type="file" name="image" id="image" accept="*/images" />
      <br><br>
      <button v-on:click="this.uploadForm">UploadPhoto</button>
  </div>
</template>

<script>
export default {
    name: 'image-uploader',
    props: ['api'],
    methods: {
        uploadForm: function () {
            const title = document.getElementById("title").value;
            const image = document.getElementById("image").files[0];

            let payload = new FormData();
            payload.append("title",title);
            payload.append("image",image);

        /*     let headers = new Headers();
            headers.append("Content-Type","multipart/form-data"); */


            fetch(this.api.upload, {
                method: "POST",
                body: payload
            }).then(response => {
                return response.json();
            }).then(data => {
                this.$emit("imageUploaded",data);
            });

        }
    }
}
</script>

<style>

</style>