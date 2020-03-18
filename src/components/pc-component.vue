<template>
  <div class="card-body m-1 p-1 pc-background rounded">
    <div class="row">
      <button
        class="col-2 btn pc-pill h6"
        v-bind:class="{ 'en-uso': enuso, 'en-espera': !enuso }"
        title="Click para iniciar o detener"
        @click="accion"
      >
        <strong>{{ pc.name }}</strong>
      </button>
      <div v-if="enuso" class="col-10">
        <div class="row m-2">
          <div class="col p-0 m-0 text-muted small">
            Inicio:
            <br />
            <span class="dato">{{ inicio | moment("h:mm:ss a") }}</span>
          </div>
          <div class="col p-0 m-0 text-muted small">
            {{ secondsToTime(tiempo) }}
            <br />
            <span class="dato">${{ totTiempo }}</span>
          </div>
          <div class="col p-0 m-0 text-muted small">
            {{ impr }}
            <img src="img/printed.png" />:
            <br />
            <span class="dato">${{ totImpr }}</span>
          </div>
          <div class="col p-0 m-0 total">${{ total }}</div>
        </div>
      </div>
      <div v-else class="col-12 text-enespera center">Máquina disponible</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PcComponent",
  props: ["pc"],
  data: function() {
    return {
      enuso: false,
      inicio: 0,
      tiempo: 0,
      impr: 0,
      totImpr: 0,
      interval: ""
    };
  },
  methods: {
    accion: function start() {
      this.enuso = !this.enuso;
      if (this.enuso) {
        this.inicio = new Date();
        this.crono();
      } else {
        clearInterval(this.interval);
        this.tiempo = 0;
        this.props.pc.docs = {};
      }
    },
    crono: function() {
      var vm = this;
      this.interval = setInterval(function() {
        vm.tiempo += 2;
      }, 2000);
    },
    secondsToTime(secs) {
      const date = new Date(0);
      date.setHours(0, 0, secs, 0);
      return date.toLocaleTimeString("es");
    }
  },
  computed: {
    totTiempo: function() {
      return 1 + Math.round((this.tiempo / 3600) * 10);
    },
    total: function() {
      return this.totTiempo + this.totImpr;
    }
  }
};
</script>

<style scoped>
.pc-background {
  background-color: #eee;
}
.pc-pill {
  border-radius: 100px;
  margin-left: -10px;
  margin-top: -10px;
}
.en-uso {
  color: #fff;
  background-color: #33f;
}
.en-espera {
  color: #666;
  background-color: #bfb;
}
.text-enespera {
  color: #bbb;
}
.dato {
  color: #000;
}
.total {
  font-size: 1.3em;
}
</style>
