# My Pwntools Custom Template

This repository provides a personal, customized `pwntools` exploit template for CTF binary exploitation challenges.

## Attribution
The base template is **heavily based on the excellent work by [Crypto-Cat](https://github.com/Crypto-Cat)** , specifically their `official_template.py` from the [CTF repository](https://github.com/Crypto-Cat/CTF). Full credit for the original structure and functions (`start()`, `find_ip()`, etc.) goes to Crypto-Cat.

## Setup
To use this template as the default for `pwn template`, clone this repo and copy the template file to your pwntools config directory:
```bash
git clone https://github.com/YOUR_USERNAME/my-pwn-template.git
mkdir -p ~/.config/pwntools/templates
cp my-pwn-template/pwnup.mako ~/.config/pwntools/templates/pwnup.mako
