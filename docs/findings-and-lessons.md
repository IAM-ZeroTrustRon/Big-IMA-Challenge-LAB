# Findings and lessons

Evidence IDs refer to the [register](evidence-register.md). “Observed” means supported by the session and artifacts, not an independent audit opinion. Root causes below describe policy mechanics, not unverified organizational motives.

## IAM01 — Public storage grants exposed objects

**Condition:** an unsigned request listed the allowed prefix and retrieved the tested object. **Criteria:** access should match the content's intended audience. **Cause:** wildcard principals were granted GetObject and prefix-conditioned ListBucket. **Impact:** names and contents were accessible without credentials. **Recommendation:** separate approved public assets from confidential content, constrain principals and enable appropriate public-access controls. **Lesson:** a listing prefix condition does not narrow a separate unrestricted object-read statement. **Evidence:** E01–E03; original read output withheld because it contains a flag.

## IAM02 — Broad queue access disclosed a useful resource link

**Condition:** unsigned ReceiveMessage was denied; the same operation using the provided challenge identity succeeded and disclosed an analytics URL. Opening it returned the answer. **Criteria:** consumers should be limited to approved application identities. **Cause:** the displayed resource policy grants wildcard-principal SendMessage/ReceiveMessage without conditions. **Impact:** a signed-in challenge identity could receive analytics content. **Recommendation:** restrict producers and consumers and review payload sensitivity. **Lesson:** wildcard policy text alone is not proof that an unsigned operation succeeds. **Evidence:** E04–E06 plus retained local signed response. SendMessage was not tested; message injection is a potential risk, not an observed result.

## IAM03 — Destination suffix check did not enforce the intended host

**Condition:** an HTTPS webhook with a query suffix matching the policy received a confirmation and then a notification. **Criteria:** subscription destinations and protocols should match the intended recipients. **Cause:** sns:Endpoint was checked as a wildcard string without restricting sns:Protocol; the suffix could appear in a URL query rather than its host. **Impact:** notification content reached an external lab-controlled endpoint. **Recommendation:** restrict subscribing principals and intended protocol/destination combinations; require review for destination changes. **Lesson:** matching endpoint text is not the same as validating delivery ownership. **Evidence:** E07–E08 and withheld local delivery originals.

## IAM04 — Admin restriction needs correct condition semantics

**Condition:** the displayed bucket policy applies ForAllValues:StringLike to aws:PrincipalArn and grants separate broad object reads. Completion is corroborated; the exact successful request sequence is pending from Gemini. **Criteria:** a principal restriction should reject missing or unintended identities. **Cause analysis:** AWS documents that ForAllValues can match absent keys and should not be used on single-valued keys. **Impact:** potential unintended access requires reconciliation with the original test outputs. **Recommendation:** use suitable principal/ARN conditions, require necessary context, and test signed, unsigned and unintended-principal requests. **Lesson:** completion evidence is not a substitute for a reproducible technical record. **Evidence:** E09/E14. This is policy analysis, not a newly reproduced exploit claim.

## IAM05 — Guest credentials could retrieve the tested private-bucket object

**Condition:** unsigned Cognito requests returned an identity and temporary credentials; STS identified the guest role; that role listed the bucket and retrieved the tested object. **Criteria:** guest permissions should cover only approved anonymous-user functionality. **Cause:** the guest role's permissions included the tested storage operations. **Impact:** no user login was needed to obtain credentials capable of reading that lab object. **Recommendation:** remove guest access if unnecessary; otherwise scope actions/resources to public guest functions and test boundaries. **Lesson:** an exposed identity pool ID is not itself a secret leak, and credentialed guest access is not anonymous S3 access. **Evidence:** E10–E14 and withheld read/credential originals.

## IAM06 — Trust policy accepted guest token for authenticated-named role

**Condition:** a guest Cognito identity token was accepted by AssumeRoleWithWebIdentity for Cognito_s3accessAuth_Role. STS confirmed the role; it enumerated buckets, listed the target bucket and retrieved the final object. It could not list the previous challenge's bucket. **Criteria:** a role intended for authenticated users should enforce the appropriate authentication-state claim as well as the trusted pool. **Cause:** the shown trust policy checks pool audience but omits the amr authenticated-state condition. **Impact:** the guest flow reached a different role and its tested data permissions. **Recommendation:** retain audience restriction, require the appropriate authenticated amr claim, review role permissions and verify guest denial versus legitimate authenticated access. **Lesson:** successful role assumption does not imply every resource is accessible; test each boundary. **Evidence:** E15–E19; final read original remains private.

## Skills demonstrated

AWS CLI, IAM JSON interpretation, S3/SQS/SNS access testing, Cognito federation, STS caller verification, positive/negative test comparison, technical troubleshooting, evidence preservation and plain-language risk communication. This work used step-by-step AI mentoring; it is not presented as an unassisted competition or professional penetration test.

## Official interpretation references

- [AWS condition key cardinality and ForAllValues](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-single-vs-multi-valued-context-keys.html)
- [Cognito role trust and permissions](https://docs.aws.amazon.com/cognito/latest/developerguide/iam-roles.html)
- [SNS HTTPS subscription endpoints](https://docs.aws.amazon.com/sns/latest/dg/sns-http-https-endpoint-as-subscriber.html)
