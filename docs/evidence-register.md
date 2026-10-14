# Evidence register

Original selected screenshots are retained unchanged. Images are linked rather than repeated throughout the repository. Credential dumps, confirmation tokens, unsubscribe links, and flag-bearing images are excluded from this public checkout; their originals remain in the local archive outside this repository.

| ID | Artifact and scope |
|---|---|
| E01 | [S3 public grants and prefix condition](../evidence/01-s3-policy.png) |
| E02 | [Unsigned prefix listing succeeded](../evidence/02-s3-anonymous-listing.png) |
| E03 | [Challenge 1 accepted; 10 points](../evidence/03-challenge-1-success.png) |
| E04 | [SQS resource policy](../evidence/04-sqs-policy.png) |
| E05 | [Unsigned ReceiveMessage denied](../evidence/05-sqs-anonymous-denied.png) |
| E06 | [Progress after Challenge 2](../evidence/06-score-20.png) |
| E07 | [Endpoint suffix condition without protocol restriction](../evidence/07-sns-policy.png) |
| E08 | [Challenge 3 accepted](../evidence/08-challenge-3-success.png) |
| E09 | [ForAllValues on principal ARN; technical handoff pending](../evidence/09-admin-bucket-policy.png) |
| E10 | [Public pool ID and application resource reference](../evidence/10-cognito-client-configuration.png) |
| E11 | [Unsigned GetId returned identity](../evidence/11-cognito-guest-id.png) |
| E12 | [Guest role caller identity verified](../evidence/12-cognito-guest-role.png) |
| E13 | [Guest role listed the lab bucket](../evidence/13-guest-bucket-listing.png) |
| E14 | [50 points and challenges 1–5 completed](../evidence/14-score-50.png) |
| E15 | [Pool audience constrained; authentication-state condition absent](../evidence/15-auth-role-trust-policy.png) |
| E16 | [Target role assumed using Cognito token](../evidence/16-auth-role-caller.png) |
| E17 | [New role denied listing on prior bucket](../evidence/17-prior-bucket-denied.png) |
| E18 | [Role could enumerate bucket names](../evidence/18-bucket-enumeration.png) |
| E19 | [Role listed target objects](../evidence/19-target-bucket-listing.png) |
| E20 | [User-provided completion certificate; printed June 2023](../evidence/20-completion-certificate.png) |

## Evidence limitations

- Challenge 2 signed ReceiveMessage and linked-object retrieval were observed in the working session. Public screenshots retain the policy, negative anonymous test, and subsequent score; the full received message is withheld because it includes operational message details.
- Challenge 3 delivery was observed at an external webhook. Raw delivery and confirmation screenshots are withheld because they include answer/token/subscription details; the policy and accepted result remain public.
- Challenge 4 completion is corroborated by E14. Its exact testing sequence and original outputs remain pending from Gemini; the policy analysis is not presented as a reproduced exploit.
- Challenge 5/6 object reads were observed in the session; originals contain flags and are not public. E20 is the supplied overall completion certificate; no final 60-point scoreboard screenshot was supplied.
- The certificate prints “June 2023.” The documented working session occurred October 14, 2026. The artifact is not altered and its printed date is not used as the exercise date. It is a CTF completion artifact, not AWS professional certification.

File hashes are in [SHA256SUMS](../evidence/SHA256SUMS.txt). Screenshots may show challenge-provided account, role and resource identifiers; these are lab context, not personal cloud credentials.
