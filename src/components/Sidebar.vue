<template>
  <b-sidebar id="sidebar-1" title="Filter" shadow>
    <div class="px-3 py-2">
      <b-form-group
        label="By Color"
        v-slot="{ ariaDescribedby }"
      >
        <b-form-checkbox-group
          v-model="selected"
          :options="colorOptions"
          :aria-describedby="ariaDescribedby"
          name="color"
          stacked
					@change="setFilterKey('color')"
        ></b-form-checkbox-group>
      </b-form-group>
      
			<b-form-group
        label="By Sex"
        v-slot="{ ariaDescribedby }"
      >
        <b-form-checkbox-group
          v-model="selected"
          :options="sexOptions"
          :aria-describedby="ariaDescribedby"
          name="sex"
          stacked
					@change="setFilterKey('sex')"
        ></b-form-checkbox-group>
      </b-form-group>
    </div>
  </b-sidebar>
</template>

<script>
export default {
  name: "Sidebar",
	data() {
		return {
			selectedColor: [],
			selectedSex: [],
			selected: [],
			filterKey: "",
			colorOptions: [
        { text: 'Blue', value: { color: 'blue' } },
        { text: 'Pink', value: { color: 'pink' } },
        { text: 'Red', value: { color: 'red' } },
        { text: 'Orange', value: { color: 'orange' } }
      ],
			sexOptions: [
        { text: 'Male', value: { sex: 'male' } },
        { text: 'Female', value: { sex: 'female' } },
      ],
		}
	},
	watch: {
		selected: function(val) {
			this.$emit("filter-color", val)
		}
	},
	methods: {
		setFilterKey(key) {
			this.filterKey = key;
		}
	}
};
</script>

<style>
</style>