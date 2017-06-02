<template>
  <!-- App -->
  <div id="app">

    <!-- Statusbar -->
    <f7-statusbar></f7-statusbar>

   <!-- Main Views -->
    <f7-views>
      <f7-view id="main-view" navbar-through :dynamic-navbar="true" main>

        <!-- Navbar -->
        <f7-navbar back-link="Back" sliding>
          <f7-nav-center sliding>Simple Calculator Bot</f7-nav-center>
        </f7-navbar>

        <!-- Pages -->
        <f7-pages>
          <f7-page>
            
              <!--<f7-list-item>
                <f7-input @keyup.enter="enterChat" type="text" placeholder="Your name" v-model:value="name" />
              </f7-list-item>-->
              <f7-block-title>Welcome to my App</f7-block-title>
            <f7-block inner>
              <p>I am built using Framework7 with Vue.js, Node.js with Express and Wit.ai</p>
            </f7-block>
            <f7-list>
              <f7-list-button v-on:click="enterChat">Enter chat</f7-list-button>

            </f7-list>
          </f7-page>
        </f7-pages>
      </f7-view>
    </f7-views>
  </div>
</template>

<script>
export default {
   data: function () {
        return{}
      },
      //App root methods
      methods: {
        enterChat: function () {
          // if (this.name.trim().length === 0) {
          //   alert("Please enter your name");
          //   return false;
          // }
          //  this.msgs.length = 0;
          this.$f7.mainView.router.load({ url: "/chat/" });
        }
      }
}
</script>