<template>
    <div class="form-notes">
        <form>
            <div class="menu-header">
                <button type="button" @click="submitRemove" class="bg-danger btn btn-delete-note">Hapus</button>
                <button type="button" @click="submitSave" class="bg-success btn" v-if="mode == 'save'">Simpan</button>
                <button type="button" @click="submitUpdate"class="bg-success btn" v-if="mode == 'update'">Ubah</button>
            </div>
            <div class="form-content">
                <input type="hidden" v-model="id">
                <input type="text" class="text" placeholder="Tulis Judul Note Kamu ..." v-model="title">
                <textarea class="text textarea" placeholder="Tulis Note Kamu disini ..." v-model="description"></textarea>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: 'FormNotes',
    props:{
        propSaveNote: {
            type: Function
        },
        propDataForm: {
            type: Object
        },
        propUpdateNote: {
            type: Function
        },
        propRemoveNote: {
            type: Function
        }
    },
    data: () => {
        return {
            id: 0,
            title: '',
            description: '',
            mode: 'save'
        }
    },
    methods:{
        submitNote(){
            this.propSaveNote(this.title, this.description)
        },
        submitUpdate(){
            this.propUpdateNote(this.id, this.title, this.description)
        },
        submitRemove(id){
            this.propRemoveNote(id)
            this.resetInput()
        },
        resetInput(){
            this.id = 0
            this.title = ''
            this.description = ''
        }
    },
    watch:{
        propDataForm: function(note){
            this.id = note.id
            this.title = note.title
            this.description = note.description
            this.mode = note.mode
        }
    }
}
</script>

<style>
.menu-header{
    background: #f7f7f7;
    padding:10px 25px;
    margin-bottom: 25px;
    text-align:right;
    border-bottom: 1px solid #e8e6e6;
}
.btn-delete-note{ 
    margin-right:10px; 
}
.form-content{
    padding: 0px 25px;
}
.text{
    display: block;
    width: 100%;
    padding: 0px;
    font-size: 20px;
    font-weight: bold;
    color: #2c3e50;
    border: none;
    margin-bottom: 10px;
    box-sizing: border-box;
    outline: none;
}
.textarea{
    min-height: 350px;
    font-size: 15px;
    font-weight: lighter;
    line-height: 30px;
}
.loader{
    vertical-align: middle;
}
</style>