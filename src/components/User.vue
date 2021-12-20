<template>
  <v-container>
    <v-row class="my-5">
      <v-col cols="8">
        <h3>Dashboard</h3>
      </v-col>
      <v-col
        cols="4"
        class="text-right"
      >
        <v-dialog
          v-model="dialog"
          persistent
          max-width="600px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="success"
              dark
              v-bind="attrs"
              v-on="on"
            >
              add user
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="mx-2">{{ isEdit ? "Edit User" : "Add User" }}</span>
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-form
                  ref="form"
                  v-model="valid"
                  lazy-validation
                >
                  <v-row>
                    <v-col
                      cols="12"
                      sm="12"
                      md="6"
                    >
                      <span>Name</span>
                      <v-text-field
                        v-model="itemUser.name"
                        outlined
                        dense
                        type="text"
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>
                    <v-col
                      cols="12"
                      sm="12"
                      md="6"
                    >
                      <span>Username</span>
                      <v-text-field
                        v-model="itemUser.username"
                        outlined
                        dense
                        type="text"
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>
                    <v-col
                      cols="12"
                      sm="12"
                      md="12"
                    >
                      <span>Email</span>
                      <v-text-field
                        type="email"
                        v-model="itemUser.email"
                        outlined
                        dense
                        required
                        :rules="emailRules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <h4>Address</h4>
                    </v-col>
                    <v-col
                      cols="6"
                      sm="6"
                      md="4"
                    >
                      <span>street</span>
                      <v-text-field
                        type="text"
                        v-model="itemAddress.street"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>

                    <v-col
                      cols="6"
                      sm="6"
                      md="4"
                    >
                      <span>suite</span>
                      <v-text-field
                        type="text"
                        v-model="itemAddress.suite"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>

                    <v-col
                      cols="6"
                      sm="6"
                      md="4"
                    >
                      <span>city</span>
                      <v-text-field
                        type="text"
                        v-model="itemAddress.city"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>

                    <v-col
                      cols="6"
                      sm="6"
                      md="4"
                    >
                      <span>zipcode</span>
                      <v-text-field
                        type="text"
                        v-model="itemAddress.zipcode"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>

                    <v-col
                      cols="6"
                      sm="6"
                      md="4"
                    >
                      <span>lat</span>
                      <v-text-field
                        type="text"
                        v-model="itemGeo.lat"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>

                    <v-col
                      cols="6"
                      sm="6"
                      md="4"
                    >
                      <span>lng</span>
                      <v-text-field
                        type="text"
                        v-model="itemGeo.lng"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>
                    <v-col
                      cols="12"
                      sm="12"
                      md="6"
                    >
                      <span>Phone</span>
                      <v-text-field
                        v-model="itemUser.phone"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                        type="text"
                      ></v-text-field>
                    </v-col>

                    <v-col
                      cols="12"
                      sm="12"
                      md="6"
                    >
                      <span>Website</span>
                      <v-text-field
                        v-model="itemUser.website"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                        type="text"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12">
                      <h4>Company</h4>
                    </v-col>
                    <v-col
                      cols="12"
                      sm="12"
                      md="12"
                    >
                      <span>name</span>
                      <v-text-field
                        type="text"
                        v-model="itemCompany.name"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>

                    <v-col
                      cols="12"
                      sm="6"
                      md="6"
                    >
                      <span>catchPhrase</span>
                      <v-text-field
                        type="text"
                        v-model="itemCompany.catchPhrase"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>

                    <v-col
                      cols="12"
                      sm="6"
                      md="6"
                    >
                      <span>bs</span>
                      <v-text-field
                        type="text"
                        v-model="itemCompany.bs"
                        outlined
                        dense
                        required
                        :rules="rules"
                        hide-details=""
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-form>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="grey darken-1"
                outlined
                class="text-capitalize"
                @click="closeDialog"
              >
                Close
              </v-btn>
              <v-btn
                color="success"
                outlined
                class="text-capitalize"
                @click="saveUser"
                :disabled="!valid"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
      <v-col cols="12">
        <v-data-table
          :headers="headers"
          :items="items"
          class="elevation-1"
          hide-default-footer
        >
          <template v-slot:item.Address="{ item }">
            <div>{{item.Address.city}}, {{item.Address.street}}, {{item.Address.suite}}, {{item.Address.zipcode}}</div>
          </template>
          <template v-slot:item.Company="{ item }">
            <div>{{item.Company.name}}</div>
          </template>
          <template v-slot:item.Id="{ item }">
            <v-btn
              class="mx-2 text-capitalize"
              color="primary"
              @click="showUserDialog(item.Id)"
            >Edit</v-btn>
            <v-btn
              color="red"
              dark
              class="text-capitalize"
              @click="showConfirmDialog(item.Id)"
            >Delete</v-btn>

          </template>
        </v-data-table>
      </v-col>
      <v-col cols="12">
        <v-dialog
          v-model="confirmDialog"
          persistent
          max-width="350"
        >
          <v-card>
            <v-card-title>Delete</v-card-title>
            <v-card-text>Are you sure you want to delete this item ?</v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                class="text-capitalize"
                color="grey darken-1"
                outlined
                @click="confirmDialog = false"
              >
                Cancel
              </v-btn>
              <v-btn
                class="text-capitalize"
                color="red darken-1"
                outlined
                @click="deleteUser()"
              >
                Delete
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      valid: true,
      id: null,
      isEdit: false,
      dialog: false,
      confirmDialog: false,
      items: [],
      itemGeo: [],
      itemCompany: [],
      itemAddress: [],
      itemUser: [],
      headers: [
        {
          text: "Name",
          sortable: false,
          value: "Name",
        },
        { text: "Username", value: "Username", sortable: false },
        { text: "Email", value: "Email", sortable: false },
        { text: "Address", value: "Address", sortable: false },
        { text: "Phone", value: "Phone", sortable: false },
        { text: "Website", value: "Website", sortable: false },
        { text: "Company", value: "Company", sortable: false },
        { text: "Action", value: "Id", sortable: false },
      ],
      rules: [(v) => !!v || "is required"],
      emailRules: [
        (v) => !!v || "E-mail is required",
        (v) => /.+@.+\..+/.test(v) || "E-mail must be valid",
      ],
    };
  },
  methods: {
    getUsers() {
      axios
        .get("https://jsonplaceholder.typicode.com/users")
        .then((response) => {
          let data = response.data;
          console.log(data);
          this.items = data.map((data) => ({
            Id: data.id,
            Username: data.username,
            Email: data.email,
            Name: data.name,
            Address: data.address,
            Company: data.company,
            Phone: data.phone,
            Website: data.website,
          }));
          console.log(this.items);
        });
    },
    saveUser() {
      if (!this.$refs.form.validate()) {
        return false;
      }

      let data = this.itemUser;
      data.company = this.itemCompany;
      data.address = this.itemAddress;
      data.address.geo = this.itemGeo;
      const headers = {
        "Content-type": "application/json; charset=UTF-8",
      };

      if (this.isEdit) {
        axios
          .put(`https://jsonplaceholder.typicode.com/users/${this.id}`, data, {
            headers: headers,
          })
          .then(function (response) {
            console.log(response);
          })
          .catch(function (error) {
            console.log(error);
          });
        this.closeDialog();
      } else {
        axios
          .post("https://jsonplaceholder.typicode.com/users", data, {
            headers: headers,
          })
          .then(function (response) {
            console.log(response);
          })
          .catch(function (error) {
            console.log(error);
          });
        this.closeDialog();
      }
    },
    showUserDialog(id) {
      this.isEdit = true;
      let array = this.items.filter((item) => item.Id == id);
      console.log(array);
      if (array.length > 0) {
        this.id = array[0].Id;
        this.itemUser.name = array[0].Name;
        this.itemUser.email = array[0].Email;
        this.itemUser.username = array[0].Username;
        this.itemUser.phone = array[0].Phone;
        this.itemUser.website = array[0].Website;
        this.itemAddress = array[0].Address;
        this.itemGeo = array[0].Address.geo;
        this.itemCompany = array[0].Company;
        this.dialog = true;
      }
    },
    showConfirmDialog(id) {
      this.id = id;
      this.confirmDialog = true;
    },
    deleteUser() {
      axios
        .delete(`https://jsonplaceholder.typicode.com/users/${this.id}`)
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
      this.confirmDialog = false;
    },
    closeDialog() {
      this.dialog = false;
      this.isEdit = false;
      this.itemUser = [];
      this.itemGeo = [];
      this.itemCompany = [];
      this.itemAddress = [];
      this.$refs.form.resetValidation();
    },
  },
  async mounted() {
    await this.getUsers();
  },
};
</script>

<style>
</style>