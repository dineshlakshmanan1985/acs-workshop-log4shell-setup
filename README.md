## Red Hat Advanced Cluster Security demo/workshop for log4shell Vulnerability Demo

### What is Log4Shell?
Log4Shell is a software vulnerability in [Apache Log4j 2](https://logging.apache.org/log4j/2.x/), a popular Java library for logging error messages in applications. The vulnerability, published as [CVE-2021-44228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44228), enables a remote attacker to take control of a device on the internet if the device is running certain versions of Log4j 2.

[Apache issued a patch](https://logging.apache.org/log4j/2.x/security.html#cve-2021-44228) for CVE-2021-44228, version 2.15, on December 6, 2021. However, this patch left part of the vulnerability unfixed, resulting in [CVE-2021-45046](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45046) and a second patch, version 2.16, released on December 13. Apache released a third patch, version 2.17, on December 17 to fix another related vulnerability, [CVE-2021-45105](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-45105). They released a fourth patch, 2.17.1, on December 28 to address another vulnerability, [CVE-2021-44832](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44832).

Attackers can exploit the vulnerability using text messages to control a computer remotely. The Apache Software Foundation, which publishes the Log4j 2 library, gave the vulnerability a [CVSS score](https://nvd.nist.gov/vuln-metrics/cvss) of 10 out of 10, the highest-level severity score, because of its potential for widespread exploitation and the ease with which malicious attackers can exploit it. While mitigation evolves and the damage unfolds, the fundamentals of the Log4j vulnerability won’t change.


### Prereqs for demo setup
1. Deploy the "Openshift 4 Advanced Cluster Security 3" catalog offering in RHPDS (under Multi-Product Demo)
2. Deploy an "AWS Blank Open Environment" in RHPDS (under Red Hat Open Environments)
3. Log in to your cluster (as an admin user) with `oc login`
4. Export the following environment variables (add your credentials and update region if desired)
    ```
    export AWS_ACCESS_KEY_ID=myaccesskeyid
    export AWS_SECRET_ACCESS_KEY=mysecretaccesskey
    export AWS_REGION=us-east-2
    ```
5. Depending on choice for this demo, you can demonstrate this use case with OpenShift(default) and/or any xKS clusters.    
6. Install Ansible dependencies on control node
   - Ansible 2.9
   - python3-boto
   - python3-boto3
   - python3-kubernetes
7. Install Ansible collections
   ```
   ansible-galaxy install -r requirements.yml
   ```
8. Ensure you have a public ssh key located at `~/.ssh/id_rsa.pub`

### Deploy
1. Execute `ansible-playbook site.yml`
2. Playbook will output required information
3. Be sure to add `ROX_API_TOKEN` to your environment variables (or store it for later)

### Notes
1. If you need to re-run this playbook multiple times, you can skip downloading the exploit server archive with `ansible-playbook site.yml --skip-tags="download_jndi"`
