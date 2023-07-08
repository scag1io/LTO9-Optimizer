# LTO9-Optimizer

This is a simple Bash script to initialize/optimize LTO9 physical tapes.

### ⚠️ This repository is just a placeholder for more visibility. You can find the script on Gitea [here](https://gitea.it/scaglio/LTO9-Optimizer)

## The Problem

Enterprise LTO9 tapes are cool, but if you buy them in stocks of 1,000, or even 2,000, you potentially need [weeks](https://www.ibm.com/docs/en/ts4500-tape-library?topic=drives-media-optimization) before using them.
A single tape is held from 20 minutes up to 2 hours in the drive, and you cannot do anything but wait.
This is the standard behavior from this LTO generation.

I find unnerving that enterprise tape libraries are sold without a feature to do this automatically, so I wrote this simple Bash script.

## The Solution

Connect the Tape Library to a Linux server using SAS or FiberChannel (I only have tested FC), then run `lsscsi -g | grep medium` to get the special device of the changer, which will be something like `/dev/sgX`.

Then you can run the command:

`optimizer.sh </dev/sgX> <parallelism>`

Where 'parallelism' is a number, which can be equal to the number of the drives of the library/partition.

The script takes **long** pauses to avoid too many load/unload commands, so... be patient.

It has been tested with both:
- IBM TS4500 Tape Library
- Quantum i6000 Tape Library

## Dependencies

The only package required is [mtx](https://linux.die.net/man/1/mtx).

## Fun Facts

As far as I know, up to today, 4th of July, 2023, none of the major brands of Tape Libraries can provide a tool capable of this.
I wrote the script in a day, then tested and fixed it.

Total time spent: 3 days.

Total money earned: none, so I'll just put it here.

## Disclaimer

Please note that this script **does not mean to replace** any of the eventual official tools that may exist – but sadly I wasn't aware of.

P.S. I am aware the script is poorly written, but I don't have a test environment anymore to test it properly. I'll do it in my spare time.
