# monaco-editor-forvue

> Monaco Editor Vue Component

> Based on [vue-monaco-editor](https://github.com/matt-oconnell/vue-monaco-editor)


## Setup

``` bash
npm install monaco-editor-forvue --save
```

## Simple Vue Use

```js
import Monaco from 'monaco-editor-forvue';

// use in component
export default {
  components: {
    Monaco
  }
}
```

## Component Props

| Option        | Type          | Default | Description
|:-------------|:-------------|:-------|:-------|
| language      | String        | `javascript` | |
| height        | Number/String | `100%` ||
| width | Number/String | `100%` ||
| code | String | `// code \n` | Initial code to show |
| theme | String | `vs-dark` | vs, hc-black, or vs-dark |
| changeThrottle | Number(ms) | `0` |  throttle `codeChange` emit |
|srcPath| String | `""` | see *Webpack Use* below
| options | Object | Merged with defaults below | See [Monaco Editor Options](https://microsoft.github.io/monaco-editor/api/interfaces/monaco.editor.ieditorconstructionoptions.html) |

## Component Events

*These events are available to parent component*

| Event        | Returns          | Description
|:-------------|:-------------|:-------|
|mounted|`editor`[editor instance]|Emitted when editor has mounted|
|codeChange|`editor`[editor instance]|Emitted when code has changed|

## Example

*Component Implementation*
```vue
<Monaco
    width="600"
    height="600"
    language="javascript"
    theme="vs"
    :code="code"
    :options="options"
    :changeThrottle="500"
    @mounted="onMounted"
    @codeChange="onCodeChange"
    >
</Monaco>
```

```js
export default {
  components: {
    Monaco
  },
  data() {
    return {
      code: '// Type away! \n'
    };
  },
  methods: {
    onMounted(editor) {
      this.editor = editor;
    },
    onCodeChange(editor) {
      console.log(this.editor.getValue());
    }
  }
}
```

```editor's common methods
set value:
this.editor.setValue(yourstring);

rerender editor:
this.editor.layout({
    width: 800,
    height: 800
});
