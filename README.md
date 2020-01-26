# nanowallets-json

![Last updated](https://img.shields.io/github/last-commit/nanowallets-guide/nanowallets-json/master?label=last%20updated)
![Contributors](https://img.shields.io/github/contributors/nanowallets-guide/nanowallets-json)

A json feature-list for wallets that support Nano, were the user have access to keys (*Not your keys, not your Nano*). Currently used by [nanowallets.guide](https://nanowallets.guide) to dynamically render a comparison view for all features between all wallets.

## Features

These are the currently added features. Feature additions can easily be made through a normal pull-request (all wallets must include all features).

All features must be in camelCase. All boolean feature values can be null if support for that feature is unknown.

|**Feature name**|**Description**|**Type**|
|----------------|---------------|--------|
|**platforms**|Platforms this wallet supports.|Array(String)|
|**openSource**|If core parts (core as in handling of funds) of the wallet are open source.|Bool|
|**changeRepSupport**|Possibility to change representative through the wallets UI.|Bool|
|**multiAssetSupport**|Allows for handling of other cryptocurrencies than Nano.|Bool|
|**ledgerSupport**|Can be used with [Ledger](https://www.ledger.com/).|Bool|
|**ledgerRecovery**|Supports [Ledger](https://www.ledger.com/) recovery.|Bool|
|**contactBook**|Can store contacts (nano addresses) within the wallet|Bool|
|**multiAccount**|Supports multiple accounts (indexes)|Bool|
|**watchOnlyAddress**|???|Bool|
|**seedImport**|Types of Seed import the wallet supports, examples being a "Nano seed", 64 character (entropy) for more on the different seed types see [Seed types](#seed-types-and-private-keys-within-the-context-of-nano)|Array(String)|
|**seedExport**|Same as import but types of Seeds you can export through the wallet.|Array(String)|
|**mnemonicImport**|Types of Mnemonic phrase types the wallets supports.|Array(String)|
|**mnemonicExport**|Same as import but types of Mnemonic phrases you can export through the wallet.|Array(String)|
|**privateKeyImport**|Can import private keys.|Bool|
|**privateKeyExport**|Can export private keys.|Bool|
|**privateKeyDerivation**|Types of derivation used for private keys|Array(String)|
|**keyStorage**|Where/how keys are stored|Array(String)|
|**hostsTheirOwnRep**|Does this wallet host their own representative.|Bool, String (*if they do value should be url to representative if applicable*)|
|**exchangeService**|Offers an exchange service.|Bool|
|**qrReader**|Can read QR codes.|Bool|
|**qrGenerator**|Can generate QR codes for transactions.|Bool|
|**authenticationMethods**|Authentication methods this wallet supports.|Array(String)|
|**moreInformation**|A url to where more information about the wallet can be found.|String|
|**other**|Any text/html with additional information about the wallet not applicable to a specific feature.|String|

## Example
```
{
    "name": "Natrium",
    "slug": "natrium",
    "logo": "https://nanowallets.guide/assets/wallet-logos/natrium.png",
    "features": {
        "platforms": ["android", "ios"],
        "openSource": true,
        "changeRepSupport": true,
        "multiAssetSupport": false,
        "ledgerSupport": false,
        "ledgerRecovery": false,
        "contactBook": true,
        "multiAccount": true,
        "watchOnlyAddress": false,
        "seedImport": ["Nano"],
        "seedExport": ["Nano"],
        "mnemonicImport": ["24-word"],
        "mnemonicExport": ["24-word"],
        "privateKeyImport": true,
        "privateKeyExport": false,
        "privateKeyDerivation": ["blake2b"],
        "keyStorage": ["local"],
        "hostsTheirOwnRep": "https://mynano.ninja/account/natrium",
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

### Nano seed
A Nano seed is 64 characters long and is what is called an [Entropy](https://en.wikipedia.org/wiki/Entropy_(computing)). Can be converted to a 24-word mnemonic phrase.

### Private keys
When a Nano seed is imported into a wallet that seed will be converted to a private key using blake2b derivation (only derivation applicable to a Nano seed). From that the Nano public key (aka account) is derived.
When a 24-word or 12-word phrase is imported that phrase will be converted to a private key using either blake2b or bip39/44 derivation.

### Bip32
A "real" seed that is 128 characters long and is equivalent with a Bip32 mnemonic.

### Mnemonic phrases
A 24-word mnemonic phrase can be converted to a Nano seed. A 12-word cannot.
