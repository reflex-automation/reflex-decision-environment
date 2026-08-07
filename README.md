# eda-decision-environment

Decision Environment image for EDA activations, replacing Red Hat's
`quay.io/ansible/ansible-rulebook` minimal DE. Pins `ansible-rulebook` and the
`ansible.eda` collection so activations keep working if Red Hat stops
publishing images.

## Pins

| Component | Version | Source |
|---|---|---|
| ansible-rulebook | 1.3.1 | PyPI |
| ansible.eda collection | 2.13.0 | Galaxy |
| ansible-core | ~=2.20.7 | PyPI |
| base image | ubi9/python-312-minimal | registry.access.redhat.com |

## Build

```bash
conda activate /Users/sm0049/miniconda3/ansible
ansible-builder build \
  --container-runtime docker \
  --tag eda-decision-environment:1.3.1 \
  -v3
```

For the amd64 k3s node (when building on Apple Silicon):

```bash
ansible-builder build \
  --container-runtime docker \
  --tag eda-decision-environment:1.3.1 \
  --extra-build-cli-args="--platform linux/amd64"
```

## Verify

```bash
docker run --rm eda-decision-environment:1.3.1 ansible-rulebook --version
```

## Updating

Bump the pins in `execution-environment.yml`, rebuild, run a smoke-test
activation against Ascender (rulebook with `run_job_template`), then push to
your registry and update the Decision Environment entry in EDA.
