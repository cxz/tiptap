<script setup lang="ts">

import { Collaboration } from '@tiptap/extension-collaboration'
import StarterKit from '@tiptap/starter-kit'
import { EditorContent, useEditor } from '@tiptap/vue-3'
import * as Y from 'yjs'

import type { TNote } from './types'

const props = defineProps<{note: TNote}>()

const doc = new Y.Doc()

const editor = useEditor({
  content: props.note.defaultContent,
  editorProps: {
    attributes: {
      class: 'm-2 p-2 border border-black rounded-lg',
    },
  },
  extensions: [
    StarterKit.configure({
      history: false, // important because history will now be handled by Y.js
    }),
    Collaboration.configure({
      document: doc,
    }),
  ],
})

</script>

<template>
  <editor-content :editor="editor"></editor-content>
</template>
