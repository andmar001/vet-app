# forma rapida de crear un proyecto de vue
npm create vite@latest admin-pacientes -- --template vue

# instalacion de taildwincss
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest

# creacion de archivo de configuracion de tailwindcss
npx tailwindcss init -p

# headless ui  - usado para crear componentes de interfaz de usuario accesibles y sin diseño
npm install @headlessui/vue
- sitio: https://headlessui.dev/vue/menu

# prevenir las acciones de envio de formulario -- mismas acciones  
submit.prevent
e.preventDefault()