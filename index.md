## Command to show GPU RAM load for Mate panel

A Command Applet can be added to the Mate panel. It shows an output of a custom user-defined command, refreshed every second by default. The command I came up with to display GPU load:

```bash
bash -c "nvidia-smi|sed -n 9p|grep -oE '[[:digit:]]+[[:alpha:]]+[[:blank:]][/][[:blank:]]+[[:alnum:]]+'"
```
```markdown
1. bash -c wraps the command, as applet does not accept pipes (|)
2. nvidia-smi outputs a text table with GPU info
3. sed -n 9p selects only line #9 with target info. This easies the task of the following grep
4. grep -o to output not the whole line, but only regexed sequence
5. -E to deploy slightly more complicated regex expression (same as --extended-regexp)

Target output is like "185MiB /  20040MiB" filtered from line which is like 
| N/A   44C    P0    N/A /  N/A |    185MiB /  20040MiB |     41%      Default |

6.  [[:digit:]] for the staff that starts with numbers
7.  + is for multiple characters of this kind
7.  [[:alpha:]] for alphabetic chars
8.  [[:blank:]] for space or tab
9.  [/] for / symbol
10. [[:alnum:]] for aplhanumeric
```
Perhaps not the most beautiful / optimal command, but it works. 
