<script>
export default {
    name: 'TreeItem',
    props: {
        model: Object
    },
    data() {
        return {
            isOpen: false
        }
    },

    computed: {
        isFolder() {
            return this.model.children && this.model.children.length
        },
    },

    methods: {
        toggle() {
            if (this.isFolder) {
                this.isOpen = !this.isOpen
            }
        },
        changeType() {
            if (!this.isFolder) {
                this.model.children = []
                this.addChild()
                this.isOpen = true
            }
        },
        addChild() {
            this.model.children.push({
                name: 'new stuff'
            })
        }

    }
}
</script>

<template>
    <li>
        <div :class="{ bold: isFolder }" @click="toggle" @dbclick="changeType">
            {{ model.name }}
            <span v-if="isFolder">[{{ isOpen? '-': '+' }}]</span>
        </div>
        <ul v-show="isOpen" v-if="isFolder">
            <TreeItem class="item" v-for="model in model.children" :model="model"></TreeItem>
            <li class="add" @click="addChildren">+</li>
        </ul>
    </li>

</template>