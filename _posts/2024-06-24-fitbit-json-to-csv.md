---
title: "Fitbit data JSON to .csv file converter"
description: "Patched an existing tool, iccir919.github.io/fitbit-json-to-csv, to fix three issues"
author: Daniel Dantas
---

A friend asked for help converting fitbit `json` files to `csv` format.

There was an [existing tool](https://iccir919.github.io/fitbit-json-to-csv/) but it no longer worked.

I [forked the repository](https://github.com/dantasfiles/fitbit-json-to-csv) and patched the three issues.

I created three pull requests ([Json2csv@4.5.4](https://github.com/iccir919/fitbit-json-to-csv/pull/1), [off-by-one issue on merge](https://github.com/iccir919/fitbit-json-to-csv/pull/2) & [incorrect filenames](https://github.com/iccir919/fitbit-json-to-csv/pull/3) on the original repository, and hosted the [fixed tool on my website](https://dantasfiles.com/fitbit-json-to-csv/) until the pull requests are accepted
