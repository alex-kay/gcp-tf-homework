# Terraform homework

![scheme](images/scheme.png)

# You should create an infrastructure, which is described on the diagram above

1. Create Network and private subnetwork.

2. Create 2 instances with LAMP stack. Instances should be in the private subnet and do not have public IP addresses.

3. You should be able to SSH to the instances with tag `ssh` only from your IP address.

4. Instance should be able to pull config from Cloud Storage.

5. LAMP stack should be installed on the instances during instance provisioning.

6. Instances should have access to the Internet.

7. Database should be in Cloud SQL service.

8. Password for database should be located inside secret manager.

9. HTMP page (index.html) should be located inside Cloud Storage bucket.

10. LAMP stack should be accessible over the internet using load balancer AND only from your IP address.

11. Backups for cloud SQL database should be configured.

## General rules

* Your code should be in EPAM GitLab repository and accessible for reviewers.

* You should create your infrastructure using one terraform command. Manual changes are not allowed.

* Terraform backend state should be in GCS.

* Needed attributes for your terraform code should be parametrized (Example: Customer may want to increase or decrease instance type if needed in some period of time).

* Use Terraform linters to meet all terraform best practices in code writing.

* Use Terraform modules as much as possible (when it is needed).

* Your infrastructure should follow best practices for GCP and Terraform.

## Homework setup

...

### Notes

Found a workaround for 'connect: cannot assign requested address' error when provisioning from CloudShell:

```bash
# Workaround https://github.com/hashicorp/terraform-provider-google/issues/6782
    sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1 net.ipv6.conf.default.disable_ipv6=1 net.ipv6.conf.lo.disable_ipv6=1 > /dev/null
    export APIS="googleapis.com www.googleapis.com storage.googleapis.com iam.googleapis.com container.googleapis.com cloudresourcemanager.googleapis.com"
    for name in $APIS
    do
      ipv4=$(getent ahostsv4 "$name" | head -n 1 | awk '{ print $1 }')
      grep -q "$name" /etc/hosts || ([ -n "$ipv4" ] && sudo sh -c "echo '$ipv4 $name' >> /etc/hosts")
    done
# Workaround end
```





## State

This is the graph of infrastructure right now (refactoring in progress):
![graph1](images/graph6.png)
