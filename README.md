# Ansible Avalanche Kite AI Template

How to use the [ash.avalanche](https://github.com/AshAvalanche/ansible-avalanche-collection) Ansible collection to an [Avalanche](https://docs.avax.network/) validator node tracking the [Kite AI](https://gokite.ai) L1.

## Requirements

- Python >=3.9 with `venv` module installed

## Setup the environment

1. Clone the Getting Started repository:

   ```bash
   git clone https://github.com/AshAvalanche/ansible-avalanche-kite-ai-template.git
   cd ansible-avalanche-kite-ai-template
   ```

2. Setup and activate Python venv:

   ```bash
   bin/setup.sh
   source .venv/bin/activate
   ```

## Provision the local Avalanche validator

1. Bootstrap the Avalanche nodes:

   ```bash
   ansible-playbook ash.avalanche.provision_nodes -i inventories/local -c local -e avalanchego_public_ip=$(curl -s ifconfig.me)
   ```

2. Track node bootstrapping:

   ```bash
   # P-Chain bootstrapping
   curl -X POST --data '{
      "jsonrpc": "2.0",
      "id"     : 1,
      "method" : "info.isBootstrapped",
      "params": {
         "chain": "P"
      }
   }' -H 'content-type:application/json;' http://127.0.0.1:9650/ext/info

   # Kite AI L1 bootstrapping
   curl -X POST --data '{
      "jsonrpc": "2.0",
      "id"     : 1,
      "method" : "info.isBootstrapped",
      "params": {
         "chain": "3USaEfTcoUhHxpKXvpAG916UKCUEyjrtkg2hBArBG3JyDP7my"
      }
   }' -H 'content-type:application/json;' http://127.0.0.1:9650/ext/info
   ```
