Encrypted whistles will be hex format AES-256 CBC encrypted

The key is the SHA256 hash of the user provided key (for demo data, this is `SeetiTel`).

The IV is the byte value of `0000000000000000` (in hex, `30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30`)

*EVERYTHING MOVES IN UTF-8 SPACE*

Test your settings [here](http://aes.online-domain-tools.com/); text input type with hex encoding, running AES on CBC with a hex key (the SHA256 hash) in hex. The IV is `30 30 30 30 30 30 30 30 30 30 30 30 30 30 30 30`.
