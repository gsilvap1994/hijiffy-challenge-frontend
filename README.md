# Hijjify Frontend Challenge

This repository has the code solution for frontend challenge of hijjify using.

## Setup

This project was created with vue-cli using `VueJs 3.0` with `SCSS` and `ESLint`.

## Project Structure

The `./src` folder has the following subfolders

- `./src/assets` -> this folder contains the static assets of the project
- `./src/components` and `./src/components/shared` -> these folders contains the macro components (root folder) and the micro components (shared folder)
- `./src/styles` -> this folder contains the globals SCSS

## Running the project

For running the project, go to the root of the project and run the following commands:

- `npm install`
- `npm run serve`

This will install the dependencies and start a server in <strong>http://localhost:8080</strong>. You will also need the mock API to see the contacts list. So open another terminal, also in the root project folder, and run the following command:

- `npx json-server db.json`

This will start de mock `json-server` at the <strong>http://localhost:3000</strong>.
