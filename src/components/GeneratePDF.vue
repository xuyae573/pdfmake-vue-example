<template>
  <div>
    <button  @click="generatePdf"> Generate PDF </button>
  </div>
</template>

<script>
export default {
  name:'MyComponent',
  data() {
    return {
      pdfMake: null,
    };
  },
  methods: {
    async loadPdfMaker() {
      if (!this.pdfMake) {
        const pdfMakeModule = await import("pdfmake/build/pdfmake");
        const pdfFontsModule = await import("pdfmake/build/vfs_fonts");
        this.pdfMake = pdfMakeModule.default;
        this.pdfMake.vfs = pdfFontsModule.default.pdfMake.vfs;
      }
    },
    async generatePdf() {
      await this.loadPdfMaker();
      const def = {
        content: "A sample PDF document generated using Vuejs and PDFMake",
      };
      this.pdfMake.createPdf(def).open();
    },
  },
};
</script>

 <style scoped>
 button {
    border-radius: 2px;
    width: 140px;
    background-color:rgb(115, 103, 240);
    height: 30px;
    z-index: 0;
    cursor: pointer;
    border: 0px;
    color: aliceblue;
}
 
 </style>
