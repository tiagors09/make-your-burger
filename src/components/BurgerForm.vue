<template>
    <div>
        <Message :message="this.msg" v-show="msg" />
        <form id="burger-form" @submit.prevent="createBurger">
            <div class="input-container">
                <label for="name">Nome do cliente</label>
                <input type="text" name="name" id="name" v-model="name" placeholder="Digite seu nome" required>
            </div>

            <div class="input-container">
                <label for="bread">Escolha o pão</label>
                <select name="bread" id="bread" v-model="bread" required>
                    <option value="">Selecione seu pão: </option>
                    <option v-for="bread in this.breads" :key="bread.id" :value="bread.tipo">{{ bread.tipo }}</option>
                </select>
            </div>

            <div class="input-container">
                <label for="meat">Escolha a carne do seu Burger: </label>
                <select name="meat" id="meat" v-model="meat" required>
                    <option value="">Selecione sua carne</option>
                    <option v-for="meat in this.meats" :key="meat.id" :value="meat.tipo">{{ meat.tipo }}</option>
                </select>
            </div>

            <div id="optional-container" class="input-container">
                <label id="optional-title" for="optional">Selecione seus opcionais: </label>
                <div v-for="optional in optionaldata" class="checkbox-container" :key="optional.id">
                    <input type="checkbox" v-model="optionalSelected" name="optional" :value="optional.tipo"><span>{{
                        optional.tipo
                    }}</span>
                </div>
            </div>

            <div class="input-container">
                <input type="submit" value="Criar meu burger" class="submit-btn">
            </div>
        </form>
    </div>
</template>

<script>
import axios from 'axios'
import Message from './Message.vue'

export default {
    name: 'BurgerForm',
    components: {
        Message
    },
    data() {
        return {
            breads: null,
            meats: null,
            optionaldata: null,
            name: null,
            bread: null,
            meat: null,
            optionalSelected: [],
            msg: null,
        }
    },
    methods: {
        async getIngredients() {
            try {
                let { data } = await axios({
                    method: 'get',
                    url: 'http://localhost:3000/ingredientes'
                })
                this.breads = data.paes
                this.meats = data.carnes
                this.optionaldata = data.opcionais
            } catch (err) {
                console.log(err)
            }
        },

        async createBurger(e) {
            try {
                let { data } = await axios({
                    method: 'post',
                    url: 'http://localhost:3000/burgers',
                    data: {
                        name: this.name,
                        meat: this.meat,
                        bread: this.bread,
                        optional: Array.from(this.optionalSelected),
                        status: 'Solicitado',
                    },
                })

                this.name = null
                this.meat = null
                this.bread = null
                this.optionalSelected = []

                this.msg = `Pedido N°${data.id} realizado com sucesso para ${data.name}`

                await setTimeout(() => {
                    this.msg = null
                }, 3e3)
            } catch (err) {
                console.log(err)
            }
        }
    },
    mounted() {
        this.getIngredients()
    }
}
</script>

<style scoped>
#burger-form {
    margin: 0 auto;
    max-width: 400px;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 15px;
    color: var(--black);
    padding: 5px 10px;
    border-left: 4px solid var(--yellow);
}

input,
select {
    padding: 5px 10px;
    width: 300px;
}

#optional-container {
    flex-direction: row;
    flex-wrap: wrap;
}

#optional-title {
    width: 100%;
}

.checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
    width: auto;
}

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn {
    background-color: var(--black);
    color: var(--yellow);
    font-weight: bold;
    border: 2px solid var(--black);
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

.submit-btn:hover {
    background-color: transparent;
    color: var(--black);
}
</style>