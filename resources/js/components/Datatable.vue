<template>
    <table class="table data-table">
        <thead>
            <tr>
              <th class="text-center">
                 <div class="custom-control custom-checkbox">
                    <input type="checkbox" v-modal="selectAll" class="custom-control-input" id="customCheck1" @click="$emit('checkAll')">
                    <label class="custom-control-label" for="customCheck1"></label>
                  </div>
              </th>
                <th v-for="column in columns" :key="column.name" @click="$emit('sort', column.name)"
                    :class="sortKey === column.name ? (sortOrders[column.name] > 0 ? 'sorting_asc' : 'sorting_desc') : 'sorting'"
                    :style="'width:'+column.width+';'+'cursor:pointer;'">
                    {{column.label}}
                </th>
            </tr>
        </thead>
        <slot></slot>
    </table>
</template>

<script>
    export default {
        props: ['columns', 'sortKey', 'sortOrders']
    }
</script>
