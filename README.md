# Airsign

Sign your ethereum transactions from a sealed Android mobile phone to avoid password leaks.

## Getting Started


### Prerequisites

You will need a pc and an mobile phone running Android os, both with camera: the mobile phone that is offline (henceworth the **offline phone**) from the internet to make sure no hacker can get access to your passwords, and one that is connected to the internet (henceworth the **online pc**). 
You need to install `parity` ethereum client on the **online pc** for this package to work. This system has not been tested with `geth` client. 



### Installing

On **offline phone** do the followings:
1. In google play install:
	- `qr code reader` - needed to read qr code from **online pc**
	- `Termux` - runs linux commands under Android
	- `Termux API` - make termux scripts able to read from clipboard
2. Execute the followings on **offline phone** in Termux:
```
pkg update
pkg upgrade
pkg install git
git clone https://github.com/r001/airsign 
cd airsign 
git checkout android-termux 
./install_android
```
3. Create ethereum account(s), and copy them to **offline phone** in the `/data/data/com.termux/files/home/.ethereum/keystore` directory.  
	- If you want to go extremel secure, then take a fresh installed pc, install parity there, create accounts there, and generate QR code from the account json data, read that QR code to **offline phone**. 
	
On **online pc** do the followings:
4. Execute the followings on **online pc**:
	- install parity from https://github.com/paritytech/parity/releases
	- sync parity
5. Install the same accounts that you have installed to **offline phone** to **online pc**. You have three alternatives here:
	Alternative a: Recommended method: 
		1. Create an account on **online pc**.
		2. Open the account key file and change the "account" fields addresss to the address of your account created in 3. ! This way the account can not be cracked, since the real account data is not available on the **online pc**, but parity will still handle the account as it was valid.
	Alternetive b: Create **external account**: In parity create new account and chose "External" in the menu. This method is secure, but a few dapps can not use it (eg. www.oasisdex.com), so it is not recommended. The advantage of this method is that parity itself will generate a QR code that has to be signed by the **offline phone**. See later. 
	Alternative c: Less secure method: Simply copy accounts to use for parity. Using this method makes it possible to brute force attack your password if adversary gets access to your account data. 
6. Do the followings:
```
git clone https://github.com/r001/airsign 
cd airsign 
git checkout android-termux 
```

## Usage

1. On **online pc** do whatever transaction with `parity` and wait for the signer to come up. **Do not sign the transaction on online pc!** The whole point of using airsign is to avoid disposing your passwords on the **online pc**.
2. On **online pc** run `airdrop`. This will read the transaction and create a QR code from it on the command line.
3. On **offline phone** run `QR code reader` and read the QR code generated in (2.). You will see that reading was successful when the transaction is written on the screen. Copy the transaction to the clipboard. 
4. On **offline phone** start Termux.
5. In Termux run the command `airsign/airsign`. This will read the transaction from the clipboard, and generate a series of QR codes. By hitting a key on keyboard you can display all the generated QR codes one by one. On **online pc** read the QR codes generated one by one by executing `airpublish`. When you have read all the QR codes, hit `CTRL-c` on **online pc**.
6. On **online pc** you can now reject the signature request in parity. This will not delete the transaction.

## Authors

* **Robert Horvath** - *Initial work* - [airsign](https://github.com/r001/airsign)

## License

This project is licensed with the GPL v3 license. 

## Acknowledgments

Thaks to Daniel Brockman and Mariano Conti for their help to develop this package.
