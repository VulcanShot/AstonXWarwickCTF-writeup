# RIP Terminal

## Solution

Whenever you see a file with weird characters, you know its a binary file. Since the challenge was Easy, I knew it was as straightforward as:

```bash
strings binary_data.txt | grep 'WMG'
```
