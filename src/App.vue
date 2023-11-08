<template>
    <div class="row p-20">
        <div class="col-lg-6 p-b-15">
            <div class="tabs-container">
                <ul class="nav nav-tabs" role="tablist">
                    <li class="active"><a class="nav-link active" data-toggle="tab" href="#tab-1" aria-expanded="true">Добавить категорию</a></li>
                    <li><a class="nav-link" data-toggle="tab" href="#tab-2">Изменить категорию</a></li>
                    <li><a class="nav-link" data-toggle="tab" href="#tab-3">Удалить категорию</a></li>
                </ul>
                <div class="tab-content">
                    <div role="tabpanel" id="tab-1" class="tab-pane active">
                        <div class="panel-body">
                            <form @submit.prevent="addCategory">
                                <div class="form-group row"><label class="col-lg-2 col-form-label">Категория</label>
                                    <div class="col-lg-10"><input type="text" placeholder="Категория" class="form-control" v-model="forms.add_category.category"></div>
                                </div>
                                <div class="form-group row"><label class="col-lg-2 col-form-label">Имя категории</label>
                                    <div class="col-lg-10"><input type="text" placeholder="Имя категории" class="form-control" v-model="forms.add_category.name"></div>
                                </div>
                                <div class="form-group row">
                                    <div style="margin-left: auto;margin-right: 15px;">
                                        <input
                                            type="submit"
                                            class="btn btn-primary"
                                            :class="Object.values(forms.add_category).includes('') ? 'disabled-btn' : ''"
                                            id="submit_category"
                                            value="Добавить"
                                            style="margin-left: auto;"
                                        >
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                    <div role="tabpanel" id="tab-2" class="tab-pane">
                        <div class="panel-body">
                            <form @submit.prevent="updateCategory">
                                <div class="form-group row">
                                    <label class="col-sm-2 control-label">Выбрать категорию</label>
                                    <div class="col-sm-10 redact_category_conatiner">
                                        <select
                                            name="selected_category"
                                            id="addmedia-mediaobjects_name"
                                            class="form-control"
                                            @input="selectCategory($event.target.value)"
                                            :value="forms.update_category.selected_category"
                                        >
                                            <option value="" disabled selected>Выберите категорию</option>
                                            <option :value="category.category" v-for="category in categories" :key="category.category">{{ category.name }}</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group row"><label class="col-lg-2 col-form-label">Категория</label>
                                    <div class="col-lg-10"><input type="text" placeholder="Категория" class="form-control" v-model="forms.update_category.category"></div>
                                </div>
                                <div class="form-group row"><label class="col-lg-2 col-form-label">Имя категории</label>
                                    <div class="col-lg-10"><input type="text" placeholder="Имя категории" class="form-control" v-model="forms.update_category.name"></div>
                                </div>
                                <div class="form-group row">
                                    <div style="margin-left: auto;margin-right: 15px;">
                                        <input
                                            type="submit"
                                            class="btn btn-primary"
                                            :class="Object.values(forms.update_category).includes('') ? 'disabled-btn' : ''"
                                            id="submit_category"
                                            value="Изменить"
                                            style="margin-left: auto;"
                                        >
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                    <div role="tabpanel" id="tab-3" class="tab-pane">
                        <div class="panel-body">
                            <form @submit.prevent="deleteCategory">
                                <div class="form-group row">
                                    <label class="col-sm-2 control-label">Выбрать категорию</label>
                                    <div class="col-sm-10 redact_category_conatiner">
                                        <select
                                            name="category"
                                            id="addmedia-mediaobjects_name"
                                            class="form-control"
                                            v-model="forms.delete_category.category"
                                        >
                                            <option value="" disabled selected>Выберите категорию</option>
                                            <option :value="category.category" v-for="category in categories" :key="category.category">{{ category.name }}</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group row">
                                    <div style="margin-left: auto;margin-right: 15px;">
                                        <input
                                            type="submit"
                                            class="btn btn-danger bg-[#ed5565]"
                                            :class="forms.delete_category.category == '' ? 'disabled-btn' : 'bg-[#ed5565]'"
                                            id="submit_category"
                                            value="Удалить"
                                            style="margin-left: auto;"
                                        >
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-lg-6 p-b-15">
            <div class="tabs-container">
                <ul class="nav nav-tabs" role="tablist">
                    <li class="active"><a class="nav-link active" data-toggle="tab" href="#tab-4" aria-expanded="true">Добавить объект</a></li>
                    <li><a class="nav-link" data-toggle="tab" href="#tab-5">Изменить объект</a></li>
                    <li><a class="nav-link" data-toggle="tab" href="#tab-6">Удалить объект</a></li>
                </ul>
                <div class="tab-content">
                    <div role="tabpanel" id="tab-4" class="tab-pane active">
                        <div class="panel-body">
                            <form @submit.prevent="addObject" action="/ru/mediarating/add-object" method="POST">
                                <div class="form-group row">
                                    <label class="col-sm-2 control-label">Выбрать категорию</label>
                                    <div class="col-sm-10 redact_category_conatiner">
                                        <select
                                            name="selected_category"
                                            id="addmedia-mediaobjects_name"
                                            class="form-control"
                                            v-model="forms.add_object.selected_category"
                                        >
                                            <option value="" disabled selected>Выберите категорию</option>
                                            <option :value="category.category" v-for="category in categories" :key="category.category">{{ category.name }}</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group row"><label class="col-lg-2 col-form-label">ID проекта</label>
                                    <div class="col-lg-10"><input name="id_project" type="text" placeholder="ID проекта" class="form-control" @input="isNumber" :value="forms.add_object.id_project"></div>
                                </div>
                                <div class="form-group row"><label class="col-lg-2 col-form-label">Имя объекта</label>
                                    <div class="col-lg-10"><input type="text" name="name" placeholder="Имя объекта" class="form-control" v-model="forms.add_object.name"></div>
                                </div>
                                <div class="form-group row"><label class="col-lg-2 col-form-label">Доп информация</label>
                                    <div class="col-lg-10"><input name="info_about" type="text" placeholder="Доп информация" class="form-control" v-model="forms.add_object.info_about"></div>
                                </div>
                                <!-- <div class="form-group field-addphoto-image">
                                    <label class="control-label" for="addphoto-image">Image</label>
                                    <input type="file" id="addphoto-image" name="image" @input="uploadImage">

                                    <div class="help-block"></div>
                                </div> -->
                                <div class="form-group row">
                                    <div style="margin-left: auto;margin-right: 15px;">
                                        <input
                                            type="submit"
                                            class="btn btn-primary"
                                            :class="getOnlyTheseValues(forms.add_object, ['info_about']).includes('') ? 'disabled-btn' : ''"
                                            id="submit_category"
                                            value="Добавить"
                                            style="margin-left: auto;"
                                        >
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                    <div role="tabpanel" id="tab-5" class="tab-pane">
                        <div class="panel-body">
                            <form @submit.prevent="updateObject" action="/ru/mediarating/update-object" method="POST">
                                <div class="form-group row">
                                    <label class="col-sm-2 control-label">Выбрать категорию</label>
                                    <div class="col-sm-10 redact_category_conatiner">
                                        <select
                                            name="selected_category"
                                            id="addmedia-mediaobjects_name"
                                            class="form-control"
                                            @input="getCategoryObjects($event.target.value)"
                                            v-model="forms.update_object.selected_category"
                                        >
                                            <option value="" disabled selected>Выберите категорию</option>
                                            <option :value="category.category" v-for="category in categories" :key="category.category">{{ category.name }}</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group row">
                                    <label class="col-sm-2 control-label">Выбрать объект</label>
                                    <div class="col-sm-10 redact_category_conatiner">
                                        <select
                                            name="selected_category_object"
                                            id="addmedia-mediaobjects_name"
                                            class="form-control"
                                            @input="selectObject($event.target.value)"
                                            :value="forms.update_object.selected_category_object"
                                        >
                                            <option value="" disabled selected>Выберите объект</option>
                                            <option :value="object.id_category" v-for="object in category_objects" :key="object.id_category">{{ object.name }}</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group row">
                                    <label class="col-sm-2 control-label">Выбрать новую категорию</label>
                                    <div class="col-sm-10 redact_category_conatiner">
                                        <select
                                            name="new_category"
                                            id="addmedia-mediaobjects_name"
                                            class="form-control"
                                            v-model="forms.update_object.new_category"
                                        >
                                            <option value="" disabled selected>Выберите новую категорию</option>
                                            <option :value="category.category" v-for="category in categories" :key="category.category">{{ category.name }}</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group row"><label class="col-lg-2 col-form-label">Имя объекта</label>
                                    <div class="col-lg-10"><input type="text" name="name" placeholder="Имя объекта" class="form-control" v-model="forms.update_object.name"></div>
                                </div>
                                <div class="form-group row"><label class="col-lg-2 col-form-label">Доп информация</label>
                                    <div class="col-lg-10"><input name="info_about" type="text" placeholder="Доп информация" class="form-control" v-model="forms.update_object.info_about"></div>
                                </div>
                                <!-- <div class="form-group field-addphoto-image">
                                    <label class="control-label" for="addphoto-image">Image</label>
                                    <input type="file" id="addphoto-image" name="image" @input="uploadImage">
        
                                    <div class="help-block"></div>
                                </div> -->
                                <div class="form-group row">
                                    <div style="margin-left: auto;margin-right: 15px;">
                                        <input
                                            type="submit"
                                            class="btn btn-primary"
                                            :class="getOnlyTheseValues(forms.update_object, ['new_category', 'info_about']).includes('') ? 'disabled-btn' : ''"
                                            id="submit_category"
                                            value="Изменить"
                                            style="margin-left: auto;"
                                        >
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                    <div role="tabpanel" id="tab-6" class="tab-pane">
                        <div class="panel-body">
                            <form @submit.prevent="deleteObject" action="/ru/mediarating/update-object" method="POST">
                                <div class="form-group row">
                                    <label class="col-sm-2 control-label">Выбрать категорию</label>
                                    <div class="col-sm-10 redact_category_conatiner">
                                        <select
                                            name="selected_category"
                                            id="addmedia-mediaobjects_name"
                                            class="form-control"
                                            @input="getCategoryObjects($event.target.value)"
                                            v-model="forms.delete_object.selected_category"
                                        >
                                            <option value="" disabled selected>Выберите категорию</option>
                                            <option :value="category.category" v-for="category in categories" :key="category.category">{{ category.name }}</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group row">
                                    <label class="col-sm-2 control-label">Выбрать объект</label>
                                    <div class="col-sm-10 redact_category_conatiner">
                                        <select
                                            name="selected_category_object"
                                            id="addmedia-mediaobjects_name"
                                            class="form-control"
                                            v-model="forms.delete_object.selected_category_object"
                                        >
                                            <option value="" disabled selected>Выберите объект</option>
                                            <option :value="object.id_category" v-for="object in category_objects" :key="object.id_category">{{ object.name }}</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group row">
                                    <div style="margin-left: auto;margin-right: 15px;">
                                        <input
                                            type="submit"
                                            class="btn btn-danger"
                                            :class="Object.values(forms.delete_object).includes('') ? 'disabled-btn' : 'bg-[#ed5565]'"
                                            id="submit_category"
                                            value="Удалить"
                                            style="margin-left: auto;"
                                        >
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import axios from "axios"

