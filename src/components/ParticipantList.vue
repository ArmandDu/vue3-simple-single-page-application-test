<!--

This component is a test with:

- composition API
- v-for directive
- custom event handler

-->
<template>
  <div id="participant-list">
    <h1>List of participants</h1>

    <AddParticipant @new-participant="addParticipant"/>

    <div id="user-table">
      <table>
        <thead>
        <tr>
          <td>Name</td>
          <td>E-mail address</td>
          <td>Phone Number</td>
          <td></td>
        </tr>
        </thead>
        <tbody>
        <tr v-for="participant in participants" v-bind:key="participant.id">
          <template v-if="isEditingParticipant !== participant.id">
            <td> {{ participant.name }}</td>
            <td> {{ participant.email }}</td>
            <td> {{ participant.phone }}</td>
            <td>
              <button @click="toggleEditParticipant(participant.id)">...</button>
              <button @click="deleteParticipant(participant.id)">X</button>
            </td>
          </template>
          <template v-else>
            <InlineEditParticipant :initialValues="participant"
                                   @save="body => updateParticipant(participant.id, body)"
                                   @cancel="toggleEditParticipant(null)"/>
          </template>
        </tr>

        </tbody>
      </table>
    </div>


  </div>
</template>

<script lang="ts">
import Faker from "faker";
import AddParticipant from "@/components/AddParticipant.vue";
import {defineComponent, ref} from "vue";
import InlineEditParticipant from "@/components/InlineEditParticipant.vue";

export interface Participant {
  id: string,
  name: string,
  email: string,
  phone: string
}

const useParticipantRepo = (initialSize: number = 20) => {
  const participants = ref<Participant[]>(Array(initialSize).fill(0).map(() => ({
    id: Faker.datatype.uuid(),
    name: `${Faker.name.firstName()} ${Faker.name.lastName()}`,
    email: Faker.internet.email().toLowerCase(),
    phone: Faker.phone.phoneNumber()
  })));

  const isEditingParticipant = ref<Participant["id"] | null>(null);

  function addParticipant(participant: Omit<Participant, "id">) {
    participants.value.push({...participant, id: Faker.datatype.uuid()});
  }

  function deleteParticipant(id: Participant["id"]) {
    participants.value = participants.value.filter(participant => participant.id !== id);
  }

  function updateParticipant(id: Participant["id"], body: Partial<Omit<Participant, "id">>) {
    participants.value = participants.value.map(participant => participant.id === id ? {...participant, ...body} : participant);
    toggleEditParticipant(null);
  }

  function toggleEditParticipant(id: Participant["id"] | null) {
    isEditingParticipant.value = id;
  }

  return {
    participants,
    addParticipant,
    deleteParticipant,
    updateParticipant,
    isEditingParticipant,
    toggleEditParticipant
  }
}

export default defineComponent({

  name: 'ParticipantList',
  components: {
    InlineEditParticipant,
    AddParticipant
  },

  //couldn't figure out how to use setup with vue-class-component
  setup() {
    return {
      ...useParticipantRepo()
    }
  },


});
</script>

<style scoped lang="scss">

#participant-list {
  margin: auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 912px;

  padding-bottom: 96px;
}

table {

  background-color: white;
  font-size: 16px;
  width: 912px;

  thead {
    font-weight: bold;
  }

  td {
    padding: 16px;
  }

  tr > td {
    border-bottom: 1px solid gray;
  }

}
</style>