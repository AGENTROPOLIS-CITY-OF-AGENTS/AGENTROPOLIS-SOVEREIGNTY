# AGENTROPOLIS AGENT-ENTITY Runtime Binding Standard v1

Status: Identity and sovereignty extension

## Rule

A persistent AGENT-ENTITY may operate through multiple approved runtimes without duplicating identity.

Each runtime MUST use a subordinate runtime credential or verification method bound to the same persistent Agent DID / AGENT-ENTITY.

The human root identity MUST NOT be copied into an agent runtime. The persistent agent root credential SHOULD NOT be copied between runtimes.

## Binding model

```text
Human controller
  -> persistent Agent DID / AGENT-ENTITY
      -> runtime binding A
      -> runtime binding B
      -> runtime binding C
```

Each binding is independently scoped, expiring and revocable.

## Verification requirements

Before an existing entity receives a new runtime binding, the trust path MUST verify:

- Agent DID / entity identifier
- controller relationship
- ProofOfControl
- ProofOfContinuity
- runtime provenance
- credential reference
- revocation state

## Authority invariant

```text
IDENTITY CONTINUITY != AUTHORITY CONTINUITY
```

A newly bound runtime receives no inherited capability authority unless an applicable policy explicitly grants it.

## Secret handling

Runtime bindings MUST reference credentials; raw private keys and sealed secrets MUST NOT be placed into prompts, continuity passports, link codes, or model context.
