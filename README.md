# chrome_passwords_kde_wallet
How to fix chrome password sync after a broken kdewallet 

## Broken kde wallet
Chrome is not able to use saved passwords even after a successful login into your google account (with the browser)

Starting chrome from the commandline showes an error something like:

```
Failed to call method: org.kde.KWallet.isEnabled: ...
```

This led me to believe somehting was wrong with my `kdewallet`. 
After some invesigation in `KWalletManager` I realized the default wallet `kdewallet` could not be opened any more (why oh why?).

## Create new wallet with auto unlock on login

* create wallet named `kdewallet`
* use blowfish password authentication
* use login password as wallet password

see https://wiki.archlinux.org/index.php/KDE_Wallet

## Fix summary

* Create new KDE Wallet in `KWallatManager`
* Select new wallet to use for passwords (`Configure Wallet -> Select wallet to use as default`)
* Delete old `Login Data` and `Login Data-journal` files from the google Chrome profile in question (located in `~/.config/google-chrome/Default`)
* Open Browser and login into account
* Check `chrome://sync-internals/` if password sync is running again

## Trouble shooting

If `chrome://sync-internals/` reports:
```
ERROR:password_sync_bridge.cc(231)] Passwords datatype error was encountered: Failed reading passwords metadata from password store.
```

than you most likely deleted the `Login Data` and `Login Data-journal` files for the wrong chrome user profile
