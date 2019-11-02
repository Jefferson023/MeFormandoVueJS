<template>
  <div class="animated fadeIn">
  
    <b-row>
      <b-col md="12">
  
        <b-card>
          <div slot="header">
            <strong>Dados</strong>
          </div>
          <b-form>
            <b-form-group
              description="Escreva seu nome completo."
              label="Nome completo"
              label-for="basicName"
              :label-cols="3"
              >
              <b-form-input id="basicName" type="text" autocomplete="name"></b-form-input>
            </b-form-group>
            <b-form-group
              
              label="CPF"
              label-for="basicName"
              :label-cols="3"
              >
              <b-form-input id="cpf" type="text" autocomplete="cpf"></b-form-input>
            </b-form-group>
            <b-form-group
              label="Turma"
              label-for="basicStatic"
              :label-cols="3"
              >
                <b-input-group>
                  <b-form-input plaintext id="turma" type="text" value="Turma X" ></b-form-input>
                  <b-button type="submit" size="sm" variant="danger"><i class="fa fa-dot-circle-o"></i> Sair da turma</b-button>
                </b-input-group>
              
            </b-form-group>
              
            <b-form-group
              label="Data de nascimento" label-for="date"
              :label-cols="3"
              >
              <b-form-input type="date" id="date"></b-form-input>
            </b-form-group>
            <b-form-group

              label="E-mail"
              label-for="basicEmail"
              :label-cols="3"
              >
              <b-form-input id="basicEmail" type="email" placeholder="Digite seu email" autocomplete="email"></b-form-input>
            </b-form-group>
            <b-form-group
              label="Digite sua Senha"
              label-for="basicPassword"
              :label-cols="3"
              >
              <b-form-input id="basicPassword" type="password" placeholder="Digite sua senha" autocomplete="current-password"></b-form-input>
            </b-form-group>
            <b-form-group
              label="Confirme sua senha"
              label-for="basicPassword"
              :label-cols="3"
              >
              <b-form-input id="basicPasswordConfirm" type="password" placeholder="Confirme sua senha" autocomplete="current-password"></b-form-input>
            </b-form-group>
            <b-form-group
              label="Cargo"
              label-for="basicInputDisabled"
              :label-cols="3"
              >
              <b-form-input id="basicInputDisabled" type="text" :disabled="true" placeholder="Comissão"></b-form-input>
            </b-form-group>
          
            <div slot="footer">
              <b-button type="submit" size="sm" variant="primary"><i class="fa fa-dot-circle-o"></i> Confirmar</b-button>
              
            </div>
          </b-form>
      
        </b-card>
       
      </b-col>
 
    </b-row>

  </div>
</template>

<script>
export default {
  name: 'forms',
  data () {
    return {
      selected: [], // Must be an array reference!
      show: true
    }
  },
  methods: {
    click () {
      // do nothing
    }
  }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
