# My Pwntools Custom Template

This repository provides a personal, customized `pwntools` exploit template for CTF binary exploitation challenges.

## Attribution
The base template is **heavily based on the excellent work by [Crypto-Cat](https://github.com/Crypto-Cat)**, specifically their `official_template.py` from the [CTF repository](https://github.com/Crypto-Cat/CTF).

## Setup
`pwn template` (from pwntools) does **not** read templates from `~/.config/pwntools/templates/` — that directory isn't used anywhere in pwntools. It always loads `pwnup.mako` from pwntools' own installed package directory. So to make this your default template, you need to overwrite the file *inside your pwntools installation*.

1. Clone this repo:
   ```bash
   git clone https://github.com/yousri25/my-pwn-template.git
   cd my-pwn-template
   ```

2. Find where pwntools is installed and overwrite its bundled template:
   ```bash
   PWN_TEMPLATES=$(python3 -c "import pwnlib, os; print(os.path.join(os.path.dirname(pwnlib.__file__), 'data', 'templates'))")
   cp pwnup.mako "$PWN_TEMPLATES/pwnup.mako"
   ```
   (Back up the original first with `cp "$PWN_TEMPLATES/pwnup.mako" "$PWN_TEMPLATES/pwnup.mako.bak"` if you ever want to restore the stock template.)

   If you installed pwntools in a virtualenv, activate it first so the `python3 -c ...` call resolves to the right pwnlib.

3. Generate a new exploit from the template:
   ```bash
   pwn template ./vuln > exploit.py
   ```

## Note on this template
`pwnup.mako` here is a static skeleton (no Mako templating logic, no `<%page args="..."/>` directive) — it's meant as a personal starting-point script you copy per challenge and edit `exe`, `offset`, and the payload by hand, not a dynamic template that reacts to `pwn template`'s `--host`/`--port`/etc. flags. If you want it to actually consume those flags, see pwntools' own [`pwnup.mako`](https://github.com/Gallopsled/pwntools/blob/dev/pwnlib/data/templates/pwnup.mako) for the Mako syntax (`<%page args=...%>`, `${...}` substitutions) to add.

## Usage
Once installed, every `pwn template` invocation will use this skeleton. You can also just copy `pwnup.mako` manually into a challenge directory, rename it `exploit.py`, and edit the `exe`, offset, and payload sections directly.
