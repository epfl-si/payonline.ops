# Configuration-as-code for payonline.epfl.ch

Based on [Ansible](https://docs.ansible.com/ansible/latest/index.html) and [ansible.suitcase](https://github.com/epfl-si/ansible.suitcase).

## Prerequisites

- Membership in Keybase groups `/keybase/team/epfl_payonline.preprod` and/or `/keybase/team/epfl_payonline.prod/`
- Access to EPFL's OpenShift managed by camptocamp, under namespaces `payonline-test` and/or `payonline-prod`

## Common Tasks

### Build a new image

This is unfortunately not yet integrated with Ansible or OpenShift.

```
git clone --recurse-submodules ssh://git@c4science.ch/diffusion/7764/payonline-epfl-ch.git
./payonline-epfl-ch/deploy_os.sh
```

### Push the configuration-as-code to test

This creates Kubernetes objects necessary for running the image and
connecting it to the outside world at https://payonline-preprod.epfl.ch/

```
./paysible
```

### Promote to Production

Likewise, but to https://payonline.epfl.ch/

```
./paysible --prod -t payonline.k8s,payonline.k8s.promote
```
