<template>
<StoreTheme/>
</template>

<script>
import StoreTheme from './components/StoreTheme.vue'

export default {
  name: 'App',
  components: {
    StoreTheme
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700&display=swap");
:root {
--body-font: "Poppins", sans-serif;
--first-blue-color: #16263f;
--first-blue-alt-color: #0d1a2f;
--second-blue-color: #3ac2cb;
--third-blue-color: #4084f4;
--middle-blue-color: #36415c;
--dark-blue-color: #040d21;
--dark-chat-color: #122139;
--bluelight-color: #a4b4cb;
--red-color: #f12e67;
--orange-color: rgba(254, 149, 24, 0.5);
--green-color: #34b53a;
--white-color: #fafafa;
--shadow-color: rgb(58 194 203 / 30%);
--border: 1px solid rgb(164 180 203 / 50%);
--border-alt: 0.969px solid #546076;
--placeholder: #546076;
--light-gray: #a4b4cb;
--yellow: #e8c842;
--dark-red-color: #cd1717;
--btn-text: #fff;
--second-gray: #959595;
--dark-input-color: #0e1e44;
--shadow-color-sm: rgb(58 194 203 / 10%);
--red-color-bg: rgba(241, 46, 103, 30%);
--orange-color-bg: rgba(254, 149, 24, 30%);
--green-color-bg: rgba(51, 181, 58, 30%);
--lighter-blue: #202f48;
--light-blue-whith-opacity: rgba(164, 180, 203, 0.1);
--dark-blue-with-opcity: rgba(22, 38, 63, 0.8);
--light-blue-shadow: rgba(164, 180, 203, 0.05);
--thumb: #edf2f4;
--second-dark-with-opacity: rgba(13, 26, 47, 0.5);
--box-shadow: 0px 1.7952675819396973px 3.051954746246338px 0px
rgba(41, 72, 152, 0.01),
0px 7.8991780281066895px 6.319342136383057px 0px rgba(41, 72, 152, 0.02),
0px 19.38888931274414px 12.602778434753418px 0px rgba(41, 72, 152, 0.03),
0px 37.34156799316406px 24.702882766723633px 0px rgba(41, 72, 152, 0.03),
0px 62.8343620300293px 45.42027282714844px 0px rgba(41, 72, 152, 0.04),
0px 96.94445037841797px 77.55555725097656px 0px rgba(41, 72, 152, 0.05);
}

body {
font-family: var(--body-font);
background-color: var(--dark-blue-color);
text-transform: capitalize;
}
</style>
