# Funky Traffic Protocol

- [Funky Traffic Protocol](#funky-traffic-protocol)
  - [Preface](#preface)
  - [Solution](#solution)

## Preface

In hindsight, the first step I made was not required to get the flag, but in these writeups I just describe how I came up with the solution.

## Solution

The name of the challenges suggests that we should filter in FTP traffic. We see a lot of stuff, but it does not seem particularly interesting. Since the challenge is 'Very Easy', the flag is in plain sight. So, `Edit -> Find Packet` and we search for the string "WMG". The first result yields the **flag**.
