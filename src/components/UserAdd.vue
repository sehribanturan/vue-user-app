<template>
  <button id="show-modal" @click="showModal = true" class="btn-modal">ADD USER</button>

  
    <!-- use the modal component, pass in the prop -->
    <Modal :show="showModal" @close="showModal = false">
      <template #header>
        <div >
          <div>
            <div class="container">
              <h4>Add New User</h4>
              <div class="data">
                <label class="label" for="name">NAME:</label>
                <input type="text" id="name" class="input" name="name" placeholder=" name" v-model="nameData">
              </div>
              <div class="data">
                <label class="label" for="name">USERNAME:</label>
                <input type="text" id="name" class="input" name="username" placeholder=" username" v-model="usernameData">
              </div>
              <div class="data">
                <label class="label" for="phone">PHONE:</label>
                <input type="text" id="phone" class="input" name="phone" placeholder=" phone number" @input="acceptNumber"
                  v-model="phoneData">

              </div>
              <div class="data">
                <label class="label" for="email">E-MAIL:</label>
                <input type="email" for="email" id="email" class="input" name="email"
                  placeholder=" e-mail" @blur="validateEmail" required v-model="emailData">
                <br />
              </div>
              <span v-if="msg">{{msg}}</span>

              <div class="">
                <button class="btn" @click="checkInfo">ADD</button>
              </div>
            </div>
          </div>
        </div>
      </template>
    </Modal>


</template>
  
  <script>
  import Modal from './Modal.vue'
  export default {
    data() {
      return {
        nameData: '',
        usernameData: '',
        phoneData: '',
        emailData: '',
        showModal: false,
        msg: "",
        
      }
    },
    components: {
      Modal
    },
    watch: {
      email(value) {
        // binding this to the data value in the email input
        this.emailData = value;
        this.validateEmail(value);
      }
    },
    methods: {
      validateEmail() {
        if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.emailData)) {// eslint-disable-line no-useless-escape
          this.msg = '';
        } else {
          this.msg = 'Please enter a valid email address';
        }
      },
      acceptNumber() {
        var x = this.phoneData.replace(/\D/g, '').match(/(\d{0,3})(\d{0,3})(\d{0,4})/);
        this.phoneData = !x[2] ? x[1] : '(' + x[1] + ') ' + x[2] + (x[3] ? '-' + x[3] : '');
      },
  
      checkInfo() {
        if (this.msg == "" && this.phoneData.length == 14) {
          this.$emit('addUser', { name: this.nameData, username: this.usernameData, phone: this.phoneData, email: this.emailData  })
          this.nameData="",
          this.usernameData="",
          this.phoneData="",
          this.emailData=""
        }
      }
    },
    props: ["users"],
  };
  </script>
  
  <style >
  .btn-modal {
    width: 200px;
    height: 50px;
    appearance: none;
    border: none;
    background: none;
    cursor: pointer;
    color: black;
    background-color:gainsboro;
    border-radius: 8px;
    font-size: 18px;
    font-weight: 500;
    box-shadow: 3px;
    margin-left: 45%;
    margin-top: 30px;
  }

  .container {
    align-items: center;
    margin-top: 30px;
    border-radius: 30px;
  }

  .input {
    border: 1px solid black;
    margin-left: 5px;
  }

 

  </style>

  