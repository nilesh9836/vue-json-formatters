<template>
  <v-container class="pa-0 ma-0" fluid>
   <v-row no-gutters>
     <v-col cols="5">
       <v-card>
         <codemirror
          class="code-mirror"
          autofocus
          :options="codeMirrorOption"
          v-model="modelValue"
        ></codemirror>
       </v-card>
     </v-col>
     <v-col class="px-4">
       <v-card class="btn-card pa-4">
        <v-row justify="center" no-gutters>
        <v-btn @click="getFormattedJson(modelValue)" outlined color="primary"  >Format</v-btn>
       </v-row>
       <v-row justify="center" no-gutters class="pa-9">
         <v-select
          hide-details
          dense
          label="Tab Space"
          :items="items"
          outlined
          v-model="tabValue"
        ></v-select>
       </v-row>
       </v-card>
     </v-col>
     <v-col cols="5">
       <v-card>
       <codemirror
          ref="codeMirrorFormated"
          :key="compKey"
          class="code-mirror"
          autofocus
          :options="codeMirrorOption"
          :value="data"
        ></codemirror>
       </v-card>
     </v-col>
   </v-row>
  </v-container>
</template>

<script>
import { codemirror } from "vue-codemirror";
import "codemirror/mode/javascript/javascript.js";
import "codemirror/addon/display/fullscreen.js";
import "codemirror/theme/solarized.css";
import "codemirror/addon/fold/foldgutter.css";
import "codemirror/addon/fold/brace-fold.js";
import "codemirror/lib/codemirror.css";
import "codemirror/addon/fold/foldcode.js";
import "codemirror/addon/fold/foldgutter.js";
import "codemirror/addon/fold/indent-fold.js";
// import "codemirror/addon/fold/markdown-fold.js";
// import "codemirror/addon/fold/xml-fold.js";
// import "codemirror/addon/fold/comment-fold.js";

export default {
  name: "JsonFormatter",
  components: {
    codemirror,
  },
  methods: {
    getFormattedJson(val) {
      try{
      this.data = JSON.stringify(JSON.parse(val), null, this.tabValue);
      }
      catch(err)
      {
        this.data = err.message;
      }
    },
    changeInput() {
      this.data = JSON.parse(this.modelValue);
      this.compkey++;
    },
    copy() {
      console.log('copy');
      this.$refs.codeMirrorFormated.text.select();
      document.execCommand("copy");
    },
    toggle() {
      this.fullscreen = !this.fullscreen
    }
  },
  watch: {
   modelValue: function() {

   }
  },
  computed: {
    getModelValue() {
      return null;
    }
  },
  data() {
    return {
      fullscreen: false,
      compkey: 0,
      tabValue: 2,
      items: [2,3,4],
      modelValue: "",
      codeMirrorOption: {
        mode: "application/ld+json",
        lineWrapping: true,
        readOnly: false,
        lineNumbers: true,
        autoRefresh: true,
        line: true,
        gutters: ["CodeMirror-linenumbers", "CodeMirror-foldgutter"],
        foldGutter: true,
        enableCodeFolding: true,
        autoCloseBrackets: true,
        matchBrackets: true,
        lint: true,
        fullScreen: false,
      },
    };
  },
  props: {
    /**
     * JSON Data required
     */
    data: {
      type: ()=>{},
      default: {},

    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.code-mirror {
  text-align: left;
}
/deep/ .CodeMirror {
  height: 90vh;
}
.btn-card {
  height: 90vh;
  background-color: black;
}
</style>
