<template>
    <v-container>
        <v-layout>
            <v-flex>
                <v-layout>
                    <v-flex md9>
                        <v-btn flat @click="showAll">Все задачи</v-btn>
                        <v-btn flat @click="filterData(1)">Провести проверку</v-btn>
                        <v-btn flat @click="filterData(2)">Контроль предписания</v-btn>
                        <v-btn flat @click="filterData(3)">Поручение</v-btn>
                    </v-flex>
                    <v-flex md3>
                        <v-layout justify-end class="pt-2">
                            <div :class="`${color(4)} + ${'indicator'}`">
                                {{result.length}}
                            </div>
                            <div :class="`${color(1)} + ${'indicator'}`">
                                {{count(1)}}
                            </div>
                            <div :class="`${color(2)} + ${'indicator'}`">
                                {{count(2)}}
                            </div>
                            <div :class="`${color(3)} + ${'indicator'}`">
                                {{count(3)}}
                            </div>
                        </v-layout>
                    </v-flex>
                </v-layout>
                <v-data-table
                        :headers="headers"
                        :items="result"
                        class="elevation-5"
                >
                    <template v-slot:items="props">
                        <td>
                            <div :class="`${color(props.item.status_id)} + ${'date'}`">
                                {{ props.item.require_date }}
                            </div>
                        </td>
                        <td class="text-md-left">{{ props.item.executor }}</td>
                        <td class="text-md-left">{{ renameType(props.item.type_id) }}</td>
                        <td class="text-md-left">{{ props.item.description }}</td>
                        <td class="text-md-left">{{ props.item.date_create }}</td>
                    </template>
                </v-data-table>
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
    import json from '../data.json';

    export default {
        data() {
            return {
                headers: [
                    {text: 'Срок', align: 'left', sortable: false},
                    {text: 'Исполнитель', align: 'left', sortable: false},
                    {text: 'Тип', align: 'left', sortable: false},
                    {text: 'Краткое содержание', align: 'left', sortable: false},
                    {text: 'Дата создания задачи', align: 'left', sortable: false},
                ],
                myJson: json,
                result: [],
            }
        },
        methods: {
            filterData: function (index) {
                this.result = this.myJson.filter(obj => obj.type_id === index);
            },
            showAll: function () {
                this.result = this.myJson
            },
            renameType: function (index) {
                switch (index) {
                    case 1:
                        return 'Провести проверку';
                    case 2:
                        return 'Контроль предписания';
                    case 3:
                        return 'Поручение';
                }
            },
            color: function (index) {
                if (index === 1) return 'green lighten-1';
                if (index === 2) return 'yellow lighten-2';
                if (index === 3) return 'red lighten-1';
                if (index === 4) return 'blue lighten-1'
            },
            count: function (index) {
                return this.result.filter(obj => obj.status_id === index).length;
            }
        },
        created() {
            this.showAll()
        }

    }
</script>
<style scoped>
    .indicator {
        border-radius: 20px;
        height: 20px;
        width: 30px;
        text-align: center;
        margin: 2px;
    }
    .date {
        border-radius: 20px;
        height: 20px;
        text-align: center;
    }
</style>
