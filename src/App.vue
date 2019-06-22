<template>
    <div class="container">
        <form>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <h1>File a Complaint</h1>
                    <hr>
                     <div class="form-group">
                        <label for="fullName">Full Name</label>
                        <input
                                type="text"
                                id="fullName"
                                class="form-control"
                                v-bind:value="userDataObject.vFullNameModel"
                                @input="userDataObject.vFullNameModel = $event.target.value">

                    </div>

                    <div class="form-group">
                        <label for="email">Mail</label>
                        <input
                                type="text"
                                id="email"
                                class="form-control"
                                v-model="userDataObject.vEmailModel">

                    </div>
                    <div class="form-group">
                        <label for="password">Password</label>
                        <input
                                type="password"
                                id="password"
                                class="form-control"
                                v-model.lazy="userDataObject.vPasswordModel">
                                <p> {{ userDataObject.vPasswordModel }} </p>
                    </div>
                    <div class="form-group">
                        <label for="age">Age</label>
                        <input
                                type="number"
                                id="age"
                                class="form-control"
                                v-model="userDataObject.vAgeModel">
                    </div>

                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 form-group">
                    <label for="message">Message</label><br>
                    <!-- Interpolation between <textarea>{{ test }}</textarea> doesn't work!-->
                    <textarea
                            id="message"
                            rows="5"
                            class="form-control"
                            v-model="vMessageModel"></textarea>
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <div class="form-group">
                        <label for="sendmail">
                            <input
                                    type="checkbox"
                                    id="sendmail"
                                    value="SendMail"
                                    v-model="vSendMailModel"> Send Mail
                        </label>
                        <label for="sendInfomail">
                            <input
                                    type="checkbox"
                                    id="sendInfomail"
                                    value="SendInfoMail"
                                    v-model="vSendMailModel"> Send Infomail
                        </label>
                    </div>

                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 form-group">
                    <label for="male">
                        <input
                                type="radio"
                                id="male"
                                value="Male"
                                v-model="vGenderModel"> Male
                    </label>
                    <label for="female">
                        <input
                                type="radio"
                                id="female"
                                value="Female"
                                v-model="vGenderModel"> Female
                    </label>
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 from-group">
                    <label for="priority">Priority</label>
                    <select 
                            id="priority"
                            class="form-control"
                            v-model="vSelectedPriorityModel">
                        <option 
                        v-for="priority in vPrioritiesModel"
                        v-bind:key="priority"
                        :selected="priority == 'Medium'"
                        > {{ priority }}</option>
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <app-switch v-model="vDataSwitchModel"></app-switch>                   
                </div>
            </div>
            <hr>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <button
                            class="btn btn-primary"
                            @click.prevent="submitted">Submit!
                    </button>
                </div>
            </div>
        </form>
        <hr>
        <div class="row" v-if="isSubmitted">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <div class="panel panel-default">
                    <div class="panel-heading">
                        <h4>Your Data</h4>
                    </div>
                    <div class="panel-body">
                        <p>Full Name: {{ userDataObject.vFullNameModel }}
                        <p>Mail: {{ userDataObject.vEmailModel }}</p>
                        <p>Password: {{ userDataObject.vPasswordModel }}</p>
                        <p>Age:{{ userDataObject.vAgeModel }}</p>
                        <p style="white-space: pre">Message: {{ vMessageModel }}</p>
                        <p><strong>Send Mail?</strong></p>
                        <ul>
                            <li 
                            v-for="mail in vSendMailModel"
                            v-bind:key="mail"
                            >{{ mail }}</li>
                        </ul>
                        <p>Gender: {{ vGenderModel }}</p>
                        <p>Priority: {{ vSelectedPriorityModel }}</p>
                        <p>Switched: {{ vDataSwitchModel }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Switcher from './Switcher.vue';
    export default {
        data () {
            return {
                userDataObject: {
                  vFullNameModel: '',
                  vEmailModel: '',
                  vPasswordModel: '',
                  vAgeModel: 27  
                },
                vMessageModel : 'A new Text',
                vSendMailModel: [],
                vGenderModel: 'Male',
                vSelectedPriorityModel: 'High',
                vPrioritiesModel: ['High', 'Medium', 'Low'],
                vDataSwitchModel: true,
                isSubmitted: false
                
            }
        },
        methods: {
            submitted() {
                this.isSubmitted = true;
            }
        },
        components: {
        appSwitch: Switcher
    }
    
    }
</script>

<style>

</style>
