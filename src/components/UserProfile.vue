<template>
    <div class="user-profile">
        <div class="user-profile__user-panel">
            <h1 class="user-profile__username">@{{ user.username }}</h1>
            <div class="user-profile__admin-badge" v-if="user.isAdmin">
                admin
            </div>
            <div class="user-profile__admin-badge" v-if="followers === 1">
                start
            </div>
            <div class="user-profile__admin-badge" v-else-if="followers > 2">
                admin
            </div>
            <div class="user-profile__admin-badge" v-else>
                admin
            </div>
            <div class="user-profile__follower-count">
                <strong> Followers: </strong> {{ followers }}
            </div>
            <form class="user-profile__create-item">
                <br>
                <label for="newItem"><strong> New Item </strong></label>
                <!-- the txt entered is synced up using v-model -->
                <textarea id="newItem" rows="3" v-model="newItemConent"/>

                <div class="user-profile__create-item-type">
                    <label for="newItemType"><strong> Type: </strong></label>
                    <select id="newItemType" v-model="selectedItemType">
                        <option :value="option.value" v-for="(option, index) in itemTypes" :key="index" >
                            {{ option.name }}
                        </option>
                    </select>
                </div>
                       
                <button>
                    Click Me
                </button>
            </form>
        </div>
        <div user-profile__wrapper style="max-width: 700px">
            <!-- for a list we always need an id and we are passing some props at the end -->
            <!-- emited click from childis received -->
            <Items 
            class="user-profile__item" 
            v-for="item in user.someList" 
            :key="item.id" 
            :username="user.username" 
            :item="item" 
            @favorite="toggle" />
        </div>
        
    </div>
</template>

<script>
import Items from "./Items";

export default {
    name: "UserProfile",
    components: { Items },
    data() {
        return {
            newItemContent: '',
            // the default for type
            selectedItemType: 'final',
            itemTypes: [
                { value: 'draft', name:'Draft'},
                { value: 'final', name:'Final'}
            ],

            followers: 0,
            user: {
                id: 1,
                username: 'ehsan-g',
                firstName: 'Ehsan',
                lastName: 'G',
                isAdmin: true,
                someList: [
                    { id: 1, content: "the first item" },
                    { id: 2, content: "the second item" },
                ]
            }
        }
    },
    watch: {
        followers(newFollower, oldFollower) {
            if (oldFollower < newFollower) {
                console.log(`${this.user.followers} has gained a new follower !!`)
            }
        }
    },
    computed: {
        fullname() {
            return `${this.user.firstName} ${this.user.lastName}`;
        }
    },
    methods: {
        followUser() {
            this.followers++;
        },
        toggle(id) {
            alert(`You clicked  id  ${id}`)
        }
    },
    mounted() {
        this.followUser();
    }
};
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: rgb(255, 255, 255);
    border-radius: 5px;
    border: 1px solid #DFE3EB;
}

.user-profile__admin-badge {
    background: rgb(225, 100, 237);
    border-radius: 5px;
    margin: auto;
    padding: 0 10px;
    font-weight: bold;
}

h1 {
    margin: 0;
}

.user-profile__wrapper {
    display: grid;
    grid-gap: 10px;
}

.user-profile__create-item {
    padding-top: 20px;
    display: flex;
    flex-direction: column;
}
</style>