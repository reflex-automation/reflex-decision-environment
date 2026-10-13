# reflex-decision-environment

Decision Environment image for Reflex (community continuation of
Event-Driven Ansible) activations, replacing Red Hat's
`quay.io/ansible/ansible-rulebook` minimal DE. Pins `ansible-rulebook` and the
`ansible.eda` collection so activations keep working even if upstream stops
publishing images.

Published at `ghcr.io/reflex-automation/reflex-decision-environment`.

## Pins

| Component | Version | Source |
|---|---|---|
| ansible-rulebook | 1.3.2 | PyPI |
| ansible.eda collection | 2.13.0 | Galaxy |
| ansible-core | ~=2.20.7 | PyPI |
| base image | ubi9/python-312-minimal (digest-pinned) | registry.access.redhat.com |

## Build

```bash
ansible-builder build \
  --container-runtime docker \
  --tag reflex-decision-environment:1.3.2 \
  -v3
```

For an amd64 cluster node (when building on Apple Silicon):

```bash
ansible-builder build \
  --container-runtime docker \
  --tag reflex-decision-environment:1.3.2 \
  --extra-build-cli-args="--platform linux/amd64" \
  -v3
```

## Verify

```bash
docker run --rm reflex-decision-environment:1.3.2 ansible-rulebook --version
```

## Updating

Bump the pins in `execution-environment.yml`, rebuild, run a smoke-test
activation against Ascender (rulebook with `run_job_template`), then push to
the registry and update the Decision Environment entry in Reflex.

## License and attribution

Apache-2.0, see [LICENSE](LICENSE). The definition derives from the minimal
decision environment example in
[ansible/ansible-rulebook](https://github.com/ansible/ansible-rulebook)
(Apache-2.0, © Red Hat, Inc. and contributors). The built image aggregates
packages under their own licenses (ansible-core is GPL-3.0; the UBI9 base is
redistributed under Red Hat's UBI terms).
