<h2>1. first apt jobs</h2>

```
$ sudo apt -y update
$ sudo apt -y upgrade
$ sudo reboot
```

<h2>2. apt install</h2>

```
$ sudo apt install -y bc bison build-essential ccache curl fakeroot flex gcc-multilib git gnupg2 libelf-dev libffi-dev libjpeg8-dev libncurses5 libncurses5-dev libssl-dev libxml2-dev libxslt1-dev ncurses-dev net-tools ntfs-3g openssh-server python-pip valgrind vim wget wget2 xz-utils zlib1g-dev zsh network-manager-l2tp network-manager-l2tp-gnome
```

<h2>3. git</h2>

```
$ git config --global init.defaultBranch main
$ git config --global user.email jr89197@hotmail.com
$ git config --global user.name QbsuranAlang
$ git config --global core.editor vim
$ git config --global gpg.program gpg2
```

<h2>4. sudoers</h2>

```
$ echo "tutu ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
```

<h2>5. ssh</h2>

```
$ sudo systemctl restart ssh
$ sudo systemctl enable ssh
```

<h2>6. tcpdump</h2>

```
$ sudo setcap cap_net_raw,cap_net_admin+eip `which tcpdump`
```

<h2>7. ssh config</h2>

```
$ sudo vim /etc/ssh/sshd_config

PermitRootLogin no
```

<h2>8. ssh keys</h2>

```
$ ssh-keygen
$ ssh-keygen -t ed25519
```

<h2>9. change root password</h2>

```
$ sudo passwd root
```

<h2>10. install zsh</h2>

```
$ sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
$ sudo apt install zsh
$ chsh -s /bin/zsh
$ logout
```

<h2>11. install golang</h2>

```
$ wget https://go.dev/dl/go1.21.5.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz

export GOPATH=$HOME/.golang
export GOROOT=/usr/local/go
export PATH=$PATH:$GOPATH/bin:$GOROOT/bin
```

<h2>12. man page</h2>

```
export LESS_TERMCAP_mb=$'\E[38;5;167m'  # begin blinking
export LESS_TERMCAP_md=$'\E[38;5;39m'   # begin bold
export LESS_TERMCAP_me=$'\E[38;5;231m'  # end mode
export LESS_TERMCAP_se=$'\E[38;5;231m'  # end standout-mode
export LESS_TERMCAP_so=$'\E[38;5;167m'  # begin standout-mode - info box
export LESS_TERMCAP_ue=$'\E[38;5;231m'  # end underline
export LESS_TERMCAP_us=$'\E[38;5;167m'  # begin underline
```

<h2>13. ccache</h2>

```
$ ccache -M 20G

export USE_CCACHE=1
export CCACHE_DIR="$HOME/.ccache"
export CC="ccache gcc"
export CXX="ccache g++"
export PATH="/usr/lib/ccache:$PATH"
```

<h2>14. shell function</h2>

```
function external_ip() {
    curl https://www.myexternalip.com/raw
}

function sc() {
    # help
    if [[ "${1}" = "help" || "$#" -le "1" ]]; then
        echo -e "sc filename[\e[0;106mfind -name xxx\e[0m] greps[\e[0;106mgrep xxx | grep xxx | grep...\e[0m]"
        return
    fi

    # colored grep command
    alias color_grep='\grep -n --color=auto'

    # replace grep command to colored grep command
    GREPS=$(echo ${2} | sed 's/grep/color_grep/g')

    # output
    for FILE in ```find . -type f -name "${1}"```; do
        CMD="cat ${FILE} | ${GREPS} | wc -l"

        # grep lines
        LINE=$(eval $CMD)

        if [ "$LINE" -ne "0" ]; then
            echo -e "\e[0;106m ====== Begin of: ${FILE} ====== \e[0m"

            # output filename
            CMD="cat ${FILE} | ${GREPS}"
            eval $CMD

            echo -e "\e[0;102m ====== End of: ${FILE} ====== \e[0m"
            echo -e "\n"
        fi
    done
}
```

<h2>15. zsh settings</h2>

```
HISTSIZE=999999999
SAVEHIST=$HISTSIZE
```

<h2>16. disable apport and enable core-dump</h2>

```
$ sudo systemctl stop apport
$ sudo systemctl disable apport
$ echo "core.%e.%p.%t" | sudo tee /proc/sys/kernel/core_pattern
```

<h2>17. github gpg</h2>

```
$ gpg --default-new-key-algo rsa4096 --gen-key
$ gpg2 --list-keys --keyid-format LONG
$ gpg --armor --export xxxxxxxxxxxxxxxxxxx
```

<h2>18. vim colors</h2>

```
$ cd ~
$ mkdir -p ~/.vim/colors
$ cp kolor.vim ~/.vim/colors
```

<h2>19. install chrome</h2>

```
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo dpkg -i google-chrome-stable_current_amd64.deb
$ sudo apt-get install -f
```

<h2>20. install L2TP/IPSec VPN</h2>

```
Following https://dotblogs.com.tw/shaynling/2020/08/05/233356
```

<h2>21. grub list</h2>

```
awk -F\' '$1=="menuentry " || $1=="submenu " {print i++ " : " $2}; /\smenuentry / {print "\t" i-1">"j++ " : " $2};' /boot/grub/grub.cfg
```

<h2>22. install Sublime</h2>

```
$ wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg > /dev/null
$ echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
$ sudo apt update
$ sudo apt install -y apt-transport-https
$ sudo apt install -y sublime-text
```

<h3>install package</h3>

```
"Agila Theme"
Copy `Packages` directory to `/home/tutu/.config/sublime-text`
```

<h3>settings</h3>

```
{
    "color_scheme": "Packages/Agila Theme/Agila Oceanic Next.tmTheme",
    "draw_white_space": "all",
    "font_face": "Monaco",
    "font_size": 14,
    "ignored_packages":
    [
        "Vintage"
    ],
    "show_definitions": false,
    "tab_size": 4,
    "theme": "Agila.sublime-theme",
    "translate_tabs_to_spaces": true
}
```
