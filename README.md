---
marp: true
paginate: true
size: 16:9
class: invert
---

<h1>Modern<br>Python Dependency Management 🐍<br>With uv 🚀</h1>

---

<style scoped>
ul {
  font-size: 19px;
}
</style>

<h2>📚 Table of Contents 📚 </h2>

- [1. 👋 Intro 👋](#1--intro-)
  - [1.1. 🤓 Me 🤓](#11--me-)
  - [1.2. ☀️ `uv` ☀️](#12-️-uv-️)
- [2. 🤷‍♀️ What Is Dependency Management? 🤷‍♀️](#2-️-what-is-dependency-management-️)
  - [2.1. 🥀 What Did We Do Before `uv`? 🥀](#21--what-did-we-do-before-uv-)
    - [2.1.1. 🤮 Why This Sucks 🤮](#211--why-this-sucks-)
  - [2.2. 👀 What Do Other Languages Do? 👀](#22--what-do-other-languages-do-)
- [3. ✨ What `uv` Can Bring Us ✨](#3--what-uv-can-bring-us-)
  - [3.1. 🏃🏽‍♀️ SPEED 🏃🏽‍♀️](#31-️-speed-️)
  - [3.2. 🛠️ One Tool To Rule Them All 🛠️](#32-️-one-tool-to-rule-them-all-️)
  - [3.3. 🙂 Simplified Workflow 🙂](#33--simplified-workflow-)
  - [3.4. 📡 Distributability 📡](#34--distributability-)
  - [3.5. ✅ Correctness ✅](#35--correctness-)
- [4. 📥 Installing 📥](#4--installing-)
- [5. 🔄 Migrating Old Projects 🔄](#5--migrating-old-projects-)
- [6. 🌱 New Project Workflow 🌱](#6--new-project-workflow-)

---

## 1. 👋 Intro 👋
### 1.1. 🤓 Me 🤓

> <img src="./img/me.png" width="256">
> 
> [Ollie Lavers](https://www.linkedin.com/in/hauteclere/)  
> She Codes Brisbane Masterclass Day  
> Saturday 2026.01.17  

---

### 1.2. ☀️ `uv` ☀️

[![](./img/astral_logo.svg) `uv` is a new-ish dependency manager for Python.](https://docs.astral.sh/uv/)

It is getting major (deserved) hype, and has completely revolutionised my toolset. 


We don't use it in She Codes, but **you should use it personally**. This talk explains why.

---

## 2. 🤷‍♀️ What Is Dependency Management? 🤷‍♀️


Dependency management is the work of obtaining and organising all of the code that we need for our projects that **we didn't write**.

- If you're coding a Django website, then Django is a dependency for your project, because your site can't work without the Django library.
- If you're coding an app in "pure Python", you still have dependencies - your app won't run without the Python interpreter!
- Even projects from compiled languages have dependencies that need to be managed during the build process.
- Dependencies shouldn't be installed globally!

---

### 2.1. 🥀 What Did We Do Before `uv`? 🥀
Python dependency management has historically been a total kludge.

You're probably familiar with the `pip` + `venv` + `requirements.txt` system that we teach at She Codes. With this toolset you would:

- Use the built-in `venv` library to create a "virtual environment". This "venv" contains a copy of the Python interpreter based on your global install that gets used to run your scripts, plus a folder for the library files that your project will depend on.
- Use the `pip` library to download and install dependencies from [the Python Package Index - "`PyPI`"](https://pypi.org/)
- Record your dependency library names + version numbers in a file, traditionally called "`requirements.txt`". 
  
---

Example requirements.txt:
  ```txt
  asgiref==3.11.0
  django==6.0.1
  django-neomodel==0.2.0
  neo4j==5.19.0
  neobolt==1.7.17
  neomodel==5.3.3
  python-dotenv==1.2.1
  pytz==2025.2
  six==1.17.0
  sqlparse==0.5.5
  typing-extensions==4.15.0
  ```

---

Example commands:

```bash
# Create a venv
python3 -m venv venv
```

```bash
# Activate the venv
source ./venv/bin/activate
```

```bash
# install dependencies
python3 -m pip install django
```

---

#### 2.1.1. 🤮 Why This Sucks 🤮

- Potential for globally installed and/or untracked dependencies
  
  <img src="./img/burning_globe.gif" width="256">

---

- Unmanaged Subdependencies
  
  <img src="./img/subdependency.drawio.png" width="512">

---

- Slow
  
  ![](./img/slowpip_reddit.png)
  ![](./img/slow_pip.png)

---

- Hard to distribute
  
  ![](./img/hard_distribution.png)

---

- Doesn't manage system software
  
  ![](./img/python_incorrect_installation.png)
  ![](./img/python_install_fail.png)
  ![](./img/python_version_conflicts.png)

---

  (this is not a new problem)
  
  <img src="./img/python_setup_failed.png" width="640">

---

### 2.2. 👀 What Do Other Languages Do? 👀
- packages installed **locally** by default
- lockfiles track subdependencies
- often no need to install packages before running them
- some consensus way of managing interpreter versions
- distribution helpers

---

## 3. ✨ What `uv` Can Bring Us ✨

![](./img/paradise.png)

[Here's an boilerplate `uv` project](https://github.com/Hauteclere/uv_example/)


---

### 3.1. 🏃🏽‍♀️ SPEED 🏃🏽‍♀️

You don't think your pip installs are annoying but that's because you're used to them. Trust me, uv just feels so much nicer to use, because it's fast.

[Don't believe me? I made a comparison video.](https://youtu.be/VNa2-I5AxA4)

---

### 3.2. 🛠️ One Tool To Rule Them All 🛠️

- You handle your python version management with `uv`.
- You handle your `.venv` creation with `uv`.
- You handle package management with `uv`.
- `uv` initialises your directory as a git repo if it isn't one already.
- `uv` builds and distributes your software.

---

### 3.3. 🙂 Simplified Workflow 🙂

- Want to install Python?
  ```bash
  uv python install 3.14
  ```
- Want to run a Python script even if you don't have a venv or installed dependencies...?
  ```bash
  uv run --with django your_script_name.py
  ```

---

- Want to run a script **even without a script file OR A PYTHON INSTALLATION???**
  ```bash
  echo '# /// script
  # dependencies = [
  #   "requests<3",
  #   "rich",
  # ]
  # ///

  import requests
  from rich.pretty import pprint

  resp = requests.get("https://peps.python.org/api/peps.json")
  data = resp.json()
  pprint([(k, v["title"]) for k, v in data.items()][:10])' | uv run -
  ```

---

- Nothing is beyond your reach!

  > Oliver remember to run this one in Windows because your Ubuntu isn't set up right. And put it in a blank directory, please.

  ```bash
  uv run --with jupyter jupyter notebook
  ```

---

### 3.4. 📡 Distributability 📡

- `uv` projects are easy to distribute
  - [A few lines in your `pyproject.toml`.](https://github.com/Hauteclere/uv_example/)
  - Get your directory structure right.
  - `uv build`
  - `uv publish --token <insert pypi token here>`
- [`uv` projects can be distributed to complete n00bs.](https://pypi.org/project/she-codes-uv-example/) 

---

### 3.5. ✅ Correctness ✅
- Lockfile means that subdependencies are handled perfectly every time, down to the smallest patch.
- `uv` is strict enough that the biggest problem people find when migrating from `pip` is that they discover their project had unresolveable dependencies all along and shouldn't technically have been possible. `pip` just swept it under the rug.

---

## 4. 📥 Installing 📥
[Shockingly, scarily easy.](https://docs.astral.sh/uv/getting-started/installation/#standalone-installer)

One terminal command on all major OS. Check the link for yours.

---

## 5. 🔄 Migrating Old Projects 🔄
1.  ```bash
    uv init .
    ```
2.  ```bash
    uv add -r requirements.txt
    ```

> Damn this presentation i going to run short isn't it...?

---

## 6. 🌱 New Project Workflow 🌱

1. create a project directory:
    ```bash
    cd ~
    ```
    ```bash
    mkdir uv_example_repo
    ```
    ```bash
    cd uv_example_repo
    ```
2. initialise the repo:
    ```bash
    uv init .
    ```

---

3. add a dependency:
    ```bash 
    uv add cowsay
    ```
4. write some code:
    ```diff
    # main.py

    + import cowsay
    
    def main():
    -   print("Hello from test-uv-example!")
    +   cowsay.cow("Hello from test-uv-example!")

    if __name__ == "__main__":
        main()

    ```

---

5. Run your program:
    ```bash
    uv run main.py
    ```

    output:

    ```
      ___________________________
    | Hello from test-uv-example! |
      ===========================
                              \
                                \
                                  ^__^
                                  (oo)\_______
                                  (__)\       )\/\
                                      ||----w |
                                      ||     ||
    ```

---

> Note that we never activated a virtual environment there! You still can if you want to, using the same command as you always have. That means that you can still run your projects with `python main.py` if you want to!
> 
> Similarly, if you still want to use the `pip` commands you're used to you can run:
> - `uv venv my_venv_name` (to create a venv)
> - `uv pip install my_package_name` (to create a package)
> - etc
---

Things we didn't cover that `uv` also nails:
- platform-specific dependencies (ask a Python educator how much they hate these)
- "development dependencies"

---

So why aren't we using it for She Codes?

> This isn't a challenge - in the live version of this talk I explain my reasoning. Basically - `uv` is still so new that you still need to know the old way of doing things for employability.
