#### User story
As a DevOps team member, I want to build infrastructure _([AWS Scenario 2](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Scenario2.html))_ in AWS using [Terraform](https://www.terraform.io/) for development purpose.

If you don't have an AWS account, create [free-tier](https://aws.amazon.com/free/) one now.

<p align="center">
  <img src="../pics/aws-infra.png" alt="AWS infra" style="width: 250px;"/>
</p>

#### Assumptions
- Latest version of Docker is installed
- AWS credentials are available at: "~/.aws/credentials"
    ```
    [default]
    aws_access_key_id = <KEY>
    aws_secret_access_key = <SECRET>
    ```

#### Prerequisite if standing up a vagrant box
If of some reason docker can not be run natively on your platform, feel free to use the provided Vagrantfile to setup a VM which will have a docker engine installed. Vagrant coppies a number of files and folders (like aws credentials) from host to guest machine _(Modify the Vagrantfile as per your needs)_
- Run `vagrant up` command to create a VM
-	Run `vagrant ssh` to log into the VM

#### Instructions
On the platform where docker engine is installed, execute the following commands to clone this repo:
1. `alias git='docker run -it --rm --name git -v $PWD:/git -w /git indiehosters/git git'`
2. `git version`
3. `git clone https://github.com/shazChaudhry/infra.git`
4. `sudo chown -R $USER infra`
5. `cd infra/terraform/two-tier`

Terraform docker image is available at https://hub.docker.com/r/hashicorp/terraform/. Execute the following commands to run terraform:
1. `alias terraform='docker run -it --rm --name terraform -v ~/.ssh/id_rsa.pub:/home/root/.ssh/id_rsa.pub -v ~/.aws/credentials:/home/root/.aws/credentials -v $PWD:/terraform -w /terraform hashicorp/terraform'`
2. `terraform --version`
3. `terraform init`
4. `terraform plan -out=tfplan`
5. `terraform apply tfplan`
6. `terraform show`

#### Clean up
1. `terraform destroy -force`

#### References
- Tutorial: https://simonfredsted.com/1459
- AWS "Scenario 2" blog: https://nickcharlton.net/posts/terraform-aws-vpc.html
- AWS environment with Terraform: https://linuxacademy.com/howtoguides/posts/show/topic/13922-a-complete-aws-environment-with-terraform