# Test Run Platform Seed Only

E2E test repo for the `kubernetes-run-platform-meta-environment` build in
buildon-github-actions.

Tests the defining RP behaviour: both children are `run-*` environments (the
two all-in-one env repos, so no cluster-scope delegation traffic muddies the
picture) and must be stamped `kaptain.org/apply-mode: seed-only` by the seed
partition. The deploy image carries one env var telling the deploy to pull
seed-only children out of the apply tree and give them the special seed
handling instead of applying them as part of the RP tree. Also covers RP
naming/derived names and the project-name-as-namespace rule for the
platform-owned set.

RP builds can themselves be job or deployment with keel or keelson, but that
part of the build is identical to the env side so it is deliberately not
re-tested here.

Children: `test-run-env-deployment-keel-all-in-one`,
`test-run-env-job-keelson-all-in-one`.

Pending notes:

- The draft `spec-kaptainpm-schema` must be faked into the build before this
  repo can build.
- Behaviour assertions (seed-only annotations present on staged children, env
  var present in the image) get added to the hooks once the reference scripts
  land.
