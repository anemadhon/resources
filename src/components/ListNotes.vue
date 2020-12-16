<template>
    <div class="list-notes">
        <ul>
            <li v-for="(row, index) in notes" :key="index">
                <button class="btn-note" @click="editNote(row.id)">
                    <label>{{row.title}}</label>
                    <span>{{row.description}}</span>
                </button>
                
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'ListNotes',
    data: () => {
        return {
            notes: [
                {
                    id: 1,
                    title: 'wegodev',
                    description: 'wegodev note'
                }
            ]
        }
    },
    props:{
        propEditNotes: {
            type: Function
        }
    },
    methods:{
        editNote(id){
            let dataForm = this.notes.find(dataNote => dataNote.id === id)

            this.$root.$emit('emitForm', dataForm)
        },
        createNewId(){
            let newId = 0
            if (this.notes.length === 0) {
                newId = 1
            } else {
                newId = this.notes[this.notes.length - 1].id + 1
            }

            return newId
        }
    },
    mounted(){
        this.$root.$on('emitRemoveNote', data => {
            let noteIndex = this.notes.findIndex(dataNote => dataNote.id === data.id)
            this.notes.splice(noteIndex, 1)
        })
        this.$root.$on('emitUpdateNote', data => {
            let noteIndex = this.notes.findIndex(dataNote => dataNote.id === data.id)
            this.note[noteIndex].title = data.title
            this.note[noteIndex].description = data.description
        })
        this.$root.$on('emitSaveNote', data => {
            let note = {
                'id': this.createNewId(),
                'title': data.title,
                'description': data.description
            }

            this.notes.push(note)
            this.editNote(this.createNewId())
        })
    }
}
</script>

<style>
ul {
    list-style-type: none;
    padding: 0;
    margin:0px;
}
.btn-note {
    text-align: left;
    border: none;
    border-bottom: 1px solid gainsboro;
    padding: 0px 15px;
    cursor: pointer;
    outline: none;
    background: #f7f7f7;
    height: 150px;
    width: 100%;
}
.btn-note:hover {
    background:#eaeaea;
}
.btn-note label{
    display:block;
    color: #444444;
    font-size: 1.5em;
    margin-bottom: 15px;
}
.btn-note span{
    color: #545454;
}
</style>