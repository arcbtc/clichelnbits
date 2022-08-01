# Cliche "lite-node" LNbits Legend Install

* Get a cheap Ubuntu 20.04 VPS at <a href="https://www.lunanode.com/">Lunanode</a>
* Go register a domain and set an `A` reord for your Lunanode VPS ip address

#### Screen 1
    screen
    cd .
    git clone https://github.com/lnbits/lnbits-legend.git
    cd lnbits-legend/
    curl -sSL https://install.python-poetry.org | python3 -
    poetry install 
    mkdir data 
    LNBITS_BACKEND_WALLET_CLASS=ClicheWallet
    poetry lnbits run
“Ctrl-A” and “d”

#### Screen 2
    screen
    wget https://github.com/fiatjaf/cliche/releases/download/v0.4.5/cliche-linux.bin.tar.gz
    tar -xf cliche-linux.bin.tar.gz 
    ./cliche -Dcliche.seed="egg turtle office supply visual wheat farm find wall coral thumb scrap"
“Ctrl-A” and “d”

#### Screen 3
    screen
    sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
    curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
    curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
    sudo apt update
    sudo apt install caddy
    caddy stop
    caddy reverse-proxy --from yourdomain.com --to 127.0.0.1:5000
“Ctrl-A” and “d”

