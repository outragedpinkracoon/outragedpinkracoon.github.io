---
title: No Openssl Found - Erlang / Asdf
layout: post
categories: [elixir, programming]
---
If you get this error 'No usable OpenSSL found' when trying to install Erlang, you may have to point it explicitly to where your openssl installation is.

First, try updating the plugin in asdf.

```bash
asdf plugin-update erlang
```

If that doesn’t fix the issue, add the following to your terminal config (e.g. .zshrc). Put in the correct version of openssl that you have installed.

```bash
export KERL_CONFIGURE_OPTIONS="--disable-debug --disable-silent-rules --without-javac --enable-shared-zlib --enable-dynamic-ssl-lib --enable-hipe --enable-sctp --enable-smp-support --enable-threads --enable-kernel-poll --enable-wx --enable-darwin-64bit --with-ssl=/usr/local/Cellar/openssl@1.1"
```
