# Laravel Vue Bulma Pagination
Vue.js pagination component for Laravel pagination with Bulma.

## Requirements

* [Vue.js](https://vuejs.org/)
* [Laravel](http://laravel.com/docs/)
* [Bulma](https://bulma.io/documentation/overview/start/)

## Install

```bash
npm install laravel-vue-bulma-pagination
```

## Usage

Controller method:

```php
$tagsData = Tag::paginate(10);
return response()->json([
    'success' => true,
    'tagsData' => $tagsData
]);
```

Register the component:

```javascript
import pagination from 'laravel-vue-bulma-pagination';

export default {
    components: {
        pagination
    }
}
```

or globaly

```javascript
Vue.component('pagination', require('laravel-vue-bulma-pagination'));
```

Use the component:

```html
<pagination v-bind:pagedata="tagsData" v-on:page-clicked="getTagsList"></pagination>

<table>
	<tr v-for="tag in tags">
	    <td>{{ tag.id }}</td>
	    <td>{{ tag.name }}</td>
	</tr>
</table>
```

```javascript
export default {
	data: () => ({
		tags: [],
		tagsData: {}
	}),
	methods: {
		getTagsList(page){
			var vm = this;
			if(page == undefined){
				var pageUrl = '/admin/posts/tags/list';
			}else{
				var pageUrl = '/admin/posts/tags/list?page=' + page;
			}
			
			axios.get(pageUrl).then(function(response){
				if(response.data.hasOwnProperty('success')){
					vm.tagsData = response.data.tagsData;
					vm.tags = response.data.tagsData.data;
				}
			}).catch(function(error){
				console.log(error);
			});
		}
	}
}
```

### Props

| Name | Type | Description |
| --- | --- | --- |
| `pagedata` | Object | An object contains the value of a [Laravel pagination](https://laravel.com/docs/5.5/pagination#paginating-eloquent-results) response. |


### Events

| Name | Description |
| --- | --- |
| `page-clicked` | Triggered when a user changes page. Passes the new `page` number as a parameter. |


## Credits

I got inspired by seeing this repository [laravel-vue-pagination](https://github.com/gilbitron/laravel-vue-pagination). 

Released under the MIT license.

## Screenshot

![Screenshot](screenshot.png)