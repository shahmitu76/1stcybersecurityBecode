# MullVad Browser



## Install 

1. Open a Terminal and download the latest release for your current user:

   cd ~/.local/share && wget https://mullvad.net/en/download/browser/linux64/latest -O mullvad-browser.tar.xz

2. Extract the content of the downloaded file into a `mullvad-browser` folder:

   `tar -xvf mullvad-browser.tar.xz mullvad-browser`

3. Delete the downloaded tar.xz file as you don’t need it anymore and enter the extracted folder:

   `rm mullvad-browser.tar.xz && cd mullvad-browser`

4. Launch Mullvad Browser with the `--register-app` flag, this should register Mullvad Browser as a desktop app for the current user:

   `./start-mullvad-browser.desktop --register-app`

   You can also run `./start-mullvad-browser.desktop --help` to see more options.

5. Run `./start-mullvad-browser.desktop --setDefaultBrowser` to set Mullvad Browser as your default browser.



That's it! MullVad browser is installed.

Reference: 

[](https://retiolus.net/posts/how-to-install-mullvad-browser-on-linux/)

