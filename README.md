NODE.js

1- Create a new project Folder and open my project in VScode
Open Terminal:

``bash:
mkdir Node.js
cd Node.js
code .``

2- Npm install (package.json)
``npm init -y``

3- Install ESLint and Prettier:
Terminal

``bash:

npm install --save-dev --save-exact prettier

npm install --save-dev eslint @eslint/js eslint-config-prettier globals``

Create eslint.config.js 

``import globals from 'globals';
import js from '@eslint/js';

export default [
  {
    languageOptions: {
      ecmaVersion: 2021,
      sourceType: 'module',
      globals: {...globals.node},
    },
  },
  js.configs.recommended,
];``

Create .prettierrc.cjs

``// sample .prettierrc.cjs
module.exports = {
  semi: true,
  singleQuote: true,
  bracketSpacing: false,
  trailingComma: 'all',
};``

4-Install nodemon:

``npm install --save-dev nodemon``

5- In package.json add 

``...
"type": "module",
"scripts": {
  "dev": "nodemon src/index.js",
  ...``

6- Create .gitignore 

``.vscode
node_modules
.DS_Store``

7- Create src/index.js folder and add: 
``// index.js
import http from 'http';
const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Welcome to my REST API!');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});``

Test your setup: `` npm run dev ``