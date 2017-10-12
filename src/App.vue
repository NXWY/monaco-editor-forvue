<template>
  <div>
    <!-- Load from webpack (note the srcPath="dist" prop) -->
    <Monaco
        :width="width"
        :height="height"
        language="typescript"
        theme="vs-dark"
        srcPath="dist"
        :code="code"
        :changeThrottle="500"
        @mounted="onMounted"
        @codeChange="onCodeChange"
        >
    </Monaco>

    <button @click="clickHandler">Log value</button>
    <button @click="adjustEditorSize">调整窗口</button>

  </div>
</template>

<script>
const Monaco = require('./Monaco.vue')

export default {
    components: {
        Monaco
    },

    data() {
        return {
            code: '// type your code \n',
            width: '100%',
            height: '500'
        }
    },

    methods: {

        onMounted(editor) {
            console.log('after mount!', editor, editor.getValue(), editor.getModel());
            this.editor = editor;
        },

        onCodeChange(editor) {
            console.log('code changed!', 'code:' + this.editor.getValue());
        },

        clickHandler() {
            console.log('here is the code:', this.editor.getValue());
        },

        adjustEditorSize() {
            this.width = '600';
            this.height = '700';
        }
    }

}
</script>

<style media="screen">

</style>
