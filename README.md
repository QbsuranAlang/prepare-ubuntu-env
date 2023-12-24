<h2>1. first apt jobs</h2>

```
$ sudo apt -y update
$ sudo apt -y upgrade
$ sudo reboot
```

<h2>2. apt install</h2>

```
$ sudo apt install -y bc bison build-essential ccache curl fakeroot flex gcc-multilib git gnupg2 libelf-dev libffi-dev libjpeg8-dev libncurses5 libncurses5-dev libssl-dev libxml2-dev libxslt1-dev ncurses-dev net-tools ntfs-3g openssh-server python-pip valgrind vim wget wget2 xz-utils zlib1g-dev zsh network-manager-l2tp network-manager-l2tp-gnome e2fsprogs apt-transport-https tree dconf-editor
```

<h2>3. ubuntu pro</h2>

```
$ sudo pro attach
```

<h2>4. git</h2>

```
$ git config --global init.defaultBranch main
$ git config --global user.email jr89197@hotmail.com
$ git config --global user.name QbsuranAlang
$ git config --global core.editor vim
$ git config --global gpg.program gpg2
```

<h2>5. sudoers</h2>

```
$ echo "tutu ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers > /dev/null
```

<h2>6. ssh</h2>

```
$ sudo systemctl restart ssh
$ sudo systemctl enable ssh
```

<h2>7. tcpdump</h2>

```
$ sudo setcap cap_net_raw,cap_net_admin+eip `which tcpdump`
```

<h2>8. ssh config</h2>

```
$ sudo vim /etc/ssh/sshd_config

PermitRootLogin no

$ sudo systemctl restart ssh
```

<h2>9. ssh keys</h2>

```
$ ssh-keygen
$ ssh-keygen -t ed25519
```

<h2>10. change root password</h2>

```
$ sudo passwd root
```

<h2>11. install zsh</h2>

```
$ sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
$ sudo apt install zsh
$ chsh -s /bin/zsh
$ kill `echo $(who -u) | awk '{print $6}'` # logout
```

<h2>12. install golang</h2>

```
$ wget https://go.dev/dl/go1.21.5.linux-amd64.tar.gz
$ sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz

# golang
export GOPATH=$HOME/.golang
export GOROOT=/usr/local/go
export PATH=$PATH:$GOPATH/bin:$GOROOT/bin
```

<h2>13. man page</h2>

```
# colors for man pages
export LESS_TERMCAP_mb=$'\E[38;5;167m'  # begin blinking
export LESS_TERMCAP_md=$'\E[38;5;39m'   # begin bold
export LESS_TERMCAP_me=$'\E[38;5;231m'  # end mode
export LESS_TERMCAP_se=$'\E[38;5;231m'  # end standout-mode
export LESS_TERMCAP_so=$'\E[38;5;167m'  # begin standout-mode - info box
export LESS_TERMCAP_ue=$'\E[38;5;231m'  # end underline
export LESS_TERMCAP_us=$'\E[38;5;167m'  # begin underline
```

<h2>14. ccache</h2>

```
$ ccache -M 20G

# ccache
export USE_CCACHE=1
export CCACHE_DIR="$HOME/.ccache"
export CC="ccache gcc"
export CXX="ccache g++"
export PATH="/usr/lib/ccache:$PATH"
```

<h2>15. ~/.zshrc</h2>

```
# function
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

<h2>16. zsh settings</h2>

```
HISTSIZE=999999999
SAVEHIST=$HISTSIZE
```

<h2>17. disable apport and enable core-dump</h2>

```
$ sudo systemctl stop apport
$ sudo systemctl disable apport
$ echo "core.%e.%p.%t" | sudo tee /proc/sys/kernel/core_pattern > /dev/null
```

<h2>18. github ssh/gpg</h2>

```
# ssh
name: tutu@tutu-ubuntu ed25519

$ cat ~/.ssh/id_ed25519.pub
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIHxPvGPMpQ6FyBYCZ6bK3gODsPojB23fZWqvqfYDO3z1 tutu@tutu-ubuntu

# gpg
name: tutu@tutu-ubuntu rsa4096

$ gpg --default-new-key-algo rsa4096 --gen-key
# or
$ gpg --full-generate-key

$ gpg --list-secret-keys --keyid-format=long
$ gpg --armor --export xxxxxxxxxxxxxxxxxxx
$ git config --global user.signingkey sxxxxxxxxxxxxxxxxxxx
$ git config --global commit.gpgsign true
```

<h2>19. vim colors</h2>

```
$ cp -R vim ~/.vim
$ cp vimrc ~/.vimrc
```

<h2>20. install chrome</h2>

```
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo dpkg -i google-chrome-stable_current_amd64.deb
$ sudo apt-get install -f
```

<h2>21. install L2TP/IPSec VPN</h2>

```
Following https://dotblogs.com.tw/shaynling/2020/08/05/233356
```

<h2>22. grub list</h2>

```
awk -F\' '$1=="menuentry " || $1=="submenu " {print i++ " : " $2}; /\smenuentry / {print "\t" i-1">"j++ " : " $2};' /boot/grub/grub.cfg
```

<h2>23. install Sublime</h2>

```
$ wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sublimehq-archive.gpg > /dev/null
$ echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list > /dev/null
$ sudo apt update
$ sudo apt install -y sublime-text
```

<h3>install package</h3>

```
"Agila Theme"

$ cp -R Packages ~/.config/sublime-text
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

<h2>24. mac wifi driver</h2>

```
$ lspci -nnk|grep 0280 -A3
e5:00.0 Network controller [0280]: Broadcom Inc. and subsidiaries BCM4364 802.11ac Wireless Network Adapter [14e4:4464] (rev 04)
    Subsystem: Apple Inc. BCM4364 802.11ac Wireless Network Adapter [106b:07bf]
    Kernel modules: brcmfmac
e6:00.0 Mass storage controller [0180]: Apple Inc. ANS2 NVMe Controller [106b:2005] (rev 01)


`106b:07bf`
$ wget https://packages.aunali1.com/apple/wifi-fw/18G2022/C-4364__s-B2/kauai.trx
$ sudo cp kauai.trx /lib/firmware/brcm/brcmfmac4364-pcie.bin
```

<h2>25. install KVM</h2>

```
$ sudo grep -E -c '(vmx|svm)' /proc/cpuinfo # cannot be zero
16
$ sudo apt install -y cpu-checker && kvm-ok
INFO: /dev/kvm exists
KVM acceleration can be used

$ sudo apt install -y qemu-kvm libguestfs-tools libvirt-clients libvirt-daemon-system bridge-utils virt-manager ovmf swtpm

$ sudo adduser $USER libvirt
$ sudo adduser $USER kvm
$ sudo adduser $USER input
$ sudo chown $USER:$USER /var/run/libvirt/libvirt-sock

$ sudo systemctl enable libvirtd
$ sudo systemctl restart libvirtd
$ sudo virsh net-start default
$ sudo virsh net-autostart default

$ virt-manager
```

<h2>26. git move head back one commit</h2>

```
$ git reset --soft HEAD~1
```

<h2>27. git GPG sign previous all commit</h2>

```
$ git rebase --exec "git commit --amend --no-edit -n -S" -i --root
$ git push --force
```
