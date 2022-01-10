# USING VUE VIA CDN

1. Create new app.js file and link it in the index.html

2. Add vue CDN to index.html 
	`<script src="https://cdn.jsdelivr.net/npm/vue@2.6.14"></script>`

3. Define new Vue istance in app.js

	```
window.addEventListener(
	'DOMContentLoaded', ()=>{
		const vueApp = new Vue({
			//root selector by ID
			el: '#vue-root',
			//vue variables
			data : {
				array : [
	              {
	                  name : 'name 1'
	              }
		          ],
		          currentTask : undefined,
		          selectedColor: '#563d7c'
			},
			methods : {
				setTask1 : function(){
					this.currentTask = 'task1'
				}
			}
		})
	})
		
	```
	
