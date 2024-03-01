<template>
    <v-app-bar>
        <v-app-bar-title>Kanban Board</v-app-bar-title>
        <v-spacer>
            <v-btn prepend-icon="mdi-github">Link to this source code</v-btn>
        </v-spacer>
    </v-app-bar>
    <v-container>
        <v-row>
            <v-col cols="4">
                <v-text-field label="Add task list" variant="outlined" v-model="newTask"></v-text-field>
            </v-col>
            <v-col>
                <v-btn prepend-icon="mdi-plus" variant="outlined" @click="addTask">Add</v-btn>
            </v-col>
        </v-row>
    </v-container>
    <v-layout>
        <v-row>
            <v-col cols="4">
                <v-container>
                    <v-card>
                        <v-card-title>Backlog</v-card-title>
                        <draggable
                            class="list-group"
                            :list="arrBacklog"
                            group="people"
                            @change="log"
                            itemKey="title"
                        >
                            <template #item="{ element, index }">
                            <div class="list-group-item">{{ element.title }} {{ element.id }}</div>
                            </template>
                        </draggable>
                    </v-card>
                </v-container>
            </v-col>
            <v-col>
                <v-container>
                    <v-card>
                        <v-card-title>Progress</v-card-title>
                        <draggable
                            class="list-group"
                            :list="arrProgress"
                            group="people"
                            @change="log"
                            itemKey="title"
                        >
                            <template #item="{ element, index }">
                            <div class="list-group-item">{{ element.title }} {{ element.id }}</div>
                            </template>
                        </draggable>
                    </v-card>
                </v-container>
            </v-col>
            <v-col>
                <v-container>
                    <v-card>
                        <v-card-title>Testing</v-card-title>
                        <draggable
                            class="list-group"
                            :list="arrTesting"
                            group="people"
                            @change="log"
                            itemKey="title"
                        >
                            <template #item="{ element, index }">
                            <div class="list-group-item">{{ element.title }} {{ element.id }}</div>
                            </template>
                        </draggable>
                    </v-card>
                </v-container>
            </v-col>
            <v-col>
                <v-container>
                    <v-card>
                        <v-card-title>Done  </v-card-title>
                        <draggable
                            class="list-group"
                            :list="arrDone"
                            group="people"
                            @change="log"
                            itemKey="title"
                        >
                            <template #item="{ element, index }">
                            <div class="list-group-item">{{ element.title }} {{ element.id }}</div>
                            </template>
                        </draggable>
                    </v-card>
                </v-container>
            </v-col>
        </v-row>
        
    </v-layout>
</template>

<script>
import { ref } from 'vue'
import draggable from 'vuedraggable'

export default {
    components: {
        draggable
    },
    data(){
        return {
            arrBacklog: [
                {id:0, title:'lorem ipsummm'},
                {id:1, title:'lorem ipsummm'},
                {id:2, title:'lorem ipsummm'},
                {id:3, title:'lorem ipsummm'},
            ],
            arrProgress: [],
            arrTesting: [],
            arrDone: []
        }
    },
    methods: {
        addTask: function(){
            const lastIndex = this.arrBacklog.length - 1
            const lastValue = this.arrBacklog[lastIndex].id + 1
            this.arrBacklog.push({id:lastValue,title:this.newTask})
            console.log({id:lastValue, title:this.newTask})
        }
    }
}
</script>

<style>
.list-group-item {
    border: 1px solid #ddd; /* Add a thin border to each list item */
    margin-top: -1px; /* Prevent double borders */
    background-color: #f6f6f6; /* Add a grey background color */
    padding: 12px; /* Add some padding */
}
</style>