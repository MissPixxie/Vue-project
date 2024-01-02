<template>
  <div class="mainHomeView">
    <div class="citat">
      <p>
        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque
        volutpat orci ac mi maximus, id malesuada ante interdum. Nunc vehicula
        sapien nibh, a auctor lacus pretium id. Vestibulum tincidunt posuere
        velit eu pellentesque. Cras quis lacus dolor. Donec nec feugiat nisl, a
        congue purus."
      </p>
    </div>
    <div class="email">
      <h3>Subscribe</h3>
      <div class="input">
        <input class="input-field" type="text" name="email" />
        <i class="fa fa-arrow-right icon"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
};
</script>

<style scoped>
.mainHomeView {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-image: url(../assets/bilder/drew-beamer-bTN-zKFy9uA-unsplash.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  min-height: 80vh;
  font-family: "Taviraj", serif;
}

.citat {
  margin-top: 7%;
  padding: 2%;
  font-style: italic;
  width: 50%;
  background-color: rgba(0, 0, 0, 0.418);
  color: white;
  font-size: 1.3em;
  text-shadow: 2px 2px #000;
  animation-name: fade;
  animation-duration: 3s;
}
@keyframes fade {
  0% {
    opacity: 0%;
  }
  100% {
    opacity: 100%;
  }
}
.email {
  margin-top: 1%;
  padding-bottom: 2%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  background-color: rgba(0, 0, 0, 0.418);
  width: 50%;
  font-family: "Taviraj", serif;
  animation-name: fade;
  animation-duration: 4s;
}
.email h3 {
  font-size: 1.5em;
}

.input {
  flex-grow: 1;
}

.input-field {
  padding: 1% 3% 1% 3%;
  color: white;
  background-color: rgba(0, 0, 0, 0.418);
  font-size: 1.3em;
  border-radius: 5px;
  width: 50%;
  outline: none;
}
.input-field:focus {
  border: 2px solid #cf8205;
  background-color: rgba(0, 0, 0, 0.774);
}
.icon {
  padding: 1% 3% 1% 3%;
  font-size: 1.6em;
  color: white;
  background-color: rgba(0, 0, 0, 0.774);
  border-radius: 5px;
  cursor: pointer;
  transition: 0.6s ease;
}
.icon:hover {
  color: #cf8205;
  background-color: rgba(0, 0, 0, 0.753);
}

@media screen and (max-width: 750px) {
  .citat {
    width: 90%;
  }
  .email {
    width: 90%;
  }
}
</style>
