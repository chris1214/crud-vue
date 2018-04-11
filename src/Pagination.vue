<script>
  export default{
    props: ["total","page","itensPerPage"],
    computed: {
      totalPages: function(){
        return Math.ceil(this.total/this.itensPerPage)
      },
      showNextButton: function(){
       return  this.page!=this.totalPages
      },
      showPreviousButton: function(){
       return this.page!=1
      }
    },
    methods: {
      goNextPage: function(){
        this.$emit('change-page',this.page+1)
      },
      goPreviousPage: function(){
        this.$emit('change-page',this.page-1)
      },
      goFirstPage: function(){
        this.$emit('change-page',1)
      },
      goLastPage: function(){
        this.$emit('change-page',this.totalPages)
      },
      goPage: function(page){
        this.$emit('change-page',page)
      }
    }
  }
</script>
<template>
    <div>
        <nav class="pagination" role="navigation">
            <a class="pagination-previous" v-show="showPreviousButton" @click="goPreviousPage()">Anterior</a>
            <a class="pagination-next" v-show="showNextButton" @click="goNextPage()">Próximo</a>
            <ul  class="pagination-list">
                <li>
                    <a class="pagination-link" v-show="showPreviousButton" @click="goFirstPage()">1</a>
                </li>
                <li>
                    <span class="pagination-ellipsis">&hellip;</span>
                </li>
                <li>
                    <a class="pagination-link" v-show="showPreviousButton" @click="goPage(page-1)">{{page-1}}</a>
                </li>
                <li>
                    <span class="button is-primary">{{page}}</span>
                </li>
                <li>
                    <a class="pagination-link" v-show="showNextButton" @click="goPage(page+1)">{{page+1}}</a>
                </li>
                <li>
                    <span v-show="showNextButton">&hellip;</span>
                </li>
                <li>
                    <a class="pagination-link" v-show="showNextButton" @click="goLastPage()" >{{totalPages}}</a>
                </li>
            </ul>
        </nav>
    </div>
</template>
