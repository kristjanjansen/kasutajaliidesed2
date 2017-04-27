<template>
    
    <div :class="field.type">
        <template v-if="field.type === 'input'">
            <h4>{{ field.label }}</h4>
            <input
                :type="field.subtype"
                :placeholder="field.placeholder"
            >
        </template>
        <template v-if="field.type === 'textarea'">
            <h4>{{ field.label }}</h4>
            <textarea
                :rows="field.rows"
                :placeholder="field.placeholder"
            ></textarea>
        </template>
        <template v-if="field.type === 'select'">
            <h4>{{ field.label }}</h4>
            <select
                v-if="field.type === 'select'"
            >
                <option v-for="option in field.options">
                    {{ option }}
                </option>
            ></select>
        </template>
        <template v-if="field.type === 'checkbox'">
        <label>
            <input type="checkbox"> {{ field.label }}
        </label>
        </template>
        <template v-if="field.type === 'radio'">
            <h4>{{ field.label }}</h4>
            <label v-for="option in field.options">
                <input type="radio" name="field.label">
                    {{ option }}
            </label>
        </template>
        <template v-if="field.type === 'help'">
            <small>{{ field.help }}</small>
        </template>
        <template v-if="field.type === 'spacer'">
            <div style="height: 2em"></div>
        </template>
        <template v-if="field.type === 'line'">
            <div style="height: 1.5em; border-bottom: 1px solid gray; width: 50%"></div>
            <div style="height: 1.5em"></div>
        </template>
    </div>

</template>

<script>

    export default {
        props: {
            field: { default: () => {} }
        },
        data: () => ({
            id: Math.random() * 100
        })
    }

</script>

<style>
</style>
