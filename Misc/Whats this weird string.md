# What's this weird string?

## Solution

We are given the following string:

> V01He0JBc0VfNjRfSXNfQVdlU29tRX0=

It looks like Base64[^1], so just let CyberChef do it for you.

From Base64 -> **flag**.

[^1] Base64 only uses alphanumeric characters, plus '/', '+', and '-'. This last one is used as padding so its only found at the end. Dead giveaway.
