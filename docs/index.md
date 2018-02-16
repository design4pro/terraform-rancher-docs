# Install Tectonic on Google Cloud Platform with Terraform

Use this guide to manually install a Rancher HA cluster on a GCP account.
## Getting Started

First, clone the Terraform Rancher repository:

``` bash
git clone https://github.com/design4pro/terraform-rancher.git
cd terraform-rancher
```

Initialise Terraform:

``` bash
terraform init platforms/gcp
```

Configure your GCP credentials. See the [Terraform Google provider](https://www.terraform.io/docs/providers/google/index.html) docs for details.

``` bash
export GOOGLE_APPLICATION_CREDENTIALS=~/.gcp/my-credentials.json
```

## Customize the deployment

Customizations to the base installation live in examples/terraform.tfvars.gcp. Export a variable that will be your cluster identifier:

``` bash
export CLUSTER=my-cluster
export GOOGLE_PROJECT=my-project-id
```

Create a build directory to hold your customizations and copy the example file into it:

```bash
mkdir -p build/${CLUSTER}
cp examples/terraform.tfvars.gcp build/${CLUSTER}/terraform.tfvars
```

Edit the parameters with your GCP details: project id, domain name, etc. [View all of the GCP specific options](/variables/gcp/) and the common [Rancher variables](/variables/)).

## Deploy the cluster

Test out the plan before deploying everything:

``` bash
terraform plan -var-file=build/${CLUSTER}/terraform.tfvars platforms/gcp
```

Next, deploy the cluster:

``` bash
terraform apply -var-file=build/${CLUSTER}/terraform.tfvars platforms/gcp
```

This should run for a little bit, and when complete, your Rancher HA cluster should be ready.
