<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <input
          type="text"
          v-model.trim="logoSearchTerm"
          placeholder="Search company..."
          @keyup="callLogoApi"
        /><br />
        <ul class="results">
          <li class="item" v-for="person in logoSearchResults" :key="person.name+1">
            <img align="center" :src=person.logo />
            <span className={person.name}>
            {{person.name}}
          </span>
          <span className={person.domain}>
            {{person.domain}}
          </span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      logoSearchTerm: "",
      logoSearchResults: [],
    };
  },
  methods: {
    callLogoApi(event) {
      console.log("-->" + event.target.value);
      fetch("https://autocomplete.clearbit.com/v1/companies/suggest?query=" + event.target.value)
        .then(response => response.json())
        .then((response) => {
          console.log(response);
          this.logoSearchResults = response;
        })
        .catch((error) => console.log(error));
    },
  },
};
</script>

<style>

ul.results{
 width: 100%; /* its width according to input width */
 border:1px solid #ccc;
 height:auto;
 padding:0px;
 margin:0px;
}

ul.results li, 
ul.results li a{
 background-color:#fff;
 color:#000;
 font-size:12px; /* according to your requirement */
 font-family:arial;
 font-weight:normal;
 padding:0 10px;
 margin:0px;
 line-height:25px; /* according to your requirement */
 display:block;
 cursor:pointer;
}

ul.results li:hover,
ul.results li a:hover{
 background-color:#ccc;
 color:#000;
 text-decoration:normal;
}
ul.results li:hover{
 background-color:#FAFFBD;
 border:1px solid #3C8DBC;
}
</style>