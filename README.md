# ZK Constraint Dataset

A dataset of zero-knowledge circuit examples for fine-tuning LLMs to identify insufficient constraints and other security vulnerabilities in ZK proof systems. Examples are framed as an auditor reviewing a piece of circuit / proof-system code and reporting the vulnerability and a fix.

## Scope

Originally Circom-only, the dataset now generalizes across ZK DSLs and frameworks. The shared system prompt reflects this:

> You are a Zero-Knowledge Proof security auditor. You review ZK circuits and proof-system code across DSLs and frameworks (such as Circom, Halo2, gnark, Arkworks, Cairo, Plonky3, and RISC Zero) to identify under-constrained signals, soundness and completeness violations, and other logical or cryptographic vulnerabilities.

Vulnerability classes covered include under-constrained / unconstrained signals, missing range and boolean checks, missing input bindings, comparator/field overflows, soundness and completeness breaks, nullifier/replay issues, and business-logic bypasses.

## Files

- `train.jsonl`: training examples (hand-written pedagogical circuits + audit-report-derived rows).
- `valid.jsonl`: held-out validation examples.
- `synthetic.jsonl`: additional synthetic examples.
- `zk_security.jsonl`: examples derived from public security audit findings; every row carries a `source` object.

## Data Sources

Audit-derived rows are built from the public [zkbugs](https://github.com/zksecurity/zkbugs) collection of ZK vulnerability reports and from public security advisories, issues, and pull requests. Findings are credited to their auditors (Veridise, ZKSecurity, Zellic, Trail of Bits, ABDK, yAcademy, Matter Labs, OpenZeppelin, HashCloak, Least Authority, NCC Group, Hexens, Inference, and independent researchers) in each row's `source` object. Where the original codebase is available the vulnerable code is used verbatim; otherwise the circuit is faithfully reconstructed from the finding's description, location, and proposed mitigation. Every audit-derived row includes a `source` object (`name`, `link`, `protocol`) so readers can open the underlying report.

## License

Original dataset structure, synthetic examples, and editorial content are released under MIT.

Audit-derived rows are based on code from upstream projects and inherit their respective licenses as documented in the table below. Users must comply with the upstream license for any rows they use or redistribute. This dataset's only source-available (non-open-source) license is BSL-1.1 (see note on Panther Protocol).

### Upstream code provenance & licensing

Each audit-derived example is based on code from the upstream project listed below. The license shown is the project's declared license; review and comply with it before redistributing or training on the corresponding rows.

<!-- LICENSE_TABLE_START -->
| Project | Upstream repository | License | Auditor(s) | Rows |
|---|---|---|---|---|
| Aptos Keyless | [aptos-labs/keyless-zk-proofs](https://github.com/aptos-labs/keyless-zk-proofs) | `GPL-3.0` | koukyosyumei | 1 |
| Arianee | [Arianee/arianee-sdk](https://github.com/Arianee/arianee-sdk) | `MIT` (package.json) | Veridise | 2 |
| arkworks r1cs-std | [arkworks-rs/r1cs-std](https://github.com/arkworks-rs/r1cs-std) | `MIT OR Apache-2.0` | arkworks | 1 |
| Blake3 Circom | [banyancomputer/hot-proofs-blake3-circom](https://github.com/banyancomputer/hot-proofs-blake3-circom) | `MIT` | koukyosyumei | 1 |
| circom-bigint | [0xbok/circom-bigint](https://github.com/0xbok/circom-bigint) | `GPL-3.0` | Veridise | 1 |
| circomlib | [iden3/circomlib](https://github.com/iden3/circomlib) | `LGPL-3.0` | Kobi Gurkan, Veridise | 9 |
| Filecoin rust-fil-proofs | [filecoin-project/rust-fil-proofs](https://github.com/filecoin-project/rust-fil-proofs) | `MIT OR Apache-2.0` | Trapdoor Tech | 1 |
| gnark | [Consensys/gnark](https://github.com/Consensys/gnark) | `Apache-2.0` | Consensys | 1 |
| Herodotus | [HerodotusDev/offchain-evm-headers-processor](https://github.com/HerodotusDev/offchain-evm-headers-processor) | `GPL-3.0` | ABDK | 7 |
| iden3 circuits | [iden3/circuits](https://github.com/iden3/circuits) | `GPL-3.0` | Trail of Bits | 1 |
| Lurk | [lurk-lab/lurk-rs](https://github.com/lurk-lab/lurk-rs) | `MIT OR Apache-2.0` | Inference | 5 |
| MACI | [privacy-scaling-explorations/maci](https://github.com/privacy-scaling-explorations/maci) | `MIT` | HashCloak | 1 |
| Neptune | [lurk-lab/neptune](https://github.com/lurk-lab/neptune) | `MIT OR Apache-2.0` | Inference | 1 |
| OpenVM | [openvm-org/openvm](https://github.com/openvm-org/openvm) | `MIT OR Apache-2.0` | OpenVM | 2 |
| Panther Protocol | [pantherfoundation/panther-core](https://github.com/pantherfoundation/panther-core) | **`BSL-1.1`** at audited commit → since relicensed **`LGPL-3.0`** (see note) | Veridise | 12 |
| Penumbra | [penumbra-zone/penumbra](https://github.com/penumbra-zone/penumbra) | `MIT OR Apache-2.0` | NCC Group, ZKSecurity | 4 |
| Polygon zkEVM | [0xPolygonHermez/zkevm-proverjs](https://github.com/0xPolygonHermez/zkevm-proverjs) | `AGPL-3.0` | Hexens | 2 |
| Rarimo Passport | [rarimo/passport-zk-circuits](https://github.com/rarimo/passport-zk-circuits) | `MIT` | koukyosyumei | 1 |
| RISC Zero | [risc0/risc0](https://github.com/risc0/risc0) | `Apache-2.0` | RISC Zero | 3 |
| RLN | [Rate-Limiting-Nullifier/circom-rln](https://github.com/Rate-Limiting-Nullifier/circom-rln) | `MIT OR Apache-2.0` | Veridise | 1 |
| Scroll MPT | [scroll-tech/mpt-circuit](https://github.com/scroll-tech/mpt-circuit) | `MIT` | Trail of Bits, Zellic | 7 |
| Scroll Poseidon | [scroll-tech/poseidon-circuit](https://github.com/scroll-tech/poseidon-circuit) | `Apache-2.0` | Zellic | 1 |
| Scroll zkEVM | [scroll-tech/zkevm-circuits](https://github.com/scroll-tech/zkevm-circuits) | `MIT` | Trail of Bits, Zellic | 26 |
| Self Protocol | [selfxyz/self](https://github.com/selfxyz/self) | `MIT` (circuits package; monorepo is per-package) | ZKSecurity | 8 |
| Semaphore | [semaphore-protocol/semaphore](https://github.com/semaphore-protocol/semaphore) | `MIT` | Veridise | 1 |
| Sismo Hydra-S2 | [sismo-core/hydra-s2-zkps](https://github.com/sismo-core/hydra-s2-zkps) | `MIT` | Veridise | 1 |
| SIV | [siv-org/verifiable-private-overrides](https://github.com/siv-org/verifiable-private-overrides) | `ISC` (package.json) | koukyosyumei | 2 |
| SP1 | [succinctlabs/sp1](https://github.com/succinctlabs/sp1) | `MIT OR Apache-2.0` | Succinct | 6 |
| Spartan-ECDSA | [personaelabs/spartan-ecdsa](https://github.com/personaelabs/spartan-ecdsa) | `MIT` (package.json) | yAcademy | 3 |
| StarkEx Perpetual | [starkware-libs/stark-perpetual](https://github.com/starkware-libs/stark-perpetual) | `Apache-2.0` | ABDK | 1 |
| Summa | [summa-dev/summa-solvency](https://github.com/summa-dev/summa-solvency) | `Apache-2.0` | Summa | 1 |
| Tangle Network | [tangle-network/protocol-solidity](https://github.com/tangle-network/protocol-solidity) | `MIT OR Apache-2.0` | Veridise | 1 |
| Telepathy | [succinctlabs/telepathy-circuits](https://github.com/succinctlabs/telepathy-circuits) | `GPL-3.0` | Trail of Bits, Veridise | 6 |
| UniRep | [Unirep/Unirep](https://github.com/Unirep/Unirep) | `MIT` | Veridise | 2 |
| WORM Proof of Burn | [worm-privacy/proof-of-burn](https://github.com/worm-privacy/proof-of-burn) | `MIT` | koukyosyumei | 1 |
| ZK Email | [zkemail/zk-email-verify](https://github.com/zkemail/zk-email-verify) | `MIT` | Matter Labs, ZKSecurity | 5 |
| Zkopru | [zkopru-network/zkopru](https://github.com/zkopru-network/zkopru) | `GPL-3.0` | Least Authority | 2 |
| zkSync Social Login | [Moonsong-Labs/zksync-social-login-circuit](https://github.com/Moonsong-Labs/zksync-social-login-circuit) | `MIT` (package.json) | OpenZeppelin | 2 |
<!-- LICENSE_TABLE_END -->

Notes:
- Licenses for the Circom projects were read from the `LICENSE`/`package.json` at the exact **audited commit** the code was taken from; for the other projects the value is GitHub's detected SPDX license on the default branch. Where a project's license changed over time, the table reflects the version relevant to the code we used.
- ⚠️ **Panther Protocol license change.** At the **audited commit** the code we used was licensed under the **Business Source License 1.1 (`BSL-1.1`)**, a source-available (not OSI-approved, not open-source) license with use restrictions. The project has **since relicensed upstream to `LGPL-3.0`**. The 12 Panther-derived rows reflect `BSL-1.1`-era code, so evaluate them against `BSL-1.1` terms (the `LGPL-3.0` relicensing does not necessarily apply retroactively to that commit). This is the dataset's only source-available (non-open-source) license.
- `MIT OR Apache-2.0` denotes dual-licensed projects (two `LICENSE-*` files); recipients may choose either license.
- Sources without a clear, verifiable license were **excluded** from the dataset: Dark Forest (`darkforest-v0.3`, all rights reserved / review-only), Inference Labs Subnet (`subnet-2-circom`, no license declared), and Reclaim Chacha20 (`circom-chacha20`, repository no longer reachable). Rows derived from these projects have been removed from all `*.jsonl` files.
- License identifiers are provided for convenience and are not legal advice.

## Data Format

Each line in a JSONL file is one complete training example. Audit-derived rows include a `source` object; purely synthetic examples may omit it.

```json
{
  "messages": [
    {"role": "system", "content": "You are a Zero-Knowledge Proof security auditor. You review ZK circuits and proof-system code across DSLs and frameworks (such as Circom, Halo2, gnark, Arkworks, Cairo, Plonky3, and RISC Zero) to identify under-constrained signals, soundness and completeness violations, and other logical or cryptographic vulnerabilities."},
    {"role": "user", "content": "Audit this circuit for vulnerabilities:\n\n```circom\n...```"},
    {"role": "assistant", "content": "Vulnerability: ...\n\nExplanation: ...\n\nFix: ...\n\n```circom\n...```"}
  ],
  "source": {
    "name": "...",
    "link": "https://...",
    "protocol": "..."
  }
}
```

The fenced code block in the `user` / `assistant` turns is tagged with the relevant language (`circom`, `rust`, `go`, `cairo`, ...) for non-Circom examples.

## Related

- Hugging Face dataset: [mourningdove/zk-constraint-data](https://huggingface.co/datasets/mourningdove/zk-constraint-data)

## Deploying

To deploy a new version of the dataset, we use the following command:

```
hf upload mourningdove/zk-constraint-data . --repo-type=dataset
```
