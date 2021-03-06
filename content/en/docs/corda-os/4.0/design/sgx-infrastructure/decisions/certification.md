---
aliases:
- /releases/release-V4.0/design/sgx-infrastructure/decisions/certification.html
date: '2020-01-08T09:59:25Z'
menu: []
tags:
- certification
title: 'Design Decision: CPU certification method'
---

[![fg005 corda b](https://www.corda.net/wp-content/uploads/2016/11/fg005_corda_b.png "fg005 corda b")](https://www.corda.net/wp-content/uploads/2016/11/fg005_corda_b.png)


# Design Decision: CPU certification method


## Background / Context

Remote attestation is done in two main steps.


* Certification of the CPU. This boils down to some kind of Intel signature over a key that only a specific enclave has
access to.
* Using the certified key to sign business logic specific enclave quotes and providing the full chain of trust to
challengers.

This design question concerns the way we can manage a certification key. A more detailed description is
[here](../details/attestation.md)


## Options Analysis


### A. Use Intel’s recommended protocol

This involves using `aesmd` and the Intel SDK to establish an opaque attestation key that transparently signs quotes.
Then for each enclave we need to do several round trips to IAS to get a revocation list (which we don’t need) and request
a direct Intel signature over the quote (which we shouldn’t need as the trust has been established already during EPID
join)


#### Advantages


* We have a PoC implemented that does this


#### Disadvantages


* Frequent round trips to Intel infrastructure
* Intel can reproduce the certifying private key
* Involves unnecessary protocol steps and features we don’t need (EPID)


### B. Use Intel’s protocol to bootstrap our own certificate

This involves using Intel’s current attestation protocol to have Intel sign over our own certifying enclave’s
certificate that derives its certification key using the sealing fuse values.


#### Advantages


* Certifying key not reproducible by Intel
* Allows for our own CPU enrollment process, should we need one
* Infrequent round trips to Intel infrastructure (only needed once per microcode update)


#### Disadvantages


* Still uses the EPID protocol


### C. Intercept Intel’s recommended protocol

This involves using Intel’s current protocol as is but instead of doing round trips to IAS to get signatures over quotes
we try to establish the chain of trust during EPID provisioning and reuse it later.


#### Advantages


* Uses Intel’s current protocol
* Infrequent rountrips to Intel infrastructure


#### Disadvantages


* The provisioning protocol is underdocumented and it’s hard to decipher how to construct the trust chain
* The chain of trust is not a traditional certificate chain but rather a sequence of signed messages


## Recommendation and justification

Proceed with Option B. This is the most readily available and flexible option.

