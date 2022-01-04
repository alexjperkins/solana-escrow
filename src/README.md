# Solana program flow:

1. Someone calls the endpoint (presumabley via the program id of the program?) 
2. The entrypoint forward the arguments to the processor.
3. The processor asks `instruction.rs` to decode the `instruction_data` argument from the entrypoint function.
4. Using the decoded data, the processor will now decide whcih processing fucntion to use to process the request.
5. The processor may use `state.rs` to encode state into or decode the state of an account which has been passed into the entrypoint.

`instruction.rs` -> Defines the API of the program.

## Escrow program:

Because we have two parties will shall need two `system_program` accounts to hold said data.
Because Alice and Bob want to exchange tokens, we shall make use of the `token_program`.

In the `token_program` to exchange a token, you will need a token account. Both Alice & Bob will need 
a token account for each token. This means will we have **four** more accounts.

Alice -> X, Y token accounts
Bob -> X, Y token accounts

We will also require another account to store metadata about any deals or transactions between the two parties.
Remember programs in Solana are stateless.

This will be owned by the Escrow program.


## Account structure:
 
main account ->  token account USDT  -> mint address USDT (mint address stores token metadata around token supply for e.g)

             ->  token account SRM -> mint address SRM


Users will have a main account, that is owned by the `system_program`.

Associated to this main account, is a token account for each token.
This token account is owned by the main account of that user.
The token account defines a `mint` field which is the mint address of the token & stores metadata about the token such as supply.

Since the owner of the token accounts is the main account of the user, the user still only needs the private key of the main account
to sign any tx from any token account.

The token account is said to `belong` to the `mint`.

This also means that for our Escrow program; we will have to create 2 new temporary token accounts,
owned by the Escrow program to hold the two tokens whilst the tx is in flux.

Or in this case a Program Derived Account.


## Program Derived Account:

...
