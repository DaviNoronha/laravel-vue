<template>
     <b-form @submit="onSubmit" @reset="onReset">
      <b-form-group label="Nome:" label-for="nome">
        <b-form-input 
          id="nome"
          v-model="form.nome"
          type="text"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group label="Telefone:" label-for="telefone">
        <b-form-input 
          id="telefonee"
          v-model="form.telefone"
          type="text"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group label="Email:" label-for="email">
        <b-form-input 
          id="email"
          v-model="form.email"
          type="email"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          nome: '',
          telefone: '',
          email: ''
        },
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()
        axios.post('/contatos', this.form)
          .then((res) => {
              this.$store.commit('addContato', res.data)
              this.$swal({
                icon: 'success',
                title: 'Perfeito',
                text: 'Salvo com sucesso!'
          })
        })        
        .catch((err) => {
            alert('Erro ao salvar')
        })
      },
      onReset(evt) {
        evt.preventDefault()
        this.form.nome = ''
        this.form.telefone = ''
        this.form.email = ''
      }
    }
  }
</script>