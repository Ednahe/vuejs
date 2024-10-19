<template>
    <div>
        <label>
            <input type="checkbox" @change="onChange"/>
            {{ label }}
        </label>
    </div>   
</template>

<script setup>
defineProps({
    label: String
})

const emits = defineEmits(['checked', 'unchecked'])
const onChange = (e) => {
    if (e.currentTarget.checked) {
        emits('checked', e.currentTarget)
    } else {
        emits('unchecked', e.currentTarget)
    }
}
</script>