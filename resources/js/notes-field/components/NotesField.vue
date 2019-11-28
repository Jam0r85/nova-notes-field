<template>
  <div :class="classes">

    <div v-if="notes.length == 0" class="flex justify-center items-center px-6 py-8">
      <div class="text-center">        
        <h3 class="text-base text-80 font-normal mb-6">
          No notes have been made.
        </h3>
      </div>
    </div>

    <note
      v-for="note in notesToShow"
      :note="note"
      :key="note.id"
      @onDeleteRequested="onNoteDeleteRequested"
    />

    <div class="flex justify-center mb-3 mt-3" v-if="hasMoreToShow">
      <span
        class="btn btn-default btn-primary leading-tight ml-2 px-3 text-sm text-center cursor-pointer"
        style="height: 24px; line-height: 24px;"
        @click="maxToShow = void 0"
      >Show all notes ({{ notes.length - maxToShow }} more)</span>
    </div>

    <note-input
      v-model.trim="note"
      @onSubmit="createNote"
      :loading="loading"
      :placeholder="field.placeholder || field.name"
    />

    <delete-note-confirmation-modal
      v-if="showDeleteConfirmation"
      @close="showDeleteConfirmation = false"
      @confirm="deleteNote(noteToDelete)"
    />
  </div>
</template>

<script>
import Note from './Note';
import NoteInput from './NoteInput';
import DeleteNoteConfirmationModal from './DeleteNoteConfirmationModal';

export default {
  components: { Note, NoteInput, DeleteNoteConfirmationModal },
  props: ['resourceName', 'resourceId', 'field', 'extraClass'],
  data: () => ({
    note: '',
    loading: true,
    notes: [],
    showDeleteConfirmation: false,
    noteToDelete: void 0,
    maxToShow: 5,
  }),
  mounted() {
    this.fetchNotes();
  },
  computed: {
    params() {
      return {
        resourceId: this.resourceId,
        resourceName: this.resourceName,
      };
    },
    notesToShow() {
      if (this.maxToShow) return this.notes.slice(0, this.maxToShow);
      return this.notes;
    },
    hasMoreToShow() {
      return this.maxToShow && this.notes.length > this.maxToShow;
    },
    classes() {
      const defaultClasses = 'notes-field overflow-hidden';
      return defaultClasses + (this.extraClass ? ` ${this.extraClass}` : '');
    },
  },
  methods: {
    async fetchNotes() {
      this.loading = true;

      const { data: notes } = await Nova.request().get(`/nova-vendor/nova-notes/notes`, {
        params: this.params,
      });
      if (Array.isArray(notes)) this.notes = notes;

      this.loading = false;
    },
    async createNote() {
      this.loading = true;

      await Nova.request().post(`/nova-vendor/nova-notes/notes`, { note: this.note }, { params: this.params });
      await this.fetchNotes();

      this.note = '';

      this.loading = false;
    },
    async deleteNote(note) {
      this.loading = true;

      await Nova.request().delete(`/nova-vendor/nova-notes/notes`, { params: this.params, data: { noteId: note.id } });
      await this.fetchNotes();

      this.showDeleteConfirmation = false;
      this.loading = false;
    },
    onNoteDeleteRequested(note) {
      this.showDeleteConfirmation = true;
      this.noteToDelete = note;
    },
  },
};
</script>

<style lang="scss" scoped>
.notes-field:not(:last-child) {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
</style>
