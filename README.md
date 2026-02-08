# FundMe Smart Contract

A decentralized crowdfunding smart contract built with Foundry that allows users to send ETH donations to the contract owner. The contract enforces a minimum donation threshold in USD using Chainlink price feeds and maintains a record of all contributors.

## Overview

FundMe is a Solidity smart contract that demonstrates:
- ETH donation acceptance with USD-based minimum requirements
- Real-time price conversion using Chainlink oracles
- Contributor tracking for potential future rewards
- Secure fund withdrawal by the contract owner

## Features

- **USD-Denominated Donations**: All donations are valued in USD, regardless of ETH price fluctuations
- **Minimum Threshold**: Enforces a minimum donation amount to prevent spam transactions
- **Chainlink Price Feeds**: Uses decentralized oracles for accurate ETH/USD pricing
- **Donor Registry**: Maintains a list of all contributors and their donation amounts
- **Owner-Only Withdrawals**: Only the contract owner can withdraw accumulated funds
- **Gas Optimized**: Built with Foundry for optimal gas efficiency

## Tech Stack

- **Solidity**: Smart contract language
- **Foundry**: Development framework and toolkit
- **Chainlink**: Decentralized price feed oracles

## Prerequisites

- [Git](https://git-scm.com/)
- [Foundry](https://book.getfoundry.sh/getting-started/installation)

## Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd foundry-FundMe
```

2. Install dependencies:
```bash
forge install
```

3. Build the project:
```bash
forge build
```

## Usage

### Compile Contracts

```bash
forge build
```

### Run Tests

```bash
forge test
```

Run tests with verbosity:
```bash
forge test -vv
```

Run tests with gas reporting:
```bash
forge test --gas-report
```

### Deploy

Deploy to a local Anvil chain:
```bash
anvil
forge script script/DeployFundMe.s.sol --rpc-url http://localhost:8545 --broadcast
```

Deploy to a testnet (e.g., Sepolia):
```bash
forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast --verify
```

### Interact with the Contract

Fund the contract:
```bash
cast send <CONTRACT_ADDRESS> "fund()" --value 0.1ether --private-key $PRIVATE_KEY --rpc-url $RPC_URL
```

Withdraw funds (owner only):
```bash
cast send <CONTRACT_ADDRESS> "withdraw()" --private-key $PRIVATE_KEY --rpc-url $RPC_URL
```

Check contract balance:
```bash
cast balance <CONTRACT_ADDRESS> --rpc-url $RPC_URL
```

## Project Structure

```
foundry-fundme/
├── src/
│   ├── FundMe.sol          # Main contract
│   └── PriceConverter.sol  # Chainlink price feed library (if applicable)
├── script/
│   └── DeployFundMe.s.sol  # Deployment script
|   └── HelperConfig.s.sol  # Helper script
|   └── Interactions.s.sol  # Interaction script
├── test/
│   ├── uint
|       └── FundMeTest.t.sol        # Unit tests
│   └── Integration                 # Integration tests
|       └── InteractionTest.t.sol
|   └── mocks
|       └── MockV3Aggregator.t.sol  # mock test
├── foundry.toml            # Foundry configuration
└── README.md
```

## Contract Functions

### Public Functions

- `fund()`: Send ETH to the contract (must meet minimum USD threshold)
- `withdraw()`: Withdraw all funds (owner only)
- `getAddressToAmountFunded(address)`: Get donation amount for a specific address
- `getFunder(uint256)`: Get funder address by index

### View Functions

- `getOwner()`: Returns the contract owner address
- `getVersion()`: Returns Chainlink price feed version
- `getConversionRate(uint256)`: Convert ETH amount to USD

## Testing

The project includes comprehensive tests covering:
- Basic funding functionality
- Minimum USD threshold enforcement
- Owner-only withdrawal restrictions
- Price feed integration
- Edge cases and security scenarios

Run specific test files:
```bash
forge test --match-path test/FundMe.t.sol
```

## Configuration

Create a `.env` file in the root directory:

```env
SEPOLIA_RPC_URL=your_sepolia_rpc_url
PRIVATE_KEY=your_private_key
ETHERSCAN_API_KEY=your_etherscan_api_key
```

**⚠️ Never commit your `.env` file to version control!**

## Security Considerations

- ✅ Employs Chainlink price feeds for reliable price data
- ✅ Implements checks-effects-interactions pattern
- ✅ Prevents reentrancy attacks
- ⚠️ Ensure proper access control on withdrawal function
- ⚠️ Always test thoroughly before mainnet deployment

## Gas Optimization

This project implements several gas optimization techniques:
- Use of `immutable` for deployment-set variables
- Efficient storage patterns
- Optimized loops and data structures

## Roadmap

- [ ] Add withdrawal to specific addresses
- [ ] Implement reward mechanism for donors
- [ ] Add time-based funding campaigns
- [ ] Create frontend interface
- [ ] Multi-signature withdrawal support

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Foundry Book](https://book.getfoundry.sh/)
- [Chainlink Documentation](https://docs.chain.link/)
- [Cyfrin Updraft](https://updraft.cyfrin.io/) - Smart contract development course

## Resources

- [Foundry Documentation](https://book.getfoundry.sh/)
- [Solidity Documentation](https://docs.soliditylang.org/)
- [Chainlink Price Feeds](https://docs.chain.link/data-feeds/price-feeds)



---

**Built with ❤️ using Foundry**
