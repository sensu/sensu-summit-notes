# Using Ansible to Manage Sensu


# Best Practices

* Divide responsibility (AKA: Monitoring as a Service):
  * Monitoring team provides monitoring infra and Ansible to deploy the client + stock checks
  * Dev team layers in monitors specific to their service
* Some teams use Jenkins to do twice-daily deployments via Ansible, just to make sure that deploys are as-expected
* Use forking to speed deployments
* Inventory
  * Some teams use a separate repo with all of the environments/inventory
    * Needed b/c part of it is Open Source, thus don't want to expose that info
  * Others keep it with their Ansible
* Managing access to dependencies (not Ansible-specific)
  * Some use Artifactory to cache and/or proxy packages
  * Others use dev-py and GemInABox
* Secrets management
  * Most use Ansible vault
  * Use different vault password per environment
* TLS key management
  * Some use a custom Docker container to generate certs, keystores per environment
  * FQDN-specific, not the wildcarded

# Auto-removal of checks

* Server is decommissioned or a check is removed from
  * Playbooks that hit Sensu API to clear stale hosts and stashes
    * Paul uses a pattern [similar to this](https://github.com/IBM/cuttle/blob/master/roles/elk/kibana/tasks/config.yml)
* Removing checks from a server
  * One team has an Ansible var that allows them to essentially rm -rf the checks, then their play lays them down new

# Pain Points

* Do people write/use proper Ansible Modules
  * One method: Takes Ansible dict and deploys the checks based on that dict
  * Another: YAML to Jinja2 templates


