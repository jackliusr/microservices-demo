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

## Code Line Mapping

| Concept | skaffold.yaml lines | Tiltfile lines |
|---------|--------------------|----------------|
| **Config header** | 15–18 | — |
| **Artifact definitions** | 26–49 | 6–17 |
| — emailservice | 26–27 | 10 |
| — productcatalogservice | 28–29 | 13 |
| — recommendationservice | 30–31 | 14 |
| — shoppingassistantservice | 32–33 | 16 |
| — shippingservice | 34–35 | 15 |
| — checkoutservice | 36–37 | 8 |
| — paymentservice | 38–39 | 12 |
| — currencyservice | 40–41 | 9 |
| — cartservice (custom dockerfile) | 42–45 | 7 |
| — frontend | 46–47 | 11 |
| — adservice | 48–49 | 6 |
| **Platform** | 20 | — |
| **Tag policy / local build** | 50–54 | — |
| **Manifest loading** | 55–58 | 21–32 |
| **Deploy strategy** | 59–60 | — |
| **loadgenerator config** | 96–115 | — |
| — artifact | 106–107 | 17 |
| — manifest | 112–113 | 34 |
| — dependency | 100–102 | 40 (`resource_deps`) |
| **Port forwards** | — | 38 |
| **Resource deps** | — | 40 |
| **Profiles** | 69–94, 116–122 | — |
