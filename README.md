chaincfg
========

Package chaincfg defines chain configuration parameters for the three standard
Einsteinium networks and provides the ability for callers to define their own custom
Einsteinium networks.

Although this package was primarily written for ltcd, it has intentionally been
designed so it can be used as a standalone package for any projects needing to
use parameters for the standard Einsteinium networks or for projects needing to
define their own network.

## Sample Use

```Go
package main

import (
	"flag"
	"fmt"
	"log"

	"github.com/ltcsuite/ltcutil"
	"github.com/emc2foundation/emc2d-chainconfig"
)

var testnet = flag.Bool("testnet", false, "operate on the testnet Einsteinium network")

// By default (without -testnet), use mainnet.
var chainParams = &chaincfg.MainNetParams

func main() {
	flag.Parse()

	// Modify active network parameters if operating on testnet.
	if *testnet {
		chainParams = &chaincfg.TestNet4Params
	}

	// later...

	// Create and print new payment address, specific to the active network.
	pubKeyHash := make([]byte, 20)
	addr, err := ltcutil.NewAddressPubKeyHash(pubKeyHash, chainParams)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(addr)
}
```

## Installation and Updating

```bash
$ go get -u github.com/emc2foundation/emc2d-chainconfig
```

## GPG Verification Key

All official release tags are signed by Conformal so users can ensure the code
has not been tampered with and is coming from the btcsuite developers.  To
verify the signature perform the following:

- Download the public key from the Conformal website at
  https://opensource.conformal.com/GIT-GPG-KEY-conformal.txt

- Import the public key into your GPG keyring:
  ```bash
  gpg --import GIT-GPG-KEY-conformal.txt
  ```

- Verify the release tag with the following command where `TAG_NAME` is a
  placeholder for the specific tag:
  ```bash
  git tag -v TAG_NAME
  ```

## License

Package chaincfg is licensed under the [copyfree](http://copyfree.org) ISC
License.
