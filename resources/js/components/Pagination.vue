
<template>
<div class="table-pagination">

<div class="pagination-list"  v-if="!client">
  <span class="page-stats">Showing Records {{pagination.from}} - {{pagination.to}} of {{pagination.total}}</span>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button type="button" class="btn btn-light" v-if="pagination.prevPageUrl" @click="$emit('prev');">Previous</button>
    <button type="button" class="btn btn-light" v-else :disabled="true" @click="$emit('next');">Previous</button>

    <button type="button" class="btn btn-light" v-if="pagination.nextPageUrl" @click="$emit('next');">Next</button>
    <button type="button" class="btn btn-light" v-else :disabled="true">Next</button>
  </div>
</div>

<div class="pagination-list"  v-else>
 <span class="page-stats">
      {{pagination.from}} - {{pagination.to}} of {{filtered.length}}
      <span v-if="filtered.length < pagination.total">(filtered from {{pagination.total}} total entries)</span>
  </span>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button type="button" class="btn btn-light" v-if="pagination.prevPage" @click="$emit('prev');">Previous</button>
    <button type="button" class="btn btn-light" v-else :disabled="true" @click="$emit('next');">Previous</button>

    <button type="button" class="btn btn-light" v-if="pagination.nextPage" @click="$emit('next');">Next</button>
    <button type="button" class="btn btn-light" v-else :disabled="true">Next</button>
  </div>
</div>

</div>
    <!-- <nav class="pagination" v-if="!client">
        <span class="page-stats">{{pagination.from}} - {{pagination.to}} of {{pagination.total}}</span>
        <a v-if="pagination.prevPageUrl" class="button is-small pagination-previous" @click="$emit('prev');">
            Prev
        </a>
        <a class="button is-small pagination-previous" v-else :disabled="true">
           Prev
        </a>

        <a v-if="pagination.nextPageUrl" class="button is-small pagination-next" @click="$emit('next');">
            Next
        </a>
        <a class="button is-small pagination-next" v-else :disabled="true">
            Next
        </a>
    </nav>

    <nav class="pagination" v-else>
        <span class="page-stats">
            {{pagination.from}} - {{pagination.to}} of {{filtered.length}}
            <span v-if="filtered.length < pagination.total">(filtered from {{pagination.total}} total entries)</span>
        </span>
        <a v-if="pagination.prevPage" class="button is-small pagination-previous" @click="$emit('prev');">
            Prev
        </a>
        <a class="button is-small pagination-previous" v-else :disabled="true">
           Prev
        </a>

        <a v-if="pagination.nextPage" class="button is-small pagination-next" @click="$emit('next');">
            Next
        </a>
        <a class="button is-small pagination-next" v-else :disabled="true">
            Next
        </a>
    </nav> -->
</template>

<script>
    export default {
        props: ['pagination', 'client', 'filtered']
    }
</script>
