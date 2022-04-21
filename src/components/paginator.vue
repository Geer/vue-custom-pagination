<template>
  <div class="d-inline-flex align-content-center">
      <div class="d-inline pa-2 accent-4">
        <v-btn
          class="mx-2"
          fab
          small
          :color="color"
          @click="firstPage($event)"
          :disabled="totalPages == 1 || currentPage == 1"
        >
          <v-icon dark>
            mdi-chevron-double-left
          </v-icon>
        </v-btn>
      </div>
      <div class="d-inline pa-2 accent-4">
        <v-btn
          class="mx-2"
          fab
          small
          :color="color"
          @click="previousPage($event)"
          :disabled="totalPages == 1 || currentPage == 1"
        >
          <v-icon dark>
            mdi-chevron-left
          </v-icon>
        </v-btn>
      </div>
      <div class="d-inline pr-2 accent-4">
        <v-text-field
          height="20"
          outlined
          filled
          class="page-number"
          v-model="page"
          @change="goToPage($event)"
        ></v-text-field>
      </div>
      <div class="d-inline pa-2 accent-4">
        <v-btn
          class="mx-2"
          fab
          small
          :color="color"
          @click="nextPage($event)"
          :disabled="totalPages == 1 || currentPage == totalPages"
        >
          <v-icon dark>
            mdi-chevron-right
          </v-icon>
        </v-btn>
      </div>
      <div class="d-inline pa-2 accent-4">
        <v-btn
          class="mx-2"
          fab
          small
          :color="color"
          @click="lastPage($event)"
          :disabled="totalPages == 1 || currentPage == totalPages"
        >
          <v-icon dark>
            mdi-chevron-double-right
          </v-icon>
        </v-btn>
      </div>
      <div class="d-inline pa-5">
        <p>Showing {{ itemsPerPage }} of {{ totalCount }}</p>
      </div>
    </div>
</template>


<script>

export default {
  name: 'PaginatorComponent',
  props: {
    totalPages: {
      default: 10,
      type: Number
    },
    currentPage: {
      default: 5,
      type: Number
    },
    totalCount: {
      default: 50,
      type: Number
    },
    itemsPerPage: {
      default: 10,
      type: Number
    },
    items: [],
    
    color: String, 
  },
  data() { 
    return {
      page: 0,
    }
  },
  methods: {
    firstPage() {
      this.$emit(`getPage(1})`)
    },
    previousPage() {
      this.$emit(`getPage(${this.currentPage - 1})`)
    },
    nextPage() {
      this.$emit(`getPage(${this.currentPage + 1})`)
    },
    lastPage() {
      this.$emit(`getPage(${this.totalPages})`)
    },
    goToPage(e) {
      this.$emit(`getPage(${e})`)
    }
  },
  created() {
    this.page = this.currentPage;
  }
}
</script>

<style scoped>
    .page-number {
        width: 40px;
        height: 20px!important;

    }
</style>