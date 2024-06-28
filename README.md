# OpenShift Virtualization automation playground

This repo is a playground for automating OpenShift Virtualization.

## Content

The `openshift/` folder contains Kubernetes resources to configure AAP using the AAP operator.
Atm. it doesn't install the operator so you will have to do this manully.

The resources needs to be created in a particular order, ie. the Ansible Controller project must be created before the Job Templates can be created.

| Filename                            | Namespace  |                                                                                                                                  |
|:------------------------------------|------------|:---------------------------------------------------------------------------------------------------------------------------------|
| 10-automation-controller.yml        | aap        | Deploys an Ansible Automation Controller in the namespace                                                                        |
| 20-controller-connection-secret.yml | vmexamples | Creates a secret with a token to connect to the Automation Controller.<br>Token and controller URL must be added before running. |
| 30-aap-project.yml                  | vmexamples | Creates a project pointing to this repo                                                                                          |
| 40-sa-credentials.yml               | vmexamples | Setup a service account and add it as credentials in AAP                                                                            |
| 50-job-templates.yml                | vmexamples | Creates job templates for the playbooks in `ansible/`                                                                            |

The `ansible/` folder contains two simple playbooks to create and delete a virtual machine.

## Resources

- [Documentation for Ansible Resource Operator](https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.4/html/deploying_the_red_hat_ansible_automation_platform_operator_on_openshift_container_platform/assembly-controller-resource-operator)
- [Resource operator repository](https://github.com/ansible/awx-resource-operator)
- [kubevirt.core collection](https://kubevirt.io/kubevirt.core/main/index.html)
- [Managing Kubevirt VMs with Ansible](https://kubevirt.io/2023/Managing-KubeVirt-VMs-with-Ansible.html)
