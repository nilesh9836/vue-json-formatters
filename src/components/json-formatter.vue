<template>
  <div class="pt-4" style="min-width:1000px;max-width:1000px:min-height:500px" :key="compkey">

      <v-card class="mb-4">
        <codemirror
          class="code-mirror"
          autofocus
          :value="getFormattedJson(data)"
          :options="codeMirrorOption"
          v-model="modelValue"
          @input="changeInput()"
        ></codemirror>
      </v-card>
    <v-row>
  </v-row>
  </div>

</template>

<script>
import { codemirror } from "vue-codemirror";
import "codemirror/mode/javascript/javascript.js";
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
      this.modelValue = JSON.stringify(val, null, 2);
      //this.compkey++;
    },
    changeInput() {
      this.data = JSON.parse(this.modelValue);
      this.compkey++;
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
      compkey: 0,
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
  height: 75vh;
}
</style>
