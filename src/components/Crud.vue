<template>
    <div class="users">
        <form class="user-form">
            <h1>Create</h1>
            <label for="email">Email</label>
            <input type="text" name="email" v-model="user.email" /><br />
            <label for="password">Password</label>
            <input type="text" name="password" v-model="user.password" /><br />
            <input type="submit" :value="option" @click.prevent="save" />
        </form>
        <div class="grid-users">
            <h1>Users</h1>
            <ul>
                <li v-for="(user, index) in users" :key="index">
                    {{ user.email }}
                    <button @click="load(index)">Carregar</button>
                    <button @click="remove(user.id)">Deletar</button>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Crud',
    data() {
        return {
            option: 'Criar',
            user: {
                email: null,
                password: null,
                id: null,
            },
            users: [],
        };
    },
    created() {
        this.populate();
    },
    methods: {
        populate() {
            this.$http.get('users').then((res) => (this.users = res.data));
        },
        load(userId) {
            this.user.id = userId;

            this.user = { ...this.users[userId] };

            this.option = 'Alterar';
        },
        clean() {
            this.user.id = '';
            this.user.email = '';
            this.user.password = '';
            this.option = 'Criar';
        },
        save() {
            const method = this.user.id ? 'patch' : 'post';

            const final = this.user.id ? `/${this.user.id}` : '';

            this.$http[method](`/users${final}`, this.user).then((_) => {
                this.clean();

                this.populate();
            });
        },
        remove(userId) {
            this.$http.delete(`users/${userId}`).then((_) => {
                this.clean();

                this.populate();
            });
        },
    },
};
</script>
