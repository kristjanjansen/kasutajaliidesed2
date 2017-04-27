<template>
    
    <div class="EditField">
        <span style="float: right" @click="onDeleteField">×</span>
        <h4>Type</h4>
        <p><span
            style="padding: 3px 6px; line-height: 1.5em; border: 1px solid #ccc; cursor: pointer;"
            :style="{background: field.type === type ? '#ccc' : 'none'}"
            v-for="type in types"
            @click="field.type = type"
        >{{ type }}
        </span></p>
        <template v-if="field.type === 'input'">
            <h4>Label</h4>
            <input
                type="text"
                v-model="field.label"
            >
            <h4>Placeholder</h4>
            <input
                type="text"
                v-model="field.placeholder"
            >
        </template>
        <template v-if="field.type === 'textarea'">
            <h4>Label</h4>
            <input
                type="text"
                v-model="field.label"
            >
            <h4>Rows: {{ field.rows }}</h4>
            <input
                type="range"
                v-model="field.rows"
                min="1"
                max="8"
            >
            <h4>Placeholder</h4>
            <input
                type="text"
                v-model="field.placeholder"
            >
        </template>
        <template v-if="field.type === 'select' || field.type === 'radio'">
            <h4>Label</h4>
            <input
                type="text"
                v-model="field.label"
            >
            <h4>Options</h4>
            <textarea v-model="options" rows="5"></textarea>
        </template>
        <template v-if="field.type === 'help'">
            <h4>Help</h4>
            <input type="text" v-model="field.help">
        </template>

    </div>

</template>

<script>

    export default {
        props: {
            field: { default: () => {} }
        },
        data: () => ({
            types: ['input', 'textarea', 'select', 'checkbox', 'radio', 'help', 'spacer', 'line'],
            options: ''
        }),
        mounted() {
            this.options = this.field.options.join("\n")
        },
        methods: {
            onDeleteField() {
                var doDelete = confirm('Are you sure you want to delete a field?')
                if (doDelete) {
                    this.$emit('deleteField')
                }
            }
        },
        watch: {
            options() {
                this.field.options = this.options.split(/\n/)
            }
        }
    }

</script>

<style>
    .EditField {
        padding: 0.5em 1em 1em 1em;
        background: #eee;
        margin-bottom: 10px;
    }
</style>
