<template>
  <section>
    <div class="uk-section uk-section-muted">

      <div class="uk-container uk-container-center uk-text-center">
        <form class="uk-form-stacked ">
          <div class="uk-margin">
            <label class="uk-form-label uk-text-large">Visita Guiada</label>
            <p>Utilize el lector de códigos QR para complementar aún más su experiencia al interior de nuestros espacios. Busca los códigos QR posicionados a un costado de las obras y léelos para recibir contenido descriptivo de estas, a través de texto, audio o video.</p>
          </div>
        </form>

        <div class="pad-top">
          <QrcodeReader
            :paused="paused"
            @decode="onDecode"
            @init="onInit">
            <div v-show="paused" class="validation-layer">

              <div class="validation-notice">
                <div v-if="validating">
                  Verificando el Código QR...
                </div>

                <div v-else-if="isValid" class="text-success">
                  Código QR válido.
                </div>

                <div v-else class="text-danger">
                  Código QR inválido.
                </div>
              </div>

            </div>
            <LoadingIndicator v-show="loading" />
          </QrcodeReader>
        </div>

        

      </div>
    </div>
  </section>
</template>

<script>
import { QrcodeReader } from 'vue-qrcode-reader'
import InitHandler from '@/mixins/InitHandler'

export default {
  name: 'VisitaGuiadaView',
  components: { QrcodeReader },
  mixins: [ InitHandler ],
  data () {
    return {
      isValid: false,
      validating: false,
      paused: false,
      content: null
    }
  },
  methods: {
    async onDecode (content) {
      this.content = content
      this.pauseCamera()
      this.validating = true
      this.isValid = await this.validate(content)
      if(this.isValid == true){
            UIkit.modal.dialog(`
        <button class="uk-modal-close-default" type="button" uk-close></button>
        <div class="uk-modal-header">
            <h2 class="uk-modal-title">Acceder a contenido descriptivo</h2>
        </div>
        <div class="uk-modal-body">
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
        </div>
        <div class="uk-modal-footer uk-text-right">
            <button class="uk-button uk-button-default uk-modal-close" type="button">Cancelar</button>
            <a class="uk-button uk-button-primary" href="`+this.content+`">Acceder</a>
        </div>`)
      }
      this.validating = false
      window.setTimeout(() => {
        this.unPauseCamera()
      }, 2000)
    },
    pauseCamera () {
      this.paused = true
    },
    unPauseCamera () {
      this.paused = false
    },
    validate (content) {
      return new Promise(resolve => {
        window.setTimeout(() => { // pretend it's taking really long
          if (content.startsWith('https://')) {
            resolve(true)
          } else {
            resolve(false)
          }
        }, 3000)
      })
    }
  }
}
</script>

<style scoped>
.validation-layer {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, .9);
  text-align: center;
  padding: 10px;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
}
.validation-notice {
  font-weight: bold;
  font-size: 1.4rem;
}
.pad-top {
  margin-top: 30px !important;
}
</style>