<template>
    <v-layout row justify-center>
            <v-card>
                <v-card-title>
                    <span class="headline">New community</span>
                </v-card-title>
                <v-card-text>
                    <v-container grid-list-md>
                        <v-layout wrap>
                          <v-flex xs6>
                              <v-text-field v-model="model.name" label="Name" required></v-text-field>
                          </v-flex>
                          <v-flex xs6>
                            <v-text-field v-model="model.image_url" label="Image" required></v-text-field>
                          </v-flex>                            <v-flex xs12>
                          <v-text-field label="Description" v-model="model.description" textarea required persistent-hint hint="More information about your community"></v-text-field>
                          </v-flex>

                          <v-flex xs12>
                              <v-btn @click="addOption()">
                                Create
                              </v-btn>
                          </v-flex>
                        </v-layout>
                    </v-container>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue darken-1" flat @click="$emit('close')">Close</v-btn>
                    <v-btn color="blue darken-1" v-bind:disabled="canSave()" flat @click.native="save()">Save</v-btn>
                </v-card-actions>
            </v-card>
    </v-layout>
</template>

<script>
import FileInput from "../../shared/FileInput";
import store from "@/store";

export default {
  props: ["show"],
  components: { FileInput },
  data() {
    return {
      model: { terms: false, options: [] }
    };
  },
  methods: {
    save() {
      store.createCommunity(this.model);
    },
    getUploadedFile(e) {
      this.image = e;
    },
    addOption() {
      this.model.options.push({ title: null, description: null });
    },
    canSave() {
      return !this.model.terms || this.model.options.length === 0;
    }
  }
};
</script>
