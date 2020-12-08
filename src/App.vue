<template>
  <div id="app">
    <div class="container py-4">
      <div class="row">
        <div class="col-12 col-md-6 col-lg-4">
          <div class="card">
            <div class="card-body">
              <form>
                <div class="form-group">
                  <label for="name">Имя</label>
                  <input
                    type="text"
                    id="name"
                    v-model="user.name"
                    class="form-control"
                  />
                </div>
                <div class="form-group">
                  <label for="surname">Фамилия</label>
                  <input
                    type="text"
                    id="surname"
                    v-model="user.surname"
                    class="form-control"
                  />
                </div>
                <div class="form-group">
                  <label for="name">Дата рождения</label>
                  <b-form-datepicker
                    id="example-datepicker"
                    v-model="user.birthDate"
                  />
                </div>
                <div class="form-group mb-0">
                  <label for="icon">Иконка</label>
                  <b-dropdown
                    id="icon"
                    text="Иконка"
                    class="d-block"
                    variant="light"
                  >
                    <b-dropdown-item
                      v-for="(select, index) in selectItems"
                      :key="index"
                      @click="user.select = select"
                    >
                      <component :is="getIcon(select)" />
                    </b-dropdown-item>
                  </b-dropdown>
                </div>
              </form>
            </div>
          </div>
        </div>
        <div class="col-12 col-md-6 col-lg-4">
          <div class="card">
            <div class="card-body px-0">
              <ul class="list-group list-group-flush">
                <li class="list-group-item">Имя: {{ user.name }}</li>
                <li class="list-group-item">Фамилия: {{ user.surname }}</li>
                <li class="list-group-item">
                  Дата рождения: {{ user.birthDate }}
                </li>
                <li class="list-group-item">Иконка: {{ user.select }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
import { mapState } from "vuex";
import { BIconStar, BIconHeart, BIconOctagon } from "bootstrap-vue";

export default {
  name: "App",
  components: {
    BIconStar,
    BIconHeart,
    BIconOctagon
  },
  data: () => ({
    user: {
      name: "",
      surname: "",
      birthDate: new Date(),
      select: ""
    }
  }),
  watch: {
    user: {
      handler() {
        if (
          this.user.name &&
          this.user.surname &&
          this.user.birthDate &&
          this.user.select
        ) {
          console.log(JSON.stringify(this.user, null, 2));
        }
      },
      deep: true
    }
  },
  computed: {
    ...mapState({
      selectItems: state => state.selectItems
    })
  },
  methods: {
    getIcon(iconName) {
      return `BIcon${iconName}`;
    }
  }
};
</script>
