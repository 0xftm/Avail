# Avail

## Perparation
```sh
sudo apt-get update
sudo apt install build-essential
sudo apt install --assume-yes git clang curl libssl-dev protobuf-compiler
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.cargo/env
rustup default stable
rustup update
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
```
## Download and install
```sh
git clone https://github.com/availproject/avail.git
cd avail
mkdir -p output
mkdir -p data
git checkout v1.8.0.3
cargo run --locked --release -- --chain goldberg --validator -d ./output
```
** Press Ctrl + C to exit the screen **

## Create service

```sh
sudo touch /etc/systemd/system/availd.service
sudo nano /etc/systemd/system/availd.service
```

```sh
[Unit] 
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0
[Service] 
User=root 
ExecStart= /root/avail/target/release/data-avail -d ./output --chain goldberg --validator --name "Flytomoon-avail"
Restart=always 
RestartSec=120
[Install] 
WantedBy=multi-user.target
```
** Change this name "Flytomoon-avail" to your own **
Save it: CTRL+X -> Yes

## To enable this to autostart on bootup run:

```sh
systemctl enable availd.service
```
## Start it manually with:

```sh
systemctl start availd.service
```

## You can check that it's working with:

```sh
systemctl status availd.service
```

## You can tail the logs with journalctllike so:

```sh
journalctl -f -u availd
```

## Check your node on https://telemetry.avail.tools
![image](https://github.com/0xftm/Avail/assets/115777868/1c5d5e62-ec9f-4058-945f-5179e27a026e)

