---
layout: post
title:  "HTTPS for Humans: Certificates"
date:   2020-12-29 22:29:31 +0200
categories: https
---

In the [first part]({% post_url 2020-12-28-https-for-humans-part-1 %}) of this series we went over the basics of how the secure communication channel can be established between two computers on the network. Using a combination of symmetric and asymmetric encryption we securely transmitted an encryption key which was then used by both parties in our communication link to encrypt and decrypt messages. 

We successfully managed to find a way to hide the information transmitted in our messages from anyone who might be “listening”. Now an attacker couldn’t really make sense of anything the user and the website sent each other, even though they could see every single byte which was sent over the network, including the public keys for encryption! 

But unfortunately this wasn’t enough to claim success. There’s still one attack angle which we didn’t cover - attackers could [“insert”](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) themselves in the middle of our communication and alter the messages! When the user is sending their “hello” over the wire and gets a “hello” back, they need some sort of proof that the party saying “hello” back is actually the website they wanted to talk to, not some sweaty dude in a basement trying to steal some credit card information.


## Certificates

We can setup a scheme akin to governments issuing passports which are then used for proof of identity. We’ll have the website show us their “passport” before we continue exchanging information with it. We’ll examine the passport to make sure it’s not fake and is not issued by the same sweaty dude in the basement and we’ll know that the website is the real deal. We’ll call those “passports” *Certificates* and the government issuing them -- a *Certificate Authority*. 


{: .centered}
![Kakie vashi dokazatelstva?](/assets/comms-drawing-7.png)

But how do we digitally create a proof of legitimacy? Turns out [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) comes to the rescue again.

## Digital Signatures

We haven’t talked about another awesome feature of RSA in the [Part 1]({% post_url 2020-12-28-https-for-humans-part-1 %}). Remember how we claimed that you can only encrypt data with public key and decrypt with private one? That’s not entirely true — you can actually flip this process and ENCRYPT data with the private key and decrypt it with public one. How is this useful though, you might ask? Public key is… public so anyone could decrypt the message and see its contents.

Turns out you can use it for signatures! The fact that you are ABLE to decrypt data means that the cipher could only come from the real holder of the private key. If someone else wanted to hack their way into this process and offer you a cipher text obtained with a wrong private key, you’ll be able to tell something is off — your public key doesn’t let you decrypt the data, i.e. when you decrypt the cipher the message doesn't make any sense!

So knowing this feature of RSA we can now make the website send a private key-encrypted piece of information we’ll call signature in its response to the user’s initial “hello” message. But which private key encrypts this signature and which public key should be used to decrypt it? In the [Part 1]({% post_url 2020-12-28-https-for-humans-part-1 %}) we established that the website has its own key pair which was used to setup the secure communication channel, but it’s not really usable here — if the signature is encrypted by the same website’s private key, the fact that we can decrypt it doesn’t prove us anything. It could be the same sweaty credit card-stealing person.

Remember, we’re trying to make this signature a proof of website’s identity, and in our government-issued passports analogy we established a trusted authority figure which we trust — a *certificate authority* (CA). So let’s ask these CA guys encrypt the website’s certificate contents with *their private key* and that would be our signature! We’ll make our website include this signature inside the certificate along with the other data it was sending to the user, so the user could then use a known public key of the CA to decrypt the signature thus verifying that the website went to the CA and registered themselves and was given a “passport”. Don't worry, the user won't need to keep track of the all known CAs' public keys -- browsers do this for them.

{: .centered}
![Hold up, imma check this](/assets/comms-drawing-8.png)

If the user managed to decrypt the signature and what they’ve got matched the certificate contents (including stuff like domain name), that would give them enough proof that some CA indeed issued this certificate to this particular website. There was indeed a government issuing this passport for this website at some point and the government’s seal in the passport matched the user’s expectations. 

So now not only our communication channel is secured with encryption, we also have a mechanism for the website to prove their identity to users using digital signatures and certificate authorities. 

The user and the website can finally talk in peace, securely.
