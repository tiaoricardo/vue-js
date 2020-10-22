<template>
  <div id="app">

    <input	v-model="busca" type="text">
    <p	v-text="resultado"></p>

    <p>Nome	Iniciado:	{{ nome	}}</p>
    <p>Nome	Filtrado:	{{ nome | formataNome }}</p>

    <p>Nome	Computado:	{{	nomeFormatado	}}</p>
    <label>Input	a	computar</label>
    <input	v-model="nomeFormatado" type="text">

    <p>{{	total	}}</p>
    <button	@click="calcula('-')">	-	</button>
    <button	@click="calcula('+')">	+	</button>

    <h1>{{ titulo }}</h1>
    <h2 v-text="subtitulo"></h2>

    <input :disabled="tarefas.length == 0" v-model="subtitulo" />
    <input type="button" value="Limpar" @click="tarefas = []" :disabled="tarefas.length == 0"  />

    <br>
    <br>

    <div  v-if="tarefas.length  <=  0">
      Não há  tarefas
    </div>
    <div  v-else>
      Existem {{tarefas.length}}  tarefas

        <ul>
            <li v-for="tarefa in  tarefas"> {{  tarefa  }}  </li>
        </ul>

    </div>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      nome: 'sebastiao ricardo',
      titulo: 'Lista de Tarefas',
      total: 10,
      subtitulo: 'Defina uma descrição',
      tarefas: ['Estudar Inglês','Fazer as tarefas', 'Programar'],
      resultado:	'',
      busca:	''
    }
  },
  mounted () {
    //setTimeout( () => this.subtitulo = "mudei",2000);
    let x = 0;
  },
  methods:	{
    calcula(	sinal	)	{
      this.total	=	(sinal	==	'-')	?	this.total	-	1	:	this.total	+
        1
    },
    recolheResposta()	{
      let	valor	=	this.busca
      setTimeout(	()	=>	{
        if(valor	==	this.busca)
          this.resultado	=	'Terminou	de	digitar...'
      },	500)
    }
  },
  filters:	{
    formataNome(	valor	)	{
      console.log('executando	filter')
      valor	=	valor.toLowerCase()
      let	corta	=	valor.split(' ')
      let	resultado	=	''
      for	(let	nome	of	corta)
        resultado	+=	nome.charAt(0).toUpperCase()	+	nome.slice(1)	+	' '
      return	resultado
    }
  },
  watch:	{
    busca:	function	(novoValor,	valorAntigo) {
      this.resultado	=	'Aguardando	o	término	da	digitação...'
      this.recolheResposta()
    }
  },
  computed:	{
    nomeFormatado:	{
      get:	function	() {
        console.log('executando	computed')
        return this.nome.toUpperCase()
      },
      set:	function	(novoValor) {
        this.nome	=	novoValor.substring(0,	3)
      }
    }
  }




}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

</style>
