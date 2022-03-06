# MicroFrontEnd - NxTools - Angular - TailwindCSS

This project was generated using [Nx](https://nx.dev).

&nbsp;

# Steps

<details>
  &nbsp;
  <summary>Create workspace</summary>
  
  Create workspace with app name shell is important for the second step
  &nbsp;
  ```
  npx create-nx-workspace@latest <WORKSPACE_NAME>
  ```
</details>

<details>
  &nbsp;
  <summary>Add TailwindCSS</summary>
  
  Add TailwindCSS (shell is the name of you first generated application)
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

</details>

<details>
  &nbsp;
  <summary>Config shell app</summary>
  
  With this command tranform you shell app to host app for microfrontend.

```
npx nx generate @nrwl/angular:setup-mfe --appName=shell --port=4200 --mfeType=host --routing --no-interactive
```

</details>

<details>
  &nbsp;
  <summary>Generated Remote Apps/Projects</summary>
  
  This command will create your remote project that will later run in your shell. We create two of this App's/Projects with separate ports and names.

  Create Project with name app1:
  &nbsp;

  ```
  npx nx g @nrwl/angular:app app1 --mfe --mfeType=remote --port=4201 --host=shell --routing=true
  ```
  Config TailwindCSS in the app1 project:

  ```
  npx nx generate @nrwl/angular:setup-tailwind app1
  ```

  &nbsp;

  Create Project with name app2:
  &nbsp;

  ```
  npx nx g @nrwl/angular:app app2 --mfe --mfeType=remote --port=4202 --host=shell --routing=true
  ```

  Config TailwindCSS in the app2 project:

  ```
  npx nx generate @nrwl/angular:setup-tailwind app2
  ```

</details>

<details>
  &nbsp;
  <summary>Config shell app router</summary>
  
  Replace the HTML code in "/apps/shell/src/app/app.component.html" with

```
<header class="text-gray-600 body-font">
<div
  class="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center"
>
  <a
    class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0"
  >
    <span class="ml-3 text-xl text-orange-500 font-bold">MicroFrontEnd</span>
  </a>
  <nav
    class="md:mr-auto md:ml-4 md:py-1 md:pl-4 md:border-l md:border-gray-400 flex flex-wrap items-center text-base justify-center"
  >
    <a routerLink="app1" class="mr-5 hover:text-orange-400 hover:cursor-pointer">App 1</a>
    <a routerLink="app2" class="mr-5 hover:text-orange-400 hover:cursor-pointer">App 2</a>
  </nav>
</div>
</header>
<main class="container mx-auto px-4">
  <router-outlet></router-outlet>
</main>
```

and after this add routs in the app.module.ts

```
import { RouterModule } from '@angular/router';
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';

@NgModule({
declarations: [AppComponent],
imports: [
  BrowserModule,
  RouterModule.forRoot(
    [
      {
        path: 'app1',
        loadChildren: () =>
          import('app1/Module').then((m) => m.RemoteEntryModule),
      },
      {
        path: 'app2',
        loadChildren: () =>
          import('app2/Module').then((m) => m.RemoteEntryModule),
      },
    ],
    { initialNavigation: 'enabledBlocking' }
  ),
],
providers: [],
bootstrap: [AppComponent],
})
export class AppModule {}

```

</details>

<details>
  &nbsp;
  <summary>Replace the npm start </summary>
  
  Replace the npm start command with the npm run-many command.

  ```
  nx run-many --target=serve --all --parallel
  ```

</details>
