<!-- ---
marp: true
_class: invert
paginate: true
size: 16:9
--- -->

<h1>Modern Python Dependency Management With UV</h1>

> <h2>Ollie Lavers<br>She Codes Brisbane Masterclass Day<br>Saturday 2026.01.17</h2>

![](./img/me.png)

---

<style scoped>
  li {
    font-size: 24px;
  }
</style>

<h2>>0. Table of Contents</h2>

- [1. What Is Dependency Management?](#1-what-is-dependency-management)
  - [1.1. What Did We Do Before UV?](#11-what-did-we-do-before-uv)
  - [1.2. What Does It Look Like In Other Languages?](#12-what-does-it-look-like-in-other-languages)
- [2. What UV Can Bring Us](#2-what-uv-can-bring-us)
  - [2.1. One Tool To Rule Them All](#21-one-tool-to-rule-them-all)
  - [2.2. SPEED](#22-speed)
  - [2.3. Simplified Workflow](#23-simplified-workflow)
  - [2.4. Distributability](#24-distributability)
  - [2.5. Correctness](#25-correctness)
- [3. Migrating Old Projects](#3-migrating-old-projects)
- [4. New Project Setup](#4-new-project-setup)

---

## 1. What Is Dependency Management?
Dependency management is the practise of obtaining and utilising all of the code that we need for our projects that **we didn't write**.

- If you're coding a Django website, then Django is a dependency for your project, because your site can't work without the Django library.
- If you're coding an app in "pure Python", you still have dependencies - your app won't run without the Python interpreter!
- Even projects from compiled languages have dependencies that need to be managed during the build process.

---

### 1.1. What Did We Do Before UV?
Python dependency management has historically been a total kludge.

You're probably familiar with the `pip` + `venv` + `requirements.txt` system that we teach at She Codes. With this toolset you would:

- Use the built-in `venv` library to create a "virtual environment". This "venv" contains a copy of the Python interpreter based on your global install that gets used to run your scripts, plus a folder for the library files that your project will depend on.
- Use the `pip` library to download and install dependencies from [the Python Package Index - "`PyPI`"](https://pypi.org/)
- Record your dependency library names + version numbers in a file, traditionally called "`requirements.txt`". For example:
  ```txt
  asgiref==3.7.2
  Django==4.2.7
  django-neomodel==0.1.1
  neo4j>=5.24.0
  neobolt==1.7.17
  neomodel==5.1.2
  python-dotenv==1.0.0
  pytz==2023.3.post1
  six==1.16.0
  sqlparse==0.4.4
  typing_extensions==4.8.0
  ```

Here's what that might look like to set up:




### 1.2. What Does It Look Like In Other Languages?

## 2. What UV Can Bring Us

### 2.1. One Tool To Rule Them All

### 2.2. SPEED

### 2.3. Simplified Workflow

### 2.4. Distributability

### 2.5. Correctness

## 3. Migrating Old Projects

## 4. New Project Setup

