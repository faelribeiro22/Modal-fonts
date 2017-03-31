<template>
  <div class="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
            <div class="status">
              <label for="">Alterar status para:</label>
              <select class="" name="">
                <option value="">Bastão recebido</option>
              </select>
            </div>
            <img src="../assets/iconeRelogio.png" class="imagemRelogioTempo"/>
            <div class="tempoAtivacao">
              <label for="">Tempo de Ativação:</label>
              <span>18 dias</span>
            </div>
            <div class="classeResponsavel">
              <div class="selectReponsavel">
                <div class="imgSelectResponsavel">
                  <img src="../assets/foto01.png">
                </div>
                <span class="spanTextoAltera">Alterar responsável para:</span>
                <div class="divMulti">
                  <multiselect v-model="value" :options="options"
                  :max-height="150" track-by="title" :custom-label="customLabel" :show-labels="false" :searchable="false"
                  :hide-selected="true">
                      <template slot="option" scope="props">
                          <img class="option__image" :src="props.option.img">
                          <div class="option__desc"><span class="option__title">{{ props.option.title }}</span><span class="option__small">{{ props.option.desc }}</span></div>
                      </template>
                  </multiselect>
                </div>
              </div>
            </div>
          </div>

          <div class="modal-body">

            <div class="divContent">
              <div class="DadosEmpresa">
                <div class="NomePontos">
                  <span class="descricaoEmpresa">SAMED</span><br>
                  <span class="pontos">18,75 pontos</span>
                  <div class="imgInterrogacao" v-show="!pontos" @click="tabelaPontos">
                    ?
                  </div>
                  <div class="ImgInterrogacaoAtiva" v-show="pontos" @click="tabelaPontos">
                    ?
                  </div>
                  <div class="detalhesPontos" v-show="pontos">
                    <table>
                      <tr>
                        <td class="tdEsquerda"><span>5 médicos</span></td>
                        <td class="tdDireita"><span>18,0 pts</span></td>
                      </tr>
                      <tr>
                        <td class="tdEsquerda"><span>80 procedimentos</span></td>
                        <td class="tdDireita"><span>22,0 pts</span></td>
                      </tr>
                      <tr>
                        <td class="tdEsquerda"><span>Conversão de dados</span></td>
                        <td class="tdDireita"><span>5,0 pts</span></td>
                      </tr>
                      <tr>
                        <td class="tdEsquerda tdTotal"><span>Total</span></td>
                        <td class="tdDireita tdTotal"><span>45,0 pts</span></td>
                      </tr>
                    </table>
                  </div>
                </div>
                <div class="divDadosResponsavel">
                  <span>Responsável:</span>
                  <h4>Thalys dos Reis Guimarães</h4>
                  <span>(34)9 9151 7110</span><br>
                  <span>eu@thalysguimaraes.com</span>
                </div>
              </div>
                <div class="taskList">
                  <h3>Bastão Recebido</h3>
                  <span>Checklist</span>
                  <ul>
                    <li class="taskDone">
                      <img src="../assets/taskDone.png">
                      <span>Recebimento de Bastão</span>
                    </li>
                    <li class="taskNotDone">
                      <img src="../assets/taskUndone.png">
                      <span>Definir analista responsável</span>
                    </li>
                    <li class="taskNotDone">
                      <img src="../assets/taskUndone.png">
                      <span>Adicionar item de checklist</span>
                    </li>
                  </ul>
                </div>
                <div class="addComentario">
                  <h4>Adicionar comentário</h4>
                  <div class="campoComentario">
                    <img src="../assets/foto02.png">
                    <textarea name="name" rows="6" cols="45"></textarea>
                    <button type="button" name="button">Comentar</button>
                  </div>
                </div>
                <div class="containerListComentarios">
                  <h4>Comentários</h4>
                  <div class="listComentarios">
                    <img src="../assets/foto01.png">
                    <div class="nomeComentario">
                      <label>Rafaela Lima</label>
                      <span>12:23 - 01/01/2017 (há 3 dias)</span>
                    </div>
                    <div class="containerComentario">
                      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </div>
                    <div class="containerComentario">
                      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </div>
                    <div class="containerComentario">
                      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </div>
                    <div class="containerComentario">
                      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
                    </div>
                  </div>
                </div>
              </div>

              <div class="divTags">
                <div class="cabecalhoTag">
                  <img src="../assets/tag.png">
                  <label for="">Tags</label>
                </div>
                <div class="listaTags">
                  <div class="tagEmpresa">
                    <img src="../assets/iconeFecharTag.png">
                    <span>Alta complexidade</span>
                  </div>
                  <div class="tagEmpresa2">
                    <img src="../assets/iconeFecharTag.png">
                    Conversão de dados
                  </div>
                </div>
                <div class="botoesTag">
                  <div class="botaoAddTag">
                    <img src="../assets/iconeMais.png" class="mais" alt="">
                    <span>Adicionar tag</span>
                    <img src="../assets/iconeSeta.png" alt="" class="seta">
                  </div>
                  <div class="botaoStandBy">
                    <img src="../assets/iconeStandBy.png" alt="">
                    <span>Colocar em standby</span>
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
  data() {
    return {
      options: [{title:'Anonimo', img:'src/assets/img/no-photo.png'},
                {title:'Anonimo2', img:'src/assets/img/no-photo.png'},
                {title:'Anonimo3', img:'src/assets/img/no-photo.png'}
      ],
      value: {title:'Anonimo', img:'src/assets/img/no-photo.png'},
      pontos: false
    }
  },
  methods: {
    customLabel(title) {
      return `${title}`;
    },
    tabelaPontos() {
      this.pontos = !this.pontos;
    }
  }
}
</script>

