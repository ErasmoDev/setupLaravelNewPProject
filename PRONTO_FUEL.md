# Setup de um Projeto Laravel usando o start kit [Pronto_fuel](https://github.com/prontostack/pronto-fuel)

**Pronto** Fuel is a heavilly opnionated starter kit for [**Laravel**](https://laravel.com/) and [**Inertia.js**](https://inertiajs.com/) powered by [**Vite**](https://vitejs.dev/). It ships with autoimporting features and leverages the latest and greatest features from [**Vue 3**](https://vuejs.org/).

## Features

-   ⏩ [Inertia.js](https://inertiajs.com/)
-   🔰 [Vue 3](https://github.com/vuejs/core)
-   ⚡️ [Vite](https://vitejs.dev/)
-   🔥 Use the [new `<script setup>` syntax](https://github.com/vuejs/rfcs/pull/227) for Vue
-   📦 [Components auto importing](https://github.com/antfu/unplugin-vue-components)
-   ⬇️ [Common Vue and Inertia APIs auto importing](https://github.com/antfu/unplugin-auto-import)
-   ❄️ [Quasar Framework](https://quasar.dev/) configured out of the box with over 70 ready to use Material Design components
-   🎨 [Tailwind CSS](https://tailwindcss.com/) configured with common [PostCSS](https://postcss.org/) plugins, like [nesting](https://github.com/csstools/postcss-plugins/tree/main/plugins/postcss-nesting) and [extend rule](https://github.com/csstools/postcss-extend-rule).
-   😃 [Use icons from any icon sets, with no compromise](https://github.com/antfu/unplugin-icons)
-   ✂️ Pages Code Splitting out of the box
-   🔔 Server Driven toast notification system with queue in place
-   🐋 [VSCode Dev Container](https://code.visualstudio.com/docs/remote/containers) with everything you need to start developing
-   🪲 Debug with [Ray](https://spatie.be/docs/ray/v1/introduction) on [port 23517](http://localhost:23517/) by default
-   👮 Enforce code quality with [ESLint](https://eslint.org/) and [StandardJS](https://standardjs.com/)


## Quick Start

```bash
# Clone the repo
git clone https://github.com/prontostack/pronto-fuel.git my-app

# Enter the project directory
cd my-app

# Create a .env files based on the provided example one
cp .env.example .env

# Install PHP dependencies
composer install

# Generate an APP key for security
php artisan key:generate

# Create the database tables
php artisan migrate

# Instal frontend dependencies
npm install

# Lift Vite's development server
npm run serve

# Go to http://localhost
```

## Quick Start with VSCode Dev Container

```bash
# Clone the repo
git clone https://github.com/prontostack/pronto-fuel.git my-app

# Enter the project directory
cd my-app

# Create a .env files based on the provided example one
cp .env.example .env

# Open the project on VSCode
code .

# *****************************************************************
# Install the Remote-Containers extensions if you still haven't
# Open VSCode's command palette (Eg.: ctrl + shift + p on Windows)
# Select "Remote-Containers: Open Folder in Container"
#
# IMPORTANT: The following commands must be executed in the VSCode
# integrated terminal, once the Dev Container has started, since it
# is running inside the container
# *****************************************************************

# Install PHP dependencies
composer install

# Generate an APP key for security
php artisan key:generate

# Create the database tables
php artisan migrate

# Instal frontend dependencies
npm install

# *****************************************************************
# At this point, before you actually run the project, you might
# need to close the remote connection to the Dev Container and
# reopen it. See Troubleshooting below for more info.
# *****************************************************************

# Lift Vite's development server
npm start

# Go to http://localhost
```

## Postgres/Meilisearch/Mailhog
- Retirar o mysql do docker-compose.yml e remover o phpmyadmin
- Colocar o meilisearch/postgres/mailhog

```bash
 depends_on:
            - pgsql
            - meilisearch
            - redis
    pgsql:
        image: 'postgres:14'
        ports:
            - '${FORWARD_DB_PORT:-5432}:5432'
        environment:
            PGPASSWORD: '${DB_PASSWORD:-secret}'
            POSTGRES_DB: '${DB_DATABASE}'
            POSTGRES_USER: '${DB_USERNAME}'
            POSTGRES_PASSWORD: '${DB_PASSWORD:-secret}'
        volumes:
            - 'sail-pgsql:/var/lib/postgresql/data'
        networks:
            - sail
        healthcheck:
            test: ["CMD", "pg_isready", "-q", "-d", "${DB_DATABASE}", "-U", "${DB_USERNAME}"]
            retries: 3
            timeout: 5s
    meilisearch:
        image: 'getmeili/meilisearch:latest'
        ports:
            - '${FORWARD_MEILISEARCH_PORT:-7700}:7700'
        volumes:
            - 'sail-meilisearch:/meili_data'
        networks:
            - sail
        healthcheck:
            test: ["CMD", "wget", "--no-verbose", "--spider",  "http://localhost:7700/health"]
            retries: 3
            timeout: 5s
    redis:
        image: 'redis:alpine'
        ports:
            - '${FORWARD_REDIS_PORT:-6379}:6379'
        volumes:
            - 'sail-redis:/data'
        networks:
            - sail
        healthcheck:
            test: ["CMD", "redis-cli", "ping"]
            retries: 3
            timeout: 5s
    debugger:
        image: butschster/buggregator:latest
        networks:
            - sail
        ports: [ '23517:8000', '1025:1025', '9912:9912', '9913:9913' ]
    mailhog:
        image: 'mailhog/mailhog:latest'
        ports:
            - '${FORWARD_MAILHOG_PORT:-1035}:1035'
            - '${FORWARD_MAILHOG_DASHBOARD_PORT:-8025}:8025'
        networks:
            - sail
networks:
    sail:
        driver: bridge
volumes:
    sail-pgsql:
        driver: local
    sail-meilisearch:
        driver: local
    sail-redis:
        driver: local

```

## Instalar dependencias e configurar de acordo com o Readme.md
