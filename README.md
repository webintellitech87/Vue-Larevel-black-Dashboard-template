# [Vue Black Dashboard Laravel]

*Frontend version*: Black Dashboard v1.0.1.
*Vue version*: Vue Black Dashboard v1.1.1.


What if your frontend came not only with reusable components, but also with a reusable backend? API-driven development is more than just a buzzword and we partnered with [UPDIVISION](https://updivision.com) to prove it. Build awesome-looking apps with a flexible architecture across a variety of devices and operating systems with Vue Black Dashboard Laravel. 

# Download

For the free version of the project you can either
- download the .zip file from the Creative Tim site and extract it or 
- make a clone from the Github repository

You will get two project folders: one for the Laravel API project and one for the Vue frontend.

# Laravel API Setup

## Introduction

JSON:API is a specification for how a client should request that resources be fetched or modified, and how a server should respond to those requests. It is designed to minimize both the number of requests and the amount of data transmitted between clients and servers. This efficiency is achieved without compromising readability, flexibility, or discoverability.

[Click here to go to the JSON:API docs](https://explore.postman.com/api/6357/laravel-jsonapi)

## Prerequisites

### JSON:API backend
The Laravel JSON:API backend project requires a proper multi-threaded web server such as Apache/Nginx environment with PHP, Composer and MySQL.

**Do not use `php artisan serve` as it will result in stalled requests due to the single-threaded nature of the built-in PHP web server.** 

We strongly recommend using [Laradock](https://laradock.io/) for Linux and Mac or [Laragon](https://laragon.org/download/) for Windows if possible.

Other options for your local environment:
- Windows: [How to install WAMP on Windows](https://updivision.com/blog/post/beginner-s-guide-to-setting-up-your-local-development-environment-on-windows)
- Linux: [How to install LAMP on Linux](https://howtoubuntu.org/how-to-install-lamp-on-ubuntu)
- Mac: [How to install MAMP on MAC](https://wpshout.com/quick-guides/how-to-install-mamp-on-your-mac/)

You will also need to install Composer 2: [https://getcomposer.org/doc/00-intro.md](https://getcomposer.org/doc/00-intro.md)

### Vue Black frontend
The Vue Black frontend project requires a working local environment with NodeJS version 8.9 or above (8.11.0+ recommended), npm, VueCLI.

Install Node: https://nodejs.org/ (version 8.11.0+ recommended)

Install NPM: https://www.npmjs.com/get-npm

Install VueCLI: https://cli.vuejs.org/guide/installation.html

## Laravel JSON:API Project Installation

1. Navigate in your Laravel API project folder: `cd your-laravel-json-api-project`
2. Install project dependencies: `composer install`
3. Create a new .env file: `cp .env.example .env`
3. Add your own database credentials in the .env file in DB_DATABASE, DB_USERNAME, DB_PASSWORD
5. Create users table: `php artisan migrate --seed`
6. Generate application key: `php artisan key:generate`
7. Install Laravel Passport: `php artisan passport:install`
8. Add your own mailtrap.io credentials in MAIL_USERNAME and MAIL_PASSWORD in the .env file

## Vue Black Dashboard Project Installation

1. Navigate to your Vue Dashboard project folder:  `cd your-vue-black-dashbord-project`
2. Install project dependencies: `npm install`
3. Create a new .env file: `cp .env.example .env`
4. `VUE_APP_BASE_URL` should contain the URL of your Vue Black Dashboard Project (eg. http://localhost:8080/)
5. `VUE_APP_API_BASE_URL` should contain the URL of your Laravel JSON:API Project. (eg. http://localhost:3000/api/v1)
6. Run `npm run dev` to start the application in a local development environment or `npm run build`  to build release distributables.

## Usage

Register a user or login using admin@jsonapi.com and secret and start testing the theme.

Besides the dashboard and the auth pages this theme also has an edit profile page. All the necessary files are installed out of the box and all the needed routes are added to `src\router\index.js`. Keep in mind that all the features can be viewed once you log in using the credentials provided above or by registering your own user.

### Dashboard

You can access the dashboard either by using the "**Dashboards/Dashboard**" link in the left sidebar or by adding **/home** in the URL.

### Login

The login functionality is fully implemented in our theme helping you to start your project in no time. To login into dashboard you just have to add **/login** in the URL and fill the login form with the credentials (user: **admin@jsonapi.com** and password: **secret**).

The `src\pages\Login.vue` is the Vue component which handles the login functinality. You can easily adapt it to your needs.

It uses the auth store located in `src\store\modules\auth.js`.

#### Login card
```
<div class="col-lg-4 col-md-6 ml-auto mr-auto">
  <form @submit.prevent="handleSubmit()">
    <card class="card-login card-white">
      <template slot="header">
        <img src="/img/card-primary.png" alt="" />
        <h1 class="card-title">Log in</h1>
      </template>

      <div>
        <ValidationProvider
          name="email"
          rules="required|email"
          v-slot="{ passed, failed, errors }"
        >
        <base-input
          required
          v-model="email"
          type="email"
          placeholder="Email"
          addon-left-icon="tim-icons icon-email-85"
          :error="errors[0]"
          :class="[{ 'has-success': passed }, { 'has-danger': failed }]">
        </base-input>
        <validation-error :errors="apiValidationErrors.email" />
        </ValidationProvider>

        <ValidationProvider
          name="password"
          rules="required|min:5"
          v-slot="{ passed, failed, errors }"
        >
        <base-input
          required
          v-model="password"
          placeholder="Password"
          addon-left-icon="tim-icons icon-lock-circle"
          type="password"
          :error="errors[0]"
          :class="[{ 'has-success': passed }, { 'has-danger': failed }]">
        </base-input>
        <validation-error :errors="apiValidationErrors.password" />
      </ValidationProvider>
      </div>

      <div slot="footer">
        <base-button native-type="submit" type="primary" class="mb-3" size="lg" block>
          Get Started
        </base-button>
        <div class="pull-left">
          <h6>
            <router-link class="link footer-link" to="/register">
              Create Account
            </router-link>
          </h6>
        </div>

        <div class="pull-right">
          <h6><a href="#pablo" class="link footer-link">Need Help?</a></h6>
        </div>
      </div>
    </card>
  </form>
  <!-- </ValidationObserver> -->
</div>
```

### Register

The register functionality is fully implemented in our theme helping you to start your project in no time. To register a new user you just have to add **/register** in the URL or click on register link from login page and fill the register form with user details.

The `src\pages\Register.vue` is the Vue component which handles the login functinality. You can easily extend it to your needs.

It uses the auth store located in `src\store\modules\auth.js`.

#### Register card
```
<div class="col-md-7 mr-auto">
  <form @submit.prevent="handleSubmit()">
    <card class="card-register card-white">
      <template slot="header">
        <img class="card-img" src="/img/card-primary.png" alt="Card image"/>
        <h4 class="card-title">Register</h4>
      </template>

      <ValidationProvider name="name" rules="required" v-slot="{ passed, failed, errors }">
        <base-input
          required
          v-model="name"
          placeholder="Full Name"
          addon-left-icon="tim-icons icon-single-02"
          type="text"
          :error="errors[0]"
          :class="[{ 'has-success': passed }, { 'has-danger': failed }]">
        </base-input>
      </ValidationProvider>

      <ValidationProvider name="email" rules="required|email" v-slot="{ passed, failed, errors }">
        <base-input
          required
          v-model="email"
          placeholder="Email"
          addon-left-icon="tim-icons icon-email-85"
          type="email"
          :error="errors[0]"
          :class="[{ 'has-success': passed }, { 'has-danger': failed }]">
        </base-input>
      </ValidationProvider>

      <ValidationProvider name="password" rules="required" v-slot="{ passed, failed, errors }">
        <base-input
          required
          v-model="password"
          placeholder="Password"
          addon-left-icon="tim-icons icon-lock-circle"
          type="password"
          :error="errors[0]"
          :class="[{ 'has-success': passed }, { 'has-danger': failed }]">
        </base-input>
      </ValidationProvider>

      <ValidationProvider name="password" rules="required" v-slot="{ passed, failed, errors }">
        <base-input
          required
          placeholder="Confirm Password"
          type="password"
          name="Password confirmation"
          v-model="password_confirmation"
          addon-left-icon="tim-icons icon-lock-circle"
          :error="errors[0]"
          :class="[{ 'has-success': passed }, { 'has-danger': failed }]">
        </base-input>
      </ValidationProvider>

      <base-checkbox v-model="boolean" class="text-left">
        I agree to the <a href="#something">terms and conditions</a>.
      </base-checkbox>

      <base-button native-type="submit" slot="footer" type="primary" round block size="lg">
        Get Started
      </base-button>
    </card>
  </form>
</div>
```

### Profile edit

You have the option to edit the current logged in user's profile information (name, email, profile picture) and password. To access this page, just click the "**Examples/Profile**" link in the left sidebar or add **/profile** in the URL.

The `src\pages\Examples\UserProfile` is the folder with Vue components that handle the update of the user information and password.

#### Edit profile component
```
<template>
  <card class="stacked-form" title="Stacked Form">
    <h4 slot="header" class="card-title">Edit Profile</h4>
    <form @submit.prevent>
      <base-input v-model="user.email" label="Email" type="email" placeholder="Enter email"/>
      <validation-error :errors="apiValidationErrors.email" /> 
      <base-input v-model="user.name" label="Name" placeholder="Name"/>
      <validation-error :errors="apiValidationErrors.name" />
      <base-button @click="updateProfile()" class="mt-3" native-type="submit" type="primary">Submit</base-button>
    </form>
  </card>
</template>

<script>
import ValidationError from "@/components/ValidationError.vue";
import formMixin from "@/mixins/form-mixin";
export default {
  mixins: [formMixin],
  components: {
    ValidationError
  },
  props: {
      user: Object
    },
  methods: {
     async updateProfile() {
        try {
          await this.$store.dispatch("profile/update", this.user)
          this.resetApiValidation();
          this.$notify({
            type: 'success',
            message: 'Profile updated successfully.',
            icon: 'tim-icons icon-bell-55',
          })
          await this.$store.getters["profile/me"]
        } catch (e) {
          this.$notify({
            type: 'danger',
            message: 'Oops, something went wrong!',
            icon: 'tim-icons icon-bell-55',
          })
          this.setApiValidation(e.response.data.errors)
        }
    }
  }
}
</script>
```
#### Edit password component
```
<template>
  <card class="stacked-form" title="Change Password">
    <h4 slot="header" class="card-title">Change Password</h4>
    <form ref="password_form" @submit.prevent>
      <div>
        <base-input v-model="password" label="Password" type="password" placeholder="Password"/>
        <validation-error :errors="apiValidationErrors.password"/>
        <base-input v-model="password_confirmation" label="Password Confirmation" type="password" placeholder="Password Confirmation"/>
        <validation-error :errors="apiValidationErrors.password_confirmation"/>
        <base-button class="mt-3" native-type="submit" type="primary" @click="changePassword()"
          >Submit</base-button
        >
      </div>
    </form>
  </card>
</template>
<script>
  import ValidationError from "@/components/ValidationError.vue";
  import formMixin from "@/mixins/form-mixin";
  export default {
    name: "edit-password-card",

    props: {
      user: Object
    },

    components: {ValidationError},

    mixins: [formMixin],

    data: () => ({
      password: null,
      password_confirmation: null,
    }),

    methods: {
      async changePassword() {
        this.user.password = this.password;
        this.user.password_confirmation = this.password_confirmation;

        try {
          this.resetApiValidation();
          await this.$store.dispatch("users/update", this.user)
          this.$notify({
            type: 'success',
            message: 'Password changed successfully.',
            icon: 'tim-icons icon-bell-55',
          })
          this.user = await this.$store.getters["profile/me"]
          this.$refs["password_form"].reset();
        } catch (e) {
          this.$notify({
            type: 'danger',
            message: 'Oops, something went wrong!',
            icon: 'tim-icons icon-bell-55',
          })
          this.setApiValidation(e.response.data.errors)
        }
      }
    }
  };
</script>
```


## File Structure
```
|   .browserslistrc
|   .eslintrc.js
|   .gitignore
|   .jshintrc
|   babel.config.js
|   CHANGELOG.md
|   package-lock.json
|   package.json
|   postcss.config.js
|   README.md
|   yarn.lock
|
+---public
|   |   .DS_Store
|   |   favicon.png
|   |   index.html
|   |
|   \---img
|       |   apple-icon.png
|       |   bg-pricing.jpg
|       |   bg3.jpg
|       |   default-avatar.png
|       |   favicon.png
|       |   image_placeholder.jpg
|       |   laravel-vue.svg
|       |   placeholder.jpg
|
|
|---src
    |   .DS_Store
    |   App.vue
    |   globalComponents.js
    |   globalDirectives.js
    |   main.js
    |
    |---assets
    |   |   .DS_Store
    |   |
    |   |---css
    |   |       demo.css
    |   |
    |   |
    |   └── sass
    │       ├── dashboard
    │       └── vendor
    │           └── bootstrap-rtl.scss
    ├── components
    │   ├── BaseAlert.vue
    │   ├── BaseButton.vue
    │   ├── BaseCheckbox.vue
    │   ├── BaseDropdown.vue
    │   ├── BaseNav.vue
    │   ├── BaseRadio.vue
    │   ├── BaseTable.vue
    │   ├── Cards
    │   │   ├── Card.vue
    │   │   └── StatsCard.vue
    │   ├── Charts
    │   │   ├── BarChart.js
    │   │   ├── config.js
    │   │   ├── LineChart.js
    │   │   └── utils.js
    │   ├── CloseButton.vue
    │   ├── index.js
    │   ├── Inputs
    │   │   └── BaseInput.vue
    │   ├── Modal.vue
    │   ├── NavbarToggleButton.vue
    │   ├── NotificationPlugin
    │   │   ├── index.js
    │   │   ├── Notifications.vue
    │   │   └── Notification.vue
    │   ├── SidebarPlugin
    │   │   ├── index.js
    │   │   ├── SidebarLink.vue
    │   │   └── SideBar.vue
    │   └── ValidationError.vue
    ├── layout
    │   ├── dashboard
    │   │   ├── AuthLayout.vue
    │   │   ├── ContentFooter.vue
    │   │   ├── Content.vue
    │   │   ├── DashboardLayout.vue
    │   │   ├── MobileMenu.vue
    │   │   └── TopNavbar.vue
    │   └── starter
    │       ├── Content.vue
    │       ├── MobileMenu.vue
    │       ├── SampleFooter.vue
    │       ├── SampleLayout.vue
    │       ├── SampleNavbar.vue
    │       └── SamplePage.vue
    ├── main.js
    ├── middleware
    │   ├── auth.js
    │   └── guest.js
    ├── mixins
    │   └── form-mixin.js
    ├── pages
    │   ├── Dashboard
    │   │   ├── TaskList.vue
    │   │   └── UserTable.vue
    │   ├── Dashboard.vue
    │   ├── Examples
    │   │   ├── UserManagement
    │   │   │   └── ListUserPage.vue
    │   │   ├── UserProfile
    │   │   │   ├── EditPasswordCard.vue
    │   │   │   └── EditProfileCard.vue
    │   │   └── UserProfile.vue
    │   ├── Icons.vue
    │   ├── Login.vue
    │   ├── Maps.vue
    │   ├── NotFoundPage.vue
    │   ├── Notifications
    │   │   └── NotificationTemplate.vue
    │   ├── Notifications.vue
    │   ├── Password
    │   │   ├── Email.vue
    │   │   └── Reset.vue
    │   ├── Profile
    │   │   ├── EditProfileForm.vue
    │   │   └── UserCard.vue
    │   ├── Profile.vue
    │   ├── Register.vue
    │   ├── TableList.vue
    │   └── Typography.vue
    ├── plugins
    │   ├── blackDashboard.js
    │   ├── globalComponents.js
    │   ├── globalDirectives.js
    │   ├── isDemo.js
    │   └── RTLPlugin.js
    ├── registerServiceWorker.js
    ├── router
    │   ├── index.js
    │   ├── routes.js
    │   └── starterRouter.js
    └── store
        ├── index.js
        ├── modules
        │   ├── alerts-module.js
        │   ├── auth.js
        │   ├── profile-module.js
        │   ├── reset.js
        │   └── users-module.js
        └── services
            ├── profile-service.js
            └── users-service.js
```

## Browser Support

At present, we officially aim to support the last two versions of the following browsers:
                                                                                                                             | Vue & Laravel                                                                                               
## Change log

Please see the [changelog](CHANGELOG.md) for more information on what has changed recently.


## Reporting Issues

We use GitHub Issues as the official bug tracker for the Black Dashboard Laravel. Here are some advices for our users that want to report an issue:

1. Make sure that you are using the latest version of the Black Dashboard Laravel. 
2. Providing us reproducible steps for the issue will shorten the time it takes for it to be fixed.
3. Some issues may be browser specific, so specifying in what browser you encountered the issue might help.





