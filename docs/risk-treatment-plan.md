# Proposed risk treatment plan

This plan translates training observations into hypothetical organizational actions. All actions remain proposed; no control was changed or retested on the challenge infrastructure. Priorities indicate review order for a confidential-data scenario, not CVSS or calculated risk scores.

| Finding | Business concern | Proposed owner | Priority | Proposed treatment | Closure evidence |
|---|---|---|---|---|---|
| IAM01 | Unapproved people can discover/read files | Data owner and cloud engineer | Before sensitive-data use | Separate public/confidential storage and restrict access | Unsigned list/read denied for confidential content; approved paths still work |
| IAM02 | Unapproved queue consumers can see workflow data | Application owner | Before sensitive-data use | Restrict approved producers/consumers; minimize payload content | Intended consumer works; unintended signed identity denied; producer tests separately documented |
| IAM03 | Notifications can reach an unintended destination | Messaging owner | Before sensitive notifications | Constrain subscribing principals, protocol and destination | Approved subscription accepted; query/path suffix tricks and disallowed protocols rejected |
| IAM04 | Identity restriction may not enforce its intent | IAM reviewer | Evidence reconciliation first | Recover original tests, correct condition type and scope | Reproduced baseline; missing-context and unintended-principal denial tests |
| IAM05 | Guest access extends to confidential objects | Application and IAM owners | Before confidential guest workflow | Disable unnecessary guest access or narrow guest permissions | Guest restricted to intended assets; authenticated use still works |
| IAM06 | Guest identity reaches an authenticated-only role | Identity platform owner | Before authenticated-only workflow | Enforce pool audience and intended authentication state; review permissions | Guest token rejected, intended authenticated identity accepted, resource boundaries tested |

## Healthcare interpretation

If an equivalent system processed clinical information, the data owner and privacy/security leads would assess relevance to access control, authentication and audit accountability. This is a hypothetical application, not proof of HIPAA applicability or a legal violation. No patient records were used. Current production residual risk is unassessed; only validated remediation could support a later risk-reduction claim.
