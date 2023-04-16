
# Dogechain Taxable Token Template
A Taxable ERC20 Template, with a Timelock contract &amp; modifier to alert users in advance of high-security functions ala changing pair/router/taxes etc.

Built for use with QuickSwap's V2 Protocol on Dogechain - but should work fine on any V2/Standard Balancer DEX.

QuickSwap's V2 Protocol on Dogechain appears to have some issues in working with contracts that auto-create their pair during construction, but do not supply LP within the same TX. This contract averts that by allowing for a pair to be configured post-launch, once LP is available.

## Setup
- Load the contract in to Remix at http://remix.ethereum.org. Ensure compiler is set to 0.8.16+.

- Deploy your contract with your chosen primary router, and your marketing/dev address. For QuickSwap V2 on Dogechain, input your router address as `0xAF96E63f965374dB6514e8CF595fB0a3f4d7763c`

- Once deployed, create your LP with a mix of your own tokens and wDoge/wwDoge at QuickSwap, or your DEX of choice.

- Once your LP is created, grab your pair address. You can find this via your last transaction on Blockscout - navigate to the UNI-V2 Token link that's present in the transaction which you used to create your LP. You should see your pool, containing your own token and the wDoge/wwDoge supplied for the LP mix. Copy the contract address from here.

- In remix, input your pair address into the `setInitialPair` function, and click "transact", or the named function button.

- Once the transaction has confirmed, input your pair address into the `addToTaxed` function, and click "transact", or the named function button.

Your token is now tradeable, and has taxes/auto-lp enabled. Please ensure that you adhere to any local or national laws in respect to token launching/trading within your respective jurisdiction before launching any liquid token pairs.

## Timelock
All high-security functions are equipped with a TimeLock modifier. To access any of these functions, you will need to input the relevant function name into the `unlockFunction` method. Note that these functions are limited to being executed by the owner of the contract - and cannot be called on a renounced contract.

An event will emit notifying any blockchain users that you intend to use the given function. 24 hours after this event emission, your requested function will unlock for one use. Following use of this function, it will automatically re-lock and require you to call the `unlockFunction` method again.

Note that you can request to unlock multiple functions at any given time, and that they will remain unlocked until executed against.

## Additional Taxable Addresses
Any address added via the `addToTaxed` function will always have Tax and Auto-LP applied, whether the address is sending or receiving any tokens. Addresses can be removed from this with the `removeFromTaxed` function.

Addresses added via the `addToExempt` function will never have any Tax or Auto-LP applied to transactions being sent, or received. This over-rides any rules set under `addToTaxed`. Addresses can be removed from the exempt list via the `removeFromExempt` function.

## The Legal Bits
Note that while we have tested all functionality under this contract, we are not acting auditors or otherwise; and can provide absolutely no guarantees to the overall safety of this contract, or any derivatives of it.

Our Token Template is provided as-is, and Dogira Studios nor any of it's staff or related personnel may be held responsible for any issues which may arise from using this contract, including but not limited to the case of total loss of assets/funds, damage to any computer software or hardware, or otherwise.

 The legality of launching tokens varies across jurisdictions, and it is entirely at the behest of the user to examine and determine if they are fully complying with any laws or financial regulations imposed on them. Dogira Studios and all related staff/personnel cannot offer any legal or financial advice when deploying, or otherwise interacting with any contracts made available through us, or any other avenues.

We strongly recommend rigorously testing any contracts prior to deployment, and speaking with a financial or legal advisor in regards to any local laws, licensing, regulation, penalties, or otherwise.

Note that we maintain zero responsibility for any other contracts deployed using our source code - and would strongly urge any individuals interacting with any smart contract to be aware of any possible dangers, such as a project deployer removing available liquidity, or failing to meet any promised functionality/utility deadlines or otherwise.

In short: You can do whatever you want with this code. It's on you to make sure you do so within legal and ethical boundaries, and you as either the contract deployer/maintainer etc or an unrelated user will bear total responsibility if anything goes wrong.

## Dogira
We develop on-chain tools, and specialize in GameFi. Find us and our products at https://dogira.net / [@DogiraOfficial](https://twitter.com/DogiraOfficial)
