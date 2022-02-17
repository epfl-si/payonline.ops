# Configuration-as-code for payonline.epfl.ch

Based on [Ansible](https://docs.ansible.com/ansible/latest/index.html) and [ansible.suitcase](https://github.com/epfl-si/ansible.suitcase).

## Prerequisites

- Membership in Keybase groups `/keybase/team/epfl_payonline.preprod` and/or `/keybase/team/epfl_payonline.prod/`
- Access to EPFL's OpenShift managed by camptocamp, under namespaces `payonline-test` and/or `payonline-prod`

## Common Tasks

### Push the configuration-as-code to test

```
./paysible
```

### Build a new image

```
./paysible -t payonline.k8s.build
```

💡 Passing the `payonline.k8s.build` tag forces the build to start now (even if the relevant Kubernetes objects have no changes)

This makes the latest version of the application available at https://payonline-preprod.epfl.ch/


### Promote to Production

Once the tests are satisfactory, here is how to push the exact same image onto https://payonline.epfl.ch/ :

```
./paysible --prod -t payonline.k8s,payonline.k8s.promote
```
