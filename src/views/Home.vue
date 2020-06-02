<template>
  <div>
    <h1 title="center">REGISTRO BIBLIOTECARIO</h1>
    <input
      v-model="name"
      placeholder="Escriba un nombre o una descripción"
      type="text"
    />
    <br />
    <br />
    <div class="filter">
      <label
        ><input type="radio" v-model="selectedCategory" value="Books" />
        Books</label
      >
      <label
        ><input type="radio" v-model="selectedCategory" value="Magazines" />
        Magazines</label
      >
      <label
        ><input type="radio" v-model="selectedCategory" value="Newspaper" />
        Newspaper</label
      >
      <label
        ><input type="radio" v-model="selectedCategory" value="Others" />
        Others</label
      >
      <label
        ><input type="radio" v-model="selectedCategory" value="All" />
        All</label
      >
    </div>

    <div v-if="name === ''">
      <ul class="items-list">
        <li :key="item.code" v-for="item in filteredExample">
          <b>Codigo:</b> {{ item.code }} - <b>Nombre:</b> {{ item.name }} -
          <b>Descripcion:</b>
          {{ item.description }}
        </li>
      </ul>
    </div>
    <div v-else>
      <ul class="items-list">
        <li :key="item.code" v-for="item in filteredList">
          <b>Codigo:</b> {{ item.code }} - <b>Nombre:</b> {{ item.name }} -
          <b>Descripcion:</b>
          {{ item.description }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  // Single component
  name: "Home",

  /* components: {
    HelloWorld
  } */

  data() {
    // like "private" properties
    return {
      name: "",
      selectedCategory: "All",
      itemsList: [
        {
          code: 23,
          name: "Economia Naranja",
          description: "Libro sobre el exito de la innovación en empresas",
          category: "Books"
        },
        {
          code: 135,
          name: "Vue for Dummies",
          description: "Guía básica de Vue js",
          category: "Books"
        },
        {
          code: 1520,
          name: "Sport #20",
          description: "Los mejores futbolistas desde el 2000",
          category: "Magazines"
        },
        {
          code: 2671,
          name: "Los Tiempos #34",
          description: "Anonymous aparece de nuevo",
          category: "Newspaper"
        },
        {
          code: 2002,
          name: "Opinion #160",
          description: "Vuelve a trabajar el transporte público en Bolivia",
          category: "Newspaper"
        },
        {
          code: 3134,
          name: "Superman #143",
          description: "Superman vuelve a su planeta natal",
          category: "Others"
        }
      ]
    };
  },

  created() {
    // http://api.com/products/{id}
  },

  mounted() {
    //
  },

  updated() {
    //
  },

  props: {
    // like "public" properties
  },

  computed: {
    filteredList() {
      var vm = this;
      var category = vm.selectedCategory;

      return this.name === ""
        ? this.itemsList
        : this.itemsList.filter(
            item =>
              (item.name.includes(this.name) ||
                item.description.includes(this.name)) &&
              (item.category === category || category === "All")
          );
    },

    filteredExample() {
      var vm = this;
      var category = vm.selectedCategory;

      if (category === "All") {
        return vm.itemsList;
      } else {
        return vm.itemsList.filter(function(item) {
          return item.category === category;
        });
      }
    }
  },

  methods: {
    save() {},
    cancel() {},
    export() {},
    getConcatNameWithGroup() {
      this.save(); // this === vm (view model)
      // this.$forceUpdate(); // $ => vue "instance" => properites, methods, global variables.
      // this.$data.name === this.name
      // return this.name + " new group is: " + this.group;
      // this === vm
      return `${this.name} new group is: ${this.group}`; // string template
    },
    changeName(newName) {
      this.name = newName;
    }
  }
};
</script>

<style scoped>
ul {
  margin-left: 0;
  padding-left: 0;
  list-style: none;
}

li {
  padding: 8px 16px;
  border-bottom: 5px solid;
  background: white;
}
input[type="text"]:focus {
  border: 3px solid #555;
  width: 230px;
}
label {
  color: white;
}
h1 {
  color: white;
}
</style>
