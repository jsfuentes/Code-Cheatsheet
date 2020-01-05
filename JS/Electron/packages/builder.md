# Electron builder

## Mac

After 10.15 need to notarize Mac apps

Create Apple Developer Account($99), and create a Developer ID Application to sign for distribution outside the app store

#### Create Certificate Signing Request

1. Launch Keychain Access located in `/Applications/Utilities`.

2. Choose Keychain Access > Certificate Assistant > Request a Certificate from a Certificate Authority.

3. In the Certificate Assistant dialog, enter an email address in the User Email Address field.

4. In the Common Name field, enter a name for the key (for example, Gita Kumar Dev Key).

5. Leave the CA Email Address field empty.

6. Choose “Saved to disk”, and click Continue.

   ![img](https://help.apple.com/developer-account/en.lproj/Art/c_create_csr.png)