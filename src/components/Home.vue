<template>
  <q-layout>
    <q-modal ref="layoutModal" :content-css="{minWidth: '80vw', minHeight: '80vh'}">
        <q-modal-layout>
            <q-toolbar slot="header" color="dark">
                <q-btn flat @click="$refs.layoutModal.close()">
                    <q-icon name="keyboard_arrow_left" />
                </q-btn>
                <div class="q-toolbar-title">
                    Add new note
                </div>
                <q-btn flat @click="save()">
                    <q-icon name="save" />
                </q-btn>
            </q-toolbar>
            <q-toolbar slot="header" color="dark">
                <div class="full-width row">
                    <div class="col-10 offset-1"><q-input
                        v-model="title"
                        dark
                        color="white"
                        float-label="Title"
                    /></div>
                </div>
            </q-toolbar>

            <div class="row">
                <div class="col-10 offset-1"><q-input v-model="content" color="dark"   :min-rows="5" float-label="Content" type="textarea" /></div>
            </div>
        </q-modal-layout>
    </q-modal>
    <q-card v-for="(note, index) in this.notes" :key="index">
      <q-card-title>
          <router-link :to="{path: '/edit/' + note.id}">{{ note.title }}</router-link>
        <q-btn
            round
            flat
            color="negative"
            @click="deleteNote(index)"
            class="pull-right"
        >
            <q-icon name="delete" />
        </q-btn>
        <span slot="subtitle">{{ format(note.date, 'DD.MM.YYYY @ HH:mm:ss') }}</span>
      </q-card-title>
      <q-card-main>
        {{ note.content }} 
      </q-card-main>
    </q-card>
    <q-btn
        round
        color="dark"
        @click="method"
        class="fixed"
        style="right: 18px; bottom: 18px"
    >
        <q-icon name="add" />
    </q-btn>
  </q-layout>
</template>

<script>
import {
    date, 
    QLayout,
    QBtn,
    QIcon,
    QModal,
    QModalLayout,
    QToolbar,
    QSearch,
    QInput,
    QCard,
    QCardTitle,
    QCardMain
} from 'quasar'

var storage = window.localStorage;
// var value = storage.getItem(key); // Pass a key name to get its value.
// storage.setItem(key, value)

export default {
  name: 'index',
  components: { 
    QLayout,
    QBtn,
    QIcon,
    QModal,
    QModalLayout,
    QToolbar,
    QSearch,
    QInput,
    QCard,
    QCardTitle,
    QCardMain
  },
  data () {
    return {
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
    method(){
        this.$refs.layoutModal.open()
    },
    save(){
        this.notes.push({ id: this.notes.length, title: this.title, content: this.content, date: Date() })
        console.log(this.title)
        for(let i = 0; i < this.notes.length; i++){
            this.notes[i].id = i;
        }
        // local storage doesn't support objects
        storage.setItem('notes', JSON.stringify(this.notes))
        this.title = null
        this.content = null
        this.$refs.layoutModal.close()
        //storage.removeItem('key')
    },
    deleteNote(index){
        console.log(index)
        this.notes.splice(index, 1)
        storage.setItem('notes', JSON.stringify(this.notes))
    }
  },
  mounted () {
      // console.log(JSON.parse(storage.getItem('key')))
      if(storage.getItem('notes')){
          console.log('if')
          this.notes = JSON.parse(storage.getItem('notes'))
      }else{
          console.log('else')
          storage.setItem('notes', JSON.stringify(this.notes)) 
      }
  },
  beforeDestroy () {
  }
}
</script>

<style lang="stylus">

</style>