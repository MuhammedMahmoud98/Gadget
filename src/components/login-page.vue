<template>
    <section class="ma-auto">
        <v-alert :value="hasErr" type="error" transition="scale-transition">
            Wrong credentials! please try again.
        </v-alert>
        <v-progress-linear
                indeterminate
                color="primary"
                :active="loading"
        ></v-progress-linear>
        <v-row>
            <v-col>
                <div class="card-bg">
                    <div class="login-header text-center">
                        <h1>Welcome Back</h1>
                        <p class="credentials-text">Enter you credentials to access your account</p>
                    </div>
                    <div class="login-body">
                        <v-form v-model="valid">
                            <v-container>
                                <v-row>
                                    <v-col cols="12">
                                        <v-text-field
                                                v-model="userName"
                                                :rules="nameRules"
                                                :counter="15"
                                                append-icon="mdi-account"
                                                label="Username"
                                                required
                                        ></v-text-field>
                                    </v-col>
                                    <v-col cols="12">
                                        <v-text-field
                                                type="password"
                                                v-model="userPassword"
                                                :rules="passwordRules"
                                                :counter="10"
                                                append-icon="mdi-lock"
                                                label="Password"
                                                required
                                        ></v-text-field>
                                    </v-col>
                                    <v-col col="12">
                                        <v-btn @click="loginWithCredentials" block :disabled="!valid || loading" class="v-text-field--full-width" color="primary">Sign in</v-btn>
                                    </v-col>
                                </v-row>
                            </v-container>
                        </v-form>
                    </div>
                </div>
            </v-col>
        </v-row>
    </section>
</template>

<script>
    import axios from 'axios';
    export default {
        data: () => ({
            valid: false,
            userName: '',
            nameRules: [
                v => !!v || 'Username is required',
                v => /.+@.+\..+/.test(v) || 'user name must be valid',
                v => v.length <= 20 || 'user name must be less than 20 characters',
            ],
            userPassword: '',
            passwordRules: [
                v => !!v || 'Username is required',
                v => v.length >= 6 || 'Password is less than 6 chars',
                v => v.length <= 10 || 'Password is greater than 10 chars',
            ],
            loading: false,
            hasErr: false,
        }),
        methods: {
            async loginWithCredentials() {
                this.loading = true;
                const loginResponse = await axios.post('https://gadget404.herokuapp.com/login', {
                    username: this.username,
                    password: this.password
                });
                this.loading = false;
                if (loginResponse.data.code === 401) {
                    return this.hasErr = true;
                }
                this.hasErr = false;
                console.log(loginResponse.data.code);
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .card-bg {
        background-color: #fff;
        border-radius: 7px;
        padding: 3rem 1.5rem;
        box-shadow: 0px 0px 10px rgba(38, 127, 255, 0.06);
    }

    .card-bg .credentials-text {
        color: #C2CCD9;
    }
</style>
