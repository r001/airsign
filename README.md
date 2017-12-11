# Airsign

Sign your ethereum transactions from a offline computer to avoid password leaks.

## Getting Started


### Prerequisites

You will need two computers with camera: one that is offline (henceworth the **offline**) from the internet to make sure no hacker can get access to your passwords, and one that is connected to the internet (henceworth the **connected**). 
You need to install `parity` ethereum client on both the **offline** and the **connected** for this package to work. This system has not been tested with `geth` client. 


```
apt-get install zbar-tools moreutils python-pip

#jshon is used by `seth` to create and parse json
git clone https://github.com/mbrock/jshon
cd jshon
make install
cd ..

#seth is the tool to access the ethereum node
git clone https://github.com/dapphub/seth
cd seth
make install
cd .. 

# the following will install a QR code generator
pip install qrcode
```

### Installing

1. You need to install the `airdrop` and `airpublish` on the **connected** and the `airsign` on the **offline**. It does not matter what folder you install the files into. 
2. You need to install your keys to both **offline** and **connected**. (Make sure you have long enough passwords to be safe!)

## Usage

1. On **connected** do whatever transaction with `parity` and wait for the signer to come up. **Do not sign the transaction on connedted!** The whole point of doing airsign is to avoid disposing your passwords on the **connected**.
2. On **connected** run `airdrop`. This will read the transaction and create a QR code from it on the command line.
3. On **offline** run `airsign` and read the QR code generated in (2.). You will see that reading was successful when the transaction is written on the screen. This will pop a signer window on parity (if the account is not unlocked), enter your password on **offline**. Once done, a QR code will be generated on the command line containing the signed raw transaction.
4. On **connected** read the QR code generated in (3.) by executing `airpublish`, this will send your transaction on the chain. The command will return the transaction hash of the mined transaction. 

Note 1: Please allow enough time for the transaction to be mined. It can take several miutes. It is perfectly safe to publish transaction data. 

Note 2: If (4.) was interrupted you can start it over until the transaction is mined. 

## Authors

* **Robert Horvath** - *Initial work* - [airsign](https://github.com/r001/airsign)

## License

This project is licensed with the GPL v3 license. 

## Acknowledgments

Thaks to Daniel Brockman and Mariano Conti for helping to develop this package.
