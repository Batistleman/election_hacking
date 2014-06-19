#Election Hacking

## QR code reading:

* Took the normalized QR code from +Bruce Helsen http://i.imgur.com/WLKZk2e.jpg
* Cleaned it up a bit with gimp
* found a place where they mail the binary format http://online-barcode-reader.inliteresearch.com/default.aspx
	* my qr code app was only encoding the acii chars: (http://pastebin.com/6fLjDLiB)
* The result for 2012: [hex_qr_2012](./hex_qr_2012)
* The result for 2014: [hex_qr_2014](./hex_qr_2014)

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

    data = open('bin_qr_201x', 'rb').read()
    print(zlib.decompress(data))
    
    
### Result 2012:

    kktHIqSXueM0YqzZLuwYpgfJ8fMvO3NipMZhevSHqMM=,11,3,nl_BE,S,311,Af//AQ==,,o/sFYmxgdLHlf8hXVXz3oBbxDrvilEaIVh6wVhRyBFgtephrWANx0p3vgymsQN8yahgxfRLrT2hSQi/cem6YX6D5zFcqOdpTbWV9nj/8endCfZ3yyVM/zW+zDj8IPdqgGms7zDqIOm9NNkYQuO8WIQFjweLKJwzE9DFiJO15HSU=

separated:

	kktHIqSXueM0YqzZLuwYpgfJ8fMvO3NipMZhevSHqMM=
	11
	3
	nl_BE
	S
	311
	Af//AQ==

	o/sFYmxgdLHlf8hXVXz3oBbxDrvilEaIVh6wVhRyBFgtephrWANx0p3vgymsQN8yahgxfRLrT2hSQi/cem6YX6D5zFcqOdpTbWV9nj/8endCfZ3yyVM/zW+zDj8IPdqgGms7zDqIOm9NNkYQuO8WIQFjweLKJwzE9DFiJO15HSU=

### Result 2014:

    hJemtRUhKGPzxUM7x0rTyyG+O0qCocOCAtK+IKo3Rng=,38,10294,O,d54axnBIQv6YKrgQGQXPlA==,XrDH4P4PQvWgDSSEFrzBCw==,75,AgIAAA==,78,DwE=,97,HQI=,iQ6vdcfI2POSQRafRa4kU1sC+aPUwmrV+Dicd7mesmyAjP0oxu5GmbCQUCXQ/l/CTiq35gPqAHpfNAxIQGzlx3/2YVZfru2dRC/mBsksDr+Gd279KK6i3dr5XtmyLuQm/REH07O8yNr+i8jZdxWjpgEJXUHiEON8wzTlXGazkPQ=

separated:

    hJemtRUhKGPzxUM7x0rTyyG+O0qCocOCAtK+IKo3Rng=
    38
    10294
    O
    d54axnBIQv6YKrgQGQXPlA==
    XrDH4P4PQvWgDSSEFrzBCw==
    75
    AgIAAA==
    78
    DwE=
    97
    HQI=
    iQ6vdcfI2POSQRafRa4kU1sC+aPUwmrV+Dicd7mesmyAjP0oxu5GmbCQUCXQ/l/CTiq35gPqAHpfNAxIQGzlx3/2YVZfru2dRC/mBsksDr+Gd279KK6i3dr5XtmyLuQm/REH07O8yNr+i8jZdxWjpgEJXUHiEON8wzTlXGazkPQ=

#### String 1:

Converting the (probably Base64) string to hex gives us the result:

    8497A6B515212863F3C5433BC74AD3CB21BE3B4A82A1C38202D2BE20AA374678

    or

    1000010010010111101001101011010100010101001000010010100001100011111100111100010101000011001110111100011101001010110100111100101100100001101111100011101101001010100000101010000111000011100000100000001011010010101111100010000010101010001101110100011001111000

265 bit... so this is probably SHA-256

#### String 5:

	MD5?

#### String 6:

	MD5?


