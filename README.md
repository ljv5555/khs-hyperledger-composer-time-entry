# Configuration
This project can run at https://composer-playground.mybluemix.net/

  *or*

From Debian 9 (64-bit), install docker and docker compose, then as root spin up runtime:
```
cat install-hlfv1.sh | bash
```

# Basic Sample Business Network

> This is the "Hello World" of Hyperledger Composer samples, which demonstrates the core functionality of Hyperledger Composer by changing the value of an asset.

This business network defines:

**Participant**
`BillingParticipant`

**Asset**
`SampleAsset`

**Transaction**
`BillingTransaction`

**Event**
`SampleEvent`

SampleAssets are owned by a BillingParticipant, and the value property on a SampleAsset can be modified by submitting a BillingTransaction. The BillingTransaction emits a SampleEvent that notifies applications of the old and new values for each modified SampleAsset.

To test this Business Network Definition in the **Test** tab:

Create a `BillingParticipant` participant:

```
{
  "$class": "com.khs.billing.BillingParticipant",
  "participantId": "Toby",
  "firstName": "Tobias",
  "lastName": "Hunter"
}
```

Create a `SampleAsset` asset:

```
{
  "$class": "com.khs.billing.SampleAsset",
  "assetId": "assetId:1",
  "owner": "resource:com.khs.billing.BillingParticipant#Toby",
  "value": "original value"
}
```

Submit a `BillingTransaction` transaction:

```
{
  "$class": "com.khs.billing.BillingTransaction",
  "asset": "resource:com.khs.billing.SampleAsset#assetId:1",
  "newValue": "new value"
}
```

After submitting this transaction, you should now see the transaction in the Transaction Registry and that a `SampleEvent` has been emitted. As a result, the value of the `assetId:1` should now be `new value` in the Asset Registry.

Congratulations!
