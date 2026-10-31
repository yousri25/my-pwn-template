# My Pwntools Custom Template

This repository provides a personal, customized `pwntools` exploit template for CTF binary exploitation challenges.

## Attribution
The base template is **heavily based on the excellent work by [Crypto-Cat](https://github.com/Crypto-Cat)**, specifically their `official_template.py` from the [CTF repository](https://github.com/Crypto-Cat/CTF).

## Setup
`pwn template` (from pwntools) always loads `pwnup.mako` from pwntools' own installed package directory. So to make this your default template, you need to overwrite the file *inside your pwntools installation*.

1. Clone this repo:
   ```bash
   git clone https://github.com/yousri25/my-pwn-template.git
   cd my-pwn-template
   ```

2. Find where pwntools is installed and overwrite its bundled template:
   ```bash
   PWN_TEMPLATES=$(python3 -c "import pwnlib, os; print(os.path.join(os.path.dirname(pwnlib.__file__), 'data', 'templates'))")
   sudo cp "$PWN_TEMPLATES/pwnup.mako" "$PWN_TEMPLATES/pwnup.mako.bak"   # back up the stock template
   sudo cp pwnup.mako "$PWN_TEMPLATES/pwnup.mako"
   ```
   (`sudo` is needed when pwntools is installed system-wide, e.g. `/usr/lib/python3/dist-packages` on Kali. Skip it inside a virtualenv. To restore the stock template: `sudo apt install --reinstall python3-pwntools`, or copy the `.bak` back.)

   If you installed pwntools in a virtualenv, activate it first so the `python3 -c ...` call resolves to the right pwnlib.

3. Generate a new exploit from the template:
   ```bash
   pwn template ./vuln > exploit.py
   ```

## Note on this template
`pwn template` renders `pwnup.mako` with Mako and passes it 8 positional arguments (`exe, host, port, user, password, libc, path, quiet`). Mako can only accept them if the file starts with a `<%page args="..."/>` line, so **that line must stay as line 1 of `pwnup.mako`**. Without it, `pwn template` crashes with:

```
TypeError: render_body() takes 1 positional argument but 9 were given
```

The rest of the file is a static skeleton: it does not use the `--host`/`--port` flags, so edit `exe`, `offset` and the payload by hand. To consume those values, use Mako substitutions such as `${binary}`, as in pwntools' own [`pwnup.mako`](https://github.com/Gallopsled/pwntools/blob/dev/pwnlib/data/templates/pwnup.mako).

Mako treats `${...}`, `<%`, and lines starting with `%` or `##` as special. Avoid those in the skeleton unless you mean them as template syntax.

## Usage
Once installed, every `pwn template` invocation will use this skeleton. You can also just copy `pwnup.mako` manually into a challenge directory, rename it `exploit.py`, and edit the `exe`, offset, and payload sections directly.
