
**This final project is an implementation of GiftCertificates as an NFT/ ERC721 token.

# ERC721 Gift Certificates

## Background

The problem when you buy a gift certificate in a shop is that once you pay for it the shop owner already has the money but you are not sure he will honor the agreement and actually let you purchase items according to the value of the certificate. The shop could also go out of business and you would lose the value of the certificate. And all this without the shop vesting any money in this setup.

What this `ERC721` token seeks to solve is that a shop owner only receives the money once you spend the certificate. It also includes a functionality for the shop owner or promoter to give the customer a discount or rather a bonus value on top of the purchase price. For example a City could fund this Token with a 10% bonus so that a customer who purchased a gift certificate of 100 USD would actually be able to spend 110 USD at a approved shop in the city.

I have implemented a whitelist to allow only shops to redeem the Gift Certificates. As redeeming them gets you a 10% bonus, we don't want everyone to be able to redeem their own Gift Certificates and get free money. The whitelist is maintained by the owner of the ERC721 contract. Shop owners can renounce their 'membership'.

Things still to be added:
- implement a validity period for each certificate. This time period would allow a customer to redeem the certificate without the bonus for instance in the case there are not enough participating shops anymore.

## install

Clone the git repository

```bash
git clone https://github.com/dev-bootcamp-2019/final-project-dirkconinx
cd final-project-dirkconinx
```

## test
These test have been written for Truffle v5 (web3 v1.0.0) which uses BN whereas Truffle v4 (web3 0.20.x) used BigNumber. Therefor these test will fail if you use Truffle v4. Please use Truffle v5

You can see the version of your Truffle installation like this
```bash
npm list -g truffle
/home/coninxd/.nvm/versions/node/v11.6.0/lib
└── truffle@5.0.0

```
To uninstall Truffle v5 and reinstall v4:
```bash
npm remove -g truffle
npm install -g truffle
```
Note: if you're having problems with (sudo related) access rights regarding npm I highly recommend [this guide](https://www.nearform.com/blog/how-to-manage-node-js-sudo-free-with-nvm/)

Also there is an [issue](https://github.com/ethereum/web3.js/issues/1916) with web3 1.0.0-beta.37 and certain events. We use the latest OpenZeppelin v2.1.0 beta2 and have modified the ERC20.sol removing all the emits as a workaround until the issue is resolved.

Run truffle develop and run the tests
```bash
truffle develop
truffle(develop)> test
Using network 'develop'.

Compiling ./../../final-project-dirkconinx/contracts/GiftCertificate.sol...
Compiling ./../../final-project-dirkconinx/contracts/StableToken.sol...
Compiling ./contracts/GiftCertificate.sol...
Compiling ./contracts/Migrations.sol...
Compiling ./contracts/StableToken.sol...
Compiling openzeppelin-solidity/contracts/access/Roles.sol...
Compiling openzeppelin-solidity/contracts/access/roles/PauserRole.sol...
Compiling openzeppelin-solidity/contracts/drafts/Counter.sol...
Compiling openzeppelin-solidity/contracts/introspection/ERC165.sol...
Compiling openzeppelin-solidity/contracts/introspection/IERC165.sol...
Compiling openzeppelin-solidity/contracts/lifecycle/Pausable.sol...
Compiling openzeppelin-solidity/contracts/math/SafeMath.sol...
Compiling openzeppelin-solidity/contracts/ownership/Ownable.sol...
Compiling openzeppelin-solidity/contracts/token/ERC20/ERC20.sol...
Compiling openzeppelin-solidity/contracts/token/ERC20/ERC20Detailed.sol...
Compiling openzeppelin-solidity/contracts/token/ERC20/IERC20.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/ERC721.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/ERC721Enumerable.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/ERC721Full.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/ERC721Metadata.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/ERC721Pausable.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/IERC721.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/IERC721Enumerable.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/IERC721Metadata.sol...
Compiling openzeppelin-solidity/contracts/token/ERC721/IERC721Receiver.sol...
Compiling openzeppelin-solidity/contracts/utils/Address.sol...

Compilation warnings encountered:

openzeppelin-solidity/contracts/drafts/Counter.sol:17:3: Warning: This declaration shadows an existing declaration.
  struct Counter {
  ^ (Relevant source part starts here and spans across multiple lines).
openzeppelin-solidity/contracts/drafts/Counter.sol:15:1: The shadowed declaration is here:
library Counter {
^ (Relevant source part starts here and spans across multiple lines).

Contract: StableToken
  ✓ TotalSupply of STBL at the start should be 0
  ✓ owner prints some STBL (138ms)
  ✓ Alice prints some STBL (119ms)
  ✓ TotalSupply of STBL should be 200 (42ms)
  ✓ Alice sends owner's STBL to Bob (497ms)

Contract: GiftCertificate
  ✓ print some STBL fior participants (224ms)
  ✓ Owner funds GFT with STBL (206ms)
  ✓ Alice buys some GFT (367ms)
  ✓ Alice spends GFT with Bob (296ms)
  ✓ Bob redeems GFT (349ms)
  ✓ Pause contract and redeem (866ms)


11 passing (4s)

truffle(development)>

```
Note: the Warnings are native to the OpenZeppelin libraries used.

## front end interface (development server)
Run ganache-cli:
```bash
ganache-cli
```
and import the BIP39 mnemonic in MetaMask.

The provided front end is a React application.
In a new terminal run
```bash
cd client
npm start
```

TODO run through the use case.

Note: When you send an ERC721 token with MetaMask, it shows as if it sending X ammount of ERC721 tokens where X is the unique ID of the ERC721 token. (see [issue 5145](https://github.com/MetaMask/metamask-extension/issues/5145) on MetaMask's github)
