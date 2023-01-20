<template>
  <div class="container">
    <div class="checkbox-select in_container">
      <div class="checkbox-select__trigger">
        <span class="checkbox-select__title">
          {{ leftTitle }}
        </span>
      </div>
      <div class="checkbox-select__wrap">
        <div v-show="showSelectAll" class="checkbox-select__col">
          <div class="checkbox-select__select-all" v-model="selectAll">          
            <label for="selectAll">
              {{ selectAllText }}
            </label>
            <input
              type="checkbox"
              id="selectAll"
              @click="selectAll"
              v-model="allSelected"
            />
          </div>
        </div>
        <div class="checkbox-select__search-wrapp">
          <input 
            type="text" 
            placeholder="Search.." 
            class="searchTerm" 
            v-model="search" 
          />
        </div>
        <div id="customScroll">       
          <div v-for="filter in filteredList">
            <div class="checkbox-select__check-wrapp">
              <input
                class="conditions-check"
                :id="filter"
                v-model="checkedFilters"
                :value="filter"
                type="checkbox"
              />
              <label :for="filter">
                {{ filter }}
              </label>
            </div>
          </div>
        </div>
        <div class="checkbox-select__info">
        <label v-show="showSelectCount" class="checkbox-select-count">{{ checkedFilters.length }} SELECTED</label>
        <label v-show="showItemCount" class="checkbox-item-count">{{ filters.length }} ITEMS</label>
        </div>
      </div>
    </div>

    <div class="middle">
      <button @click="moveRight">&#8250;</button>
      <button @click="moveLeft">&#8249;</button>
    </div>

    <div id="app" class="checkbox-select in_container">
      <div class="checkbox-select__trigger">
        <span class="checkbox-select__title">
          {{ rightTitle }}
        </span>
      </div>
      <div>
        <div v-show="showSelectAll" class="checkbox-select__col">
          <div class="checkbox-select__select-all" v-model="selectAllRight">
            <label for="selectAllRight">
              {{ selectAllTextRight }}
            <label>
            <input
              type="checkbox"
              id="selectAllRight"
              @click="selectAllRight"
              v-model="allSelectedRight"
            />
          </div>
        </div>
        <div class="checkbox-select__search-wrapp">
          <input
            type="text"
            placeholder="Search.."
            v-model="searchRight"
            class="searchTerm"
          />
        </div>
        <div id="customScroll">
          <div v-for="filterRight in filteredListRight">
            <div class="checkbox-select__check-wrapp_Right">
              <input
                :id="filterRight"
                class="conditions-check-right"
                v-model="checkedFiltersRight"
                :value="filterRight"
                type="checkbox"
              />
              <label :for="filterRight">
                {{ filterRight }}
              </label>
            </div>
          </div>
        </div>
         <div class="checkbox-select__info">
        <label v-show="showSelectCount" class="checkbox-select-count">{{ checkedFiltersRight.length }} SELECTED</label>
        <label v-show="showItemCount"  class="checkbox-item-count">{{ filtersRight.length }} ITEMS</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'transfer',
  props: {
    leftTitle: {
      type: String,
      required: true
    },
    rightTitle: {
      type: String,
      required: true
    },
    filters: {
      type: Array,
      required: true
    },
    filtersRight: {
      type: Array,
      required: true
    },
    showSelectCount: {
    type: Boolean,
    default: false
    },
    showItemCount: {
    type: Boolean,
    default: false
    },
    showSelectAll: {
    type: Boolean,
    default: false
    },
  },

  data() {
    return {
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
      this.allSelected = !this.allSelected;
      this.checkedFilters = [];
      this.selectAllText =
        this.selectAllText == 'Select All' ? 'Clear All' : 'Select All';
      if (this.allSelected) {
        for (let filter in this.filteredList) {
          this.checkedFilters.push(this.filteredList[filter].toString());
        }
      }
    },
    selectAllRight: function () {
      this.allSelectedRight = !this.allSelectedRight;
      this.checkedFiltersRight = [];
      this.selectAllTextRight =
        this.selectAllTextRight == 'Select All' ? 'Clear All' : 'Select All';
      if (this.allSelectedRight) {
        for (let filterRight in this.filteredListRight) {
          this.checkedFiltersRight.push(
            this.filteredListRight[filterRight].toString()
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
  font-family: 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
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
  background-color: #EE7200;
  color: #fff;
  border: none;
}
.checkbox-select {
  border: 1px solid #ddd;
  background: #f9f9f9;
  overflow: auto;
  display: flex;
  flex-direction: column;
  margin: 10px;
}
#customScroll{
  min-height: 150px;
  max-height: 150px;
  overflow-y: auto;
  overflow-x: hidden;
  border: 1px solid #ddd;
  border-top: none;
  background-color: #fff;
}
.in_container {
  min-height: 150px;
  min-width: 175px;
  padding: 8px;
}
.checkbox-select__select-all{
    border-top: 1px solid #ddd;
}
.searchTerm{
  border: 1px solid #ddd;
  border-bottom: none;
  height: 20px;
}
.checkbox-select__select-all label{
  cursor: pointer;
}
/* .checkbox-select__select-all input {
  display: none;
} */
.checkbox-select__title, button{
  font-size: 17px;
  font-weight: 500;
}
.checkbox-select__select-all, .searchTerm, #customScroll{
  padding: 5px 5px 1px 5px;
}
.checkbox-select__trigger{
  padding: 0px 5px 5px 5px;
}
.checkbox-select__info{
  margin-top: 8px;
  font-size: 11px;
}
.checkbox-select__info{
  padding: 0px 5px;
}
.checkbox-select-count{
  float: left;
}
.checkbox-item-count{
  float: right;
}
</style>
