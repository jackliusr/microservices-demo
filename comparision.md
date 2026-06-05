# Tiltfile vs skaffold.yaml Comparison

| Aspect | skaffold.yaml | Tiltfile | Status |
|--------|---------------|----------|--------|
| **Artifacts** | 12 images (email/productcatalog/recommendation/shoppingassistant/shipping/checkout/payment/currency/cart/frontend/ad/loadgenerator) | All 12 | Match |
| **Context dirs** | Same 12 mappings | Same 12 mappings | Match |
| **cartservice dockerfile** | Explicit `dockerfile: Dockerfile` | Implicit (same context `src/cartservice/src`) | Equivalent |
| **Platform** | `platforms: ["linux/amd64"]` | Not specified (host default) | Minor diff |
| **Tag policy** | `gitCommit` | Tilt default tagging | Equivalent |
| **BuildKit** | Explicit `useBuildkit: true` | Tilt uses BuildKit by default | Equivalent |
| **Manifests** | `kustomize(kubernetes-manifests)` | `k8s_yaml` listing 10 individual files | Diff — bypasses kustomize but deploys same YAML |
| **loadgenerator** | Separate config `requires: [app]` | `k8s_yaml` + `resource_deps=['frontend']` | Equivalent |
| **Port forwards** | None | `frontend: 8080` | Extra — Tilt-only nicety |
| **Profiles** | `gcb`, `debug`, `network-policies` | None | Missing — skaffold-specific features |
