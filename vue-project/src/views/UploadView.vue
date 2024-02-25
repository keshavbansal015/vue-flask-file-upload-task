<template>
  <div>
    <h2>Upload Word Document</h2>
    <form @submit.prevent="handleUpload">
      <label for="file">Select file:</label>
      <input type="file" id="file" ref="fileInput" accept=".doc,.docx" />
      <button type="submit">Upload</button>
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    handleUpload() {
      const file = this.$refs.fileInput.files[0];

      // Prepare a FormData object for the upload
      const formData = new FormData();
      formData.append("file", file);
      formData.append("TESTS", "this is a string");

      // Log FormData contents to the console
      formData.forEach((value, key) => {
        console.log(`${key}: ${value}`);
      });

      // Send the post request to your server-side endpoint (adjust the URL)
      fetch("http://127.0.0.1:5000/api/upload", {
        method: "POST",
        body: formData,
      })
        .then((response) => response.json())
        .then((data) => {
          // Handle successful upload response from server
          console.log("File uploaded successfully:", data);
        }).then(() => {
          window.alert("File uploaded successfully!")
        })
        .catch((error) => {
          console.error("Error uploading file:", error);
        });
    },
  },
};
</script>
