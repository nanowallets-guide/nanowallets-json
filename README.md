<div align="center">
    <img src="https://nanowallets.guide/assets/logo-color.png" alt="Logo" width='200px' height='auto'/>
</div>

# nanowallets-json

![Last updated](https://img.shields.io/github/last-commit/nanowallets-guide/nanowallets-json/master?label=last%20updated)
![Contributors](https://img.shields.io/github/contributors/nanowallets-guide/nanowallets-json)

A json feature-list for wallets that support Nano, were the user have access to keys (*Not your keys, not your Nano*). Currently used by [nanowallets.guide](https://nanowallets.guide) to dynamically render a comparison view for all features between all wallets.

## Features

These are the currently added features. Feature additions can easily be made through a normal pull-request (all wallets must include all features). `featureComplete` is used to indicate if all feature data has been filled and completed.
All features must be in camelCase. All boolean feature values can be null if support for that feature is unknown.

|**Feature name**|**Description**|**Type**|
|----------------|---------------|--------|
|**platforms**|Platforms this wallet supports. For example Win, MacOS, Linux, iOS, Android.|Array(String)|
|**openSource**|If core parts (core as in handling of funds) of the wallet are open source. Link to repository.|String|
|**changeRepSupport**|Possibility to change representative through the wallets UI.|Bool|
|**multiAssetSupport**|Allows for handling of other cryptocurrencies than Nano.|Bool|
|**ledgerSupport**|Can be used with [Ledger](https://www.ledger.com/).|Bool|
|**ledgerRecovery**|Supports [Ledger](https://www.ledger.com/) recovery.|Bool|
|**contactBook**|Can store contacts (nano addresses) within the wallet|Bool|
|**transactionNote**|Custom transaction message for wallet owner.|Bool|
|**multiAccount**|Supports multiple accounts (indexes)|Bool|
|**watchOnlyAddress**|Can track the amount of any Nano address (public key). A watch-only address can not receive or send funds because there is no private key (or seed) involved.|Bool|
|**seedImport**|Types of Seed import the wallet supports, examples being a "nano seed", a 64 character entropy. For more on the different seed types see [Seed types](#seed-types-and-private-keys-within-the-context-of-nano)|Array(String)|
|**seedExport**|Same as import but types of Seeds you can export through the wallet.|Array(String)|
|**mnemonicImport**|Types of Mnemonic phrase the wallets supports. For example 12-word, 24-word.|Array(String)|
|**mnemonicExport**|Same as import but types of Mnemonic phrases you can export through the wallet.|Array(String)|
|**privateKeyImport**|Can import private keys. Also called an Ad-hoc wallet.|Bool|
|**privateKeyExport**|Can export private keys.|Bool|
|**privateKeyDerivation**|Types of derivation used for private keys. Find out more under [Private keys](#seed-types-and-private-keys-within-the-context-of-nano).|Array(String)|
|**walletSweep**|Can read a seed and/or a private key and automatically transfer the funds to it's own wallet.|Array(String)|
|**keyStorage**|Where/how keys are stored. For example none, local, remote.|Array(String)|
|**fileBackup**|Support backup whole wallet to a file and restore on another device.|Bool|
|**hostsTheirOwnRep**|Does this wallet host their own representative. Link to representative.|String|
|**exchangeService**|Offers an exchange service to sell and/or buy Nano for other currencies.|Bool|
|**qrReader**|Can read QR codes for sending Nano.|Bool|
|**qrGenerator**|Can generate/display QR codes to aid transactions.|Bool|
|**authenticationMethods**|Authentication methods this wallet supports. password, pin, biometrics, 2fa|Array(String)|
|**moreInformation**|A url to where more information about the wallet can be found.|String|
|**other**|Any text/html with additional information about the wallet not applicable to a specific feature.|String|

## Example
```
{
    "name": "Natrium",
    "slug": "natrium",
    "logo": "https://nanowallets.guide/assets/wallet-logos/natrium.png",
    "featureComplete": true,
    "features": {
        "platforms": ["android", "ios"],
        "openSource": "https://github.com/appditto/natrium_wallet_flutter",
        "changeRepSupport": true,
        "multiAssetSupport": false,
        "ledgerSupport": false,
        "ledgerRecovery": false,
        "contactBook": true,
        "transactionNote": false,
        "multiAccount": true,
        "watchOnlyAddress": false,
        "seedImport": ["nano", "bip32"],
        "seedExport": ["nano", "bip32"],
        "mnemonicImport": ["12-word", "24-word"],
        "mnemonicExport": ["12-word", "24-word"],
        "privateKeyImport": true,
        "privateKeyExport": true,
        "privateKeyDerivation": ["blake2b", "bip39/44"],
        "walletSweep": ["nano seed","privKey"],
        "keyStorage": ["local"],
        "fileBackup": false,
        "hostsTheirOwnRep": "https://nanocharts.info/address/nano_1natrium1o3z5519ifou7xii8crpxpk8y65qmkih8e8bpsjri651oza8imdd",
        "exchangeService": false,
        "qrReader": true,
        "qrGenerator": true,
        "authenticationMethods": ["password", "pin", "biometrics"],
        "moreInformation": "https://natrium.io/",
        "other": "iWatch, Appia support, supported by the Nano Foundation.<br><a href=\"https://medium.com/appditto/natrium-v2-1-security-audit-and-more-26ebec66bd5b\" target=\"_blank\">Natrium audited by Red4Sec</a>."
    }
}
```

## Seed types and private keys within the context of Nano

### Seed types
* A **Nano seed** is a 64 long hexadecimal string and is what is called an [Entropy](https://en.wikipedia.org/wiki/Entropy_(computing)). Can be converted to a 24-word mnemonic phrase, for example, by using [bip39.entropyToMnemonic()](https://www.npmjs.com/package/bip39).
* A **Bip32 seed** is a 128 long hexadecimal string and can also be converted to a 24-word phrase that is called a Bip32 mnemonic, for example by using [nanocurrency-web-js](https://github.com/numsu/nanocurrency-web-js)

### Private keys and derivation types
* When a Nano seed, a Bip32 seed or mnemonic is imported into a wallet that seed will be converted to one or more private keys using either **blake2b** or **bip39/44** derivation. From that the Nano public key (aka account/address) is derived.
* For example, a Ledger hardware wallet and most multi-currency wallets are using bip39/44 while blake2b is the recommended method for native Nano wallets. However, there is nothing stopping wallets from supporting both.

### Public keys
* A public key is a 64 long hexadecimal string and is equivalent to a Nano account/address.

### Mnemonic phrases
* A **24-word** mnemonic phrase can be converted to a Nano seed (entropy) or a Bip32 seed. A **12-word** mnemonic is used in some wallets but has a lower entropy and not recommended. A Ledger hardware wallet is using a 24-word recovery phrase by default.

To test all this in practice you can jump over to [KeyTools Key Converter](https://tools.nanos.cc/?tool=seed). That can be used to verify different wallets and to determine what derivation method they use. When using real keys, it's recommended to download the tool and run offline. Download link and info can be found at the tool´s home page.
