<template>
<div class="user-profile">
    <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ user.username }}</h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile__follower-count">
            <strong>followers: {{ followers }}</strong>
        </div>
        <button v-on:click="followUser">Follow</button> <!-- Method followUser is bieng called on button press -->
    </div>
    <div class="user-profile__tw00ts-wrapper">
        <div class="user-profile__tw00t" v-for="tw00t in user.tw00ts" :key="tw00t.id">
            {{ tw00t.content }}
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'UserProfile',
    data() { //We can add various data points for default sate of component
        return {
            followers: 0,
            user: {
                id: 1,
                username: "CJHackerz",
                firstname: 'Chirag',
                lastname: 'Jariwala',
                email: 'cjhackerz@1337.com',
                isAdmin: true,
                tw00ts: [{
                        id: 1,
                        content: 'The original twitter is cancer, welcome to amazing tw00ter'
                    },
                    {
                        id: 2,
                        content: "Don't forget to follow me back!"
                    }
                ]
            }
        }
    },
    watch: {
        followers(newFollowersCount, oldFollowerCount) {
            if (oldFollowerCount < newFollowersCount) {
                console.log(`${this.user.username} has gained a follower`)
            }
        }
    },
    computed: { //Process data
        fullName() {
            return `${this.user.firstname} ${this.user.lastname}`;
        }
    },
    methods: { //Reactive methods that will get executed on certain user interaction such as press of a button
        followUser() {
            this.followers++
        }
    },
    mounted() {
        this.followUser();
    }
}
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
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile__admin-badge {
    background: green;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;

}
</style>
