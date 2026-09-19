# AIAB enclave release configuration

This directory contains only measured deployment settings, a policy manifest, and a pinned measurement workflow. The measured v0.1.1 release uses CVM 0.14.9 and passed live enclave acceptance on 2026-09-19.

Application image: `ghcr.io/lucid-computing-labs/aiab-introspection-enclave@sha256:e42c2af9be20bd0aac1550f216b104b88f7f73121797558818c177b786e7f0db`

Offline policy digest: `8d03b314f111446aba77f1b944fda015919b0e0e222b0026b9057fee47cc1092`

Measured Tinfoil release digest (v0.1.1): `34b158a1d180c004daa1e0fde014848726be04c0b4506da6b6ed861ee264496c`.

Live enclave: `aiab-introspection.lucid-computing.containers.tinfoil.dev`.
Independent verification matched the release and policy digests above; the verified
gateway then passed allowed, blocked, signed-report, wrong-pin, direct-token
rejection, and public-route checks. The exact accepted container is scheduled to
stop on 2026-09-26 at 04:12:28 UTC.

The runtime image is **PRIVATE** and contains executable AIAB source and classifier definitions. The source GitHub repository also remains **PRIVATE**. Only this small measured configuration repository is public. Tinfoil must pull the private image using its configured registry credential; image visibility and shared credentials must not be changed to work around access failures.

Repository secrets: TINFOIL_API_KEY, ANTHROPIC_API_KEY, AIAB_GATEWAY_TOKEN. Secret values never belong in this repository. Standard Tinfoil deployment secrets are accessible to Tinfoil infrastructure.

## Image verification

Source commit: `85dbae29ec47915caa4e917174a8674afaa4f0f5` (private source repository).

Two independent clean local builds from the committed source, with GitHub checkout file modes (0644 files, 0755 directories), matched the published registry manifest digest exactly. The local development checkout uses 0664 source files; its earlier digest differs because COPY preserves those permissions.

Image config digest: `sha256:e22afb3f006bbb4940ece646e67561f2d20a91fe7dda2eae37c4b7980d93085b`. Both OCI exports were inspected across all layers and contain no Python bytecode or application cache directories.

This public config contains no provider credentials or private repository history. The private runtime image contains the application and classifier definitions; those files are not published by this configuration repository. Browser TLS terminates at the host, and governed inference is sent to Anthropic over HTTPS; neither is claimed to execute confidentially.
