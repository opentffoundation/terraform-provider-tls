---

<!-- Please do not edit this file, it is generated. -->
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "tls_public_key Data Source - terraform-provider-tls"
subcategory: ""
description: |-
  Get a public key from a PEM-encoded private key.
  Use this data source to get the public key from a PEM (RFC 1421) https://datatracker.ietf.org/doc/html/rfc1421 or OpenSSH PEM (RFC 4716) https://datatracker.ietf.org/doc/html/rfc4716 formatted private key, for use in other resources.
---

# tls_public_key (Data Source)

Get a public key from a PEM-encoded private key.

Use this data source to get the public key from a [PEM (RFC 1421)](https://datatracker.ietf.org/doc/html/rfc1421) or [OpenSSH PEM (RFC 4716)](https://datatracker.ietf.org/doc/html/rfc4716) formatted private key, for use in other resources.

## Example Usage

```typescript
// Code generated by 'cdktf convert' - Please report bugs at https://cdk.tf/bug
import { Construct } from "constructs";
import { Fn, Token, TerraformStack } from "cdktf";
/*
 * Provider bindings are generated by running `cdktf get`.
 * See https://cdk.tf/provider-generation for more details.
 */
import { DataTlsPublicKey } from "./.gen/providers/tls/data-tls-public-key";
import { PrivateKey } from "./.gen/providers/tls/private-key";
class MyConvertedCode extends TerraformStack {
  constructor(scope: Construct, name: string) {
    super(scope, name);
    const ed25519Example = new PrivateKey(this, "ed25519-example", {
      algorithm: "ED25519",
    });
    new DataTlsPublicKey(this, "private_key_openssh-example", {
      privateKeyOpenssh: Token.asString(Fn.file("~/.ssh/id_rsa_rfc4716")),
    });
    new DataTlsPublicKey(this, "private_key_pem-example", {
      privateKeyPem: ed25519Example.privateKeyPem,
    });
  }
}

```

<!-- schema generated by tfplugindocs -->
## Schema

### Optional

- `privateKeyOpenssh` (String, Sensitive) The private key (in  [OpenSSH PEM (RFC 4716)](https://datatracker.ietf.org/doc/html/rfc4716) format) to extract the public key from. This is _mutually exclusive_ with `privateKeyPem`. Currently-supported algorithms for keys are: `rsa`, `ecdsa`, `ed25519`.
- `privateKeyPem` (String, Sensitive) The private key (in [PEM (RFC 1421)](https://datatracker.ietf.org/doc/html/rfc1421) format) to extract the public key from. This is _mutually exclusive_ with `privateKeyOpenssh`. Currently-supported algorithms for keys are: `rsa`, `ecdsa`, `ed25519`.

### Read-Only

- `algorithm` (String) The name of the algorithm used by the given private key. Possible values are: `rsa`, `ecdsa`, `ed25519`.
- `id` (String) Unique identifier for this data source: hexadecimal representation of the SHA1 checksum of the data source.
- `publicKeyFingerprintMd5` (String) The fingerprint of the public key data in OpenSSH MD5 hash format, e.g. `aa:bb:cc:`. Only available if the selected private key format is compatible, as per the rules for `publicKeyOpenssh` and [ECDSA P224 limitations](../../docs#limitations).
- `publicKeyFingerprintSha256` (String) The fingerprint of the public key data in OpenSSH SHA256 hash format, e.g. `sha256:`. Only available if the selected private key format is compatible, as per the rules for `publicKeyOpenssh` and [ECDSA P224 limitations](../../docs#limitations).
- `publicKeyOpenssh` (String) The public key, in  [OpenSSH PEM (RFC 4716)](https://datatracker.ietf.org/doc/html/rfc4716) format. This is also known as ['Authorized Keys'](https://www.ssh.com/academy/ssh/authorized_keys/openssh#format-of-the-authorized-keys-file) format. This is not populated for `ecdsa` with curve `p224`, as it is [not supported](../../docs#limitations). **NOTE**: the [underlying](https://pkg.go.dev/encoding/pem#Encode) [libraries](https://pkg.go.dev/golang.org/x/crypto/ssh#MarshalAuthorizedKey) that generate this value append a `\n` at the end of the PEM. In case this disrupts your use case, we recommend using [`trimspace()`](https://www.terraform.io/language/functions/trimspace).
- `publicKeyPem` (String) The public key, in [PEM (RFC 1421)](https://datatracker.ietf.org/doc/html/rfc1421) format. **NOTE**: the [underlying](https://pkg.go.dev/encoding/pem#Encode) [libraries](https://pkg.go.dev/golang.org/x/crypto/ssh#MarshalAuthorizedKey) that generate this value append a `\n` at the end of the PEM. In case this disrupts your use case, we recommend using [`trimspace()`](https://www.terraform.io/language/functions/trimspace).

<!-- cache-key: cdktf-0.17.1 input-025d5bde39901a91ba6cb60272c97a78a0c01a6de59d77d7dea035490ff6ee0a -->