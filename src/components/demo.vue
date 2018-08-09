<template>
<section class="uk-section">
    <form action="" class="uk-form uk-form-width-large uk-margin-auto uk-card uk-card-default uk-padding" v-on:submit.prevent="onSubmit">
        <div>
        <label for="email" class="uk-form-label">Email</label>
        <input type="email" name="email" v-model="email" class="uk-input">
</div>
<div>
    <label for="amount" class="uk-form-label">Amount</label>
    <input type="number" class="uk-number uk-input" v-model="amount">
</div>
<div>
<paystack 
    :amount="amount * 100" 
    :email="email" 
    :paystackkey="paystackkey"
    :reference="reference"
    :callback="callback"
    :close="close"
    :embed="false"></paystack>
</div>
    </form>
    
    </section>
</template>
<script>
import paystack from "vue-paystack";
export default {
  name: "Paystack-demo",
  components: { paystack },
  data() {
    return {
      paystackBtnText: "Submit Transaction",
      paystackkey: "pk_test_c8ecaf63516a5641318043495c4ad8094027069b", //public key
      email: "", //Customer email
      amount: 10 //kobo
    };
  },
  computed:{
      reference(){
          let text="";
          let possible="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
          for(let i=0;i<10;i++){
              text += possible.charAt(Math.floor(Math.random() * possible.length));
          }
          return text;
      }
  },
  methods:{
      callback: function(response){
        console.log(response)
      },
      close: function(){
          console.log("Payment closed")
      }
  }
};
</script>

