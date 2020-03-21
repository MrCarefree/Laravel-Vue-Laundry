<!-- HTML SECTION -->
<template>
    <div class="login-box">
        <div class="login-logo">
            <router-link :to="{ name: 'home' }">
                <b>AB</b>Laundry
            </router-link>
        </div>
        <!-- /.login-logo -->
        <div class="card">
            <div class="card-body login-card-body">
                <p class="login-box-msg">Sign in to start your session</p>

                <div class="alert alert-danger alert-dismissible fade show" v-if="errors.invalid">
                    <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                    <h5>
                        <i class="icon fas fa-ban"></i> Invalid
                    </h5>
                    {{ errors.invalid }}
                </div>

                <form action="../../index3.html" method="post">
                    <div class="input-group mb-3">
                        <input
                            type="email"
                            class="form-control"
                            :class="{'is-invalid': errors.email}"
                            placeholder="Email"
                            v-model="data.email"
                        />
                        <div class="input-group-append">
                            <div class="input-group-text">
                                <span class="fas fa-envelope"></span>
                            </div>
                        </div>
                        <div class="invalid-feedback" v-if="errors.email">{{ errors.email[0] }}</div>
                    </div>
                    <div class="input-group mb-3">
                        <input
                            type="password"
                            class="form-control"
                            placeholder="Password"
                            v-model="data.password"
                            :class="{'is-invalid': errors.password}"
                        />
                        <div class="input-group-append">
                            <div class="input-group-text">
                                <span class="fas fa-lock"></span>
                            </div>
                        </div>
                        <div class="invalid-feedback" v-if="errors.password">{{ errors.password[0] }}</div>
                    </div>

                    <div class="row">
                        <div class="col-8">
                            <div class="icheck-primary">
                                <input type="checkbox" id="remember" v-model="data.remember_me"/>
                                <label for="remember">Remember Me</label>
                            </div>
                        </div>
                        <!-- /.col -->
                        <div class="col-4">
                            <button
                                type="submit"
                                class="btn btn-primary btn-block"
                                @click.prevent="postLogin"
                            >Sign In
                            </button>
                        </div>
                        <!-- /.col -->
                    </div>
                </form>
                <!-- /.login-card-body -->
            </div>
        </div>
        <!-- /.login-box -->
    </div>
</template>

<!-- JAVASCRIPT SECTION -->
<script>
    import {mapActions, mapMutations, mapGetters, mapState} from "vuex";

    export default {
        data() {
            return {
                data: {
                    email: "",
                    password: "",
                    remember_me: false
                }
            };
        },
        //SEBELUM COMPONENT DI-RENDER
        created() {
            //KITA MELAKUKAN PENGECEKAN JIKA SUDAH LOGIN DIMANA VALUE isAuth BERNILAI TRUE
            if (this.isAuth) {
                //MAKA DI-DIRECT KE ROUTE DENGAN NAME home
                this.$router.push({name: "home"});
            }
        },
        computed: {
            ...mapGetters(["isAuth"]), //MENGAMBIL GETTERS isAuth DARI VUEX
            ...mapState(["errors"])
        },
        methods: {
            ...mapActions("auth", ["submit"]), //MENGISIASI FUNGSI submit() DARI VUEX AGAR DAPAT DIGUNAKAN PADA COMPONENT TERKAIT. submit() BERASAL DARI ACTION PADA FOLDER STORES/auth.js
            ...mapMutations(["CLEAR_ERRORS"]),

            //KETIKA TOMBOL LOGIN DITEKAN, MAKA AKAN MEMINCU METHODS postLogin()
            postLogin() {
                //DIMANA TOMBOL INI AKAN MENJALANKAN FUNGSI submit() DENGAN MENGIRIMKAN DATA YANG DIBUTUHKAN
                this.submit(this.data).then(() => {
                    //KEMUDIAN DI CEK VALUE DARI isAuth
                    //APABILA BERNILAI TRUE
                    if (this.isAuth) {
                        this.CLEAR_ERRORS();
                        //MAKA AKAN DI-DIRECT KE ROUTE DENGAN NAME home
                        this.$router.push({name: "home"});
                    }
                });
            }
        }
    };
</script>
