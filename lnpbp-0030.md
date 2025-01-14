```
LNPBP: 0030
Aliases: RGB30
Vertical: Smart contracts
Title: Interface for fungible RGB assets with decentralized issue (RGB-30)
Authors: Dr Maxim Orlovsky <orlovsky@lnp-bp.org>
Comments-URI: <https://github.com/LNP-BP/LNPBPs/discussions/140>
Status: Proposal
Type: Standards Track
Created: 2021-06-23
Updated: 2023-05-10
Finalized: ~
Copyright: (0) public domain
License: CC0-1.0
```

- [Abstract](#abstract)
- [Background](#background)
- [Motivation](#motivation)
- [Design](#design)
- [Specification](#specification)
- [Compatibility](#compatibility)
- [Rationale](#rationale)
- [Reference implementation](#reference-implementation)
- [Acknowledgements](#acknowledgements)
- [References](#references)
- [Copyright](#copyright)


## Abstract


## Background


## Motivation


## Design



## Specification

Interface specification is the following Contractum code:

```haskell
-- Defined by LNPBP-31 standard in `rgb.sty` file
import moment_shirt_uranium_E2hfuv3Za3kVo7MSCvSxC6uhYJEvkmZJ1NPz4g4oZWNw as RGBTypes

interface RGB30
    -- Asset specification containing ticker, name, precision etc.
    global spec :: RGBTypes.DivisibleAssetSpec

    -- Contract text and creation date is separated from the spec since it must
    -- not be changeable by the issuer.
    global terms :: RGBTypes.RicardianContract
    global created :: RGBTypes.Timestamp

    -- Ownership right over assets
    owned assetOwner* :: RGBTypes.Amount
    
    -- Point for applying state extensions
    valency issueRight

    genesis       -> spec, terms, issueRight

    op Transfer    :: previous assetOwner+ 
                   -> beneficiary assetOwner+
                   !! nonEqualAmounts

    op PegIn       :: issueRight
                    , reserves RGBTypes.PoR
                   -> beneficiary assetOwner+, issuedSupply
                   !! supplyMismatch 
                    | insufficientReserves 
                    | invalidProof(RGBTypes.PoR)
```

## Compatibility


## Rationale

Include from
- <https://github.com/LNP-BP/LNPBPs/issues/27>
- <https://github.com/LNP-BP/LNPBPs/issues/28>
- <https://github.com/LNP-BP/LNPBPs/issues/50>

## Reference implementation

<https://github.com/RGB-WG/rgb-wallet/blob/master/std/src/interface/rgb20.rs>

## Acknowledgements


## References


## Copyright

This document is licensed under the Creative Commons CC0 1.0 Universal license.

<p xmlns:dct="http://purl.org/dc/terms/">
  <a rel="license"
     href="http://creativecommons.org/publicdomain/zero/1.0/">
    <img src="http://i.creativecommons.org/p/zero/1.0/88x31.png" style="border-style:none;" alt="CC0" />
  </a>
  <br />
  To the extent possible under law,
  <a rel="dct:publisher" href="https://lnp-bp.org">
    <span property="dcl:title">LNP/BP Standards Association</span></a>
  has waived all copyright and related or neighboring rights to this work.
</p>
