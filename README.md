# Cliche "lite-node" & LNbits Legend Install on a VPS

Quick install for setting up <a href="https://github.com/lnbits/lnbits-legend">LNbits Legend</a> on a cheap VPS runining a <a href="https://github.com/fiatjaf/cliche">Cliche lite-node</a> and requesting a <a href="https://github.com/btcontract/hosted-channels-rfc">hosted channel</a> for instant inbound liquidity! 👀 🚀

* Get a cheap Ubuntu 20.04 VPS at <a href="https://www.lunanode.com/">Lunanode</a>
* Register a domain with some registra and set an "A" reord for your Lunanode VPS ip address
![image](https://user-images.githubusercontent.com/33088785/182130029-7f063ec4-f7fe-4263-9ed9-00d127f047cf.png)

## Installation

#### Screen 1
    screen
    cd .
    git clone https://github.com/lnbits/lnbits-legend.git
    cd lnbits-legend/
    curl -sSL https://install.python-poetry.org | python3 -
    poetry install 
    mkdir data 
    
    LNBITS_BACKEND_WALLET_CLASS=ClicheWallet
    LNBITS_DATA_FOLDER="./data"
    cp .env.example .env # You can edit more variables in .env if you like 'sudo nano .env'
    
    poetry lnbits run
“Ctrl-A” and “d”

#### Screen 2
    screen
    wget https://github.com/fiatjaf/cliche/releases/download/v0.4.5/cliche-linux.bin.tar.gz
    tar -xf cliche-linux.bin.tar.gz 
    ./cliche # You'll get an error, use the wordlist it provides
    ./cliche -Dcliche.seed="egg turtle office supply visual wheat farm find wall coral thumb scrap"
    request-hc --port 80 --host 134.209.228.207 --pubkey 02cd1b7bc418fac2dc99f0ba350d60fa6c45fde5ab6017ee14df6425df485fb1dd
“Ctrl-A” and “d”

#### Screen 3
    screen
    sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
    curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
    curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
    sudo apt update
    sudo apt install caddy
    caddy stop
    caddy reverse-proxy --from yourdomain.com --to 127.0.0.1:5000 # Change yourdomain.com
“Ctrl-A” and “d”

To see the 3 screens you have made use `screen -ls`, to reattach to one use `screen -r TheScreenID`
## Additional

> *WARNING: Hosted channels are custoidal, but if they steal your money you have a cryptographic proof you can go complain to then with.*

> *You can use the SCRUB or BOLTZ LNbits extensions to push funds to another wallet or onchain, so your risk profile can be low.*

> *There are still not many providers of hosted channels. For now we will use this node https://amboss.space/node/02cd1b7bc418fac2dc99f0ba350d60fa6c45fde5ab6017ee14df6425df485fb1dd*
