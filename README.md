# vue-paging
This is a component to handle pagination. All you need to do is pass in acouple variables and your list of items.

## Requirements
This component is written to be compiled with Vueify.

## Usage
In the component calling this component add the following HTML to where you want to have the page numbers to display.
```
<paging :items="items" :count.sync="30" type="type"></paging>
```
items is an array of items
count is the number of items per page
type is a string (useful if you have multiple items you want to page on the same page)

In the data section, you will want to add these two variables:
```
activePage: 1
offset: 0
```
Then add this to your events section:
```
'page-type': function(page) {
   this.activePage = page;
   this.offset = page * this.count;
}
```

Be sure to check this [live example](https://jsfiddle.net/xakvbzur/4/)

