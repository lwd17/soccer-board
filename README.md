# soccer-board

A password-protected snapshot of a matchday odds board.

`index.html` is AES-256 encrypted with [StatiCrypt](https://github.com/robinmoisson/staticrypt);
the deployed file is ciphertext plus the script that decrypts it in the browser.
No model code, no data pipeline and no source lives in this repository — only
the rendered page.

To regenerate and re-encrypt:

```bash
soccerbet update
soccerbet export "$(date -u +%F)" site/index.html
npx staticrypt site/index.html --password "$PASSPHRASE" --short -d out --remember 7
cp out/index.html index.html && git commit -am "card $(date -u +%F)" && git push
```

The passphrase can be brute-forced offline against the downloaded ciphertext,
so a long random one is worth more than a memorable one.
