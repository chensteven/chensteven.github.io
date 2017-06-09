---
layout: post
title: "Guide to Authentication in Node.js - Part 1"
date: 2016-11-23 22:17:02 -0500
description: "This a short guide to the concepts used in authentication"
tags: [authentication, node.js, javascript]
comments: true
---

### Introduction to Authentication

Authentication is a very important functionality for all web applications that involve registering users.

There are two basic approaches to authentication over HTTP:
- Cookies
- Siging requests by using POST.

### Cookies

This is the least secure way to secure web applications in browsers. It has a main problem because they can be hijacked (network sniifers) or stolen.

### Signing requests

Post request is sent by the browser to the server. Popualar ways include basic authentication and third party authentication. SSL connection is required to secure the information, without it user credentials are in plain text.

### Crypto Module

When I was learning how to create an authentication system, I first came across Node's crypto module.

The module was last updated 3 years ago (2011) and I took some time to look over the documentation on NPM.

The module offers a way of encapsulating secure credentials to be used as a part of a secure HTTPS net or http connection. Pretty much it offers a set of wrappers for OpenSSL's hash, hmac, cipher/decipher, sign and verify methods.

- "http://nodejs.org/api/crypto.html"

### Hash

So what are all these terms?

A Hash algorithmn is a one-way mathematical equation that takes in an arbitrary length input and produces a fixed length output string. The output is called a hash value and is unique.

Simply, if you hash any plain text and you can't get the original plain text back. In this case, hash is unidirectional and irreversible.

Hash is good for checking validity of input data which is when you want to compare a value but can't store the plain representation. Password is a good use case.

In the case of password, hash(password) is not good enough, usually you want to add salt - hash (password + salt). However, the best way is to use a stretched hash mechanism, also known as key strengthening, for example:

var hash = password + salt;
for (var i = 0; i < 5000; i++) {
    hash = sha512(hash + password + salt);
}

What you're doing is iterating over a hash many times. PBKDF2 is a good way to do that in the crypto library.

There are many hash types, such as md5, sha1, sha256, sha512 and the list is in order of length from shortest to longest.

### SHA-2
SHA-2 is a set of cryptographic hash functions designed by NASA. SHA stands for secure hash algorithmn.

SHA-2 includes significant changes from its predecessor, SHA-1. The SHA-2 family consists of six hash functions with digests (hash values) that are 224, 256, 384 or 512 bits.

SHAs are not weak because they are cryptographically weak (though some are), it is weak because they are fast.

"http://forums.udacity.com/questions/6016855/hashing-passwords-using-sha256-is-not-enough-today"

### Encryption
Encryption is bidirectional. Encrypted plain text can be decrypted using a key.
Encryption is good when we need to get the data back such as credit card numbers.
Given this, hashing is good for authorization and encryption is good for transmitting data


### Node_Hash Module

Node_Hash module is a wrapper for Node's crypto library. It is suppose to be a super simple hashing library for Node.js.

### BCrypt.js and Node.Bcrypt.js

Bcrypt is an adaptive hash algorithmn, which is different from other hash algorithmn. Bcrypt is backed by Blowfish, designed by Bruce Schneier.

Bcrypt aims to be slow which is safer than crypto. Also, salts are built into the bcrypt algorithmn.

### Scrypt

Then there is Scrypt, the newest kid on the block. It allows you to specify not only processing power used for password hashing, but also memory usage.

### OpenSSL

OpenSSL is an open source project that implements SSL (Secure Sockets Layer) and TLS (Transport Layer Security) protocols with a general purpose cryptography library.

### OAuth 2.0

Created in 2006, OAuth 2.0

### Passport

For Node.js, Passport is probabaly the most popular and robust authentication module for Node/Express right now.

Passport supports different strategies for authentication. It offers local and social media OAuth such as Facebook, Twitter, Google+

###
