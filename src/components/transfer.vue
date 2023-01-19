<template>
  <div class="container">
    <div class="checkbox-select in_container">
      <div class="checkbox-select__trigger">
        <span class="checkbox-select__title"
          >Source ({{ filters.length }})</span
        >
      </div>
      <div class="checkbox-select__dropdown">
        <div class="checkbox-select__search-wrapp">
          <input type="text" placeholder="search filters..." v-model="search" />
        </div>
        <div class="checkbox-select__col">
          <div class="checkbox-select__select-all" v-model="selectAll">
            <label for="selectAll">{{ selectAllText }}</label>
            <input
              type="checkbox"
              id="selectAll"
              @click="selectAll"
              v-model="allSelected"
            />
          </div>
          <div class="checkbox-select__info">
            {{ checkedFilters.length }} SELECTED
          </div>
        </div>
        <div id="customScroll" class="checkbox-select__filters-wrapp">
          <div v-for="(filter, index) in filteredList">
            <div class="checkbox-select__check-wrapp">
              <input
                :id="index"
                class="conditions-check"
                v-model="checkedFilters"
                :value="filter"
                type="checkbox"
              />
              <label :for="index">{{ filter }}</label>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="middle">
      <button @click="moveRight">&gt;</button>
      <button @click="moveLeft">&lt;</button>
    </div>

    <div id="app" class="checkbox-select in_container">
      <div class="checkbox-select__trigger">
        <span class="checkbox-select__title"
          >Target ({{ filtersRight.length }})</span
        >
      </div>
      <div>
        <div class="checkbox-select__search-wrapp">
          <input
            type="text"
            placeholder="search filters..."
            v-model="searchRight"
          />
        </div>
        <div class="checkbox-select__col">
          <div class="checkbox-select__select-all" v-model="selectAllRight">
            <label for="selectAllRight">{{ selectAllTextRight }}</label>
            <input
              type="checkbox"
              id="selectAllRight"
              @click="selectAllRight"
              v-model="allSelectedRight"
            />
          </div>
          <div class="checkbox-select__info">
            {{ checkedFiltersRight.length }} SELECTED
          </div>
        </div>
        <div id="customScrollRight" class="checkbox-select__filters-wrapp">
          <div v-for="(filterRight, indexRight) in filteredListRight">
            <div class="checkbox-select__check-wrapp_Right">
              <input
                :id="indexRight"
                class="conditions-check"
                v-model="checkedFiltersRight"
                :value="filterRight"
                type="checkbox"
              />
              <label :for="indexRight">{{ filterRight }}</label>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'transfer',
  props: {
    msg: String,
  },

  data() {
    return {
      filters: [
        'Bungalow',
        'Chalet',
        'Guesthouse',
        'Hotel',
        'Townhouse',
        'Apartment',
        'Boutique hotel',
        'Cabin',
        'Guest suite',
        'Hostel',
        'Loft',
        'Villa',
      ],
      filtersRight: [],
      search: '',
      searchRight: '',
      checkedFilters: [],
      checkedFiltersRight: [],
      allSelected: false,
      allSelectedRight: false,
      selectAllText: 'Select All',
      selectAllTextRight: 'Select All',
    };
  },
  computed: {
    filteredList() {
      return this.filters.filter((item) => {
        return item.toLowerCase().includes(this.search.toLowerCase());
      });
    },
    filteredListRight() {
      return this.filtersRight.filter((item) => {
        return item.toLowerCase().includes(this.searchRight.toLowerCase());
      });
    },
  },
  methods: {
    selectAll: function () {
      this.checkedFilters = [];
      this.selectAllText =
        this.selectAllText == 'Select All' ? 'Clear All' : 'Select All';
      if (this.allSelected) {
        for (filter in this.filters) {
          this.checkedFilters.push(this.filters[filter].toString());
        }
      }
    },

    selectAllRight: function () {
      this.checkedFiltersRight = [];
      this.selectAllTextRight =
        this.selectAllTextRight == 'Select All' ? 'Clear All' : 'Select All';
      if (this.allSelectedRight) {
        for (filterRight in this.filtersRight) {
          this.checkedFiltersRight.push(
            this.filtersRight[filterRight].toString()
          );
        }
      }
    },

    moveRight() {
      if (!this.checkedFilters.length) return;
      for (let i = this.checkedFilters.length; i > 0; i--) {
        let idx = this.filters.indexOf(this.checkedFilters[i - 1]);
        this.filters.splice(idx, 1);
        this.filtersRight.push(this.checkedFilters[i - 1]);
        this.checkedFilters.pop();
      }
    },
    moveLeft() {
      if (!this.checkedFiltersRight.length) return;
      for (let i = this.checkedFiltersRight.length; i > 0; i--) {
        let idx = this.filtersRight.indexOf(this.checkedFiltersRight[i - 1]);
        this.filtersRight.splice(idx, 1);
        this.filters.push(this.checkedFiltersRight[i - 1]);
        this.checkedFiltersRight.pop();
      }
    },
  },
};
</script>
<style>
.container {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizeLegibility;
  display: flex;
  flex-flow: row nowrap;
  align-items: center;
  cursor: default;
}
.middle > button {
  min-width: 30px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 5px;
}
.checkbox-select {
  flex: 1 1 auto;
  border: 1px solid #ddd;
  background: #f9f9f9;
  border-radius: 3px;
  overflow: auto;
  display: flex;
  flex-direction: column;
  margin: 20px;
}
.in_container {
  max-width: 0px;
  min-width: 180px;
  min-height: 400px;
  overflow-y: auto;
  padding: 10px;
}
.vue-list-picker .list-picker-panel {
  min-height: 400px;
  overflow-y: auto;
}
</style>
