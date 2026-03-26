# gwpgen.py

**gwpgen.py** is an entropy-driven, cryptographically sound password generator
written in Python.

It generates strong random passwords using the operating system's
cryptographically secure random number generator and calculates password
length from a desired entropy target.

## Features

- cryptographically secure randomness (`os.urandom`)
- entropy-driven password length calculation
- no modulo bias (rejection sampling)
- Fisher–Yates shuffle for unbiased character ordering
- configurable character classes
- optional grouping for human-friendly passwords
- WiFi QR string output
- entropy presets for common security levels
- optional enforcement of character classes
- configurable safety limits

## Installation

Clone the repository:

```bash
git clone https://github.com/georgwallisch/gwpgen.git
cd gwpgen
```

Run directly:

```bash
$ ./gwpgen.py
```

Or install it somewhere in your $PATH.

## Basic usage

Generate a strong password with 128 bits of entropy:

```bash
$ ./gwpgen.py --strong -a -m
```

Example output: kF7!dP3$wQ9r#N8TzB6M

Generate a password of fixed length:

```bash
$ ./gwpgen.py -L 20 -a -m
```

Generate multiple passwords:

```bash
$ ./gwpgen.py --strong -a -m -N 5
```

Group characters for better readability:

```bash
$ ./gwpgen.py --strong -a -m -g 4
```

Example: vT8d-9Xk3-ZP4q-Lm2B

Pad the last group to full group size:

```bash
$ ./gwpgen.py --strong -a -m -g 4 -p
```

## Character classes

You must select at least one character class.

```bash
Option	Description
-a, --alphanum	Uppercase, lowercase and digits
-u, --upper	Uppercase letters
-l, --lower	Lowercase letters
-d, --digits	Digits
-m, --symbols	Symbols (optional custom set)
-x, --hex-lower	Hexadecimal lowercase
-X, --hex-upper	Hexadecimal uppercase
```

```bash
$ ./gwpgen.py --strong -u -l -d -m
```

## Entropy presets

```bash
Preset	Entropy
--weak	50 bits
--good	70 bits
--strong	100 bits
--stronger	128 bits
--tough	192 bits
--paranoid	256 bits
--insane	512 bits
```

Example:

```bash
$ ./gwpgen.py --paranoid -a -m
```

## Entropy vs length

Instead of specifying a password length, you can specify a target entropy:

```bash
$ ./gwpgen.py -b 128 -a -m
```

The program will automatically calculate the required password length based on the size of the selected alphabet.

## WiFi QR code strings

gwpgen can output passwords in WiFi QR format compatible with Android and many QR code generators.

Example:

```bash
$ ./gwpgen.py --strong -a -m -W MyNetwork
```

Output example: WIFI:T:WPA;S:MyNetwork;P:abcDEF123!;

Hidden network:

```bash
$ ./gwpgen.py --strong -a -m --wifi-hidden MyNetwork
```

## Output options

Write passwords to a file:

```bash
$ ./gwpgen.py --strong -a -m -o passwords.txt
```

Write both to file and stdout:

```bash
$ ./gwpgen.py --strong -a -m -o passwords.txt --tee
```

## Safety limits

To avoid accidental misuse, gwpgen enforces limits by default:

- entropy	1000 bits
- length	250 characters
- number of passwords	500

Disable limits:

```bash
$ ./gwpgen.py --no-limits
```

## Security properties

gwpgen was designed to avoid common pitfalls found in many password generators.

Security features include:

- operating system CSPRNG (os.urandom)
- rejection sampling to avoid modulo bias
- Fisher–Yates shuffle
- entropy-based password generation
- optional character class enforcement
- configurable alphabet

## Example

Generate five strong passwords grouped for readability:

```bash
$ ./gwpgen.py --strong -a -m -g 4 -N 5
```

Example output:

T4p!-9Xm2-rQ6d-Lz7A
3Kq%-Lm9P-x2fD-aT8Z
hV3#-F8kW-rP2q-M9bC
8Qw@-sF3T-vX9d-H4mL
N7x!-q2pD-KM9f-Wz3R

Short options can be grouped together:

`$ ./gwpgen.py --strong -vapg`

Equivalent to:

`$ ./gwpgen.py --strong -v -a -p -g`

Generate a numeric password for embedded devices such as pay terminals using a dot as separator:

```bash
$ ./gwpgen.py -L 24 -dpg 4 -s "." -o mywifi.txt --tee
```

Example output: 3109.4236.2589.1904.1843.7841

Generate a strong password for some login:

```bash
$ ./gwpgen.py --strong -apg 4
```
Example output: r3s6-y9O6-xYRd-tylt-Z5lW

or stronger: 

```bash
$ ./gwpgen.py --stronger -apg 4
```

Shorthand method: Group size default 4 and -G combines -g and -p:

```bash
$ ./gwpgen.py --stronger -aG
```

Example output: OLS5-9YKM-291c-vfv7-su5h-38Sx

or with symbols and not grouped:

```bash
$ ./gwpgen.py --stronger -am
```

Example output: 7a&b+GoJy(SNV;RdlM53M

## License

![License](https://img.shields.io/github/license/georgwallisch/gwpgen)

Copyright (c) 2026 Georg Wallisch

MIT License – see [LICENSE](./LICENSE)
