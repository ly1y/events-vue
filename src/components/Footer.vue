<template>
    <section id="footer">
        <div class="container">
    <form @submit.prevent="submitForm">
      <div class="input-container">
            <input class="input-email" v-model="email" type="email" placeholder="Enter your Email and get notified" required>
            <button type="submit">→</button>
        </div>
    </form>
        </div>
        <div v-if="successPopup || errorPopup" class="overlay" @click="closePopup"></div>

        <div v-if="successPopup" class="popup success">
           
            <span class="icon-close" @click="closePopup">&times;</span>
            <p class="successTitle">{{ successTitle }}</p> 
            <p class="successMessage">{{ successMessage }}</p>
            <button class="btn-close" @click="closePopup">Close</button>
        </div>

   <div v-if="errorPopup" class="popup error">
    <p class="errorTitle">{{ errorTitle }}</p>
    <p class="errorMessage">{{ errorMessage }}</p>
   </div>
         
    </section>
</template>


<script>
export default {
  name: 'App',
  data() {
    return {
      email: '',
      successPopup: false,
      errorPopup: false,
      successTitle: '',
      successMessage: '',
      errorTitle: '',
      errorMessage: '',
      visible: Boolean,
      
    };
  },
  methods: {
    sendRequest(method, url, body) {
      const headers = {
        'Content-Type': 'application/json'
      };


      const fakeResponse = {
        success: true,
        messageTitle: 'SUCCESS!',
        message: 'You have successfully subscribed to the email newsletter'
      };

      const delay = 1000; 

      return new Promise((resolve, reject) => {
        setTimeout(() => {
          resolve(fakeResponse);
        }, delay);
      });
    },
    submitForm() {
      const requestURL = 'https://example.com/subscribe';
      const body = { email: this.email };

      this.sendRequest('POST', requestURL, body)
        .then(data => {
          this.successTitle = data.messageTitle;
          this.successMessage = data.message;
          this.successPopup = true;
        })
        .catch(err => {
          this.errorTitle = 'Error'
          this.errorMessage = 'There was a problem with the fetch operation: ' + err;
          this.errorPopup = true;
        });
    },
    closePopup() {
      this.successPopup = false;
      this.errorPopup = false;
    }
  }
};
</script>
<style>
#footer{
  position: fixed;
        left: 0;
        bottom: 0;
        width: 100%;
        background-color: rgba(22, 44, 78, 1);
        color: white;
        display: flex;
    justify-content: center;
    align-items: center;
}

.container {
        padding: 20px;
    }

    .input-email{
    border-radius: 40px;
    background-color: #fff;
    padding: 16px 55px 16px 27px; 
    border: none;
    text-decoration: none;
    width: 440px;
    height: 59px;
    box-sizing: border-box;
    position: relative;
}

.input-email::placeholder {
    font-size: 18px;
    color: rgba(0, 0, 0, 0.6);
}

.input-container {
    position: relative;
}

.input-container button {
    position: absolute;
    right: 8px;
    top: 50%;
    transform: translateY(-50%); 
    width: 43px;
    height: 43px;
    padding: 0; 
    background-color: red;
    color: white;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    font-size: 16px;
    line-height: 43px; 
    text-align: center;
}

.overlay {
    position: fixed;
    top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(22, 44, 78, 0.6);
  z-index: 999;
}

.popup {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px;
  background-color: #fff;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
    flex-direction: column;
    align-items: center;
  z-index: 1000;
}
.success, .error {
 text-align: center;
 margin: 0 auto;
 width: 320px;
 height: 370px;
 background-color: #fff;
 text-align: center;
}

.successTitle,.errorTitle{
    margin-top: 97px;
    margin-bottom: 28px;
    font-weight: bold;
    font-size: 36px;
    line-height: 104%;
    color: rgba(22, 44, 78, 1);
}

.successMessage, .errorMessage{
    margin-bottom: 29px;
    font-weight: normal;
    font-size: 16px;
    line-height: 150%;
    color: rgba(0, 0, 0, 0.8);
}
.btn-close{
    background: rgba(29, 65, 105, 1);
    color: #fff;
    border-radius: 40px;
    font-size: 18px;
    line-height: 150%;
    padding: 16px 74px;
  text-align: center;
    margin-top: 10px;
    cursor: pointer;
}

.icon-close {
  position: absolute;
    top: 10px;
    right: 10px;
    cursor: pointer;
  font-size: 56px;
  color: #999;
}

.icon-close:hover {
  color: #000;
}

@media screen and (max-width: 360px) and (max-height: 812px) {
  .input-email{
    width: 280px;
    padding: 10px 20px;
  }

  .input-email::placeholder {
    font-size: 14px;
    line-height: 150%;
}

@media (max-width: 768px) and (max-width:1024px) {
  .input-email{
    width: 360px;
    height: 41px;
    
}
}
}

</style>