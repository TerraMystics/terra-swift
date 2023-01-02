<br/>
<p align="center">
    <a href="https://github.com/TheArchitect123"><img src="./swift.png" align="center" width=450/></a>
</p>

<p align="center">
The Official Swift SDK for the Terra Ecosystem (LUNC/USTC/LUNA2)
</p>
<br/>

<p align="center">
  <a href="https://github.com/TerraMystics/terra-Swift">
  <img alt="GitHub" src="https://img.shields.io/github/license/terra-money/terra.js">
  </a>

  <a href="https://github.com/TerraMystics/terra-Swift">
  <img alt="GitHub" src="https://img.shields.io/pub/v/terra_dart">
  </a>
  
  
  <a href="https://github.com/TerraMystics/terra-Swift">
  <img alt="GitHub" src="https://img.shields.io/pub/likes/terra_dart?color=red">
  </a>
</p>

<p align="center">
  <a href="https://docs.terra.money/"><strong>Explore the Docs »</strong></a>
  <br />
  <br/>
  <a href="https://github.com/TerraMystics/terra-Swift">Example App</a>
  ·
  <a href="https://github.com/TerraMystics/terra-Swift">API Reference</a>
  ·
  <a href="https://github.com/TerraMystics/terra-Swift">Pub Package</a>
  ·
  <a href="https://github.com/TerraMystics/terra-Swift">GitHub</a>
</p>

TerraSwift is a Swift SDK for writing applications that interact with the Terra blockchain from either Android and/or Swift/Java Environments and provides simple abstractions over core data structures, serialization, key management, and API request generation.

## Features

- **Written in Dart**, with type definitions
- Versatile support for [key management](https://docs.terra.money/develop/feather-js/keys) solutions
- Works iOS & OS X Native Ecosystem
- Exposes the Terra API through [`LCDClient`](https://docs.terra.money/develop/terra-py/client/lcd/lcdclient)
- Parses responses into native Swift types

We highly suggest using TerraSwift in a code editor that has support for type declarations, so you can take advantage of the helpful type hints that are included with the package.

## Installation & Configuration

Grab the latest version off [pub.dev]()

```sh
terra_dart: latest
```

Inside your Startup Class (Where you initialize your application), please call the following method, and configure your environment
```dart
// Here we're targeting the Classic Blockchain
TerraStartup.initializeKernel(TerraEnvironment.classic);
```
That's it! Now you're ready to start communicating with the blockchain! 

## Usage

TerraSwift can be used for Mobile & Web Developers. Supports all Flutter & Dart Environments.

### Getting Blockchain data
:exclamation: TerraSwift can connect to both the terra-classic (LUNC/USTC) and LUNA2 networks. If you want to communicate with the classic chain, you have to set your Enviornment on **TerraStartup.InitializeKernel** to **TerraEnvironment.Classic**.

Below we're going to pull balance information on a sample wallet.
```dart
void fetchBalanceInformation() async {
    
    //fetch the LCDClient from the Kernel
    var lcd = TerraStartup.getLCDClient();
    
    // get the current balance of "terra1x46rqay4d3cssq8gxxvqz8xt6nwlz4td20k38v"
    var balance = await lcd.bank.getBalance("terra1x46rqay4d3cssq8gxxvqz8xt6nwlz4td20k38v");
    print(balance);
}
```

### Broadcasting transactions

First, [get](https://faucet.terra.money/) some testnet tokens for "terra1x46rqay4d3cssq8gxxvqz8xt6nwlz4td20k38v", or use [LocalTerra](https://github.com/terra-rebels/LocalTerra).

```dart
void broadcastTransaction() async {
    
    //fetch the LCDClient from the Kernel
    var lcd = TerraStartup.getLCDClient();
    
    // create a key out of a mnemonic
    var mk = MnemonicKey("notice oak worry limit wrap speak medal online prefer cluster roof addict wrist behave treat actual wasp year salad speed social layer crew genius");

    // create a simple message that moves coin balances
    var send = MsgSend(
      "terra1x46rqay4d3cssq8gxxvqz8xt6nwlz4td20k38v",
      "terra17lmam6zguazs5q5u6z5mmx76uj63gldnse2pdp",
      new List<Core.Coin>() { new Core.Coin(CoinDenoms.ULUNA, 20) }
    );

    // Prepare & Configure your wallet
    var wallet = lcd.createWallet(PreconfiguredWallets.TEST_NET_WALLET, mk);
     
    // Prepare Transaction for Upload
    var tx = await wallet.createTxAndSignTx([send])

    // Broadcast the transaction
    var broadcast = await wallet.broadcastTx.broadcast(tx);     
    print("Uploaded Tx Hash ${broadcast.txhash}");
}
```

## Require Payment Integration for LUNC/USTC?

If you need to integrate with an external payment system or gateway like Apple/Google in app purchases, please make sure to install the [following library](https://github.com/terra-rebels/terra-dart-payments) in your project.

## License

This software is licensed under the MIT license. See [LICENSE](./LICENSE) for full disclosure.

© 2022 TerraMystics.
