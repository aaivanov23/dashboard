<template>
    <v-container>
        <v-layout>
            <v-flex>
                <v-btn>Все задачи</v-btn>
                <v-data-table
                        :headers="headers"
                        :items="myJson"
                        class="elevation-1"
                >
                    <template v-slot:items="props">
                        <td>{{ props.item.require_date }}</td>
                        <td class="text-md-left">{{ props.item.executor }}</td>
                        <td class="text-md-left">{{ props.item.type_id }}</td>
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
            }
        },
        methods: {
        }
    }
</script>
