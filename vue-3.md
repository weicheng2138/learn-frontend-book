# Vue 3

## Vscode tooling&#x20;

* use <mark style="color:orange;">volar</mark> for highlight and linting your code. Use it do not come back to vetur!!!

### Composition API to do the parent-child v-model (setup script)

Our purpose is to make a bi-directional data from parent to child.

```
// Parent.vue
<InputDropdown v-model:infoData="inputData" />
```

```
// Child.vue
<script setup>
import { reactive, ref } from "vue";

const props = defineProps({
	infoData: String,
});
const emit = defineEmits(["update:infoData"]);

const setDropdownSelected = (item) => {
	if (item !== "backspace") {
		dropdown.selectedItem += item;
		emit("update:infoData", dropdown.selectedItem);
	} else {
		dropdown.selectedItem = dropdown.selectedItem.slice(0, -1);
		emit("update:infoData", dropdown.selectedItem);
	}
};
</script>
```

### Pass data through router-link

```
// routes.js
export const routes = [
	{ path: "/", component: Home, meta: { title: "Home" } },
	{
		path: "/businfo",
		meta: { title: "公車動態" },
		component: BusInfo,
		name: "BusInfo",
		props: true,
	},
	{ path: "/:path(.*)", component: NotFound },
];
```

```
// Home.vue
<router-link :to="{ name: 'BusInfo', params: { inputData } }">go</router-link>
```

```
// Destination.vue
<script setup>
const props = defineProps({
	inputData: String,
});
</script>
```
