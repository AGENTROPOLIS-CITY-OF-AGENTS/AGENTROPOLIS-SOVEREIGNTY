# AGENTROPOLIS Agent DID Runtime Standard v1

Status: System-wide identity baseline

## Constitutional rule

No autonomous entity executes without an identity. No identity acts without a mandate. No mandate implies unrestricted authority. Every privileged action produces a verifiable receipt.

## Authority chain

NEURO DID -> Delegation Credential -> Agent DID -> Mandate -> AEGIS Policy -> Capability Grant -> Tool/MCP/API -> Execution -> Signed Receipt -> Audit Ledger.

Agents MUST NOT impersonate the human root identity. Each persistent agent MUST operate under its own DID and cryptographic key material.

## Required agent identity envelope

Each agent identity record MUST include:

- `did`: globally unique agent DID
- `controller`: human or authorized parent DID
- `role`: declared operational role
- `district`: AGENTROPOLIS district membership
- `public_key`: verification material or reference
- `capabilities`: explicit allow-list
- `denied_capabilities`: explicit deny-list where applicable
- `delegation`: issuer, scope, audience, expiry, nonce/replay controls
- `budget`: token, compute, spend, and/or rate limits
- `policy`: AEGIS policy references
- `receipt_required`: boolean, default true for privileged actions

## Delegation

Delegation MUST be attenuating. A child agent can never receive more authority than the parent possesses or more than the parent was delegated for the current task.

Delegation credentials SHOULD be task-scoped, audience-bound, time-limited, revocable, and non-replayable.

## Execution corridor

Identity -> Mandate -> Plan -> Policy -> Capability -> Execute -> Receipt -> Audit

Execution MUST fail closed if identity verification, mandate validation, policy evaluation, or capability authorization fails.

## Receipts

Privileged actions MUST emit a signed receipt containing at minimum:

- agent DID
- controller/issuer DID
- mandate or delegation reference
- capability exercised
- target resource
- tool/provider identifier
- timestamp
- outcome
- policy decision reference
- execution hash or tamper-evident event identifier when available

## Root authority

The NEURO DID is a human root/controller identity. It authorizes agents; it is never copied into an agent persona, runtime credential, or tool identity.

## Cross-repo requirement

Any AGENTROPOLIS runtime, MCP gateway, policy layer, security layer, finance rail, deployment plane, mission-control surface, or agent registry MUST preserve this identity and delegation model at trust boundaries.
