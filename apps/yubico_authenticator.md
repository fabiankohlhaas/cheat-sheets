# Yubico Authenticator

Software from [yubico](https://www.yubico.com/products/yubico-authenticator/) to retrive 2FA tokens stored on a yubikey.

# Linux

The following instructions were tested against Pop!_OS 22.04 and should be considered a reference. If you're using a Linux distribution other than Pop!_OS or another Ubuntu derivative, you may need to adapt these instructions accordingly, as package names, etc. may differ.

1. Install required packages by running the following command in Terminal.

```bash
sudo apt install gnupg scdaemon pcscd pcsc-tools
```

2. Create or edit the file ~/.gnupg/scdaemon.conf, and add the following line to it.

```bash
disable-ccid
```

3. Since GPG relies on pcscd (PC/SC Smart Card Daemon) to communicate with the YubiKey, enable it to start with the system by running the following command in Terminal.

```bash
sudo systemctl enable --now pcscd
```

4. Reboot the system to clear any GPG locks

5. Following the reboot, open Terminal, and run the following commands. These commands assume you have a certificate enrolled on the YubiKey.

```bash
pkcs11-tool --login --test
pkcs11-tool --list-slots
```

6. Open a second Terminal, and in it, run the following commands.

```bash
gpg --card-edit
quit (at the gpg/card> prompt)
```
