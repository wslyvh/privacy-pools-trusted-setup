# Welcome The Privacy Pools Demo Trusted Setup Ceremony!
Contributing to the ceremony requires some command line skillz, but it should be simple.

The definitive guide on how to run a trusted setup can be found in the [snarkjs](https://github.com/iden3/snarkjs) readme. There's no script within this repo to do the contribution! We are going to run the raw snarkjs commands directly, because we like tinkering in the terminal more than we like being comforted behind the ever sweet convenience of JavaScript.

Again, I recommend that you definitely should have read the [snarkjs](https://github.com/iden3/snarkjs) readme at least one time, but doing a quick refresher might not hurt in case it's been a while.

# Dependencies
 - [npm](https://www.npmjs.com/) / [yarn](https://yarnpkg.com/)
 - [rust](https://www.rust-lang.org/tools/install) / [circom2](https://docs.circom.io/getting-started/installation/)

# Steps
## 1. Verify and/or download the ptau file.
 - To verify the hash, run

```sh
node scripts/verifyPtauBlake2Hash.js
```
 - If it is incorrect, you can download it
```sh
bash setup.sh
```
The blake2 hashes for each ptau file are found [here](https://github.com/iden3/snarkjs#).

## 2. Compile the Circuits
Use the command
```sh
circom -o=./build --r1cs --sym --wasm
```

## 2. Contribute
You will have to check the latest number that hasn't been used yet by inspecting the [zkeys](./zkeys) direction, and use that value for the trusted setup ceremony. For example, with the following keys:
```
/zkeys/withdraw_from_subset_simple_0000.zkey
/zkeys/withdraw_from_subset_simple_0001.zkey
/zkeys/withdraw_from_subset_simple_0002.zkey
```

You would run
```
snarkjs zkc ./zkeys/withdraw_0002.zkey ./zkeys/withdraw_0003.zkey
```
from the root directory to generate the next contribution. Then, commit and push to your fork. We'll use a random blockhash for the beacon portion of the ceremony.

#### DO NOT SHARE THE ENTROPY WITH ANYONE! Your input is a random value that can be used to deterministically break the proving keys if they are gathered with all other contributions.

The last step of the ceremony is to initiate a pull request with your newly generated contribution file. The file should be saved to the [/zkeys](./zkeys) directory, before submitting a pull request.


Wallah! That's it.

# Last Steps
Pull to your own fork, have someone merge into your branch.