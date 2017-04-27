<template>

    <div id="app" style="display: flex">
        <div style="flex: 1">
        <component
            v-for="field in fields"
            is="ShowField"
            :field="field"
            key="field"
        >    
        </component>
        </div>
        <div style="flex: 1">
        <component
            v-for="(field, key) in fields"
            is="EditField"
            :field="field"
            @deleteField="deleteField(key)"
            key="field"
        >    
        </component>
        <big @click="addField">+</big>
        </div>
    </div>

</template>

<script>

    import ShowField from './components/ShowField.vue'
    import EditField from './components/EditField.vue'

    export default {
        name: 'App',
        components: { ShowField, EditField },
        methods: {
            addField() {
                this.fields.push({
                    type: 'input',
                    subtype: 'text',
                    label: 'I am a field',
                    placeholder: 'I am a placeholder',
                    rows: 5,
                    options: ['Some', 'Options'],
                    help: 'I am help text'
                })
            },
            deleteField(key) {
                this.$delete(this.fields, key)
            }
        },
        data: () => ({ fields: []}),
        mounted() {
            this.$watch(
                'fields',
                fields => localStorage.fields = JSON.stringify(fields),
                { deep: true }
            )
            
            if (localStorage.fields) {
                this.fields = JSON.parse(localStorage.fields)
            } else {
                this.addField()
            }
            
        }
    }

</script>

<style>

    body {
        font-family: sans-serif;
        margin: 0;
        padding: 2rem;
        font-size: 16px;
    }

    input, textarea, select, option {
        ddisplay: block;
        font-size: 16px;
        border: 2px solid #ccc;
        padding: 0.5em;
        border-radius: 3px;
    }
    hr {
        border: 1px solid #ddd;
    }
    p {
        margin: 0.5em 0;
        display: block;
    }
    h4 {
        margin: 0.75em 0 0.5em 0;
    }
    h4:first-child {
        margin-top: 0;
    }
    small {
        opacity: 0.5;
        font-size: 1em;
        margin: 0.25em 0;
        display: block;
    }
    label, input {
        display: block;
    }
    input[type=radio], input[type=checkbox] {
        display: inline;
    }
</style>
