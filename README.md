# Awesome Windows Attestation [![Awesome](https://cdn.jsdelivr.net/gh/sindresorhus/awesome@d1b8710/media/badge.svg)](https://github.com/sindresorhus/awesome)

> A curated list of Windows attestation, endpoint integrity, TPM / CMS-signed
> reporting, DFIR, and post-quantum readiness tooling.

Attestation = producing **tamper-evident, verifiable evidence** that a system is
in the state it claims to be. On Windows this means TPM quotes, BitLocker
sealing, CMS-signed machine-health reports, and supply-chain provenance. This
list collects the tools, libraries, and methodology that make that real.

## Contents
- [Windows-native attestation](#windows-native-attestation)
- [TPM & crypto libraries](#tpm--crypto-libraries)
- [Supply-chain attestation](#supply-chain-attestation)
- [DFIR & endpoint integrity](#dfir--endpoint-integrity)
- [Post-quantum readiness](#post-quantum-readiness)
- [Methodology & reading](#methodology--reading)

## Windows-native attestation
- [zqm-attestation-toolkit](https://github.com/ZQM-Labs/zqm-attestation-toolkit) — Forensic PowerShell suite producing CMS-signed, SHA256-anchored machine-health reports. Independent 2nd-method verification discipline. *(Maintained by ZQM-Computing.)*
- [zqm-public-tools](https://github.com/ZQM-Labs/zqm-public-tools) — Sanitized PowerShell helpers for Windows attestation (safe subset of the toolkit).
- [zqm-security-policy](https://github.com/ZQM-Labs/zqm-security-policy) — Baseline Windows endpoint posture rules (policy-as-code).

## TPM & crypto libraries
- [google/go-attestation](https://github.com/google/go-attestation) — Libraries to abstract TPM interaction for attestation (Go).
- [keylime](https://github.com/keylime/keylime) — CNCF project to bootstrap & maintain trust on edge/cloud nodes via TPM.
- [GrapheneOS/Auditor](https://github.com/GrapheneOS/Auditor) — Hardware-based attestation & intrusion detection (reference for what good attestation looks like).

## Supply-chain attestation
- [in-toto/witness](https://github.com/in-toto/witness) — Pluggable framework for software supply-chain risk management & verification.
- [chainloop-dev/chainloom](https://github.com/chainloop-dev/chainloop) — SDLC evidence store & policy engine for supply-chain attestation.
- [zqm-attestation-briefs](https://github.com/ZQM-Labs/zqm-attestation-briefs) — Buyer-facing attestation methodology & sample outputs.

## DFIR & endpoint integrity
- [LOLBAS](https://github.com/LOLBAS-Project/LOLBAS) — Living Off The Land Binaries, Scripts and Libraries (attestation baselines must account for these).
- [awesome-forensics](https://github.com/cugu/awesome-forensics) — Curated forensic analysis tools & resources.
- [awesome-incident-response](https://github.com/meirwah/awesome-incident-response) — Curated incident-response tooling.

## Post-quantum readiness
- [zqm-pqc-readiness-toolkit](https://github.com/ZQM-Labs/pqc-readiness-toolkit) — NIST/ETSI/CNSA 2.0 post-quantum readiness for Windows fleets. *(Maintained by ZQM-Computing.)*
- [cloudflare/circl](https://github.com/cloudflare/circl) — Interoperable reusable cryptographic library (PQ algorithms).
- [bcgit/bc-csharp](https://github.com/bcgit/bc-csharp) — BouncyCastle.NET cryptography (PQ-capable).

## Methodology & reading
- **Independent 2nd-method verification** — every attestation claim should be confirmed by a separate, independent technique and labeled CONFIRMED / CORROBORATED / BLOCKED. See `zqm-attestation-toolkit`'s `verify-claims.ps1`.
- **CMS detached signatures** — sign payloads with `openssl cms -sign -nodetach` (DER); verify with `openssl cms -verify -partial_chain -purpose any`. The toolkit ships `verify_zq_sig.py` as a cross-platform verifier.
- **SHA256 anchoring** — hash every evidence artifact; store the hash chain alongside the report.

## Contributing
PRs welcome — add tools that produce or verify Windows attestation evidence.
Keep entries specific and link to source.

## License
[CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) — public domain.
