<template>
    <div id="burger-table">
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#</div>
                <div>Cliente</div>
                <div>Pão</div>
                <div>Carne</div>
                <div>Opcionais</div>
                <div>Status</div>
            </div>
            <div id="burger-table-rows">
                <div class="burger-table-row" v-for="burger in this.burgers" :key="burger.id">
                    <div class="order-number">{{ burger.id }}</div>
                    <div>{{ burger.name }}</div>
                    <div>{{ burger.bread }}</div>
                    <div>{{ burger.meats }}</div>
                    <div>
                        <ul>
                            <li v-for="(optional, index) in burger.optional" :key="index">{{ optional }}</li>
                        </ul>
                    </div>
                    <div>
                        <select name="status" class="status" @change="handlerStatus">
                            <option value="">{{ burger.status }}</option>
                            <option v-for="{ id, tipo } in this.status" :key="id" :value="tipo">{{ tipo }}</option>
                        </select>
                        <button @click="deleteBurger(burger.id)" class="delete-btn">Cancelar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Dashboard',
    data() {
        return {
            burgers: null,
            burger_id: null,
            status: []
        }
    },
    methods: {
        async getPedidos() {
            try {
                const { data } = await axios({
                    method: 'get',
                    url: 'http://localhost:3000/burgers'
                })

                this.burgers = data
            } catch (err) {
                console.log(err)
            }
        },

        async getAllStatus() {
            try {
                const { data } = await axios({
                    method: 'get',
                    url: '/status',
                    baseURL: 'http://localhost:3000'
                })

                this.status = data
            } catch (error) {
                console.log(error)
            }
        },
        async deleteBurger(burgerId) {
            try {
                const { data } = await axios({
                    method: 'delete',
                    url: `/burgers/${burgerId}`,
                    baseURL: 'http://localhost:3000',
                })
                this.getPedidos()
            } catch (err) {
                console.log(err)
            }
        }
    },
    mounted() {
        this.getPedidos()
        this.getAllStatus()
    }
}
</script>

<style scoped>
#burger-table {
    max-width: 1200px;
    margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
    display: flex;
    flex-wrap: wrap;
}

#burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

#burger-table-heading div,
.burger-table-row div {
    width: 19%;
}

.burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
    width: 5%;
}

select {
    padding: 12px 6px;
    margin-right: 12px;
}

.delete-btn {
    background-color: var(--black);
    color: var(--yellow);
    border: 2px solid var(--black);
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    font-weight: bold;
    transition: .5;
}

.delete-btn:hover {
    background-color: transparent;
    color: var(--black)
}
</style>