# Client (User)

Clients have two ways to submit their transactions to the transaction orderer.

1. **Using secure-rpc**:\
   Clients send their signed raw transactions to secure-rpc. The secure-rpc retrieves the necessary encryption key and other data from the DKG, encrypts the transaction, and forwards it to the tx\_orderer. When the tx\_orderer responds with an encrypted pre-confirmation, the secure-rpc then provides the decryption key. This ensures that transactions can only be decrypted after encrypted pre-confirmations are received.
2. **Using radius-snap**:\
   Clients can generate or import their private key through the radius-snap. This allows the snap to sign raw transactions and encrypt them using an encryption key obtained from the DKG locally. Once signed and encrypted, the transaction is sent directly to the tx\_orderer.

### Client ↔ Secure RPC ↔ Tx\_Orderer

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption><p>via Secure RPC</p></figcaption></figure>

1. **Client** sends a raw transaction to Secure RPC.
2. **Secure RPC** fetches SKDE parameters and the encryption key from the Distributed Key Generation (DKG) Service.
3. **Secure RPC** encrypts the transaction.
4. **Secure RPC** sends the encrypted transaction to the tx\_orderer.

### Client ↔ Snap ↔ Tx\_Orderer

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption><p>via Radius Snap</p></figcaption></figure>

1. **Client** generates or imports a private key.
2. **Client** sends a raw transaction to the Snap.
3. **Snap** fetches SKDE parameters and the encryption key from the Distributed Key Generation (DKG) Service.
4. **Snap** encrypts the transaction using `.wasm`.
5. **Snap** sends the encrypted transaction to the tx\_orderer.

For details on **radius-snap**, refer to its [GitHub repository](https://github.com/radiusxyz/radius-snap).
