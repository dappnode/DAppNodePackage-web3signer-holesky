## Welcome to the Web3signer for Göerli/Holesky:

- This package is the entrypoint for handling your validator keystores
- The Web3signer takes care of signing requests for your validator, so that your Consensus Layer (CL) client can be changed with just a few clicks.
- The Web3signer supports client diversity in this way; working with different clients such as:
  - [Prysm-Holesky](http://my.dappnode/#/installer/prysm-holesky.dnp.dappnode.eth)
  - [Lighthouse-Holesky](http://my.dappnode/#/installer/lighthouse-holesky.dnp.dappnode.eth)
  - [Teku-Holesky](http://my.dappnode/#/installer/teku-holesky.dnp.dappnode.eth)
  - [Nimbus-Holesky](http://my.dappnode/#/installer/nimbus-holesky.dnp.dappnode.eth)
- All Staking Management is now in the Comprehensive [StakersUI](http://my.dappnode/#/stakers/holesky)
- The Flyway service takes care of importing the previous version's slashing protection database when an update is installed, so it's meant to run only once per update, and it is normal to see that the Flyway service is stopped
