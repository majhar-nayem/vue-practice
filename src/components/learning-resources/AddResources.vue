<template>
    <base-card>
        <form @submit.prevent="submitForm">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" name="title" id="title" v-model="formData.title">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea name="description" id="description" rows="3" v-model="formData.description"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="text" name="link" id="link" v-model="formData.link">
            </div>
            <div class="form-control">
                <base-button
                type="submit"
                >
                Add Resource
                </base-button>
            </div>
            <base-dialog 
            v-if="isInputInvalid"
            title = "Invalid Input"
            @close="closeDialog"
            >
            <template #default>
                <p>All the field is Required! Please enter atleast few char</p>
            </template>
            <template #action>
                <base-button @click="closeDialog">Close</base-button>
            </template>
            </base-dialog>
        </form>
    </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseDialog from '../UI/BaseDialog.vue';
export default {
  components: { BaseDialog, BaseButton },
    data(){
        return {
            isInputInvalid : false,
            formData : {
                id : Math.random(),
                title : '',
                description  : '',
                link : '',
            }
        }
    },
    inject : ['addResource'],
    methods : {
        submitForm(){
            if(this.formData.title.trim() === '' ||
             this.formData.description.trim() === '' ||
              this.formData.link.trim() === ''){
                this.isInputInvalid = true;
                return;
            }
            this.addResource(this.formData);
        },
        resetData(){
            this.formData.id = null;
            this.formData.title = '';
            this.formData.description = '';
            this.formData.link = '';
        },
        closeDialog(){
            this.isInputInvalid =false;
        }
    }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>