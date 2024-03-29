# 🚀 PNPM

## What Is It?

PNPM (Performant Node Package Manager) is an alternative to the popular NPM (Node Package Manager). It replaces all uses of NPM commands with PNPM commands that take less disk space and are not as buggy as basic NPM.

{% embed url="https://www.youtube.com/watch?t=2s&v=hiTmX2dW84E" %}

## What Are The Benefits?

* **Space Savings** - Exponentially lowers file size used on your hard disk for packages
* **Less Bugs** - We've seen NPM bugs cause hard drives to fill up with recursive packages
* **Faster** - All commands in general just run must faster than NPM
* **Drop-In Replacement** - There's no good reason to not just replace NPM commands with PNPM

## Windows PowerShell Privileges

To enable windows PowerShell to install PNPM,, there's an additional step we may need to do.

* On Windows PC's, press the windows key
* Type 'PowerShell'
* Right click the PowerShell icon and choose open as administrator.
* Type the following command and press enter
  * `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine`
* Press 'Y' when prompted.

## SSH-Agent

On Windows, we need to make sure we have a valid SSH agent running before we can attach our private Github keys to it.

* On Windows PC's, press the windows key
* Type 'PowerShell'
* Right click the PowerShell icon and choose open as administrator.
* Type the following command and press enter
* ```
  Get-Service -Name ssh-agent | Set-Service -StartupType Manual
  ```
* Now check if SSH-Agent is running by running another terminal command
* ```
  Get-Service ssh-agent
  ```
* If your SSH agent is stopped or disabled, you can manually start it using another command
* ```
  ssh-agent start
  ```
* Now if you run the `Get-Service ssh-agent` command again, it should show the service is running.

## Installation Instructions

* Make sure you have NPM installed already
* In a Visual Studio Code terminal, run the `npm install -g pnpm` command to install PNPM globally so it will be available regardless of directory or what project is open
* If your using private github repositories, follow the instructions at the bottom

## Usage Instructions

* Simply replace all use cases of NPM commands with PNPM commands
* EX: `pnpm install @babylonjs/core`

## Cache Cleaning

After updating a package with PNPM, you may encounter a scenario where Vite is still using an outdated version of that package when you run the `pnpm run dev` command and test your projects that use said package.&#x20;

This is because Vite makes a copy of your global PNPM packages when testing and it will need to be wiped before your changes can be pulled in.

To clear this cache, inside your project delete the `node_modules/vite` folder in your project hierarchy. It will be recreated the next time you run the `pnpm run dev` and copy your latest global packages.

## Private GitHub Repositories

The commands for accessing private GitHub repositories is the same as with standard NPM.

However accessing private GitHub repositories does not work out of the box for PNPM. In standard NPM you can authenticate using an automatic web browser popup that has you sign into your GitHub account.

We can get around this by creating an SSH key from our machine and uploading it to our GitHub organization so they can handshake. Follow the video below to setup your local machine accordingly.

{% embed url="https://youtu.be/JuQhNFYMFcE" %}

## Test Your Connection To Your Private Github

{% hint style="info" %}
This step isn't always necessary, but it's highly recommended.

The act of testing a PC for a connection to Github forces the Windows Terminal to authenticate the ID key that Github provides,&#x20;

It is believed this authentication step fixes some issues with SSH not connecting regardless of the previous steps in this guide being done correctly.
{% endhint %}

On Windows in your Terminal window, type the command below and press enter

* `ssh -T git@github.com`
* When prompted, enter in your github email and press enter
* You may see a security warning, agree to it to continue
* Afterwards if your SSH agent was properly setup, you should see a success message like the one below
  * `Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.`
* If you encountered issues connecting PNPM to your private github, but this check is successful, try running your commands in terminal again.&#x20;
