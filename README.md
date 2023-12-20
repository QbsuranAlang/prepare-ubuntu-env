1. first apt jobs
----------
```
$ sudo apt -y update
$ sudo apt -y upgrade
$ sudo reboot
```

2. apt install
----------
```
$ sudo apt install -y bc bison build-essential ccache curl fakeroot flex gcc-multilib git gnupg2 libelf-dev libffi-dev libjpeg8-dev libncurses5 libncurses5-dev libssl-dev libxml2-dev libxslt1-dev ncurses-dev net-tools ntfs-3g openssh-server python-pip valgrind vim wget wget2 xz-utils zlib1g-dev zsh network-manager-l2tp network-manager-l2tp-gnome
```

3. git
----------
```
$ git config --global init.defaultBranch main
$ git config --global user.email jr89197@hotmail.com
$ git config --global user.name QbsuranAlang
$ git config --global core.editor vim
$ git config --global gpg.program gpg2
```

4. sudoers
----------
```
$ echo "tutu ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
```

5. ssh
----------
```
$ sudo systemctl restart ssh
$ sudo systemctl enable ssh
```

6. tcpdump
----------
```
$ sudo setcap cap_net_raw,cap_net_admin+eip `which tcpdump`
```

7. ssh config
----------
```
$ sudo vim /etc/ssh/sshd_config

PermitRootLogin no
```

8. ssh keys
----------
```
$ ssh-keygen
$ ssh-keygen -t ed25519
```

9. change root password
----------
```
$ sudo passwd root
```

10. install zsh
----------
```
$ sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
$ sudo apt install zsh
$ chsh -s /bin/zsh
$ logout
```

11. install golang
----------
```
$ wget https://go.dev/dl/go1.21.5.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz

export GOPATH=$HOME/.golang
export GOROOT=/usr/local/go
export PATH=$PATH:$GOPATH/bin:$GOROOT/bin
```

12. man page
----------
```
export LESS_TERMCAP_mb=$'\E[38;5;167m'  # begin blinking
export LESS_TERMCAP_md=$'\E[38;5;39m'   # begin bold
export LESS_TERMCAP_me=$'\E[38;5;231m'  # end mode
export LESS_TERMCAP_se=$'\E[38;5;231m'  # end standout-mode
export LESS_TERMCAP_so=$'\E[38;5;167m'  # begin standout-mode - info box
export LESS_TERMCAP_ue=$'\E[38;5;231m'  # end underline
export LESS_TERMCAP_us=$'\E[38;5;167m'   # begin underline
```

13. ccache
----------
```
$ ccache -M 20G

export USE_CCACHE=1
export CCACHE_DIR="$HOME/.ccache"
export CC="ccache gcc"
export CXX="ccache g++"
export PATH="/usr/lib/ccache:$PATH"
```

14. shell function
----------
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

15. zsh settings
----------
```
HISTSIZE=999999999
SAVEHIST=$HISTSIZE
```

16. disable apport and enable core-dump
----------
```
$ sudo systemctl stop apport
$ sudo systemctl disable apport
$ echo "core.%e.%p.%t" | sudo tee /proc/sys/kernel/core_pattern
```

17. github gpg
----------
```
$ gpg --default-new-key-algo rsa4096 --gen-key
$ gpg2 --list-keys --keyid-format LONG
$ gpg --armor --export xxxxxxxxxxxxxxxxxxx
```

18. vim colors
----------
```
$ cd ~
$ mkdir -p ~/.vim/colors
$ cp kolor.vim ~/.vim/colors
```

19. install chrome
----------
```
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo dpkg -i google-chrome-stable_current_amd64.deb
$ sudo apt-get install -f
```

20. install L2TP/IPSec VPN
----------
```
Following https://dotblogs.com.tw/shaynling/2020/08/05/233356
```

21. grub list
----------
```
awk -F\' '$1=="menuentry " || $1=="submenu " {print i++ " : " $2}; /\smenuentry / {print "\t" i-1">"j++ " : " $2};' /boot/grub/grub.cfg
```