<style src="vue-multiselect/dist/vue-multiselect.min.css"></style>

<style>

  @font-face {
    font-family: open-sans-regular;
    src: url('../fonts/OpenSans-Regular.ttf');
  }

  @font-face {
    font-family: open-sans-bold;
    src: url('../fonts/OpenSans-Bold.ttf');
  }

  @font-face {
    font-family: open-sans-extra-bold;
    src: url('../fonts/OpenSans-ExtraBold.ttf');
  }

  @font-face {
    font-family: open-sans-semi-bold;
    src: url('../fonts/OpenSans-Semibold.ttf');
  }

  @font-face {
    font-family: open-sans-light;
    src: url('../fonts/OpenSans-Light.ttf');
  }

  .modal-header .imagemRelogioTempo {
    width: 18px;
    height: 21px;
    position: relative;
    top: 19px;
    left: 25px;
  }

  .detalhesPontos {
    background-image: url("../assets/DetalhesPontos.png");
    height: 130px;
    width: 346px;
    position: absolute;
    top: 96px;
    left: 770px;
  }

  .detalhesPontos table{
    width: 273px;
    height: 88px;
    position: relative;
    left: 46px;
    top: 14px;
    font-family: open-sans-regular;
    font-size: 14px;
    color: #605959;
  }

  .tdTotal {
    color: #d97575;
  }
  .tdDireita {
    text-align: right;
  }
  .tdEsquerda {
    text-align: left;
  }
  .modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .5);
    display: table;
    transition: opacity .3s ease;
  }

  .modal-wrapper {
    display: table-cell;
    vertical-align: middle;
  }

  .modal-header {
    height: 81px;
    display: inline-flex;
    border-bottom: 1px solid #A0AFC0;
    width: 720px;
    margin: 0;
  }

  .modal-container {
    width: 720px;
    margin: 0 auto;
    padding-top: 15px;
    padding-bottom: 5px;
    background: #fff;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
    transition: all .3s ease;
    border-radius: 8px;
  }

  .status {
    width: 191px;
    font-family: open-sans-regular;
    font-size: 13px;
    color: #605959;
    padding-left: 30px;
  }

  .status select {
    width: 191px;
    height: 39px;
    background-color: #EFF0F3;
    border: 1px solid #BDBDBD;
    font-size: 13px;
    line-height: 18px;
    color: #605959;
  }

  .tempoAtivacao {
    width: 130px;
    position: relative;
    left: 30px;
    top: 10px;
  }

  .tempoAtivacao label {
    font-size: 13px;
    line-height: 18px;
    color: #605959;
    font-family: open-sans-regular;
  }

  .tempoAtivacao span {
    font-family: open-sans-semi-bold;
    font-size: 15px;
    font-weight: 600;
    line-height: 20px;
    color: #605959;
  }

  .selectReponsavel {
    width: 275px;
    height: 60px;
    border: 1px solid #DCDCDC;
    border-radius: 3px;
    background-color: #EFF0F3;
  }

  .imgSelectResponsavel {
    width: 52px;
    height: 57px;
    background-color: #EFF0F3;
  }

  .imgSelectResponsavel img {
    width: 100%;
    height: 60px;
  }

  .multiselect {
    width: 228px;
    height: 55px;
    bottom: 61px;
  }

  .multiselect__tags,.multiselect__single {
    background-color: #EFF0F3;
  }

  .divMulti{
    position: relative;
    top: 5px;
    left: 48px;
    height: 55px;
    width: 275px;
  }

  .multiselect--active {
    width: 100%;
  }

  .spanTextoAltera {
    position: relative;
    bottom: 54px;
    left: 61px;
    font-size: 13px;
    line-height: 18px;
    color: #605959;
    font-weight: normal;
  }

  .classeResponsavel {
    position: relative;
    left: 48px;
  }

  .divTags {
    width: 25%;
    background-color: #EFF0F3;
    -webkit-flex: 1;
    -ms-flex: 1;
    -webkit-box-flex: 1;
    -moz-box-flex: 1;
    flex: 1;
  }

  .modal-body {
    display: flex;
  }

  .DadosEmpresa {
    display: flex;
    border-bottom: 1px solid #DFDFDF;
    height: 32%;
    padding-bottom: 12px;
  }

  .divContent {
      flex: 2;
      margin-left: 27px;
      margin-top: 14px;
      padding-bottom: 13px;
      margin-right: 32px;
      height: 100%;
  }

  .NomePontos {
    -webkit-box-flex: 2;
    flex: 2;
  }

  .divDadosResponsavel {
    flex: 2;
    margin-left: 79px;
  }

  .divDadosResponsavel span {
    font-size: 12px;
    font-family: open-sans-regular;
    line-height: 15px;
    color: #605959;
  }

  .divDadosResponsavel h4 {
    margin: 3px;
    margin-left: 0;
    font-family: open-sans-regular;
    color: #605959;
    font-size: 12px;
  }

  .imgInterrogacao {
    width: 19px;
    height: 19px;
    position: relative;
    bottom: 22px;
    left: 120px;
    background-color: #A4AABB;
    border-radius: 11px;
    padding: 2px;
    text-align: center;
    color: #fff;
  }


  .ImgInterrogacaoAtiva {
    border-radius: 11px;
    padding: 2px;
    text-align: center;
    color: #A4AABB;
    border: 1px solid #A4AABB;
    background-color: #fff;
    width: 19px;
    height: 19px;
    position: relative;
    bottom: 22px;
    left: 120px;
  }



  .descricaoEmpresa {
    font-size: 26px;
    font-family: open-sans-semi-bold;
    color: #605959;
  }

  .pontos {
    font-family: open-sans-regular;
    font-size: 18px;
    color: #605959;
  }

  .cabecalhoTag {
    padding-left: 24px;
    padding-top: 31px;
  }

  .cabecalhoTag label {
    font-family: open-sans-semi-bold;
    font-size: 15px;
    line-height: 20px;
    color: #605959;
  }

  .cabecalhoTag img {
    position: relative;
    top: 3px;
  }

  .listaTags {
    padding-top: 20px;
    padding-left: 25px;
    font-family: open-sans-regular;
    font-size: 14px;
    color: #fff;
    line-height: 20px;
  }

  .tagEmpresa {
    border-radius: 2px;
    background-color: #D87171;
    display: inline-block;
    padding: 4px 9px 5px 8px;
    padding-top: 5px;
    padding-right: 9px;
    padding-bottom: 7px;
    margin-bottom: 7px;
  }

  .tagEmpresa2 {
    border-radius: 2px;
    background-color: #54BEAC;
    display: inline-block;
    padding: 4px 9px 5px 8px;
    margin-bottom: 7px;
  }

  .listaTags img {
    width: 13px;
    height: 13px;
    position: relative;
    bottom: 12px;
    left: 100%;
  }

  .botaoAddTag {
    width: 175px;
    height: 39px;
    background-color: #34BB91;
    border-radius: 8px;
    margin-left: 24px;
    margin-bottom: 8px;
  }

  .botaoAddTag span {
    color: #fff;
    font-family: open-sans-regular;
    font-size: 14px;
    left: 20px;
    position: relative;
    top: 5px;
  }

  .botaoAddTag .mais {
    position: relative;
    top: 10px;
    left: 11px;
  }

  .seta {
    position: relative;
    top: 8px;
    left: 43px;
  }

  .botaoStandBy {
    width: 175px;
    height: 39px;
    background-color: #959AA4;
    border-radius: 8px;
    color: #fff;
    margin-left: 24px;
  }

  .botaoStandBy span {
    font-family: open-sans-regular;
    font-size: 14px;
    left: 13px;
    position: relative;
    top: 3px;
  }

  .botaoStandBy img {
    position: relative;
    left: 11px;
    top: 8px;
  }

  .botoesTag {
    margin-top: 32px;
  }

  .taskList {
    overflow-y: scroll;
    margin-top: 17px;
    height: 178px;
  }

  .taskList h3 {
    margin-bottom: 0;
    margin-top: 0;
    color: #605959;
    font-family: open-sans-semi-bold;
    font-size: 16px;
  }

  .taskList span {
    color: #5f697a;
    font-size: 12px;
    font-family: open-sans-regular;
  }

  .taskList ul {
    list-style: none;
    padding: 0;
  }
  .taskList li {
    margin-bottom: 15px;
  }

  .taskDone {
    font-size: 14px;
    font-family: open-sans-regular;
    color: #605959;
  }

  .taskDone img {
    position: relative;
    top: 6px;
  }

  .taskDone span {
    margin-left: 8px;
    line-height: 19px;
    text-decoration: line-through;
  }

  .taskNotDone {
    font-family: open-sans-regular;
    font-size: 14px;
    line-height: 19px;
    color: #605959;
  }

  .taskNotDone span {
    margin-left: 8px;
  }

  .taskNotDone img {
    position: relative;
    top: 6px;
  }

  .addComentario {
    margin-top: 34px;
    border-top: 1px solid #DFDFDF;
  }

  .addComentario h4{
    margin-bottom: 16px;
    font-family: open-sans-regular;
    font-size: 14px;
    line-height: 19px;
    color: #605959;
    font-weight: normal;
  }

  .campoComentario img {
    border-radius: 10px;
    width: 35px;
    height: 34px;
    position: relative;
    bottom: 62px;
  }

  .campoComentario textarea {
    resize: none;
    border: 1px solid #C8C8C8;
    border-radius: 8px;
    margin-left: 19px;
    background-color: #EFF0F3;
  }

  .campoComentario button {
    width: 91px;
    height: 36px;
    background-color: #25B485;
    border: 1px solid #25B485;
    border-radius: 8px;
    color: #fff;
    font-family: open-sans-semi-bold;
    position: relative;
    left: 350px;
    top: 4px;
  }

  .containerListComentarios {
    margin-top: 27px;
    border-top: 1px solid #DFDFDF;
  }

  .containerListComentarios h4 {
    font-size: 14px;
    font-family: open-sans-regular;
    line-height: 19px;
    color: #605959;
    font-weight: 400;
  }

  .containerComentario {
    width: 384px;
    background-color: #EFF0F3;
    border: 1px solid #C8C8C8;
    border-radius: 8px;
    box-sizing: border-box;
    margin-left: 56px;
    padding: 10px;
    font-size: 14px;
    line-height: 21px;
    color: #827D7D;
    font-family: open-sans-regular;
    font-weight: 400;
  }

  .nomeComentario label {
    margin-left: 60px;
    font-size: 14px;
    font-family: open-sans-regular;
    font-weight: 600;
    line-height: 21px;
    color: #2570B3;
  }

  .nomeComentario span {
    font-size: 10px;
    line-height: 21px;
    color: #8B8B8B;
  }

  .listComentarios img {
    position: relative;
    top: 42px;
  }


  ::-webkit-scrollbar-track {
      background-color: #F4F4F4;
  }
  ::-webkit-scrollbar {
      width: 6px;
      background: #F4F4F4;
  }
  ::-webkit-scrollbar-thumb {
      background: #dad7d7;
  }

</style>
