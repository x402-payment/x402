# @facilitator/contracts

EIP-7702 Delegate contract for [x402](https://github.com/x402-payment/x402) gasless payment intents.

## Install

### Foundry

```
forge install melonask/facilitator
```

Add to your `remappings.txt`:

```
@facilitator/=lib/facilitator/packages/
```

Or add to your `foundry.toml`:

```
remappings=[
    "@facilitator/=lib/facilitator/packages/"
]
```

## Usage

```solidity
import {Delegate} from "@facilitator/contracts/src/Delegate.sol";
```

## Overview

`Delegate` is an [EIP-7702](https://eips.ethereum.org/EIPS/eip-7702) delegate contract that enables gasless ERC-20 and ETH transfers via signed payment intents. A relayer submits the EIP-712 signed intent on behalf of the user.

### Structs

- **`PaymentIntent`** — ERC-20 transfer: `token`, `amount`, `to`, `nonce`, `deadline`
- **`EthPaymentIntent`** — Native ETH transfer: `amount`, `to`, `nonce`, `deadline`

### Functions

| Function                         | Description                                |
| -------------------------------- | ------------------------------------------ |
| `transfer(intent, signature)`    | Execute a signed ERC-20 payment intent     |
| `transferEth(intent, signature)` | Execute a signed native ETH payment intent |
| `invalidateNonce(nonce)`         | Cancel a pending intent (owner only)       |

### Security

- Each nonce can only be used once (replay protection)
- Intents expire after `deadline` (timestamp)
- Only the delegated account (`address(this)`) can sign valid intents
- Uses OpenZeppelin's `ECDSA`, `EIP712`, and `SafeERC20`

## Development

```bash
forge build
forge test -vv
```

## License

MIT
