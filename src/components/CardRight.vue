<template>
  <div class="uk-card uk-card-default uk-grid-collapse uk-child-width-1-2@s uk-margin uk-card-hover" uk-grid>
      <div class="uk-flex-last@s uk-card-media-right uk-cover-container">
          <img :src="actividad.attachments[0].guid" alt="" class="img-tamaño-1"
            style="
              max-width: none;
              position: absolute;
              left: 50%;
              top: 50%;
              -webkit-transform: translate(-50%,-50%);
              transform: translate(-50%,-50%);" >
          <canvas width="600" height="300"></canvas>
      </div>
      <div>
          <div class="uk-card-body uk-text-left">
            <div class="uk-card-badge-left uk-label" :style="{ background: actividad.area_color + '!important' }">
              {{ actividad.area }}
            </div>

            <div class="visible-note oculto-note">
              <div class="date centro">
                <span class="month">{{actividad.fecha_inicio_formato_month}}</span>
                <h1 class="day">{{actividad.fecha_inicio_formato_day}}</h1>
              </div>
              <h3 class="uk-card-title sinmar"> {{ actividad.nombre }}</h3>
            </div>

            <div class="visible-movil oculto-movil">
              <div class="uk-grid-small uk-flex-middle" uk-grid>
                <div class="uk-width-auto">
                  <div class="date">
                    <span class="month">{{actividad.fecha_inicio_formato_month}}</span>
                    <h1 class="day">{{actividad.fecha_inicio_formato_day}}</h1>
                  </div>
                </div>
                <div class="uk-width-expand">
                  <h3 class="uk-card-title sinmar"> {{ actividad.nombre }}</h3>
                </div>
              </div>
            </div>  
          
            <p class="uk-text-small uk-text-muted">
              Publicado: {{actividad.creado_el}}.
            </p>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'CardRight',
  props: {
    actividad: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.uk-card-badge-left {
    position: absolute;
    top: 30px;
    left: 30px; 
    z-index: 1;
}
.date {
	display: block;
	width: 100px;
	height: 110px;
	margin: 40px 0px;
	background: #fff;
	text-align: center;
	font-family: 'Helvetica', sans-serif;
	position: relative;
}
.date .binds {
	position: absolute;
	height: 15px;
	width: 60px;
	background: transparent;
	border: 2px solid #999;
	border-width: 0 5px;
	top: -6px;
	left: 0;
	right: 0;
	margin: auto;
}
.date .month {
	background: #555;
	display: block;
	padding: 8px 0;
	color: #fff;
	font-size: 12px;
	font-weight: bold;
	border-bottom: 2px solid #333;
	box-shadow: inset 0 -1px 0 0 #666;
}
.date .day {
	display: block;
	margin: 0;
	padding: 10px 0;
	font-size: 48px;
	box-shadow: 0 0 3px #ccc;
	position: relative;
}
.date .day::after {
	content: '';
	display: block;
	height: 100%;
	width: 96%;
	position: absolute;
	top: 3px;
	left: 2%;
	z-index: -1;
	box-shadow: 0 0 3px #ccc;
}
.date .day::before {
	content: '';
	display: block;
	height: 100%;
	width: 90%;
	position: absolute;
	top: 6px;
	left: 5%;
	z-index: -1;
	box-shadow: 0 0 3px #ccc;
}
.sinmar {
  margin-top: 0px !important;
}
.oculto-note {
  display: none;
  visibility: hidden;
}
.visible-movil {
  display: block;
  visibility: visible;
}
@media only screen and (min-width: 640px) {
  .visible-note {
    display: block;
    visibility: visible;
  }
  .oculto-movil {
    display: none;
    visibility: hidden;
  }
}
.centro{
  margin-left: auto !important;
  margin-right: auto !important;
}
@media only screen and (max-width: 639px) {
  .img-tamaño-1 {
    width: 700px !important;
  }
}
@media only screen and (min-width: 640px) and (max-width: 959px) {
  .img-tamaño-1 {
    height: 500px !important;
  }
}
@media only screen and (min-width: 960px) {
  .img-tamaño-1 {
    height: 600px !important;
  }
}
</style>