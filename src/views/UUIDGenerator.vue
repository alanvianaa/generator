<template>
    <div>
        <div>
            <Menubar></Menubar>
        </div>
        <div class="container">
            <div class="row justify-content-md-center">
                <div class="col-md-auto">
                    <div class="text-center">
                        <br>
                        <div class="card ">
                            <div class="card-header">
                                <h2>Gerador de UUID</h2>
                            </div>
                            <br>
                            <div>
                                <button class="btn btn-dark" v-on:click="newUUID()">Gerar um novo UUID</button>
                            </div>
                            <div class="card-body">
                                <blockquote class="blockquote mb-0">
                                    <h4 ref="text"><b>UUID:</b> {{uuid}}
                                        <button
                                                v-clipboard:copy="uuid"
                                                v-clipboard:success="copySuccess"
                                                v-clipboard:error="copyError"
                                                class="btn btn-dark"
                                                title="Copiar o UUID para área de transferencia">
                                            <span v-if="copySucceeded === null">Copiar <i class="fa fa-copy"></i></span>
                                            <span v-if="copySucceeded === true">Copiado <i
                                                    class="fa fa-check-circle"></i></span>
                                            <span v-if="copySucceeded === false">Erro ao copiar use CTRL+C <i
                                                    class="fa fa-copy"></i></span>
                                        </button>

                                    </h4>
                                    <footer class="blockquote-footer">UUID versão 4</footer>
                                </blockquote>
                            </div>
                            <div class="card-footer text-muted">
                                UUID é um identificador universalmente exclusivo utilizado para identificação de
                                qualquer
                                coisa no
                                mundo da computação. O UUID é um número de 128 bits representado por 32 dígitos
                                hexadecimais
                            </div>
                        </div>
                    </div>
                    <br>
                    <div class="row">
                        <div class="col-sm-3">
                            <div class="card border-dark">
                                <div class="card-header">UUID Versão 1</div>
                                <div class="card-body">
                                    <p class="card-text">São gerados a partir de um tempo e um node id (geralmente o
                                        endereço MAC).</p>
                                </div>
                            </div>
                        </div>
                        <div class="col-sm-3">
                            <div class="card border-dark">
                                <div class="card-header">UUID Versão 2</div>
                                <div class="card-body">
                                    <p class="card-text">São gerados a partir de um identificador (geralmente um id de
                                        grupo
                                        ou usuário), tempo e um node id.</p>
                                </div>
                            </div>
                        </div>
                        <div class="col-sm-3">
                            <div class="card border-dark">
                                <div class="card-header">UUID Versão 3 e 5</div>
                                <div class="card-body">
                                    <p class="card-text">Produzem UUIDs gerados por hashing de um identificador de
                                        namespace
                                        e nome.</p>
                                </div>
                            </div>
                        </div>
                        <div class="col-sm-3">
                            <div class="card border-dark">
                                <div class="card-header">UUID Versão 4</div>
                                <div class="card-body">
                                    <p class="card-text">São gerados usando um número aleatório ou pseudo-aleatório.</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    import Menubar from "../components/Menubar";
    import axios from 'axios';

    export default {
        components: {
            Menubar
        },
        data() {
            return {
                copySucceeded: null,
                uuid: null
            }
        },
        methods: {
            copySuccess() {
                this.copySucceeded = true;
                console.log('Sucesso')
            },
            copyError() {
                this.copySucceeded = false;
                console.log('Sucesso ')
            },
            newUUID: function () {
                axios
                    .get('https://www.uuidgenerator.net/api/version4')
                    .then(response => (this.uuid = response.data))
                    .catch(error => console.log(error));
                this.copySucceeded = null
            }
        },
        mounted() {
            this.newUUID()
        }
    }
</script>
<style>

</style>