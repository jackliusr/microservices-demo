# Generated from skaffold.yaml
# See https://skaffold.dev for the original config reference.

# ── Docker builds ────────────────────────────────────────────────────────────

docker_build('adservice',              'src/adservice')
docker_build('cartservice',             'src/cartservice/src')
docker_build('checkoutservice',        'src/checkoutservice')
docker_build('currencyservice',        'src/currencyservice')
docker_build('emailservice',           'src/emailservice')
docker_build('frontend',               'src/frontend')
docker_build('paymentservice',         'src/paymentservice')
docker_build('productcatalogservice',  'src/productcatalogservice')
docker_build('recommendationservice',  'src/recommendationservice')
docker_build('shippingservice',        'src/shippingservice')
docker_build('shoppingassistantservice', 'src/shoppingassistantservice')
docker_build('loadgenerator',          'src/loadgenerator')

# ── Deploy ───────────────────────────────────────────────────────────────────

k8s_yaml([
    'kubernetes-manifests/adservice.yaml',
    'kubernetes-manifests/cartservice.yaml',
    'kubernetes-manifests/checkoutservice.yaml',
    'kubernetes-manifests/currencyservice.yaml',
    'kubernetes-manifests/emailservice.yaml',
    'kubernetes-manifests/frontend.yaml',
    'kubernetes-manifests/paymentservice.yaml',
    'kubernetes-manifests/productcatalogservice.yaml',
    'kubernetes-manifests/recommendationservice.yaml',
    'kubernetes-manifests/shippingservice.yaml',
])

k8s_yaml('kubernetes-manifests/loadgenerator.yaml')

# ── Resource configuration ───────────────────────────────────────────────────

k8s_resource('frontend', port_forwards=8080)

k8s_resource('loadgenerator', resource_deps=['frontend'])
