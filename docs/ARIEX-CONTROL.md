# ARIEX Control Contract

## Role
Reusable GitHub Actions and automation workflow library.

## Observed baseline
- Python CI
- Node CI
- Security scanning
- Docker build/publish workflows

## Advanced upgrade track
1. Pin third-party actions to immutable SHAs.
2. Add reusable workflow contract tests.
3. Add OIDC-based cloud authentication instead of long-lived credentials.
4. Add SBOM/provenance generation.
5. Add concurrency and cancellation policies.
6. Publish workflow compatibility and security status to the fleet dashboard.

## Definition of done
A reusable workflow must be independently testable, least-privilege, provenance-aware and fail closed on security/test failures.
