# 02 Feb 2019

## JWT

JSON Web Token (JWT) is a compact, URL-safe means of representing [`claims`](#claim-set) to be transferred between two parties.

The claims in a JWT are `encoded` as a 
- `JSON object` that is used as the payload of a `JSON Web Signature (JWS)` structure or
- as the `plaintext` of a `JSON Web Encryption (JWE)` structure

Enabling the claims to be digitally signed.

* [JWT structure](#jwt-structure)
    * [JOSE Header](#jose)
    * [Claim Set](#claim-set)
    * [Signature](#signature)
* [Signed JWT : JWS and JWE](#jws-and-jwe)
* [Unsecured JWT](#unsecured-jwt)
* [Other Links](#other-links)

### JWT structure

![validation structure](https://raw.githubusercontent.com/harryosmar/what-do-i-learn-today/master/02-02-2019/images/jwt-debug.jpg)

Sample `encoded` `JSON Object` of JWT from Google OpenID

```
eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc4YjRjZjIzNjU2ZGMzOTUzNjRmMWI2YzAyOTA3NjkxZjJjZGZmZTEifQ.eyJpc3MiOiJhY2NvdW50cy5nb29nbGUuY29tIiwic3ViIjoiMTEwNTAyMjUxMTU4OTIwMTQ3NzMyIiwiYXpwIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiZW1haWwiOiJwcmFiYXRoQHdzbzIuY29tIiwiYXRfaGFzaCI6InpmODZ2TnVsc0xCOGdGYXFSd2R6WWciLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiYXVkIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiaGQiOiJ3c28yLmNvbSIsImlhdCI6MTQwMTkwODI3MSwiZXhwIjoxNDAxOTEyMTcxfQ.TVKv-pdyvk2gW8sGsCbsnkqsrS0T-H00xnY6ETkIfgIxfotvFn5IwKm3xyBMpy0FFe0Rb5Ht8AEJV6PdWyxz8rMgX2HROWqSo_RfEfUpBb4iOsq4W28KftW5H0IA44VmNZ6zU4YTqPSt4TPhyFC9fP2D_Hg7JQozpQRUfbWTJI
```

Break/split the content above by `periods` (`.`).

- The 1st content will be [`JOSE Header`](#jose)
```
eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc4YjRjZjIzNjU2ZGMzOTUzNjRmMWI2YzAyOTA3NjkxZjJjZGZmZTEifQ
```

- The 2nd content will be [`Claim Set`](#claim-set)
```
eyJpc3MiOiJhY2NvdW50cy5nb29nbGUuY29tIiwic3ViIjoiMTEwNTAyMjUxMTU4OTIwMTQ3NzMyIiwiYXpwIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiZW1haWwiOiJwcmFiYXRoQHdzbzIuY29tIiwiYXRfaGFzaCI6InpmODZ2TnVsc0xCOGdGYXFSd2R6WWciLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiYXVkIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiaGQiOiJ3c28yLmNvbSIsImlhdCI6MTQwMTkwODI3MSwiZXhwIjoxNDAxOTEyMTcxfQ
```

- the 3rd content, will be the [`Signature`](#signature).
```
TVKv-pdyvk2gW8sGsCbsnkqsrS0T-H00xnY6ETkIfgIxfotvFn5IwKm3xyBMpy0FFe0Rb5Ht8AEJV6PdWyxz8rMgX2HROWqSo_RfEfUpBb4iOsq4W28KftW5H0IA44VmNZ6zU4YTqPSt4TPhyFC9fP2D_Hg7JQozpQRUfbWTJI
```

For more detail open this [jwt debugger](https://jwt.io/#debugger-io?token=eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc4YjRjZjIzNjU2ZGMzOTUzNjRmMWI2YzAyOTA3NjkxZjJjZGZmZTEifQ.eyJpc3MiOiJhY2NvdW50cy5nb29nbGUuY29tIiwic3ViIjoiMTEwNTAyMjUxMTU4OTIwMTQ3NzMyIiwiYXpwIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiZW1haWwiOiJwcmFiYXRoQHdzbzIuY29tIiwiYXRfaGFzaCI6InpmODZ2TnVsc0xCOGdGYXFSd2R6WWciLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiYXVkIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiaGQiOiJ3c28yLmNvbSIsImlhdCI6MTQwMTkwODI3MSwiZXhwIjoxNDAxOTEyMTcxfQ.TVKv-pdyvk2gW8sGsCbsnkqsrS0T-H00xnY6ETkIfgIxfotvFn5IwKm3xyBMpy0FFe0Rb5Ht8AEJV6PdWyxz8rMgX2HROWqSo_RfEfUpBb4iOsq4W28KftW5H0IA44VmNZ6zU4YTqPSt4TPhyFC9fP2D_Hg7JQozpQRUfbWTJI)

### JWS and JWE

- A signed `JWT` is known as a `JWS (JSON Web Signature)`.
- In fact a JWT is `abstract class` it need to be a `concrete implementations` either :
	- `JWS` or
	- `JWE (JSON Web Encryption)`.

### JOSE

`JOSE`/`Javascript Object Signing and Encryption` Header.

JOSE is a IETF working group which works on : "standardizing the representation of integrity-protected-data using JSON"

```php
var_dump(base64_decode('eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc4YjRjZjIzNjU2ZGMzOTUzNjRmMWI2YzAyOTA3NjkxZjJjZGZmZTEifQ'));
```

output
```json
{
    "alg": "RS256",
    "kid": "78b4cf23656dc395364f1b6c02907691f2cdffe1"
}
```

The JOSE header above, `both the `alg` and `kid` elements there, are not defined in the JWT specification, but in the `JSON Web Signature (JWS)` specification.

- The JWT specification only defines two elements (`typ` and `cty`) in the JOSE header,
- Both the `JWS` and `JWE` specifications extend it to add more appropriate elements.


### Unsecured JWT

- `JWS` object where in the `JOSE header`, the value of the `alg` element is set to `none`.
- unsecured `JWT` is a `JWS` without a signature

```json
{
    "alg": "none"
}
```


### Claim Set

```php
var_dump(base64_decode('eyJpc3MiOiJhY2NvdW50cy5nb29nbGUuY29tIiwic3ViIjoiMTEwNTAyMjUxMTU4OTIwMTQ3NzMyIiwiYXpwIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiZW1haWwiOiJwcmFiYXRoQHdzbzIuY29tIiwiYXRfaGFzaCI6InpmODZ2TnVsc0xCOGdGYXFSd2R6WWciLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiYXVkIjoiODI1MjQ5ODM1NjU5LXRlOHFnbDcwMWtnb25ub21ucDRzcXY3ZXJodTEyMTFzLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiaGQiOiJ3c28yLmNvbSIsImlhdCI6MTQwMTkwODI3MSwiZXhwIjoxNDAxOTEyMTcxfQ'));
```

output
```json
{
    "iss": "accounts.google.com",
    "sub": "110502251158920147732",
    "azp": "825249835659-te8qgl701kgonnomnp4sqv7erhu1211s.apps.googleusercontent.com",
    "email": "prabath@wso2.com",
    "at_hash": "zf86vNulsLB8gFaqRwdzYg",
    "email_verified": true,
    "aud": "825249835659-te8qgl701kgonnomnp4sqv7erhu1211s.apps.googleusercontent.com",
    "hd": "wso2.com",
    "iat": 1401908271,
    "exp": 1401912171
}
```

> The "identity provider" can include additional elements into the JWT claim set.

### Signature

Signature used as `sign` which make sure that the data transfered between 2 parties is secure, data integrity is protected/encrypted.

The signature parameters :
- `private` key
- data : [`claim set`](#claim-set) , header [`jose`](#jose)
- `algo` which is defined in [`jose header`](#jose)
If one of the parameter is changed, the signature will be changes too.

Google OpenID use `alg` : [`RS256`](https://github.com/Spomky-Labs/jose/blob/master/src/Algorithm/Signature/RS256.php) as explained in [Jose Header](#jose).

`RS256` algo wil use 
- [`openssl`](http://php.net/manual/en/function.openssl-sign.php) with parameters : 
    - `private` key and
    - `signature_alg` : `sha256`.

`RS256` use `rsa` encryption, which use pair of `private` and `public` key.
- The `private` key used to `sign`
- The `public` key used to `verify`, see in this jwt-debug sample
    - [with valid public key](https://jwt.io/#debugger-io?token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.TCYt5XsITJX1CxPCT8yAV-TVkIEq_PbChOMqsLfRoPsnsgw5WEuts01mq-pQy7UJiN5mgRxD-WUcX16dUEMGlv50aqzpqh4Qktb3rk-BuQy72IFLOqV0G_zS245-kronKb78cPN25DGlcTwLtjPAYuNzVBAh4vGHSrQyHUdBBPM&publicKey=-----BEGIN%20PUBLIC%20KEY-----%0AMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDdlatRjRjogo3WojgGHFHYLugd%0AUWAY9iR3fy4arWNA1KoS8kVw33cJibXr8bvwUAUparCwlvdbH6dvEOfou0%2FgCFQs%0AHUfQrSDv%2BMuSUMAe8jzKE4qW%2BjK%2BxQU9a03GUnKHkkle%2BQ0pX%2Fg6jXZ7r1%2FxAK5D%0Ao2kQ%2BX5xK9cipRgEKwIDAQAB%0A-----END%20PUBLIC%20KEY-----)
    - [with empty public key](https://jwt.io/#debugger-io?token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.TCYt5XsITJX1CxPCT8yAV-TVkIEq_PbChOMqsLfRoPsnsgw5WEuts01mq-pQy7UJiN5mgRxD-WUcX16dUEMGlv50aqzpqh4Qktb3rk-BuQy72IFLOqV0G_zS245-kronKb78cPN25DGlcTwLtjPAYuNzVBAh4vGHSrQyHUdBBPM)


The example of [`RS256 Test`](https://github.com/harryosmar/sample-phpunit-test/blob/jwt-signature/tests/unit/RS256Test.php).
- The `private` key example for this test case [private.key](https://github.com/harryosmar/sample-phpunit-test/blob/jwt-signature/tests/unit/private.key)
- The `public` key for this test case [public.key](https://github.com/harryosmar/sample-phpunit-test/blob/jwt-signature/tests/unit/public.key)

### Other Links
- https://tools.ietf.org/html/rfc7519
- https://medium.facilelogin.com/jwt-jws-and-jwe-for-not-so-dummies-b63310d201a3
- https://jwt.io/#debugger-io
- https://github.com/Spomky-Labs/jose
- http://php.net/manual/en/function.openssl-sign.php
- http://php.net/manual/en/function.hash.php
