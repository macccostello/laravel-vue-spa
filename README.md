# Laravel-Vue SPA 

## Features

- Laravel 5.8 
- Vue + VueRouter + Vuex + VueI18n + ESlint

## Installation

- `composer create-project --prefer-dist /laravel-vue-spa`
- Edit `.env` and set your database connection details
- (When installed via git clone or download, run `php artisan key:generate` and `php artisan jwt:secret`)
- `php artisan migrate`
- `npm install`

## Usage

#### Development

```bash
# build and watch
npm run watch

# serve with hot reloading
npm run hot
```

#### Production

```bash
npm run production
```

