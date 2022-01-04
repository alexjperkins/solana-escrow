# Escrow

An escrow smart contract (or program in solana parlance) essentially allows
a trusted third party to act as an intermediary for a given transactions once
certain conditions are met.

Alice & Bob don't trust one another to exchange some coin, S.

Alice can give the asset for the transaction to a third party, C.
Bob, the counter party can give the pair, U also to C.

Once both transactions:

- Alice (S) -> C
- Bob (U) ->

Have been finalized & confirmed by the network, then C can exchange the funds & complete the
original transaction.

- C (S) -> Bob
- C (U) -> Alice

If neither party completes the transaction to C under some condition (if any), then C simply returns
the funds back to party that made it.

In this context, C will be a smart contract (program) on the blockchain, in this case solana.
