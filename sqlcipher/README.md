# About This Image

Easy Encrypt and Decrypt [SQLite](https://www.sqlite.org) databases with [SQLCipher](https://www.zetetic.net/sqlcipher).

# How to Use this Image

This image contains 2 utils `sqlenc` (encrypt) and `sqldec` (decrypt) that do the hard work for you.

### Encrypt

```bash
docker run -v <workdir>:/sqlcipher pallocchi/sqlcipher sqlenc <db-plain> <db-encrypted> <PASSPHRASE>
```

### Decrypt

```bash
docker run -v <workdir>:/sqlcipher pallocchi/sqlcipher sqldec <db-encrypted> <db-plain> <PASSPHRASE>
```
### Parameters

| Name                       | Description                                                                                                                           |
|----------------------------|---------------------------------------------------------------------------------------------------------------------|
| `workdir`                | Local directory where `db-plain` is present and  `db-encrypted` will be created. |
| `db-plain`               | Filename of the database to encrypt (must be present in `workdir`).                       |
| `db-encrypted`      | Filename of the encrypted database which will be created.                                         |
| `passphrase`         | Passphrase used by SQLCipher to encrypt the database                                              |

## Example

Our database to encrypt is in `./databases`directory.

```bash
$ ls databases
$ my.db
```
Encrypt the database, generating the `my-encrypted.db` file.

```bash
$ docker run -v ${PWD}/databases:/sqlcipher pallocchi/sqlcipher sqlenc my.db my-encrypted.db test
```

Verify that the new database was created.

```bash
$ ls databases
$ my.db my-encrypted.db
```

Let's decrypt the previously generated database.

```bash
$ docker run -v ${PWD}/databases:/sqlcipher pallocchi/sqlcipher sqldec my-encrypted.db my-decrypted.db test
```

Verify that the new database was created.

```bash
$ ls databases
$ my.db my-encrypted.db my-decrypted.db
```

# Feedback

Please direct all feedback to [pallocchi/docker](https://github.com/pallocchi/docker/issues).