export default {
    name: 'App',
    components: {
    },
    data: () => ({
        categories: [],
        category_objects: [],
        forms: {
            add_category: {
                category: '',
                name: '',
            },
            update_category: {
                selected_category: '',
                category: '',
                name: '',
            },
            delete_category: {
                category: '',
            },
            add_object: {
                selected_category: '',
                name: '',
                info_about: '',
                id_project: '',
            },
            update_object: {
                selected_category: '',
                selected_category_object: '',
                new_category: '',
                name: '',
                info_about: '',
            },
            delete_object: {
                selected_category: '',
                selected_category_object: '',
            },
        }
    }),
    methods: {
        isNumber(event) {
            let value = event?.target?.value ?? '';
            
            const numberRegex = /^\d+$/
            const isNumber = numberRegex.test(value)

            console.log('isNumber(event)', !isNumber && value !== '');

            if (!isNumber && value !== '') {
                value = this.forms.add_object.id_project;
                this.forms.add_object.id_project = undefined;
            }

            this.forms.add_object.id_project = value
        },
        getOnlyTheseValues(obj, except_keys) {
            return Object.keys(obj).filter(key => !except_keys.includes(key)).map(key => obj[key])
        },
        getCategories() {
            axios.get("/ru/mediarating/categories")
                .then(response => {
                    this.categories = response.data ?? []
                })
                .catch(err => console.log(err))
        },
        getCategoryObjects(category) {
            axios.get(`/ru/mediarating/get-category-objects?category=${category}`)
                .then(response => {
                    this.category_objects = response.data
                })
                .catch(err => console.log(err))
        },
        selectObject(id_category) {
            console.log('selectObject - id_category', id_category);
            const selected_object = this.category_objects.find(object => object.id_category == id_category);

            this.forms.update_object.name = selected_object?.name;
            this.forms.update_object.info_about = selected_object?.information_about;
            this.forms.update_object.selected_category_object = id_category ?? '';
        },
        selectCategory(category) {
            const selected_category = this.categories.find(object => object.category == category);

            this.forms.update_category.name = selected_category?.name;
            this.forms.update_category.category = this.forms.update_category.selected_category = category;
        },
        addCategory() {
            this.fetchPost('add', 'category')
        },
        updateCategory() {
            this.fetchPost('update', 'category')
        },
        deleteCategory() {
            this.fetchPost('delete', 'category')
        },
        addObject() {
            this.fetchPost('add', 'object')
        },
        updateObject() {
            this.fetchPost('update', 'object')
        },
        deleteObject() {
            this.fetchPost('delete', 'object')
        },
        fetchPost(action_type, entity) {

            const form_type = action_type+"_"+entity;
            const request_type = action_type+"-"+entity;

            const formData = new FormData();

            Object.keys(this.forms[form_type]).forEach(param => {
                formData.append(param, this.forms[form_type][param]);
                this.forms[form_type][param] = '';
            })

            console.log('formData', formData);
            console.log('delete_object', this.forms[form_type]);

            // axios.post("/ru/mediarating/add-object", formData)
            // axios({
            //     method: "post",
            //     url: `/ru/mediarating/${request_type}`,
            //     data: FormDataEvent,
            //     headers: { "Content-Type": "application/json" }, // multipart/form-data | application/json
            // })
            axios.post(`/ru/mediarating/${request_type}`, formData)
                .then(response => {
                    console.log(`${request_type}`, response);
                })
                .catch(err => console.log(err))
        },
        uploadImage(e) {
            const image = e.target.files[0];
            const reader = new FileReader();
            reader.readAsDataURL(image);
            reader.onload = e => {
                this.forms.add_object.image = e.target.result;
                console.log(this.forms.add_object.image);
            };
        },
    },
    mounted() {
        this.getCategories()
    },
}
</script>
  
<style>
.disabled-btn {
    background-color: rgb(209, 213, 219) !important;
    border-color: rgb(209, 213, 219) !important;
    pointer-events: none !important;
}
</style>
  