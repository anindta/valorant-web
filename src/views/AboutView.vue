<!-- AgentList.vue -->
<template>
  <div class="flex px-5">
    <div class="agent-list-container flex-none">
      <ul>
        <li v-for="agent in agents" :key="agent.uuid" class="font-valorant text-red-500 text-xl text-white"
          @click="selectAgent(agent)">
          {{ agent.displayName }}
          <img :src="agent.killfeedPortrait" :alt="agent.displayName" class="w-full h-full" />
        </li>
      </ul>
    </div>
    <div v-if="selectedAgent" class="flex-auto w-96 h-screen items-center justify-center -my-16">
      <img :src="selectedAgent.fullPortrait" :alt="selectedAgent.displayName"
        class="object-cover max-h-full max-w-full" />
    </div>
    <div v-if="selectedAgent" class="flex-auto w-2 px-3 ">
      <h2 class=" text-sm  text-white">{{ selectedAgent.role.displayName }}</h2>
      <h2 class="font-valorant text-2xl  text-white">{{ selectedAgent.displayName }}</h2>
      <h2 class=" text-sm text-white pr-6 mt-2">{{ selectedAgent.description }}</h2>
      <div class="flex flex-wrap">
        <ul v-for="ability in selectedAgent.abilities" :key="ability.uuid" class="ability-item flex-1 p-4"
        @click="selectAbility(ability)"> 
          <li class="text-white text-center">
            <img :src="ability.displayIcon" :alt="ability.displayName" class="w-32 h-full bg-slate-50 bg-opacity-25 p-4 hover:bg-red-500 active::bg-red-500" />
            {{ ability.displayName }}
     
          </li>
        </ul>
      </div>
      <div v-if="selectedAbility" class="text-white">
          {{ selectedAbility.description }}
        </div>
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.cdnfonts.com/css/valorant');

.agent-list-container {
  max-height: 800px;
  overflow-y: auto;
}

.agent-list-container::-webkit-scrollbar {
  width: 0;
  /* Remove scrollbar width */
  background: transparent;
  /* Optional: Set a background color if needed */
}

.font-valorant {
  font-family: 'VALORANT';
}
</style>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      agents: [],
      selectedAgent: null,
      selectedAbility: null
    };
  },
  mounted() {
    this.fetchAgents();
  },
  methods: {
    async fetchAgents() {
      try {
        const response = await axios.get('https://valorant-api.com/v1/agents');
        this.agents = response.data.data;
      } catch (error) {
        console.error('Error fetching agents:', error);
      }
    },
    selectAgent(agent) {
      this.selectedAgent = agent;
    },
    selectAbility(ability) {
      this.selectedAbility = ability;
   
    },
  },
};
</script>
