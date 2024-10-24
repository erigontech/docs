# Lighthouse

Lighthouse is another popular client that combined with Erigon can be used for block building.

Documentation can be found here: <https://lighthouse-book.sigmaprime.io>

The basic steps to run Erigon together with Lighthouse are:
1. Install and run Erigon. Erigon will automatically create a JWT secret.
2. Install and run Lighthouse, pointing to JWT secret created by Erigon.