# micro-blocker

Simple scripts to prevent editing the host file in Linux for productivity purposes, blocking access to tools like nano, nvim, and vim.

## Getting Started

Include the websites you wish to block in the host file.

```
0.0.0.0 youtube.com
0.0.0.0 www.youtube.com
```

Then, add the following to `~/.bashrc` : 

```
sudo() {
    if { [ "$1" = "nano" ] || [ "$1" = "nvim" ] || [ "$1" = "vim" ]; } && [ "$2" = "/etc/hosts" ]; then
        echo "Editing /etc/hosts is disabled."
        return 1
    else
        command sudo "$@"
    fi
}
```

To prevent the root user from accessing, include in `/root/.bashrc` :

```
nano() {
    for arg in "$@"; do
        if [[ "$arg" == "/etc/hosts" ]]; then
            echo "Editing /etc/hosts is disabled for root."
            return 1
        fi
    done
    command nano "$@"
}

vim() {
    for arg in "$@"; do
        if [[ "$arg" == "/etc/hosts" ]]; then
            echo "Editing /etc/hosts is disabled for root."
            return 1
        fi
    done
    command vim "$@"
}

nvim() {
    for arg in "$@"; do
        if [[ "$arg" == "/etc/hosts" ]]; then
            echo "Editing /etc/hosts is disabled for root."
            return 1
        fi
    done
    command nvim "$@"
}
```
