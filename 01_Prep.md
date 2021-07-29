# Prepping for React Workshop
This is a step-by-step guide that will go over everything you need to do before our workshop in detail!
Let's get started!

**Outline**:
  * [1. Create a `myproject` folder](#1-create-a-myproject-folder)
    * [Check if you already have Node.js or npm](#check-if-you-already-have-nodejs-or-npm)
  * [2. Install Node.js](#2-install-nodejs)
    * [macOS with nodenv](#macos-with-nodenv)
    * [Windows with nvm-windows](#windows-with-nvm-windows)
  * [3. Install a Sample React App](#3-install-a-sample-react-app)
  * [⚠️ Got an error?](#️-got-an-error)
  * [📺 YouTube Quick Videos Going Over the Node Install & Create-React-App](#-quick-videos-going-over-the-node-install--create-react-app)

---

## 1. Create a `myproject` folder
Somewhere inside your Document folder will be good.

### Check if you already have Node.js or npm
React requires **Node ≥ 10.16** & **npm ≥ 5.6**  
Go **inside** the `myproject` folder.

  ```shell
  $ node -v
  $ npm -v
  ```

---

## 2. Install Node.js
If Node & npm are missing, let's install them!

**Options**:
  * [macOS with nodenv](#macos-with-nodenv)
  * [Windows with nvm-windows](#windows-with-nvm-windows)

### macOS with [nodenv](https://github.com/nodenv/nodenv)
We recommend installing Node.js using [nodenv](https://github.com/nodenv/nodenv) to manage node versions. This allows your computer to have a specific Node.js version per project.

⚠️ Remove any existing installations of Node.js before installing nodenv! ⚠️  
Having different Node.js installations can lead to conflict issues.

**Step 1**: Install nodenv with [Homebrew](https://brew.sh/)
  * Update Homebrew:

    ```shell
    brew update && brew upgrade
    ```

  * Install nodenv:

    ```shell
    brew install nodenv
    ```

**Step 2**: Set up nodenv shell integration
  * Run the initialization command:

    ```shell
    nodenv init
    ```

  * Do as instructed by appending the following line into your shell's rc/profile file:

    ```shell
    eval "$(nodenv init -)"
    ```

    * For Zsh users:

      ```shell
      $ echo 'eval "$(nodenv init -)"' >> ~/.zshrc
      $ cat < ~/.zshrc
      ```

    * For Bash users:

      ```shell
      $ echo 'eval "$(nodenv init -)"' >> ~/.bash_profile
      $ cat < ~/.bash_profile
      ```

**Step 3**: Implement the changes

Close & open a new Terminal window for the changes to take place.

Optional: Verify that nodenv is properly set up using [nodenv-doctor](https://github.com/nodenv/nodenv-installer/blob/master/bin/nodenv-doctor) script.
  * For those using Z shell (Zsh) shell:

    ```shell
    curl -fsSL https://github.com/nodenv/nodenv-installer/raw/master/bin/nodenv-doctor | bash
    ```

  * Expected result:

    ```shell
    Checking for `nodenv' in PATH: /usr/local/bin/nodenv
    Checking for nodenv shims in PATH: OK
    Checking `nodenv install' support: /usr/local/bin/nodenv-install (node-build 3.0.22-4-g49c4cb9)
    Counting installed Node versions: none
      There aren't any Node versions installed under `~/.nodenv/versions'.
      You can install Node versions like so: nodenv install 2.2.4
    Auditing installed plugins: OK
    ```

**Step 4**: Install Node.js inside the React Workshop folder (`myproject`)
  * Now you're ready to install specific Node.js versions!
  * **Inside** `myproject` folder, install Node.js version `14.5.0`:

    ```shell
    $ cd myproject/
    $ nodenv install 14.5.0
    $ nodenv local 14.5.0
    ```

Alright! Your Mac is now armed with Node.js!  
Skip down to the [3. Install a Sample React App](#3-install-a-sample-react-app) section!

---

### Windows with [nvm-windows](https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows)
The following steps are straight from the Microsoft Docs on [Set up NodeJS on native Windows](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-windows). We recommend installing and managing Node.js with [nvm-windows](https://github.com/coreybutler/nvm-windows#node-version-manager-nvm-for-windows)

⚠️ Remove any existing installations of Node.js before installing nvm-windows! ⚠️  
Having different Node.js installations can lead to conflict issues.

**Step 1**: Go to the [windows-nvm's latest release](https://github.com/coreybutler/nvm-windows/releases).

**Step 2**: Download the **nvm-setup.zip** file for the most recent release.

**Step 3**: Once downloaded, open the zip file, then open the **nvm-setup.exe** file.

**Step 4**: The Setup-NVM-for-Windows installation wizard will walk you through the setup steps, including choosing the directory where both nvm-windows and Node.js will be installed.
  * ![install-nvm-for-windows-wizard.png](https://docs.microsoft.com/en-us/windows/images/install-nvm-for-windows-wizard.png)

**Step 5**: After the installation is complete, open PowerShell & enter `nvm ls`
  * `nvm ls` lists out installed Node versions (should be none at this point)
  * ![windows-nvm-powershell-no-node.png](https://docs.microsoft.com/en-us/windows/images/windows-nvm-powershell-no-node.png)

**Step 6**: Install Node.js inside the React Workshop folder (`myproject`)
  * Now you're ready to install specific Node.js versions!
  * Inside `myproject` folder, install Node.js version `14.5.0`:

    ```powershell
    $ cd .\Documents\myproject
    $ nvm install 14.5.0
    $ nvm use 14.5.0
    ```

Alright! Your Windows is now armed with Node.js!  
Skip down to the [3. Install a Sample React App](#3-install-a-sample-react-app) section!

---

## 3. Install a Sample React App
Still inside the `myproject` folder, let's install a React App named `frontend`.

Install:  
  * `npx create-react-app frontend`

Starting it up:  
  * Go **inside** the `frontend` folder
  * `npm start`

## ⚠️ Got an error?
  * Make sure you are **inside** the `myproject` folder when setting up Node.js
    * Mac: `nodenv local 14.5.0`
    * Windows: `nvm use 14.5.0`
  * Make sure you are **inside** the `frontend` folder when running `npm start`!

## ![YouTube](https://user-images.githubusercontent.com/30670749/92354102-a05c4000-f11c-11ea-8964-f96f052b1457.png) Quick Videos Going Over the Node Install & Create-React-App

<p align="center">
  <a href="https://youtu.be/4Kw-i_rX3tY">
    <img height="200" alt="Installing Node.js & Create a New React App YouTube Thumbnail"
      src="https://img.youtube.com/vi/4Kw-i_rX3tY/mqdefault.jpg">
  </a>
</p>
