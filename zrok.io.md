# Introduction
Enables publicizing localhost URLs so anyone on the internet can reach your localhost port via tunneling. tunnel is #ephemeral by default, but can be set as "reserved" to chope the zrok URL.
# Installation
  1. Go to https://github.com/openziti/zrok/releases/tag/v0.4.26, copy the arm64.tar.gz URL
  2. On linux `/` directory, `wget <url>`
  3. `mkdir /tmp/zrok && tar -xf ./zrok*linux*.tar.gz -C /tmp/zrok`
  4. `install /tmp/zrok/zrok ~/usr/bin/`
  5. `PATH=~/usr/bin:$PATH`
  6. `zrok version`
# How To Use
## Basic Commands
```
//makes zrok invite you to create an account (required to create an account token)
zrok invite

//enable zrok account
zrok enable <account  token>

//see zrok status
zrok status

//creates "share token" of public or private resource/endpoint
zrok share <public/private> <resource/endpoint>
eg:
zrok share public http://localhost:3000

//access a private endpoint
zrok access private <share token>

//create reserved "share token" (so that it will not be ephemeral)
zrok reserve public <resource/endpoint>
//share the reserved token
zrok share reserved <resource/endpoint>
//release the reserved token (so it can never be used again)
zrok release <resource/endpoint>
