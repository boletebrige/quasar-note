<template>
    <div class="row">
        <div class="col-10 offset-1">
            <q-layout
                ref="layout"
                view="lHh Lpr fff"
                :left-class="{'bg-grey-2': true}"
            >
            <q-input v-model="title" color="dark" />
            <q-input
            color="dark"
                v-model="content"
                type="textarea"
                float-label="Content"
                />
            </q-layout>
        </div>
        <q-btn
        round
        color="dark"
        @click="editNote"
        class="fixed"
        style="right: 18px; bottom: 18px"
    >
        <q-icon name="save" />
    </q-btn>
    </div>
</template>
<script>

import { 
    QLayout ,
    QInput,
    QBtn,
    QIcon
} from 'quasar'
var storage = window.localStorage;

export default {
    components: {
        QLayout,
        QInput,
        QBtn,
        QIcon
    },
    data () {
    return {
        id: this.$route.params.id,
        title: null,
        content: null,
        notes: []
    }
  },
  computed: {
  },
  methods: {
    format(noteDate, dateFormat){
        return date.formatDate(noteDate, dateFormat)
    },
    editNote(){
        console.log('test')
        for(let i = 0; i < this.notes.length; i++){
            if(this.notes[i].id == this.id){
                this.notes[i].title = this.title;
                this.notes[i].content = this.content;
                this.notes[i].date = Date();
                storage.setItem('notes', JSON.stringify(this.notes))
            }
        }
    }
  },
  mounted () {
      let that = this;
      if(storage.getItem('notes')){
          this.notes = JSON.parse(storage.getItem('notes'))
          this.notes.filter(function(el){
              if(that.id == el.id){
                  console.log(el)
                  that.title = el.title;
                  that.content = el.content;
              }
          })
      }else{
          storage.setItem('notes', JSON.stringify(this.notes)) 
      }
  }
}
</script>

