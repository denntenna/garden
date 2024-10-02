---
tags:
  - elixir
---
**Install Erlang prerequisites**
```sh
sudo apt-get install build-essential autoconf libncurses5-dev \ 
openssl libssl-dev fop xsltproc unixodbc-dev libwxgtk3.0-gtk3-dev \ 
libgl1-mesa-dev libglu1-mesa-dev libpng-dev
```

**Install `asdf` to manage various versions of elixir and erlang**
```sh
git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.10.2
echo ". $HOME/.asdf/asdf.sh" >> ~/.bashrc
source ~/.bashrc
```


**Install asdf plugins for elixir and erlang**
```sh
asdf plugin add erlang
asdf plugin add elixir
```

**List all available versions**
```sh
asdf list-all erlang
asdf list-all elixir
```

**Install specific versions**
```sh
asdf install erlang 27.0
asdf install elixir 1.17.2-otp-27
```

**Set active versions for elixir and erlang**
```sh
asdf global elixir 1.17.2-otp-27
asdf global elixir 27.0
```

**Test Elixir installation**
```sh
echo "IO.puts(1+2)" >> hello.exs
elixir hello.exs
```

