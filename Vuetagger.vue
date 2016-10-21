<template>
  <div>
    <div class="tag-container">

      <div class="tag-list">
        <span v-for="tag in tags" class="tag">
          {{ tag }} <span class="remover" @click="remove(tag)">&times;</span>
        </span>
      </div>

      <input type="email"
        id="vuetagger-input"
        v-model="newTag"
        @keydown.enter="append"
        @keydown.delete="removeLastTag"
      />

    </div>
  </div>
</template>

<script>
  export default {

    props: {
      value: {
        type: Array,
        default: ''
      },
      pattern: {
        type: String,
        default: null
      }
    },

    data() {
      return {
        newTag: '',
        tags: []
      }
    },

    mounted() {
      this.initialize()
    },

    ready() {
      this.initialize()
    },

    methods: {

      /**
       * Initialize the tags
       */
      initialize() {
        const initialTags = this.value
        initialTags.forEach((tag) => {
          this.tags.push(tag)
        })
      },


      /**
       * Append new tag
       */
      append() {

        /**
         * Don't allow empty tag.
         */
        if (this.newTag.trim() === '') {
          return false
        }

        /**
         * Don't allow duplicate tags.
         */
        let duplicate = false

        this.tags.forEach((tag) => {
          if (tag === this.newTag.trim()) {
            duplicate = true
          }
        })

        if (duplicate) return false

        /**
         * Check new tag with regex pattern
         */
        const regex = new RegExp(this.pattern)
        if (this.pattern && ! regex.test(this.newTag)) {
          return false
        }

        /**
         * Everything looks good, let's add new tag.
         */
        this.tags.push(this.newTag.trim())
        this.newTag = ''
        this.$emit('change', this.tags)
      },


      /**
       * Remove the selected tag
       * @param {string} tag  Tag name
       */
      remove(tag) {
        const index = this.tags.indexOf(tag)
        this.tags.splice(index, 1)
        this.$emit('change', this.tags)
      },


      /**
       * Remove the last tag
       */
      removeLastTag() {
        if (this.newTag === '' && this.tags.length > 0) {
          this.tags.pop()
          this.$emit('change', this.tags)
        }
      }

    }
  }
</script>

<style scoped>
  .tag-container {
    display: table;
    border: 1px solid #cecece;
    padding: 4px 8px;
    width: 100%;
  }

  .tag-list {

  }

  .tag {
    background: #f0f0f0;
    padding: 0 0 0 8px;
    display: inline-block;
    margin-right: 4px;
    margin-bottom: 2px;
    cursor: default;
  }

  #vuetagger-input {
    padding: 4px;
    /*border: none;*/
    display: table-cell;
    outline: none;
    width: 100%;
    box-sizing: border-box;
  }

  .tag:hover .remover{
    background: #cecece;
    color: white;
  }

  .remover {
    padding: 4px 8px;
    display: inline-block;
    cursor: default;
    margin-left: 4px;
  }
</style>
