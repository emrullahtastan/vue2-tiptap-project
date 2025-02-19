<template>
  <div v-if="editor" class="container">
    <div class="control-group">
      <div class="button-group">
        <button @click="editor.chain().focus().toggleBold().run()" :disabled="!editor.can().chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }">
          Bold
        </button>
        <button @click="editor.chain().focus().toggleItalic().run()" :disabled="!editor.can().chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }">
          Italic
        </button>
        <button @click="editor.chain().focus().toggleStrike().run()" :disabled="!editor.can().chain().focus().toggleStrike().run()" :class="{ 'is-active': editor.isActive('strike') }">
          Strike
        </button>
        <button @click="editor.chain().focus().toggleCode().run()" :disabled="!editor.can().chain().focus().toggleCode().run()" :class="{ 'is-active': editor.isActive('code') }">
          Code
        </button>
        <button @click="editor.chain().focus().unsetAllMarks().run()">
          Clear marks
        </button>
        <button @click="editor.chain().focus().clearNodes().run()">
          Clear nodes
        </button>
        <button @click="editor.chain().focus().setParagraph().run()" :class="{ 'is-active': editor.isActive('paragraph') }">
          Paragraph
        </button>
        <button @click="editor.chain().focus().toggleHeading({ level: 1 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }">
          H1
        </button>
        <button @click="editor.chain().focus().toggleHeading({ level: 2 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 2 }) }">
          H2
        </button>
        <button @click="editor.chain().focus().toggleHeading({ level: 3 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 3 }) }">
          H3
        </button>
        <button @click="editor.chain().focus().toggleHeading({ level: 4 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 4 }) }">
          H4
        </button>
        <button @click="editor.chain().focus().toggleHeading({ level: 5 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 5 }) }">
          H5
        </button>
        <button @click="editor.chain().focus().toggleHeading({ level: 6 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 6 }) }">
          H6
        </button>
        <button @click="editor.chain().focus().toggleBulletList().run()" :class="{ 'is-active': editor.isActive('bulletList') }">
          Bullet list
        </button>
        <button @click="editor.chain().focus().toggleOrderedList().run()" :class="{ 'is-active': editor.isActive('orderedList') }">
          Ordered list
        </button>
        <button @click="editor.chain().focus().toggleCodeBlock().run()" :class="{ 'is-active': editor.isActive('codeBlock') }">
          Code block
        </button>
        <button @click="editor.chain().focus().toggleBlockquote().run()" :class="{ 'is-active': editor.isActive('blockquote') }">
          Blockquote
        </button>
        <button @click="editor.chain().focus().setHorizontalRule().run()">
          Horizontal rule
        </button>
        <button @click="editor.chain().focus().setHardBreak().run()">
          Hard break
        </button>
        <button @click="editor.chain().focus().undo().run()" :disabled="!editor.can().chain().focus().undo().run()">
          Undo
        </button>
        <button @click="editor.chain().focus().redo().run()" :disabled="!editor.can().chain().focus().redo().run()">
          Redo
        </button>
        <button @click="editor.chain().focus().setColor('#958DF1').run()" :class="{ 'is-active': editor.isActive('textStyle', { color: '#958DF1' }) }">
          Purple
        </button>
      </div>
    </div>
    <editor-content :editor="editor" class="tiptap" />
  </div>
</template>

<script>
import { Color } from '@tiptap/extension-color'
import ListItem from '@tiptap/extension-list-item'
import TextStyle from '@tiptap/extension-text-style'
import StarterKit from '@tiptap/starter-kit'
import { Editor, EditorContent } from "@tiptap/vue-2";

export default {
  name:'TiptapComponent',
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
        Color.configure({ types: [TextStyle.name, ListItem.name] }),
        TextStyle.configure({ types: [ListItem.name] }),
        StarterKit,
      ],
      content: `
        <h2>
          Hi there,
        </h2>
        <p>
          this is a <em>basic</em> example of <strong>Tiptap</strong>. Sure, there are all kind of basic text styles you’d probably expect from a text editor. But wait until you see the lists:
        </p>
        <ul>
          <li>
            That’s a bullet list with one …
          </li>
          <li>
            … or two list items.
          </li>
        </ul>
        <p>
          Isn’t that great? And all of that is editable. But wait, there’s more. Let’s try a code block:
        </p>
        <pre><code class="language-css">body {
  display: none;
}</code></pre>
        <p>
          I know, I know, this is impressive. It’s only the tip of the iceberg though. Give it a try and click a little bit around. Don’t forget to check the other examples too.
        </p>
        <blockquote>
          Wow, that’s amazing. Good work, boy! 👏
          <br />
          — Mom
        </blockquote>
      `,
    })
  },

  beforeUnmount() {
    this.editor.destroy()
  },
}
</script>

<style lang="scss">
/* Container ve Düğme Stilleri */
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.control-group {
  margin-bottom: 20px;
}

.button-group {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 16px;
}

.button-group button {
  background-color: #f3f4f6;
  border: 1px solid #d1d5db;
  border-radius: 4px;
  padding: 8px 12px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.2s, border-color 0.2s;
}

.button-group button:hover {
  background-color: #e5e7eb;
  border-color: #9ca3af;
}

.button-group button.is-active {
  background-color: #3b82f6;
  color: white;
  border-color: #3b82f6;
}

.button-group button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

/* Editör Alanı Stilleri */
.tiptap {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  padding: 16px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  background-color: white;
  min-height: 300px;
  outline: none;
  text-align: left;
}

/* Başlık Stilleri */
.tiptap h1 {
  font-size: 24px;
  font-weight: 600;
  margin: 24px 0 16px;
}

.tiptap h2 {
  font-size: 20px;
  font-weight: 600;
  margin: 20px 0 12px;
}

.tiptap h3 {
  font-size: 18px;
  font-weight: 600;
  margin: 16px 0 8px;
}

/* Paragraf Stilleri */
.tiptap p {
  font-size: 16px;
  line-height: 1.6;
  margin: 12px 0;
}

/* Liste Stilleri */
.tiptap ul,
.tiptap ol {
  padding-left: 24px;
  margin: 12px 0;
}

.tiptap li {
  margin: 4px 0;
}

/* Kod Blokları */
.tiptap pre {
  background-color: #1e293b;
  color: #f8fafc;
  padding: 12px;
  border-radius: 4px;
  margin: 12px 0;
  overflow-x: auto;
}

.tiptap code {
  background-color: #e2e8f0;
  color: #1e293b;
  padding: 2px 4px;
  border-radius: 4px;
  font-family: monospace;
}

/* Blockquote Stilleri */
.tiptap blockquote {
  border-left: 4px solid #3b82f6;
  padding-left: 12px;
  margin: 12px 0;
  color: #4b5563;
  font-style: italic;
}

/* Yatay Çizgi */
.tiptap hr {
  border: none;
  border-top: 1px solid #d1d5db;
  margin: 16px 0;
}
</style>
