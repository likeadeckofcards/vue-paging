<template>
    <ul class="pagination">

        <li v-if="active > 3">
            <a href="#" @click.stop.prevent="update(0)">{{ 1 }}</a>
        </li>

        <li v-if="active > 3" class="disabled">
            <a href="#">...</a>
        </li>

        <li v-for="n in numbers" :class="{'active' : n == active}">
            <a href="#" @click.stop.prevent="update(n)">{{ n+1 }}</a>
        </li>

        <li v-if="active < length-4" class="disabled">
            <a href="#">...</a>
        </li>

        <li v-if="active < length-4">
            <a href="#" @click.stop.prevent="update(length-1)">{{ length }}</a>
        </li>

    </ul>
</template>

<script>

    export default{

        data() {
            return {
                n: 0,
                active: 0
            }
        },

        props:['items', 'count', 'type'],

        computed: {
            length: function() {
                console.log(this.items.length % this.count)
                return Math.ceil(this.items.length / this.count);
            },

            min: function() {
                if(this.active < 4) {
                    return 0;
                } else if ( this.active > this.length - 4) {
                    return this.length-5;
                } else  {
                    return this.active-2;
                }
            },

            max: function() {
                if (this.length < 6) {
                    return this.length;
                } else if(this.active < 4) {
                    return 6;
                } else if ( this.active > this.length - 5) {
                    return this.length;
                } else  {
                    return this.active+3;
                }
            },

            numbers: function() {
                var temp = [];
                for(var i = this.min; i < this.max; i++) {
                    temp.push(i);
                }
                return temp
            }
        },

        methods: {
            update: function(n){
                this.active = n;
                this.$dispatch('page-' + this.type, this.active);
            }
        }
    }
</script>