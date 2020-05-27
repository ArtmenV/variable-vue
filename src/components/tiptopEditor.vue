<template>
  <div class="editor">
    <h2>This is how it works</h2>
    <editor-content class="editor__content" :editor="editor" />
      <!-- <button
        class="menubar__button"
        @click="inputRules"
      >
    <icon name="suggestion" />
  </button> -->
  </div>
</template>

<script>
import Icon from './icon'
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import {
  Blockquote,
  CodeBlock,
  HardBreak,
  Heading,
  HorizontalRule,
  OrderedList,
  BulletList,
  ListItem,
  TodoItem,
  TodoList,
  Bold,
  Code,
  Italic,
  Link,
  Strike,
  Underline,
  History,
} from 'tiptap-extensions'
export default {
  components: {
    EditorContent,
    EditorMenuBar,
    Icon,
  },
  data() {
    return {
      editor: new Editor({      
        onUpdate: ({ getHTML }) => {
        const newPost = getHTML()
        //look for the letter i and change it
        if (newPost.match(/\s\i\s/g)) {
          const data = newPost.replace(/\s\i\s/g, ' I ')
          this.editor.setContent(data, true, { preserveWhitespace: true })
        }
        //look in each paragraph for the first letter not capitalized and change it
        if (newPost.match(/<p>[a-z]/g)) {
          const dataParse = newPost.split(/<p>(.*?)<\/p>/g)
          const strTrim = dataParse.filter(el => el.length)
          const strChange = strTrim.map(el => '<p>' + el.charAt(0).toUpperCase() + el.slice(1) + '</p>')
          const result = strChange.join(' ')
          this.editor.setContent(result, true, { preserveWhitespace: true })
        }
      },
        extensions: [
          new Blockquote(),
          new BulletList(),
          new CodeBlock(),
          new HardBreak(),
          new Heading({ levels: [1, 2, 3] }),
          new HorizontalRule(),
          new ListItem(),
          new OrderedList(),
          new TodoItem(),
          new TodoList(),
          new Link(),
          new Bold(),
          new Code(),
          new Italic(),
          new Strike(),
          new Underline(),
          new History(),
        ],
        content: ``,
      }),
    }
  },

  methods: {
    // triggerSuggestion () {
    //   const { view } = this.editor
    //   // inserts char programmatically
    //   debugger
    //   insertText(view.state[0].toUpperCase() + view.state[0].slice(1))(view.state, view.dispatch, view)
    //   // give focus back to editor
    //   this.editor.focus()
    // }, 

  //   getSchemaInput() {

  //   },
  //   inputRules({ type }) {
  //   return [
  //     new inputRule(/<p>[a-z](.*?)\s/gi, (state, match, start, end) => 
  //       insert(state[0].toUpperCase() + start[1], type.create()),
  //     ),
  //   ];
  // }

  },
  beforeDestroy() {
    this.editor.destroy()
  },
}
</script>

<style>
.ProseMirror {
  border: 1px solid silver;
  margin: 0 auto;
  max-width: 860px;
}
</style>