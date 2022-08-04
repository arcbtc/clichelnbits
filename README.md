# Guide - Cliche "lite-node"/LNbits Legend on a VPS

Quick install for setting up <a href="https://github.com/lnbits/lnbits-legend">LNbits Legend</a> on a cheap VPS runining a <a href="https://github.com/fiatjaf/cliche">Cliche lite-node</a> and requesting a <a href="https://github.com/btcontract/hosted-channels-rfc">hosted channel</a> for instant inbound liquidity! 👀 🚀

* Get a cheap Ubuntu 20.04 VPS at <a href="https://www.lunanode.com/">Lunanode</a>
* Register a domain with some registra and set an "A" reord for your Lunanode VPS IP address
![image](https://user-images.githubusercontent.com/33088785/182130029-7f063ec4-f7fe-4263-9ed9-00d127f047cf.png)

## Installation



#### Screen 1 - Cliche (the lite-node)
    wget https://github.com/fiatjaf/cliche/releases/download/v0.4.5/cliche-linux.bin.tar.gz
    tar -xf cliche-linux.bin.tar.gz
    
    screen -S cliche
    
    ./cliche # You'll get an error, use the wordlist it provides
    ./cliche -Dcliche.seed="egg turtle office supply visual wheat farm find wall coral thumb scrap"
    request-hc --port 80 --host 134.209.228.207 --pubkey 02cd1b7bc418fac2dc99f0ba350d60fa6c45fde5ab6017ee14df6425df485fb1dd
“Ctrl-A” and “d” to exit screen

#### Screen 2 - LNbits
    git clone https://github.com/lnbits/lnbits-legend.git
    cd lnbits-legend/
    
    sudo apt update
    sudo apt install software-properties-common
    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt install python3.9
    
    curl -sSL https://install.python-poetry.org | python3 -
    export PATH="/home/ubuntu/.local/bin:$PATH"
    
    screen -S lnbits
    
    poetry env use python3.9

    poetry install
    mkdir lnbits/data 
    

    cp .env.example .env
    sudo nano .env
    # Set "LNBITS_BACKEND_WALLET_CLASS=ClicheWallet"
    
    poetry run lnbits
“Ctrl-A” and “d” to exit screen

#### Screen 3 - Caddy (the reverse proxy and https server)
    sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
    curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
    curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
    sudo apt update
    sudo apt install caddy
    caddy stop
    
    screen -S caddy
    
    caddy reverse-proxy --from yourdomain.com --to 127.0.0.1:5000 # Change yourdomain.com
“Ctrl-A” and “d” to exit screen

To see the 3 screens created use `screen -ls`, reattach to screens using `screen -r lnbits`, `screen -r cliche`, `screen -r caddy`
## Additional

> *WARNING: Hosted channels are custoidal, but if they steal your money you have a cryptographic proof you can go complain to then with.*

> *You can use the SCRUB or BOLTZ LNbits extensions to push funds to another wallet or onchain, so your risk profile can be low.*

> *There are still not many providers of hosted channels. For now we will use this node https://amboss.space/node/02cd1b7bc418fac2dc99f0ba350d60fa6c45fde5ab6017ee14df6425df485fb1dd*
