# n2t-web
N2T Web content including:
- askspect.txt - The ARK Identifier Scheme
- cdl_ebi_prefixes.yaml - joint N2T/Identifiers.org prefix list
- compact_ids.html - Compact Identifiers (CURIEs)
- n2t_full_prefixes.yaml - full set of N2T prefix records
- n2t_prefixes.yaml - 
- Towards_Electronic_Persistence_Using_ARK_Identifiers.pdf


Sceptre Deployment
------------------

`buildspec.yaml` pushes images to ECR repository based on git tags.

two cycles:
- tag push builds
- scheduled builds

application updates
  triggers on git tag push to repo
  assigns built image the following tags:
  - <git-tag>
  - <git-tag>-<timestamp>

  example (assume git tag is semver "v2.4.6"):
  - v2.4.6
  - v2.4.6-20260910

regular patching updates
  triggers on AWS::scheduler::schedule
  retrive current deployed tag from manifest (ssm)
  checkout deployed tag
  assign tags as above

