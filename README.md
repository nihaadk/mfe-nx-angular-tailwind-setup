# MicroFrontEnd - NxTools - Angular - TailwindCSS

This project was generated using [Nx](https://nx.dev).

## Steps

## Create workspace (with app name shell is important for the second Step)

```
npx create-nx-workspace@latest <WORKSPACE_NAME>
```

## Add TailwindCSS (shell is the name of you first generated application)

```
npx nx generate @nrwl/angular:setup-tailwind shell
```

Add in "/apps/shell/src/app/app.component.html" this code:

```
<header class="text-gray-600 body-font">
  <div class="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center">
    <a class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0">
      <span class="ml-3 text-xl text-orange-500 font-bold">MicroFrontEnd</span>
    </a>
    <nav class="md:mr-auto md:ml-4 md:py-1 md:pl-4 md:border-l md:border-gray-400	flex flex-wrap items-center text-base justify-center">
      <a class="mr-5 hover:text-orange-400 hover:cursor-pointer">App 1</a>
      <a class="mr-5 hover:text-orange-400 hover:cursor-pointer">App 2</a>
    </nav>
  </div>
</header>
```
# mfe-nx-angular-tailwind-setup
