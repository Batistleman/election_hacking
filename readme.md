#Election Hacking

## QR code reading:

* Took the normalized QR code from +Bruce Helsen http://i.imgur.com/WLKZk2e.jpg
* Cleaned it up a bit with gimp
* found a place where they mail the binary format http://online-barcode-reader.inliteresearch.com/default.aspx
	* my qr code app was only encoding the acii chars: (http://pastebin.com/6fLjDLiB)
* The result: http://pastebin.com/bUKSUew5

      789c0dc7c97282300000d00f6a6622cd48c3810316285002452cdba5a34212565964cbd7db777b75fdb4ec214ce6821cd24164eebca63da30ea664f19157f624e3c5125a03212a90248040d7fc9d0c1002f43f8d42a805aa0ac0034e66da6e2c77ad86629e4489408fd36dd3c7a56c8cab1d71798df8793f99ec59f47c8c356f3bf468617b3b051edeaf9c6df4ec8e97771e0625bc17ad9c26b27e14e67df0f3fe728b23a5ab202ebafc936668df230245fc26f40adb3ff9c0bedae943e883edb78ae7d56930fb38b603b35a0bf7db5985a1e866e9f8d2d10a7fd517628a5246

## Data contents:

* according to Anthony: "According to the docs, this needs to somehow get uncompressed with zlib. "
* True: the header reads: 78 9C = default zlib compression

Converting the hex data to binary format: 

    xxd -r -p hex_qr > bin_qr

## Decompressing: 

Just do: 

    qr_decompressor

Code:

    #! /usr/bin/env python

    import zlib

    data = open('bin_qr', 'rb').read()
    print(zlib.decompress(data))
    
    
Result:

    kktHIqSXueM0YqzZLuwYpgfJ8fMvO3NipMZhevSHqMM=,11,3,nl_BE,S,311,Af//AQ==,,o/sFYmxgdLHlf8hXVXz3oBbxDrvilEaIVh6wVhRyBFgtephrWANx0p3vgymsQN8yahgxfRLrT2hSQi/cem6YX6D5zFcqOdpTbWV9nj/8endCfZ3yyVM/zW+zDj8IPdqgGms7zDqIOm9NNkYQuO8WIQFjweLKJwzE9DFiJO15HSU=
    
Some nice csv!