<template>
    <div>
        <p>Componente de mensagem</p>
        <form id="burger-form">
            <div class="input-container">
                <label for="name">Nome do cliente</label>
                <input type="text" name="name" id="name" v-model="name" placeholder="Digite seu nome">
            </div>

            <div class="input-container">
                <label for="bread">Escolha o pão</label>
                <select name="bread" id="bread" v-model="bread">
                    <option value="">Selecione seu pão: </option>
                </select>
            </div>

            <div class="input-container">
                <label for="meat">Escolha a carne do seu Burger: </label>
                <select name="bread" id="bread" v-model="bread">
                    <option value="">Selecione sua carne</option>
                </select>
            </div>

            <div class="input-container">
                <label for="optional">Selecione seus opcionais: </label>
                <div class="checkbox-container">
                    <!-- <input type="checkbox" v-model="optional" name="optional" value="Salame"><span>Salame</span> -->
                </div>
            </div>

            <div class="input-container">
                <input type="submit" value="Criar meu burger" class="submit-btn">
            </div>
        </form>
    </div>
</template>

<script>
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
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #FCBA03;
}

input,
select {
    padding: 5px 10px;
    width: 300px;
}

#opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionais-title {
    widht: 100%;
}

/* .checkbox-container {
    display: flex;
} */
</style>