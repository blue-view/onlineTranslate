<template>
    <div class="translateform row">
        <div class="col-md-6 col-md-offset-3">
            <form action="" @submit="formSubmit" class="well form-inline transform">
                <input class="form-control" type="text" placeholder="输入需要翻译的内容" v-model="textToTransLate">
                <select class="form-control" name="" id="" v-model="language">
                    <option value="en">English</option>
                    <option value="ru">russian</option>
                    <option value="kor">korean</option>
                    <option value="jp">japan</option>
                </select>
                <input class="btn btn-primary" type="submit" value="翻译">
            </form>
        </div>

    </div>
</template>

<script>
export default {
    name: 'translateform',
    data() {
        return {
            textToTransLate: '',
            language: ''
        }
    },
    methods: {
        formSubmit: function(e) {
            // alert(this.textToTransLate);
            this.$emit("formSubmit", this.textToTransLate, this.language);
            e.preventDefault();

        }
    },
    created:function(){
        this.language="en";
    }
}
</script>

<style scoped>
.transform{
    border: 1px solid #ccc;
    border-radius: 10px;
}
</style>
