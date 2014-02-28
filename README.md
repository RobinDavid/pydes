pydes
=====

Basic but pure DES implementation in Python
I have written it for fun because nothing else.


How it works ?
--------------

Everything is made within a class called "des". This class can be instanciated once and used to cipher and decipher multiple datas.
It also support padding using the PKCS5 specification. (So the data is padding even if it is multiple of 8 to be sure that the last byte il be padding data).
The generation of all the keys used is made in the method generatekeys and substitute apply the SBOX permutation.
The main method is run which is called by both encrypt and decrypt but in a different mode. This method do basically all the stuff, it loop
throught all the blocks and for each do the 16th rounds.

Be careful: This module implement DES in ECB mode, so you can't make it weaker. I didn't made it to be strong but for fun.

How to use it ?
---------------

I have not done any interface to take argument in command line so this module can't be used as a script. (feel free to modify it).
To use it from python shell or in another module do:

    from pydes import des

    key = "secret_k"
    text= "Hello wo"
    d = des()
    ciphered = d.encrypt(key,text)
    plain = d.decrypt(key,ciphered)
    print "Ciphered: %r" % ciphered
    print "Deciphered: ", plain

Note: In this exemple no padding is specified so you have to provide a text which is multiple of 8 bytes. The key is cut to 8 bytes if longer.

To use padding:

    from pydes import des

    key = "secret_k"
    text= "Hello world !"
    d = des()
    ciphered = d.encrypt(key,text,padding=True) #Or just True in third arg
    plain = d.decrypt(key,ciphered,padding=True)
    print "Ciphered: %r" % ciphered
    print "Deciphered: ", plain
