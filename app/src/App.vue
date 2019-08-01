<template>
  <div id="app">
    <!-- <b-navbar toggleable="sm" type="dark" variant="info">
      <b-navbar-brand href="#">NavBar</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#">Link</b-nav-item>
          <b-nav-item href="#" disabled>Disabled</b-nav-item>
        </b-navbar-nav>

        Right aligned nav items
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
            <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
          </b-nav-form>

          <b-nav-item-dropdown text="Lang" right>
            <b-dropdown-item href="#">EN</b-dropdown-item>
            <b-dropdown-item href="#">ES</b-dropdown-item>
            <b-dropdown-item href="#">RU</b-dropdown-item>
            <b-dropdown-item href="#">FA</b-dropdown-item>
          </b-nav-item-dropdown>

          <b-nav-item-dropdown right>
            Using 'button-content' slot
            <template slot="button-content">
              <em>User</em>
            </template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>-->

    <div>
      <b-nav tabs align="end">
        <b-nav-item active>Active</b-nav-item>
        <b-nav-item>Link</b-nav-item>
        <b-nav-item>Another Link</b-nav-item>
        <b-nav-item disabled>Disabled</b-nav-item>
      </b-nav>
    </div>

    <b-container class="bv-example-row">
      <b-row>
        <b-col
          col-sm="4"
        >Lorem ipsum dolor sit amet consectetur, adipisicing elit. Eveniet qui minima, repudiandae beatae veniam reiciendis quaerat asperiores suscipit quidem inventore pariatur, doloremque ad rem ipsa placeat, delectus assumenda dolor aliquam!</b-col>
        <b-col
          col-sm="4"
        >Lorem ipsum dolor sit amet consectetur, adipisicing elit. Labore tempora quas officia sed ipsa illum eius. Dolorem officiis maxime nemo consectetur, corrupti earum aperiam nihil? Neque explicabo debitis accusamus deleniti.</b-col>
        <b-col
          col-sm="4"
        >Lorem ipsum dolor sit amet consectetur adipisicing elit. Aspernatur dolores hic iure architecto, eveniet ab quidem quo pariatur omnis odio fugiat fuga neque quod explicabo dicta natus vitae non quas.</b-col>
      </b-row>

      <b-row align-h="center" align-v="center" class="height">
        <b-col>
          <b-button variant="primary">Primary Button</b-button>
        </b-col>
        <b-col>
          <b-button variant="success">Success Button</b-button>
        </b-col>
        <b-col>
          <b-button variant="dark">Dark Button</b-button>
        </b-col>
      </b-row>

      <b-row align-v="center" class="height">
        <b-col>
          <b-button variant="outline-primary">Primary Button</b-button>
        </b-col>

        <b-col>
          <b-button variant="outline-success" @click="showAlert">Success Button</b-button>

          <b-alert
            :show="dismissCountDown"
            dismissible
            variant="warning"
            @dismissed="dismissCountDown=0"
            @dismiss-count-down="countDownChanged"
          >
            <p>This alert will dismiss after {{ dismissCountDown }} seconds...</p>
            <b-progress variant="warning" :max="dismissSecs" :value="dismissCountDown" height="4px"></b-progress>
          </b-alert>
        </b-col>

        <b-col>
          <b-button variant="outline-dark" @click="handleClick">Dark Button</b-button>
        </b-col>
      </b-row>
    </b-container>

    <!-- Form template -->
    <div>
      <b-form @submit="onSubmit" @reset="onReset" v-if="show">
        <b-form-group
          id="input-group-1"
          label="Email address:"
          label-for="input-1"
          description="We'll never share your email with anyone else."
        >
          <b-form-input
            id="input-1"
            v-model="form.email"
            type="email"
            required
            placeholder="Enter email"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
          <b-form-input id="input-2" v-model="form.name" required placeholder="Enter name"></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Food:" label-for="input-3">
          <b-form-select id="input-3" v-model="form.food" :options="foods" required></b-form-select>
        </b-form-group>

        <b-form-group id="input-group-4">
          <b-form-checkbox-group v-model="form.checked" id="checkboxes-4">
            <b-form-checkbox value="me">Check me out</b-form-checkbox>
            <b-form-checkbox value="that">Check that out</b-form-checkbox>
          </b-form-checkbox-group>
        </b-form-group>

        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
      </b-form>

      <b-card class="mt-3" header="Form Data Result">
        <pre class="m-0">{{ form }}</pre>
      </b-card>
    </div>
    <!-- Modals -->
    <div>
      <b-button v-b-modal.modal-1>Launch demo modal</b-button>

      <b-modal id="modal-1" title="Custom Dialog box">
        <p class="my-4">Hello from modal!</p>
      </b-modal>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      form: {
        email: "",
        name: "",
        food: null,
        checked: []
      },
      foods: [
        { text: "Select One", value: null },
        "Carrots",
        "Beans",
        "Tomatoes",
        "Corn"
      ],
      show: true,
      dismissSecs: 10,
      dismissCountDown: 0,
      showDismissibleAlert: false
    };
  },
  methods: {
    handleClick() {
      alert(`Hello`);
    },
    countDownChanged(dismissCountDown) {
      this.dismissCountDown = dismissCountDown;
    },
    showAlert() {
      this.dismissCountDown = this.dismissSecs;
    },
    onSubmit(evt) {
      evt.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      (this.form.email = "")((this.form.name = ""))((this.form.food = null))(
        (this.form.checked = [])
      )(
        // Trick to reset/clear native browser form validation state
        (this.show = false)
      );
      this.$nextTick(() => {
        this.show = true;
      });
    }
  }
};
</script>

<style>
.height {
  min-height: 5rem;
  background-color: beige;
}
</style>
