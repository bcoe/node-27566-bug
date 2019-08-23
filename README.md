# Demonstrate Block Coverage Bug

This repo demonstrates that Node.js 12+ drops block coverage information when
executing a source file with many functions.

This behavior only seems to occur on certain linux distributions.

## Setup

Clone this repository to a Linux machine running a nightly build of Node.js,
I'm running `v13.0.0-nightly20190819ec16fdae54` on 
`Debian GNU/Linux 10 (buster)`.

## Running Demonstration

From the `node-27566-bug` folder, run:

```bash
npm i
npm run bug
```

Note that `failure.js` indicates that it has `100%` of its functions executed,
even though `0` were invoked.

Note that `success.js`, correctly, indicates that `0%` of functions were
executed.

The only difference between the two files is that `success.js` has fewer
functions than `failure.js`.

## What's Happening?

The coverage information output by the v8 inspector does not include block
information for `failure.js`, it does include block information for
`success.js`.
