<template>
    <div class="ct-modal ct-fixed ct-z-50 ct-top-0 ct-left-0 ct-flex ct-items-center ct-justify-center" :class="{'ct-opacity-0': this.$store.state.addRequestFeatureActive,'ct-pointer-events-none': this.$store.state.addRequestFeatureActive, 'ct-modal-active': this.$store.state.addRequestFeatureActive}">
        <div class="ct-modal-overlay ct-absolute ct-w-screen ct-h-screen ct-bg-gray-800 ct-opacity-50"></div>

        <!-- Form Card -->

        <div class="ct-card ct-bg-white ct-flex ct-flex-col ct-p-4 ct-z-50 ct-rounded ct-shadow-lg z-50">
            <div class=" ct-px-2 ct-flex ct-flex-row ct-justify-between ct-align-items ct-mt-2">
               <p class="ct-flex ct-justify-start ct-text-2xl ct-font-bold">Request Feature</p>
               <div class="ct-cursor-pointer ct-flex" @click="modalControl">
                   <img src="@/assets/closeicon.svg" alt="" class="ct-w-4 ct-h-4 ct-mt-2"/>
               </div>
            </div>

            <!-- Request form start -->
            <form class="ct-w-full ct-px-2 ct-pt-10 ct-flex ct-flex-col" @submit.prevent="addRequestedFeatures()">
                <div class="ct-mb-20">
                    <div class="ct-flex ct-flex-col ct-mb-4">
                        <label class="ct-font-bold ct-mb-2" for="username">Username</label>
                        <input type="text" name="username" class="ct-shadow ct-appearance-none ct-w-full ct-bg-white ct-text-gray-700 ct-border ct-rounded ct-py-3 ct-px-4 ct-mb-3 ct-focus:outline-none ct-focus:bg-white" id="username" v-model="data.userName">
                    </div>
                    <div class="ct-flex ct-flex-col ct-mb-4">
                        <label class="ct-font-bold ct-mb-2" for="requestname">Name of Request</label>
                        <input type="text" name="requestname" class="ct-shadow ct-appearance-none ct-w-full ct-bg-white ct-text-gray-700 ct-border ct-rounded ct-py-3 ct-px-4 ct-mb-3 ct-focus:outline-none ct-focus:bg-white" id="requestname" v-model="data.requestName">
                    </div>
                    <div class="ct-flex ct-flex-col">
                        <div class="ct-mb-2">
                            <label class="ct-font-bold" for="votingtime">Allocated time for voting </label><span>(in minutes)</span>
                        </div>
                        <input type="text" name="votingtime" class="ct-shadow ct-appearance-none ct-w-full ct-bg-white ct-text-gray-700 ct-border ct-rounded ct-py-3 ct-px-4 ct-mb-3 ct-focus:outline-none ct-focus:bg-white" id="votingtime" v-model="data.votingTime">
                    </div>
                </div>
                <div class="ct-cursor-pointer ct-flex ct-justify-end ct-mt-4">
                    <button type="submit" class="ct-w-36  ct-bg-green-500 ct-p-3 ct-px-4 hover:ct-bg-green-400 ct-rounded ct-text-white">Request Feature</button>
                </div>
            </form>
        <!-- Request form end -->

        </div>
    </div>
</template>

<script>
import { mapActions } from 'vuex'
    export default {
        name: 'RequestFeatureModal',
        data() {
            return {
                data: {
                userName: '',
                votingTime: '',
                requestName: '',
                }
            }
        },
        methods: {
            ...mapActions([
                'addRequestedFeatures'
            ]),
            modalControl(){
                this.$store.commit('toggleRequestModal');
            },
            async addRequestedFeatures() {
                try {
                    let user_name = this.data.userName
                    let voting_time = this.data.votingTime
                    let request_name = this.data.requestName
                    const payload = {
                        user_name,
                        voting_time,
                        request_name
                    }
                    this.addRequestedFeatures(payload)
                } catch (err) {
                    console.log(err)
                }
            }
        },
        computed:{
        },
    }
</script>

<style scoped>
.ct-modal {
    transition: opacity 0.25s ease;
    width: 100vw;
    height: 100vh;
}
.ct-card {
    width: 420px;
    height: auto;
}
body.ct-modal-active {
    overflow-x: hidden;
    overflow-y: visible !important;
}

button{
    width: 13rem !important;
}

input{
    border-color: #A1A1A1 !important;
}

</style>