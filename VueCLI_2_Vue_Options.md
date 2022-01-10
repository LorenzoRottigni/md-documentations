#	VueCLI - 3 Vue Options

You can reach variables, methods, computed and props using `this` clause.
##	DATA
Contains the variables of vue.
Must be a function that returns an object

```
<script>
export default{
	name : '<file-name>',
	data(){
		return {
			text : 'this is a string',
			number: 7,
			active: true,
			objectsArray ; [
				{
					name : 'Lorenzo',
					surname : 'Rottigni',
					age : 21
				},
				{
					name : 'Giacomo',
					surname : 'Verderio',
					age : 16
				}
			]
		}
	}
}
<script>
```
##	METHODS

Contains methods of vue component

```
<script>
export default{
	name : '<file-name>',
	data(){
		return {
			text : 'this is a string'
		}
	},
	methods : {
		logText(){
			console.log(this.text)
		}
	}
}
<script>
```

##	COMPUTED

Computed are simple functions that are refreshed with vue app, they must have a return clause:

```
<script>
export default{
	name : '<file-name>',
	data(){
		return {
			text : 'this is a string'
		}
	},
	computed : {
		textConcat(){
			return this.text + this.text
		}
	}
}
<script>
```

##	WATCHERS


##	PROPS

Props are variables sent from root component:


```
<script>
export default{
	name : '<file-name>',
	props : {
		firstProp : String,
		secondProp : Array
	}
}
<script>
```

At component import on root component

`<component-name :firstProp="this is prop" secondProp="[2,3,4,5]" \>`

## STATES

```
<script>
export default{
	name : '<file-name>',
	data(){
		return{
			text : 'this is text'
		}
	},
	//before the vue app is created
	beforeCreate(){
		console.log(this.text)
	},
	//when the vue app is created
	created(){
		console.log(this.text)
	},
	//before the vue app is mounted
	beforeMount(){
		console.log(this.text)
	},
	//when the vue app is mounted
	mounted(){
		console.log(this.text)
	},
	//before the virtualDOM is updated
	beforeUpdate(){
		console.log(this.text)
	},
	//when the VirtualDOM is updated
	updated(){
		console.log(this.text)
	},
	//when a kept-alive component is activated
	activated(){
		console.log(this.text)
	},
	//when a kept-alive component is deactivated
	deactivated(){
		console.log(this.text)
	},
	//before the vue app is destroyed
	beforeDestroy(){
		console.log(this.text)
	},
	//when vue app is destroyed
	destroyed(){
		console.log(this.text)
	},
	//when an error occures
	errorCaptured(){
		console.log(this.text)
	},
	
}
<script>
```
