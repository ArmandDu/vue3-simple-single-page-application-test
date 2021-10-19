<template>
  <td><input placeholder="Full Name" v-model="body.name"/></td>
  <td><input placeholder="E-mail address" v-model="body.email"/></td>
  <td><input placeholder="Phone Number" v-model="body.phone"/></td>
  <td>
    <button type="submit" @click="$emit('save', body)">Save</button>
    <button @click="$emit('cancel')">Cancel</button>
  </td>
</template>

<script lang="ts">
import {defineComponent} from 'vue'
import {Participant} from "@/components/ParticipantList.vue";

export default defineComponent({
  name: "InlineEditParticipant",
  props: ["initialValues"],
  emits: ['save', 'cancel'],

  data(): { body: Participant } {

    return {
      body: {...this.initialValues}
    }
  }
})
</script>

<style scoped lang="scss">

tr > td {
  border-bottom: 1px solid gray;
}

input {
  margin: 16px;
  height: 40px;
}

</style>