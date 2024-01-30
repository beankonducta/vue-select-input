<template>
    <div class="vue-select-input">
        <input type="text" v-model="searchTerm" @input="handleInput" @focus="selected = true" @blur="selected=false" :placeholder="placeholder" :disabled="disabled" @keydown="checkKeypress($event)"/>
        <ul class="items-panel" v-if="selected">
            <li v-for="item in filteredItems" :key="item.id" @mousedown="selectedItem(item)">{{ item.name }}</li>
            <li class="no-found" v-if="filteredItems.length === 0">No results found</li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'VueSelectInput',
    props: {
        items: {
            type: Array,
            required: true,
        },
        disabled: {
            type: Boolean,
            default: false,
        },
        placeholder: {
            type: String,
            default: 'Search...',
        }
    },
    data() {
        return {
            searchTerm: '',
            selected: false,
        };
    },
    computed: {
        filteredItems() {
            if(!this.items) return [];
            return this.items.filter(item => item.name.toLowerCase().includes(this.searchTerm.toLowerCase()));
        }
    },
    methods: {
        handleInput(event) {
            if(!event) return;
            this.searchTerm = event.target.value;
        },
        selectedItem(item) {
            if(!item) return;
            this.searchTerm = item.name;
            this.$emit('selected', item);
        },
        checkKeypress(event) {
            if(!event) return;
            const key = event.keyCode;
            // selects the first item in the list if the user presses enter
            if (key === 13) {
                this.selectedItem(this.filteredItems[0]);
            }
            // deletes the search term if the user presses backspace and the search term is the same as the selected item
            if (key === 8) {
                const hasValue = this.items.some(item => item.name === this.searchTerm);
                if(hasValue) {
                    this.searchTerm = '';
                }
            }
        }
    }
};
</script>

<style scoped>
.vue-select-input {
    position: relative;
    margin-bottom: 10px;
    max-width: 500px;
}

.vue-select-input input {
    width: 100%;
    padding: 0.5rem;
    border: .25px solid #ccc;
    outline: none;
}

.vue-select-input input:focus {
    border-color: #aaa;
    outline: none;
}

.vue-select-input input:disabled {
    background: #eee;
    cursor: not-allowed;
}

.vue-select-input input:disabled:focus {
    border-color: #ccc;
    outline: none;
}

.vue-select-input input::placeholder {
    color: #aaa;
}

.vue-select-input input::-webkit-input-placeholder {
    color: #aaa;
}

.vue-select-input ul {
    width: 100%;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
    border-left: .25px solid #aaa;
    border-right: .25px solid #aaa;
    border-bottom: .25px solid #aaa;
    z-index: 99;
    max-height: 500px;
    overflow-y: auto;
}

.vue-select-input li {
    width: 100%;
    margin-left: -0.5rem;
    padding: 0.5rem;
}

.vue-select-input li:not(.no-found) {
    cursor: pointer;
}

.vue-select-input li:hover:not(.no-found) {
    background: #ccc;
}
.items-panel {
    list-style: none;
    padding: 0;
    margin: 0;
    position: absolute;
    top: 100%;
    left: 0;
    background: white;
}
</style>
