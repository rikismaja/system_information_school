<template>
    <header id="page-topbar">
        <div class="navbar-header">
            <div class="d-flex">
                <div class="navbar-brand-box">
                    <a href="index.html" class="logo logo-dark">
                        <span class="logo-sm">
                            <img src="/vendor/template/images/logo-sm-dark.png" alt="" height="22">
                        </span>
                        <span class="logo-lg">
                            <img src="/vendor/template/images/logo-dark.png" alt="" height="20">
                        </span>
                    </a>
                    <a href="index.html" class="logo logo-light">
                        <span class="logo-sm">
                            <img src="/vendor/template/images/logo-sm-light.png" alt="" height="22">
                        </span>
                        <span class="logo-lg">
                            <img src="/vendor/template/images/logo-light.png" alt="" height="20">
                        </span>
                    </a>
                </div>
                <button type="button" class="btn btn-sm px-3 font-size-24 header-item waves-effect" id="vertical-menu-btn">
                    <i class="mdi mdi-backburger"></i>
                </button>
                <form class="app-search d-none d-lg-block" @submit.prevent="searchData">
                    <div class="position-relative">
                        <input type="text" class="form-control" placeholder="Search..." v-model="searchingData">
                        <span class="mdi mdi-magnify"></span>
                    </div>
                </form>
            </div>
            <div class="d-flex">
                <div class="dropdown d-inline-block d-lg-none ml-2">
                    <button type="button" class="btn header-item noti-icon waves-effect" id="page-header-search-dropdown" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        <i class="mdi mdi-magnify"></i>
                    </button>
                    <div class="dropdown-menu dropdown-menu-lg dropdown-menu-right p-0" aria-labelledby="page-header-search-dropdown">
                        <form class="p-3" @submit.prevent="searchData">
                            <div class="form-group m-0">
                                <div class="input-group">
                                    <input type="text" class="form-control" placeholder="Search ..." aria-label="Recipient's username" v-model="searchingData">
                                    <div class="input-group-append">
                                        <button class="btn btn-primary" type="submit"><i class="mdi mdi-magnify"></i></button>
                                    </div>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
                <div class="dropdown d-inline-block">
                    <button type="button" class="btn header-item waves-effect" id="page-header-flag-dropdown" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        <img class="" src="/vendor/template/images/flags/us.jpg" alt="Header Language" height="14">
                    </button>
                    <div class="dropdown-menu dropdown-menu-right">
                        <a href="javascript:void(0);" class="dropdown-item notify-item">
                            <img src="/vendor/template/images/flags/spain.jpg" alt="user-image" class="mr-2" height="12"><span class="align-middle">Spanish</span>
                        </a>
                        <a href="javascript:void(0);" class="dropdown-item notify-item">
                            <img src="/vendor/template/images/flags/us.jpg" alt="user-image" class="mr-2" height="12"><span class="align-middle">English</span>
                        </a>
                    </div>
                </div>
                <div class="dropdown d-inline-block">
                    <button type="button" class="btn header-item noti-icon right-bar-toggle waves-effect">
                        <i class="mdi mdi-tune"></i>
                    </button>
                </div>
                <div class="dropdown d-inline-block">
                    <button type="button" class="btn header-item waves-effect" id="page-header-user-dropdown" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        <img class="rounded-circle header-profile-user" :src="'/storage/image/' + user.avatar" alt="Avatar Profile">
                        <span class="d-none d-sm-inline-block ml-1">{{user.name}}</span>
                        <i class="mdi mdi-chevron-down d-none d-sm-inline-block"></i>
                    </button>
                    <div class="dropdown-menu dropdown-menu-right">
                        <a class="dropdown-item" href="#"><i class="mdi mdi-lock font-size-16 align-middle mr-1"></i> Lock screen</a>
                        <div class="dropdown-divider"></div>
                        <a class="dropdown-item" href="#" v-on:click="logout"><i class="mdi mdi-logout font-size-16 align-middle mr-1"></i> Logout</a>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>
<script>
export default{
    data() {
        return {
            user : this.$store.state.Users.user,
            searchingData : ''
        }
    },
    methods : {
        async searchData() {
            if(this.searchingData == '') {
                return false;
            } else {
                let User = JSON.parse(window.localStorage.getItem('users'));
                if (User && User.user.role == 'admin' || User.user.role == 'administrator') {
                    return window.location.href = '/admin/search/' + this.searchingData;
                }
                if(User && User.user.role == 'teacher') {
                    return window.location.href = '/teacher/search/' + this.searchingData;
                } 
            }
        },
        logout() {
            window.localStorage.removeItem('users');
            return window.location.href = '/';
        }
    }
}
</script>