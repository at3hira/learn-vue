<template>
    <v-container>
        <v-card class="mx-auto" outlined max-width="1200">
            <v-card-title>
                <v-text-field placeholder="タスクを入力してください" v-model="task"></v-text-field>
                <v-select class="mt-2" :items="assignees" label="作業者を選択してください" v-model="assignee"></v-select>
                <v-btn dark class="mb-2" @click="addTask">追加</v-btn>
            </v-card-title>
            <v-data-table :headers="headers" :items="items" :items-per-page="5" class="elevation-1">
                <template v-slot:item.control="{ item }">
                    <v-btn class="mx-2" fab dark x-small color="error" @click="deleteTask(item)">
                        <v-icon dark>mdi-minus</v-icon>
                    </v-btn>
                </template>
            </v-data-table>
        </v-card>
    </v-container>
</template>

<script>
export default {
    name: 'TodoList',
    data: () => ({
        // テーブルのヘッダー
        headers: [
            {
                text: "タスク",
                sortable: true,
                value: "task",
                width: "70%"
            },
            {
                text: '担当者',
                sortable: true,
                value: "assignee"
            },
            {
                text: "操作",
                sortable: false,
                value: "control"
            }
        ],
        items: [],
        // 担当者を選択するセレクトボックス
        assignees: [
            "A",
            "B",
            "C",
            "D",
        ],
        task: "",
        assignee: ""
    }),
    methods: {
        addTask: function() {
            if (!this.task || !this.assignee) {
                // 未入力エラー
                alert("タスクと担当者を入力してください");
                return
            }
            // タスク追加
            this.items.push({
                "task": this.task,
                "assignee": this.assignee,
            });
            // 追加後入力フォームをクリア
            this.task = "";
            this.assignee = "";
        },
        // タスク削除
        deleteTask: function(item) {
            this.items.splice(this.items.indexOf(item), 1);
        }
    }
};
</script>