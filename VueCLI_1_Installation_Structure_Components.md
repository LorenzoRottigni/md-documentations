# VueCLI - 1 Installation, Structure, Components

## INSTALLATION

1. Install VueCLI
	`npm install -g @vue/cli`
2. Create new VueCLI project
	`vue create <project-name>`
	`default (Vue 2)` => Vue 2 CLI project 
	`default (Vue 3)` => Vue 3 CLI project 
	`Manually select features` => babel, sass, typescript, eslint, vuex, router...
	
	You can save a default VueCLI configuration by name
	
## PROJECT STRUCTURE

* /public => contains the index.html where the vue app is injected
* /src => 
	*	/assets => images and static files
	* 	/components => vue components
	*  app.vue => vue app root
	*  main.js => javascript imports, vue mount, plain javascript 

	
## VUE COMPONENTS

Files with extension .vue written in CamelCase

###	COMPONENT STRUCTURE
Template contains the HTML of the component.
Requires only 1 root container

```
<template>
	<div id="container">
	
	</div
</template>
```
Export the name of the component name

```
<script>
export default{
	name : '<file-name>'
}
<script>
```
Contains styles of the component.
Scoped means that styles afflict only the component, they are not global.

```
<style lang="sass" scoped>
</style>
```

###	IMPORT A COMPONENT

```
<template>
<component-name\>
</template>

<script>
import <component-name> from "./components/<component-name>.vue
	
export default{
		name : '<filename>',
		components : {
		<component-name>
	}
}
</script>
```
