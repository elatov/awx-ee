# awx-ee
## Setup prereqs
Install the necessary tools:

```bash
pip install --user ansible-builder
```

Clone the repo:

```bash
git clone git@github.com:elatov/awx-ee.git
cd awx-ee
```

Install docker and configure dockerhub credentials.

## Run the Build
Create your image:

```bash
ansible-builder build --tag elatov/awx-custom-ee:0.0.4
```

## Test the image locally
If you have docker installed you can run it locally and make sure a basic run succeeds:

```bash
> docker run --user 0 --entrypoint /bin/bash -it --rm elatov/awx-custom-ee:0.0.4  
bash-4.4# git clone git@github.com:elatov/ansible-tower-samples.git
bash-4.4# cd ansible-tower-samples
bash-4.4# ansible-playbook -vvv hello_world.yml
```

## Push Image to Docker Hub
If all is well push the image:

```bash
> docker push elatov/awx-custom-ee:0.0.4
```

## Test with AWX
If you using the [awx-operator](https://github.com/ansible/awx-operator), you can use the [Deploying a specific version of AWX](https://github.com/ansible/awx-operator#deploying-a-specific-version-of-awx) instructions to create an Execution Environment, by adding the following section:

```yaml
---
spec:
  ...
  ee_images:
    - name: custom-awx-ee
      image: elatov/awx-custom-ee:0.0.4
```

Then deploy your awx instance and run a sample test job to make sure it looks good.