# windows-setup
Instructions to help you set up the Linux subsystem on Windows 10

VIDEO WALKTHOUGH:
https://youtu.be/pwn4zknR5TU

1. Install the Windows Subsystem for Linux
    - Control Panel -> Programs -> Turn Windows Features on or off
    - Select Windows Subsystem for Linux -> OK
    - Restart computer

1. Install Ubuntu 20 and the Windows Terminal from the Windows Store
    - If you can't install from the Windows Store, make sure you're signing in with your Microsoft Account and have verified your device (Settings -> Accounts)
    - Also, make sure you're using the most recent version of Windows 10. On the Windows Terminal page in the Store, select System Requirements -> Update
    - Open Ubuntu and let it finish installation. When prompted, enter a username (e.g. your first name) and a password. This is the username that Linux will run as by default. For Full Name, Room Number, etc. you can hit Enter to leave them blank
    - If it says installing for more than 5 minutes, close the Ubuntu window and re-open it

1. Configure your Windows Terminal
    - Open your Windows Terminal application and select the dropdown next to the new tab button then select Settings
    - Scroll down until you find this section:
 
    ```js
       {
                "guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
                "hidden": false,
                "name": "Ubuntu-20.04",
                "source": "Windows.Terminal.Wsl"
       },
    ```

    Copy the value of the "guid" field, then paste it in to the `defaultProfile` property near the top of the file.
    
    ```js
        "defaultProfile": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
    ```
    
    - Next, add these properties to the Ubuntu section. (The same section you got the "guid" from in the previous step).

    ```js
    "colorScheme": "One Half Dark",
    "startingDirectory": "//wsl$/Ubuntu-20.04/home/[your_username]"
    ```

    Once you have pasted it in, your Linux section should look like this (but instead of josep, it would say YOUR username. you are not josep.):

    ```js
            {
                "guid": "{07b52e3e-de2c-5db4-bd2d-ba144ed6c273}",
                "hidden": false,
                "name": "Ubuntu-20.04",
                "source": "Windows.Terminal.Wsl",
                "colorScheme": "One Half Dark",
                "startingDirectory": "//wsl$/Ubuntu-20.04/home/josep"
            },
    ```

1. Restart the Windows Terminal and install zsh and make it the default shell
    - Put this command into your terminal: `sudo apt-get install zsh`
    - Then this command: `chsh -s $(which zsh)`
    - Restart the Windows Terminal
    - If you get a page full of info about "This is the Z Shell configuration for new users...", press q (Quit and do nothing)
    
1. Install oh-my-zsh from inside the Windows Terminal
    - Enter this command into your terminal (note that it's one long line, even if it displays as two lines on the page where you're reading this): `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
    - Restart the terminal and open an Ubuntu tab with the little plus button in the top left corner
    - If the prompt in your terminal window is now a little arrow and a tilde (~), instead of "yourname@...", that's OK (you'll change it again in a later step)
    
1. Install VS Code if it isn't already installed
    - https://code.visualstudio.com/download
    
1. In your Ubuntu terminal, open VS Code with `code .`

1. Install the following VS Code extensions
    - Remote - WSL
    - Live Share (online students only)
    
1. Restart your terminal

1. Open VS Code again with `code .`
    - This should begin downloading the VS Code Server
    - When prompted for access (by Windows Defender Firewall), click "Allow access"
    
1. Install nvm
    - Enter this command into your terminal: `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash`
    
1. Move the 3 nvm lines from the bottom of `.bashrc` to the bottom of `.zshrc`
    - This is the trickest step. Run this command to open your .bashrc config file: `code ~/.bashrc`
    - Scroll down to the bottom of the file and cut the three lines at the bottom that look like this: 

    ```j
        export NVM_DIR="$HOME/.nvm"
        [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
        [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
    ```

    - Run this command to open your .zshrc file: `code ~/.zshrc`
    - Paste the nvm lines you cut from the .bashrc file down at the bottom of the .zshrc file.

1. Change the oh-my-zsh theme to 'bira'
    - Scroll to the top of the .zshrc file and replace the ZSH_THEME= value with 'bira'
    
1. Install the latest version of nvm 
    - Run this command in your terminal:`nvm install --lts`
    
1. In your Windows Terminal install some global npm packages
 - Just copy/paste in this entire chunk of code (if you get a warning about multiple lines of text, click "Paste anyway"):
 
    ```sh
    npm install -g \
    eslint@5.16.0 \
    babel-eslint@10.0.1 \
    eslint-config-standard@12.0.0 \
    eslint-plugin-import@2.17.3 \
    eslint-plugin-node@9.1.0 \
    eslint-plugin-promise@4.1.1 \
    eslint-plugin-react@7.13.0 \
    eslint-plugin-standard@4.0.0
    ```
    
    You are done!
    
