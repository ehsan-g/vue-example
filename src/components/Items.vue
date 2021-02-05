<template>
    <div class="items">
        <div class="user-profile__item">
            <div class="items__user">
                @{{ username }}
            </div>
            <div class="items__content">
                {{ item.content }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Items",
    props: {
        username: {
            type: String,
            required: true
        },
        item: {
            type: Object,
            required: true
        }
    }
};
</script>

<style>
.items {
    padding:20px;
    background-color: azure;
    border-radius: 5px;
    border: 1px solid #dfdfdf;
    box-sizing: border-box;
    cursor: pointer;
    transition: all 0.2s ease;
}

.items:hover {
    transform: scale(1.1, 1.1);
}

.items_user {
    font-weight: bold;
}

</style>