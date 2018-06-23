## EOS docker workbench

### Running

To run
```bash
docker-compose up -d
```
To view stdout/stderr
```bash
docker-compose logs -f
```


### Creating 1st wallet

SSH into the docker container
```bash
docker-compose exec eosio /bin/bash
```

From within container, kill and then start any `keosd` processes using custom
port to listen on (`8899`)
```bash
pkill keosd
keosd --http-server-address=localhost:8899
```

In new terminal/shell ssh back into the docker container as before, and run
```bash
cleos --wallet-url=http://localhost:8899 wallet open
```
Save password. This will create a `default` account for new.

Make sure default wallet is unlocked.
```bash
cleos --wallet-url=http://localhost:8899 wallet unlock
cleos --wallet-url=http://localhost:8899 wallet list
```
Enter your password, and there should be a `*` beside the default wallet in the
result.

Next create the public/private key pair.
```bash
cleos --wallet-url=http://localhost:8899 create key
Private key: 5JXppxoXQUuc8VxtfmwfVrVx2JeyNpcpg9cVerSuxF8qNS2ARNQ                  
Public key: EOS5WUgzgXaFKZBbLcw6eNjPTekB6GskwM6N4MeHTWeGjVY4niQRo
```

Now import both the genesis key (default: `5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3`)
and the key from above step
```bash
cleos --wallet-url=http://localhost:8899 wallet import 5JXppxoXQUuc8VxtfmwfVrVx2JeyNpcpg9cVerSuxF8qNS2ARNQ
cleos --wallet-url=http://localhost:8899 wallet import 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
```

Now with default wallet unlocked, and containing keys, you can create an account
```bash
cleos --wallet-url=http://localhost:8899 create account eosio myaccount EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV EOS5WUgzgXaFKZBbLcw6eNjPTekB6GskwM6N4MeHTWeGjVY4niQRo
```
The 1st public key above (`EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV`)
is the public key of the `eosio` genesis account.



####
# The genesis account: eosio
# @see https://github.com/EOSIO/eos/issues/4154#issuecomment-397820824
#
# - eosio public key: EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
# - eosio private key: 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3
###
