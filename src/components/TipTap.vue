<template>
  <div>
      <editor-content :editor="editor" placeholder="content here"/>
  </div>
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-2'
import StarterKit from '@tiptap/starter-kit'
// import Placeholder from '@tiptap/extension-placeholder'

export default {
  components: {
    EditorContent,
  },

  data() {
    return {
      editor: null,
    }
  },

  mounted() {
    this.editor = new Editor({
      extensions: [
          StarterKit,
        // Placeholder.configure({
        //   // Use a placeholder:
        //   placeholder: 'Write something …',
        //   // },
        // }),
      ],
      content: '',

      // extensions: [StarterKit],
      onUpdate: () => {
        // HTML
        this.$emit('tipTap', this.editor.getHTML())

        // JSON
        // this.$emit('input', this.editor.getJSON())
      },
    })
  },

  beforeDestroy() {
    this.editor.destroy()
  },
}
</script>
