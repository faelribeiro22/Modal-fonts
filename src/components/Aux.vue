<template>
    <div class="modal">
            <div class="modal-mask">
                <div class="modal-wrapper">
                    <div class="modal-container">

                        <div class="modal-header a">
                            <div class="statusTexto">
                              Alterar status para:
                            </div>
                            <div class="status">
                              <select class="selectStatus">
                                <option v-for="estado in status"
                                 v-model="estado.descricao" v-bind:value="estado.id">
                                    {{estado.descricao}}
                                </option>
                              </select>
                            </div>
                            <div class="tempoAtivacao">
                              <img src="src/assets/img/clock2.svg"
                               class="imgRelogio">
                              <span class="txtTempoAtivacao">
                                  Tempo em ativação:
                              </span><br>
                              <span class="qtdDias">18 dias</span>
                            </div>
                            <div class="boxSelect">
                                <div class="imgResponsavel">
                                    <img v-lazy="img"/>
                                </div>
                                <div class="txtAlterarResponsavel">
                                    Alterar responsável para:
                                </div>
                                    <multiselect v-model="value" :options="options"
                                    :max-height="150" track-by="title" :custom-label="customLabel" :show-labels="false" @select="onSelect" :searchable="false"
                                    :hide-selected="true">
                                        <template slot="option" scope="props">
                                            <img class="option__image" :src="props.option.img">
                                            <div class="option__desc"><span class="option__title">{{ props.option.title }}</span><span class="option__small">{{ props.option.desc }}</span></div>
                                        </template>
                                    </multiselect>
                            </div>

                            <div class="botaoFechar">
                              <img src="src/assets/img/close.svg"
                              @click ="$emit('close')">
                            </div>
                        </div>

                        <div class="modal-body">

                            <div class="">
                                <div class="descricaoEmpresa">
                                    <p>{{cliente.descricao}}</p>
                                </div>
                                <label>{{cliente.pontuacao}} pontos</label>
                                <div class="detalhes">
                                    <span>?</span>
                                </div>
                                <div class="responsavelInfo">
                                    <span class="txtResponsavel">
                                        Responsável:
                                    </span><br>
                                    <span class="txtResponsavelNome">
                                        {{cliente.responsavel_nome}}
                                    </span><br>
                                    <span class="txtResponsavelEmail">
                                        (99) 9999-9999
                                    </span><br>
                                    <span class="txtResponsavelEmail">
                                        email@email.com
                                    </span>
                                </div>
                            </div>

                            <div class="divTags">
                                <div class="imgTagicone">
                                    <img src="src/assets/img/tag.svg" alt="">
                                </div>
                                <span class="textTag">Tags</span>
                                <br>
                                <br>
                                <div class="containerTags">

                                    <div v-for="tag in listTags"
                                     class="listTags">
                                         <div class="botaoExcluirTags" @click="excluirTag(tag)">
                                         </div>
                                        <span class="estiloTag">{{tag.descricao}}</span>
                                    </div>

                                </div>

                                <div class="divImgAddTagIcone addTags"
                                v-show="showAddtag === false"
                                @click="showAddtag = true">
                                    <img class="imgAddTagIcone"
                                    src="src/assets/img/add.svg" alt="">
                                    <span class="textoAddTag">
                                        Adicionar tag
                                    </span>
                                </div>
                                <div class="divCampoAddTag"
                                v-show="showAddtag === true">
                                    <div class="btnAdd">
                                        <div class="cabecalhoAddTag">
                                            <div class="">
                                                <img src="src/assets/img/add.svg" @click="fechar">
                                            </div>
                                            <span class="textoAddTagCabecalho">Adicionar tags</span>
                                        </div>

                                        <div class="divListAllTags">
                                            <div class="estiloTag" v-for="tag in allTags" @click="addTags(cli.id,tag)">
                                                <span>{{tag.descricao}}</span>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="botaoStandBy" v-show="showAddtag === false">
                                    <div class="imgStandBy">

                                    </div>
                                    <span class="textoStandBy">Colocar em standby</span>
                                </div>
                            </div>

                            <div class="divCheckList">
                                <span>Checklist</span>
                                <ul class="checkList">
                                    <li v-for="task in cliente.tasks"
                                     v-bind:class="{'listTask' : true, 'listTaskDone': classTaskDone(task.done)}">
                                        <img src="src/assets/img/check.svg"
                                        v-show="task.done !== 1"
                                         class="iconeTask"
                                          @click="taskDone(task)">
                                        <img src="src/assets/img/check2.svg"
                                         v-show="task.done === 1"
                                         class="iconeTaskDone"
                                         @click="taskDone(task)">
                                        {{task.descricao}}
                                    </li>
                                    <li v-show="showAddTasks === false">
                                        <img src="src/assets/img/add.svg"
                                           class="addIcon"
                                          @click="showAddTasks=
                                           true">Adicionar item a checklist
                                    </li>
                                    <li v-show="showAddTasks === true"
                                     class="listAddTask">
                                        <input type="text" v-model="task"
                                         class="campoAddTasks">
                                        <img src="src/assets/img/add.svg"
                                        class="iconeAddTask"
                                         @click="showAddTasks = false">
                                    </li>
                                </ul>
                            </div>

                            <div class="divComentarios">
                                <h4 class="textAddComentario">Adicionar comentário</h4>
                                <div class="tetxComentarios">
                                    <div class="imgAvatarCampoComentario">
                                        <img src="src/assets/img/no-photo.png" alt="">
                                    </div>
                                    <textarea v-model="comentario"
                                     rows="5" cols="25"
                                      placeholder="Escreva seu comentário"
                                       class="textArea"></textarea>
                                    <button type="button" name="button"
                                     class="botaoComentario"
                                      @click="addComentario(comentario)">
                                      Comentar
                                  </button>
                                </div>
                                <div class="listComentarios">
                                    <h4>Comentários</h4>
                                    <div class="caixaComentarios" v-for="comentario in this.comentarios">
                                        <div class="imgAvatar">
                                            <img src="src/assets/img/no-photo.png" alt="">
                                        </div>
                                        <span class="txtSpanComentario">comentario</span> <span class="horarioComentario">12:23 - 01/01/2017 (há 3 dias)</span>
                                        <div class="textAreaComentarios">
                                            {{comentario.descricao}}
                                        </div>
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
import Multiselect from 'vue-multiselect';
export default {
    components: {
        Multiselect
    },
    props: {
        cliente: {
            type: Object,
            default: function () {
                return null;
            }
        },
        status: {
            type: Array,
            default: function () {
                return null;
            }
        }
    },
    data: function () {
        return {
            showAddtag: false,
            toHideButtons: false,
            showAddTasks: false,
            mostrarModal: false,
            task: null,
            comentario: '',
            comentarios: [],
            listResponsaveis: [],
            responsavel: {},
            listTasks: [],
            listTags: [],
            allTags: [],
            valueStatus: null,
            valueResponsavel: null,
            options: [{title:'Anonimo', img:'src/assets/img/no-photo.png'},
                      {title:'Anonimo2', img:'src/assets/img/no-photo.png'},
                      {title:'Anonimo3', img:'src/assets/img/no-photo.png'}
            ],
            value: {title:'Anonimo', img:'src/assets/img/no-photo.png'},
            img: null
        }
    },
    methods: {
        customLabel: function ({title, desc, img}) {
            this.img = img;
            return `${title}`;
        },
        onSelect: function (val) {

        },
        addComentario: function(comentario) {
            var listComentarios = this.comentarios;

            $.ajax({
                type: "POST",
                url: "../ajax/api/novo-comentario.jsp",
                data: {
                    empresa_id: this.cliente.id,
                    descricao: comentario
                },
                contentType: "application/x-www-form-urlencoded; charset=UTF-8",
                success: function (data) {
                    var coment = data.value;
                    listComentarios.push(coment);
                }
            });
            // this.comentarios = listComentarios.sort(function (a,b) {
            //     return b.id - a.id;
            // });
            this.comentario = '';
        },

        addTags: function (id,tag) {
            var self = this;
            var selfAllTags = this.allTags;
            $.ajax({
                type: "POST",
                url: "../ajax/api/add_tag.jsp",
                data: {
                    tag_id: tag.id,
                    empresa_id: id
                },
                contentType: "application/x-www-form-urlencoded; charset=UTF-8",
                success: function (data) {
                    if (!data.success) {
                        return alert('Erro ao tentar adicionar a tag: ' + data.value);
                    }
                    self.listTags.push(tag);
                    var index = self.allTags.indexOf(tag);
                    if (index > -1) {
                        selfAllTags.allTags.splice(index, 1);
                    }
                }
            });
        },

        excluirTag: function (tag) {
            var index = this.listTags.indexOf(tag);
            if (index > -1) {
                var elem = this.listTags[index];
                this.allTags.push(elem)
                this.listTags.splice(index, 1);
            }

        },
        taskDone: function (task) {
            var tasks = this.listTasks;
            var self = this;
            $.ajax({
                type: "POST",
                url: "../ajax/api/taskDone.jsp",
                data: {
                    id: task.id,
                    done: + !task.done
                },
                contentType: "application/x-www-form-urlencoded; charset=UTF-8",
                success: function (data) {
                    if (!data.success) {
                        return alert('Erro ao tentar atualiza a task: ' + data.value);
                    }

                    self.listTasks.map(function(element) {
                        if (element.id == task.id) {
                            element.done = + !element.done;
                        }
                    });

                }
            });
        },
        classTaskDone: function (value) {
            return value == 1;
        },
        fechar: function () {
            this.showAddtag = false;
        },
    },
    created: function () {
        this.$http.get("../ajax/api/responsavel.jsp").then(function(response) {
            var responsavel = response.body.value;
            this.listResponsaveis = responsavel;
        });

        this.$http.get("../ajax/api/buscarTags.jsp").then(function(response) {
            var listAllTag = response.body.value;
            var tags = this.cliente.tags;
            var listResult = [];

            var tagsEmpresaIDS = tags.map(function(element) {
                return element.id;
            });

            var tagsNaoEmpresa = listAllTag.filter(function(element) {
                return tagsEmpresaIDS.indexOf(element.id) < 0;
            });

            this.allTags = tagsNaoEmpresa;
        });
    },
    mounted: function() {
        this.comentarios = this.cliente.comentarios.slice();
        this.listTasks = this.cliente.tasks.slice();
        this.listTags = this.cliente.tags.slice();
    }
}
</script>
<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>
<style>

    .modal {
        height: 100%;
        overflow-y: auto;
    }

    .detalhes {
        width: 19px;
        height: 19px;
        background-color: #A4AABB;
        color: #FFFFFF;
        position: relative;
        left: 126px;
        bottom: 19px;
        padding: 3px;
        padding-left: 7px;
        border-radius: 10px;
    }

    .detalhesOpen {
        width: 19px;
        height: 19px;
        background-color: #FFFFFF;
        color: #A4AABB;
        position: relative;
        left: 126px;
        bottom: 19px;
        padding: 3px;
        padding-left: 7px;
        border: 1px solid #A4AABB;
        border-radius: 10px;
    }

    .imgResponsavel {
        position: relative;
        left: 10px;
        z-index: 9999;
        top: 9px;
        width: 41px;
        height: 40px;
    }

    .txtAlterarResponsavel {
        width: 153px;
        height: 18px;
        font-size: 13px;
        line-height: 18px;
        color: #605959;
        top: -38px;
        position: relative;
        z-index: 9999;
        left: 64px;
    }

    .multiselect__tags,
    {
        width: 201px;
        background-color: #EFF0F3;
        border: 0;
    }

    .option__title {
        position: relative;
        left: 30px;
        bottom: 25px;
    }

    .multiselect > .multiselect__tags {
        width: 201px;
        background-color: #EFF0F3;
        border: 0;
    }

    .multiselect > .multiselect__select {
        left: 200px;
        top: -11px;
    }

    .multiselect--active {
        z-index: 53;
    }

    .multiselect {
        bottom: 42px;
        width: 81%;
        left: 35px;
        height: 35px;
    }

    .multiselect__single {
        background: #EFF0F3;
        color: #605959;
        position: relative;
        left: 15px;
    }

    .selectBoxResponsavel {
        width: 181px;
        position: relative;
        bottom: 36px;
        left: 33px;
    }

    .botaoExcluirTags {
        width: 13px;
        height: 13px;
        background-color: #CC3C3C;
        position: relative;
        top: 1px;
        left: 90%;
    }

    .tasgEstiloGenerico {
        width: 150px;
        padding: 10px;
        background-color: blue;
        border-radius: 2px;
        padding: 7px;
        margin: 2px;
        margin-top: 7px;
    }

    .estiloTagAdd {
        background-color: red;
        border-radius: 2px;
        color: #FFFFFF;
        padding: 6px;
        margin: 2px;
        margin-top: 7px;
    }

    .modal-mask {
        position: absolute;
        z-index: 9998;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, .5);
        display: table;
        transition: opacity .3s ease;
    }

    .textAreaComentarios h4 {
        position: relative;
    }

    .imgAvatarCampoComentario {
        position: relative;
        right: 51px;
        top: 33px;
    }

    .imgAvatar {
        position: relative;
        right: 51px;
        top: 56px;
    }

    .listComentarios h4 {
        margin-left: -30px;
    }

    .caixaComentarios {
        position: relative;
        bottom: 40px;
    }

    .textAddComentario {
        margin-top: 0;
        position: relative;
        position: relative;
        bottom: 5px;
    }

    .txtSpanComentario {
        position: relative;
        bottom: 5px;
        font-size: 14px;
        font-weight: 600;
        line-height: 21px;
        color: #2570B3;
    }

    .horarioComentario {
        position: relative;
        bottom: 6px;
        font-family: "Open Sans";
        font-size: 10px;
        line-height: 21px;
        color: #8B8B8B;
    }

    .divListAllTags {
        width: 176px;
        width: 217px;
        position: relative;
        right: 156px;
        top: 40px;
    }

    .txtResponsavel {
        width: 66px;
        height: 15px;
        font-family: "Open Sans";
        font-size: 11px;
        line-height: 15px;
        color: #8A9096;
    }

    .txtResponsavelNome {
        width: 162px;
        height: 18px;
        font-family: "Open Sans";
        font-size: 13px;
        font-weight: 600;
        line-height: 18px;
        color: #605959;
    }

    .txtResponsavelEmail {
        width: 129px;
        height: 15px;
        font-family: "Open Sans";
        font-size: 11px;
        line-height: 15px;
        color: #605959;
    }

    .addTags {
        width: 175px;
        height: 39px;
        background-color: #34BB91;
        border-radius: 8px;
        margin-top: 10px;
    }

    .modal-wrapper {
        display: table-cell;
        vertical-align: middle;
    }

    .tempoAtivacao {
        position: relative;
        bottom: 36px;
        position: relative;
        left: 214px;
    }

    .modal-container {
        width: 720px;
        font-family: "Open Sans", open-sans, sans-serif;
        padding: 20px 30px;
        background-color: #fff;
        border-radius: 7px;
        box-shadow: 0 2px 8px rgba(0,0,0, .33);
        transition: all .3s ease;
        top: 150px;
        left: 362px;
        height: 100%;
    }

    .statusTexto {
        width: 112px;
        height: 18px;
        font-family: "Open Sans";
        font-size: 13px;
        line-height: 18px;
        color: #605959;
    }

    .qtdDias,
    .txtTempoAtivacao,
    .imgRelogio {
        position: relative;
    }

    .qtdDias {
        left: 26px;
        width: 49px;
        height: 20px;
        font-family: "Open Sans";
        font-size: 15px;
        font-weight: 600;
        line-height: 20px;
        color: #605959;
    }

    .textoStandBy {
        font-size: 14px;
        line-height: 17px;
        color: #FFFFFF;
        position: relative;
        top: 10px;
        left: 28px;
    }

    .txtTempoAtivacao {
        left: 5px;
        width: 118px;
        height: 18px;
        font-family: "Open Sans";
        font-size: 13px;
        line-height: 18px;
        color: #605959;

    }

    .divComentarios h4 {
        margin-left: -30px;
    }

    .imgRelogio {
        top: 10px;
    }

    .iconeAddTask {
        position: relative;
        top: 8px;
    }

    .modal-header {
        border-bottom: 1px solid #A0AFC0;
        height: 112px;
    }

    .modal-header h3 {
        margin-top: 0;
        color: #42b983;
    }

    .descricaoEmpresa {
        word-wrap: break-word;
        width: 60%;
        font-family: "Open Sans", open-sans, sans-serif;
    }

    .botaoComentario {
        position: relative;
        top: 9px;
        left: 293px;
        width: 91px;
        height: 36px;
        background-color: #25B485;
        border-radius: 8px;
        color: #ffffff;
        border: 1px solid #25B485;
    }

    .cabecalhoAddTag {
        display: flex;
        width: 130px;
        position: relative;
        right: 145px;
        top: 29px;
        border-bottom: 1px solid #DADADA;
        padding-bottom: 11px;
    }

    .cabecalhoAddTag span {
        margin-top: 5px;
        margin-left: 10px;
    }

    .textArea {
        width: 384px;
        height: 101px;
        background-color: #EAEBEE;
        border: 1px solid #C8C8C8;
        border-radius: 8px;
        padding: 12px;
        resize: none;
        margin-bottom: 20px;
    }

    .textComentarios {
        position: relative;
        bottom: 40px;
    }

    .textAreaComentarios {
        width: 384px;
        background-color: #EAEBEE;
        border: 1px solid #C8C8C8;
        border-radius: 8px;
        padding: 12px;
        resize: none;
        margin-bottom: 20px;
    }

    h4 {
        width: 141px;
        height: 19px;
        font-family: "Open Sans";
        font-size: 14px;
        line-height: 19px;
        color: #605959;
    }
    .textArea:placeholder-show {
        width: 150px;
        height: 19px;
        font-family: "Open Sans";
        font-size: 14px;
        line-height: 19px;
        color: #A39E9E;
    }

    .addIcon {
        position: relative;
        right: 5px;
        top: 6px;
    }

    .textoAddTag {
        position: relative;
        left: 14px;
        width: 84px;
        height: 19px;
        font-family: "Open Sans";
        font-size: 14px;
        line-height: 17px;
        color: #FFFFFF;
    }

    .textoAddTagCabecalho {
        font-size: 14px;
        line-height: 17px;
        color: #646464;
    }

    .divTags {
        position: relative;
        left: 64%;
        bottom: 151px;
        width: 263px;
        height: 100%;
        background-color: #EFF0F3;
        padding: 20px;
    }

    .divCampoAddTag {
        position: relative;
        top: 48px;
        left: 3px;
    }

    .divComentarios {
        width: 61%;
        position: relative;
        bottom: 15px;
        left: 33px;
    }

    .option__image {
        position: relative;
        left: -10px;
    }

    .botaoStandBy {
        width: 175px;
        height: 39px;
        background-color: #959AA4;
        border-radius: 8px;
        margin-top: 8px;
    }

    .campoAddTasks {
        width: 263px;
        height: 33px;
        background-color: #EAEBEE;
        border: 1px solid #C8C8C8;
        border-radius: 8px;
    }

    .listTags {
        margin-top: 7px;
        height: 28px;
        display: table;
    }

    .estiloTag {
        background-color: red;
        border-radius: 2px;
        color: #FFFFFF;
        padding: 6px;
        margin-top: 7px;
    }

    .divImgAddTagIcone img{
        position: relative;
        top: 8px;
        left: 8px;
    }

    .btnAdd {
        box-sizing: border-box;
        width: 22px;
        height: 22px;
        position: relative;
        bottom: 27px;
        left: 152px;
    }
    .imgTagIcone {
        position: relative;
        left: 22px;
        bottom: 17px;
    }

    .responsavelInfo {
        position: relative;
        left: 274px;
        bottom: 62px;
    }

    .textTag {
        position: relative;
        bottom: 20px;
        left: 26px;
        width: 31px;
        height: 20px;
        font-family: "Open Sans";
        font-size: 15px;
        font-weight: 600;
        line-height: 20px;
        color: #605959;
    }

    .boxSelect {
        width: 275px;
        height: 55px;
        background-color: #EFF0F3;
        border: 1px solid #DCDCDC;
        border-radius: 3px;
        position: relative;
        bottom: 82px;
        left: 382px;
    }

    .status {
        position: relative;
        top: 3px;
        left: 0px;
    }

    .selectStatus {
        width: 201px;
        height: 39px;
        background-color: #EAEBEE;
        border: 1px solid #BDBDBD;
    }

    .selectStatus option {
        font-size: 13px;
        line-height: 31px;
        color: #605959;
        background-color: #EAEBEE;
        height: 39px;
    }

    .botaoFechar {
        position: relative;
        bottom: 219px;
        left: 660px;
        padding-top: 15px;
        width: 21px;
        height: 21px;
    }

    .modal-body {
        margin: 20px 0;
    }

    .listComentarios {
        margin-top: 0;
        border-top: 1px solid #DFDFDF;
    }

    .modal-body h3 {
        width: 88px;
        height: 36px;
        font-family: "Open Sans";
        font-size: 26px;
        font-weight: 600;
        line-height: 36px;
        color: #605959;
    }

    .divCheckList {
        border-top: 1px solid #DFDFDF;
        box-sizing: border-box;
        border-bottom: 1px solid #DFDFDF;
        padding-bottom: 17px;
        padding-top: 15px;
        margin-top: -110px;
        width: 423px;
        height: 230px;
        position: relative;
        bottom: 45px;
        overflow-y: scroll;
    }

    .checkList {
        list-style: none;
        line-height: 20px;
        padding: 13px;
    }

    .listTask img {
        position: relative;
        top: 8px;
        right: 5px;
    }

    .listTask {
        font-family: "Open Sans";
        font-size: 14px;
        line-height: 19px;
        color: #605959;
    }

    .listTaskDone {
        font-family: "Open Sans";
        font-size: 14px;
        line-height: 19px;
        color: #989898;
        text-decoration: line-through;
    }

    .modal-body label {
        width: 106px;
        height: 24px;
        font-family: "Open Sans";
        font-size: 18px;
        line-height: 24px;
        color: #605959;
    }

    .modal-default-button {
        float: right;
    }
    .campoTextoTag {
        width: 141px;
        height: 31px;
        background-color: #EAEBEE;
        border: 1px solid #C8C8C8;
        border-radius: 8px;
    }

    @media only screen and (max-width: 1920px){
        .modal-container {
            position: relative;
            left: 600px;
        }
    }


</style>
