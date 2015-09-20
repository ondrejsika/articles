---
layout: default
title: Trezor mnemonic to xprv
---

[bitcoin](.)

# {{ page.title }}

I had a problem, i have a backup seed ([BIP 39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki)) from Trezor and I want generate a private keys for address.

I used two python utils [python-mnemotic](https://github.com/trezor/python-mnemonic) and [pycoin](https://github.com/richardkiss/pycoin).

This is a simple example of generation xprv, xpub, wallet private key and address.

    from pycoin.key.BIP32Node import BIP32Node
    from mnemonic import Mnemonic

    words = 'abandon ability able about above absent absorb abstract absurd abuse access accident account accuse achieve acid acoustic acquire across act action actor actress actual'

    node = BIP32Node.from_master_secret(Mnemonic.to_seed(words), 'BTC')
    print 'xprv', node.wallet_key(True)
    print 'xpub', node.wallet_key()

    print 'trezor address'
    for i in range(10):
        subnode = node.subkey_for_path("44'/0'/0'/0/%d" % i)
        print subnode.wif(), subnode.address()


