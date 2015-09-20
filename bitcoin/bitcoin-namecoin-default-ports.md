---
layout: default
title: Bitcoin, Namecoin default ports
---

[bitcoin](.)

# {{ page.title }}

This is a basic table with default Bitcoin and Namecoin port numbers.

<table>
    <tr>
        <td></td>
        <td></td>
        <td>connect</td>
        <td>rpc</td>
    </tr>
    <tr>
        <td>bitcoin</td>
        <td>mainnet</td>
        <td>8333</td>
        <td>8332</td>
    </tr>
    <tr>
        <td>bitcoin</td>
        <td>testnet</td>
        <td>18333</td>
        <td>18332</td>
    </tr>
    <tr>
        <td>bitcoin</td>
        <td>regtest</td>
        <td>18444</td>
        <td>18332</td>
    </tr>
    <tr>
        <td>namecoin</td>
        <td>mainnet</td>
        <td>8334</td>
        <td>8336</td>
    </tr>
    <tr>
        <td>namecoin</td>
        <td>testnet</td>
        <td>18334</td>
        <td>18336</td>
    </tr>
    <tr>
        <td>namecoin</td>
        <td>regtest</td>
        <td>18444</td>
        <td>18336</td>
    </tr>
</table>

I proposed change default namecoin regtest connect port (for easy run bitcoin and namecoin regtest on same machine) to 18445 or 18555. I opened an issue on Github: <https://github.com/namecoin/namecore/issues/4>

