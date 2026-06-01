# Crypto

Pure-Rux cryptographic primitives — no external dependencies, no platform-specific code.

## Primitives

| Primitive | Standard | Source |
|-----------|----------|--------|
| SHA-1 | FIPS 180-4 | `Sha1.rux` |
| SHA-256 | FIPS 180-4 | `Sha256.rux` |
| SHA-512 | FIPS 180-4 | `Sha512.rux` |
| SHA-3-256 / SHA-3-512 | FIPS 202 | `Sha3.rux` |
| HMAC-SHA1 / HMAC-SHA256 / HMAC-SHA512 | RFC 2104 | `Hmac.rux` |
| PBKDF2-HMAC-SHA256 | RFC 2898 | `Hmac.rux` |
| AES-128 / AES-256 (ECB, CBC) | FIPS 197 | `Aes.rux` |
| ChaCha20 | RFC 8439 | `ChaCha20.rux` |
| Poly1305 | RFC 8439 | `Poly1305.rux` |
| Hex encode/decode | — | `Encoding.rux` |
| Base64 encode/decode | — | `Encoding.rux` |

## Usage

```rux
import Crypto::{ Sha256Hash, HmacSha256, AesInitEncrypt, AesCbcEncrypt };
```

One-shot hash:

```rux
var digest: uint8[32];
Sha256Hash("abc" as *const uint8, 3u, &digest[0]);
```

HMAC:

```rux
var out: uint8[32];
HmacSha256(&key[0], 20u, "Hi There" as *const uint8, 8u, &out[0]);
```

AES-CBC:

```rux
var ctx: AesContext;
AesInitEncrypt(&ctx, &key[0], 128u32);
AesCbcEncrypt(&ctx, &iv[0], &pt[0], &ct[0], 16u32);
```

## Self-tests

Call `CryptoSelfTest()` at startup to verify correctness against known-answer vectors:

```rux
import Crypto::CryptoSelfTest;

if !CryptoSelfTest() {
    // abort — build is broken
}
```

## Package

```toml
[Package]
Name = "Crypto"
Version = "0.1.0"
Type = "Source"
```

## License

MIT — see LICENSE.
