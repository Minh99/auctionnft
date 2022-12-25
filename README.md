## Begin
Requirements
Node.js version >= 14.17.0 or above (which can be checked by running node -v). You can use nvm for managing multiple Node versions on a single machine installed.
Yarn. Yarn is a performant package manager for JavaScript and replaces the npm client.

## Important NOTE

### How to checkout a release
```
//If you are using a fork
git fetch upstream --tags

git checkout tags/<tag> // this will bring the contents of the tag into your current branch

// OR 
git checkout tags/<tag> -b <your local branch name> // this will make a new branch for you

To swich to a new release

git checkout tags/<tag> -b new_version_branch /// this will take the new tag and bring it into  anew branch
//Switch back to the branch you want the new changes in
git rebase new_version_branch
```

## Installing

Clone the repo, and run `yarn start` to deploy.

```bash
$ git clone https://github.com/Minh99/auctionnft.git
$ cd auctionnft/js
$ yarn install && yarn bootstrap && yarn build
$ yarn start
```

Navigate to `http://localhost:3000/` to explore the deployed application.

## after init store
After store initialization completes, you must save your new store addresses. In the Store configuration section on the store page click on the Copy button and paste in the .env file in js/packages/web.

## Rust Programs

The Rust programs will soon be added to this repo with JavaScript
bindings that allow interactivity.

# Protocol
```
# Change to devnet
solana config set --url devnet

# Build the project (takes a few mins)
cd rust
cargo build-bpf

# While you wait for the previous step to complete, find the current program id
# of the program you plan to test by searching the code base.  Save this for
# later.

# After the build step completes, deploy the program to devnet
solana program deploy ./path/to/the_program.so -u devnet

# NOTE: If you receive an error stating insufficient funds, recoup the funds
# used during the failed deployment. You may also see the following error which
# also means insufficient funds:
#     "Error: Deploying program failed: Error processing Instruction 1: custom program error: 0x1"
solana program close --buffers

# NOTE: If you had an insufficient funds, airdrop yourself some SOL, then run the deploy
# command again. I needed roughly 5 SOL to deploy the auction contract.
solana airdrop 5

# After successful deploy, a new Program Id will be printed to your terminal. Copy this
# and update the program's id everywhere in the code base. This way, during testing, we
# always call the version of the program we are testing instead of the stable one.
# DO NOT SKIP THIS STEP or you won't test your changes

# Next, comment out your js/packages/web/.env variables to force creation of a fresh new store

# Now start up the UI
cd ../js/packages
yarn && yarn bootstrap
yarn start

# Open the site in a browser in *incognito* mode http://localhost:3000

# In the incognito browser, create a new wallet by visiting https://sollet.io
# Copy the wallet address

# You'll need SOL added to the new wallet
solana airdrop 4 NEW_WALLET_ADDRESS

# Now visit the site (in incognito mode)
# Connect your new wallet
# Create a new store
# Test your program changes
```
