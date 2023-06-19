<template>
    <div class="q-pa-md">
        <q-btn color="blue" label="VOLTAR" icon="arrow_left" densed @click="this.$router.push('/admin/quadras')" /> <q-btn
            color="green" label="SALVAR" icon="save" densed @click="this.salvar()" />
        <div class="row q-mt-md">
            <div class="col-12 col-lg-6 col-md-6 col-sm-12 q-pa-sm">
                <q-input square filled clearable v-model="dados.name" type="Nome" label="Nome" />
            </div>
            <div class="col-12 col-lg-6 col-md-6 col-sm-12 q-pa-sm">
                <q-input square filled clearable v-model="dados.description" type="Descrição" label="Descrição" />
            </div>
            <div class="col-12 col-lg-12 col-md-6 col-sm-12 q-pa-sm">
                <q-input square filled clearable v-model="dados.location" type="Local" label="Local" />
            </div>
        </div>
    </div>
</template>
  
<script>

import { Notify } from 'quasar'

export default {
    data() {
        return {
            dados: {
                name: '',
                description: '',
                location: '',
                owner: ''
            }
        }
    },
    methods: {
        async salvar() {
            try {
                let id = this.$route.params.id
                this.dados.owner = localStorage.getItem('user');

                await this.$gf.executeMethod(id ? 'PUT' : 'POST', id ? '/sportsCourt/' + id : '/sportsCourt', this.dados)
                Notify.create({
                    type: 'positive',
                    message: 'Quadra criada com sucesso!'
                })
                this.$router.push('/admin/quadras')

            } catch (err) {
                Notify.create({
                    type: 'negative',
                    message: 'Ocorreu um erro ao tentar fazer a autenticação.'
                })
            }
        }
    },
    async created() {
        let id = this.$route.params.id

        if(id) this.dados = (await this.$gf.executeMethod('GET', `/sportsCourt/${id}`)).data.sportsCourt
    }
}
</script>
  