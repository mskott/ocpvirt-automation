# Decision environment for Event Driven Ansible

Event Driven Ansible require a decision environment to run the rulebook. If the rulebook use sources that are not part of any default decision environments, then you can create your own.

## Creating a decision environment

You need two things to create a decision environment:

- a defition file
- ansible-builder

You need to install the ansible-builder to create a decision environment. The ansible-builder can also be used to create execution environments.

Below is an example of a definition file that add the 'sabre1041.eda' collection to the decision environment.

```yaml
version: 3

images:
  base_image:
    name: 'registry.redhat.io/ansible-automation-platform-24/de-minimal-rhel8:latest'

dependencies:
  galaxy:
    collections:
      - sabre1041.eda
  python_interpreter:
    package_system: "python39"

options:
  package_manager_path: /usr/bin/microdnf
```

## Build the container image

To build the container image locally, execute the following command in the directory containing the provided `ansible builder file`:

   ```bash
   ansible-builder build -t decision-environment -f decision-environment.yml
   ```

## Push the container image to a registry

To push the container image in a remote repository log-in, tag and push the image:

   ```bash
   podman login <REGISTRY_HOST>
   podman tag decision-environment <REGISTRY_HOST>/<YOUR_USERNAME>/decision-environment
   podman push <REGISTRY_HOST>/<YOUR_USERNAME>/decision-environment
   ```

You now have a decision environment that you can use with EDA that include the collection(s) that you need for your rulebook.
