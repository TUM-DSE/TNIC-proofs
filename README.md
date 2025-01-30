# T-NIC Protocol Verification

This repository contains a Tamarin model and lemmas for the protocols employed by the T-NIC architecture.
For installation of the Tamarin prover (version 1.8.0) refer to the [Tamarin documentation](https://tamarin-prover.com/manual/master/book/002_installation.html).

The model and lemmas are specified in `tnic_protocols.spthy`, the model is generated with respect to the
protocols explained in Section 4.3 of the paper as well as the functions defined in Algorithm 1.

The full output including the proof generated by Tamarin is contained in `tnic_protocols_analyzed.spthy`.
The proof was automatically generated using `tamarin-prover --prove tnic_protocols.spthy`, and successfully finished after 3min on an *Intel(R) Xeon(R) Gold 6438Y+* processor with *500GB* of RAM. An automatically generated summary of summaries is contained in `summary.txt`. Tamarin calls `tnic_oracle.py` to speed up the computation of certain lemmas during the proving process.

The model can also be explored interactively by running `tamarin-prover interactive .` in this directory.


## Assumptions

We assume that all the assumptions of the symbolic model and the tamarin prover hold, including:

* All messages are composed of atomic terms using predefined functions.
* All cryptographic functions are perfect with no side-effects.
* Attackers can read and delete all messages that are sent on the network and modify them in accordance with the set of available functions.

We additionally make the following assumptions about the mTLS handshake:

* The handshake verifies that both parties are in possesion of the private key corresponding to the certificates used for the handshake, without revealing them
* After the handshake both parties obtain the same secret and fresh 'master_secret'