<template>
  <notes-field :field="field" :resourceName="resourceName" :resourceId="resourceId" :extraClass="'-mx-6 -my-px'" />
</template>

<script>
import NotesField from './components/NotesField';

export default {
  components: { NotesField },
  props: ['field', 'resourceId', 'resourceName'],
};
</script>
