<template>

<div class="app flex-row align-items-center">
    <div class="container">

        <!-- nao esta sendo usado agora, troquei pelo toast -->
        <p v-if="errors.length">
            <b-alert v-for="error in errors" variant="danger" show>
                {{ error }}
            </b-alert>
        </p>

        <b-row class="justify-content-center">
            <b-col md="6" sm="8">
                <b-card no-body class="mx-4">
                    <b-card-body class="p-4">
                        <b-form>
                            <h1>Registro</h1>
                            <p class="text-muted">Crie sua conta</p>
                            <b-input-group class="mb-3">
                                <b-input-group-prepend>
                                    <b-input-group-text><i class="icon-user"></i></b-input-group-text>
                                </b-input-group-prepend>
                                <b-form-input type="text" v-model="nome" class="form-control" placeholder="Nome Completo" autocomplete="nome" required/>
                            </b-input-group>

                            <b-input-group class="mb-3">
                                <b-input-group-prepend>
                                    <b-input-group-text>123</b-input-group-text>
                                </b-input-group-prepend>
                                <b-form-input type="text" v-model="cpf" class="form-control" placeholder="CPF" autocomplete="cpf" required/>
                            </b-input-group>

                            <b-input-group class="mb-3">
                                <b-input-group-prepend>
                                    <b-input-group-text>@</b-input-group-text>
                                </b-input-group-prepend>
                                <b-form-input type="email" v-model="email" class="form-control" placeholder="Email" autocomplete="email" required/>
                            </b-input-group>

                            <b-input-group class="mb-3">
                                <b-input-group-prepend>
                                    <b-input-group-text><i class="icon-lock"></i></b-input-group-text>
                                </b-input-group-prepend>
                                <b-form-input type="password" v-model="senha" class="form-control" placeholder="Senha" autocomplete="new-password" required/>
                            </b-input-group>
                            <p class="text-muted">Mínimo de 8 caracteres</p>

                            <b-input-group class="mb-4">
                                <b-input-group-prepend>
                                    <b-input-group-text><i class="icon-lock"></i></b-input-group-text>
                                </b-input-group-prepend>
                                <b-form-input v-model="confirmar_senha" type="password" class="form-control" placeholder="Confirme a senha" autocomplete="new-password" required/>
                            </b-input-group>

                            <b-button variant="success" block @click="cadastrar()"> Finalizar Cadastro </b-button>

                            <b-button variant="danger" block to="/pages/login"> Cancelar </b-button>
                        </b-form>
                    </b-card-body>

                </b-card>
            </b-col>
        </b-row>
    </div>
</div>

</template>

<script>

import axios from 'axios';
import qs from 'qs';

export default {
    name: 'Register',
    data() {
        return {
            email: "",
            nome: "",
            cpf: "",
            senha: "",
            confirmar_senha: "",
            errors: []
        }
    },
    methods: {
        cadastrar() {
            this.errors = []

            if (this.senha == this.confirmar_senha) {
                const data = qs.stringify({
                    email: this.email,
                    senha: this.senha,
                    nome: this.nome,
                    cpf: this.cpf
                })
                const header = {
                    'content-type': 'application/x-www-form-urlencoded;charset=utf-8'
                }
                axios.post(process.env.VUE_APP_API + "/usuario/registrar", data, header).then((response) => {
                    if (response.status == 201) {
                        this.$router.push('/pages/login')
                    } else {
                        //nao usado agora, trocado pelo toast
                        //this.errors.push(response.headers.erro)

                        this.$bvToast.toast(response.headers.erro, {
                            title: "Erro:",
                            variant: "danger",
                            toaster: "b-toaster-top-center",
                            solid: true,
                            autoHideDelay: 8000,
                            appendToast: true
                        })
                    }
                }).catch(() => {
                    this.$router.push('/pages/500')
                })
            } else {
                //nao usado agora, trocado pelo toast
                //this.errors.push("As senhas nao conferem")

                this.$bvToast.toast("As senhas nao conferem", {
                    title: "Aviso:",
                    variant: "warning",
                    toaster: "b-toaster-top-center",
                    solid: true,
                    autoHideDelay: 8000,
                    appendToast: true
                })
            }
        }
    }
}

</script>
