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
                            <v-card-text class="list-group-item">
                                <div> {{ element.title }} </div>
                                <div> {{ element.severity }} </div>    
                                <div> {{ element.date }}</div>
                            </v-card-text>
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
                            <v-card-text class="list-group-item">
                                <div >{{ element.title }}</div>
                                <div >{{ element.severity }}</div>   
                                <div> {{ element.date }}</div> 
                            </v-card-text>
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
                            <v-card-text class="list-group-item">
                                <div >{{ element.title }}</div>
                                <div >{{ element.severity }}</div>    
                                <div> {{ element.date }}</div>
                            </v-card-text>
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
                            <v-card-text class="list-group-item">
                                <div >{{ element.title }}</div>
                                <div >{{ element.severity }}</div>    
                                <div> {{ element.date }}</div>
                            </v-card-text>
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

const uuid4 = () => {
    return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'
    .replace(/[xy]/g, function (c) {
        const r = Math.random() * 16 | 0, 
            v = c == 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
    });
}
const randomDate = () => {
    const startDate = new Date('2022-01-01');
    const endDate = new Date('2022-12-31');
    const timeDiff = endDate.getTime() - startDate.getTime();
    const randomTime = Math.random() * timeDiff;
    const randomDate = new Date(startDate.getTime() + randomTime);
    return randomDate.toISOString().slice(0, 10);
}
export default {
    components: {
        draggable
    },
    data(){
        return {
            arrBacklog: [
                {id:uuid4(), title:'lorem ipsummm', status:'ongoing', severity:'low', date: randomDate()},
                {id:uuid4(), title:'lorem ipsummm', status:'ongoing', severity:'low', date: randomDate()},
                {id:uuid4(), title:'lorem ipsummm', status:'ongoing', severity:'medium', date: randomDate()},
                {id:uuid4(), title:'lorem ipsummm', status:'ongoing', severity:'high', date: randomDate()},
            ],
            arrProgress: [],
            arrTesting: [],
            arrDone: []
        }
    },
    methods: {
        addTask: function(){
            this.arrBacklog.push({id:uuid4(),title:this.newTask,status:'ongoing',severity:'low',date: randomDate()})
            console.log({id:uuid4(), title:this.newTask})
        }
    }
}
</script>

<style>
.list-group-item {
    border: 1px solid #ddd; /* Add a thin border to each list item */
    margin-top: 10px; /* Prevent double borders */
    margin-bottom: 22px;
    margin-left: 20px;
    margin-right: 20px;
    background-color: #f6f6f6; /* Add a grey background color */
    padding: 12px; /* Add some padding */
}
</style>