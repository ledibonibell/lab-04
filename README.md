# Report-04

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в прошлый раз. Настройте сборочные процедуры на различных платформах:

# Task 1

Используйте GitHub Actions для сборки на операционной системе Linux с использованием компиляторов gcc и clang

Clone the Remote repository from the previous LR to the current one

```
$ git clone https://github.com/ledibonibell/lab-03 lab-04
$ cd ~/lab-04
$ git remote remove origin
$ git remote add origin https://github.com/ledibonibell/lab-04.git
```
![Снимок экрана от 2023-03-19 11-45-56](https://user-images.githubusercontent.com/125737299/226168945-d269c627-e590-4d2b-97ca-58e4046cf4a5.png)


And we make the folder `~/lab-04/.github/workflows`
```
$ mkdir .github
$ cd ~/lab-04/.github
$ mkdir workflows
$ cd ~/lab-04/.github/workflows
```
![Снимок экрана от 2023-03-19 11-47-55](https://user-images.githubusercontent.com/125737299/226168959-1f395faa-d6c6-4e5d-8acb-de0c122ceaeb.png)

```
$ cat >> Linux.yml << EOF
> EOF
$ nano Linux.yml
```

Содержимое файла Linux.yml:

```
name: CMake

on:
 push:
  branches: [master]
 pull_request:
  branches: [master]

jobs: 
 build_Linux:

  runs-on: ubuntu-latest

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build

  - name: Configure HelloWorld
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/buildс
```

```
$ git add Linux.yml
$ git commit -m "Linux.yml - 1"
$ git push origin master
```
![Снимок экрана от 2023-03-19 12-53-41](https://user-images.githubusercontent.com/125737299/226168997-4253e284-d152-4166-a08b-50fb8544141f.png)


The script was executed

# Task 2

Используйте GitHub Actions для сборки на операционной системе Windows

```
$ cat >> Windows.yml << EOF
> EOF
$ nano Windows.yml
```


Содержимое файла Windows.yml:

```
name: CMake

on:
 push:
  branches: [master]
 pull_request:
  branches: [master]

jobs: 
 build_Windows:

  runs-on: windows-latest

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build

  - name: Configure HelloWorld
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/build
```

```
$ git add Windows.yml
$ git commit -m "Windows.yml - 1"
$ git push origin master
```
![Снимок экрана от 2023-03-19 13-06-35](https://user-images.githubusercontent.com/125737299/226169021-d6f8e74d-6d17-4cfd-b0c5-2665d3b60524.png)


The script was executed
![Снимок экрана от 2023-03-19 13-07-10](https://user-images.githubusercontent.com/125737299/226169029-e6fe7071-ce9c-4336-8ece-48884db76cfb.png)
