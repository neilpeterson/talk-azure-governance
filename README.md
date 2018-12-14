# Azure Blueprints demos

[![Build Status](https://nepeters-devops.visualstudio.com/azure-blueprints/_apis/build/status/azure-blueprints-CI?branchName=master)](https://nepeters-devops.visualstudio.com/azure-blueprints/_build/latest?definitionId=8?branchName=master)

## Azure RBAC

**Portal Intro to RBAC**

- Show subscription and established roles (1 owner, 1 reader)
- Log in as reader and attempt to create something
- Update reader to Restart VM (custom role) and show result

**Automation**

Create custom role with Azure CLI:

Two sample in the repo:

- [Read / Write Container Instances](./rbac/container-instances-all.json)
- [Restart Virtual Machines](./rbac/vm-restart.json)

**Read / Write Container Instances:**

```
cd ~/storage/speaking-engagements/talk-azure-governance/rbac
az role definition create --role-definition container-instances-all.json
```

Assign custom role with Azure CLI

```
cd ~/storage/speaking-engagements/talk-azure-governance/rbac
az role assignment create --role "Container Instances Read / Write" --assignee rebecca@nepeters.com
```

## Azure Policy

**Audit / Resource Group Location**

Manually create policy to demo portal and build in policy.

**Automation**

Create policy with Azure CLI:

Three sample in the repo:

- [Deny: Enforce naming by resource type](./policy/name-by-type/azuredeploy.json)
- [Deny: Enforce resource tag](./policy/tag-deny/azuredeploy.json)
- [Append: resource tag](./policy/tag-append/azuredeploy.json)

**Deny: Enforce naming by resource type**

Enforce a **naming convention** for a **named resource type**, **deny** if not met.

```
cd ~/storage/speaking-engagements/talk-azure-governance/policy/name-by-type
sh ./policyEnforceName.sh
```

**Deny: Enforce resource tag**

Enforce a tag, **deny** if not specified.

```
cd ~/storage/speaking-engagements/talk-azure-governance/policy/tag-deny
sh ./policyTagDeny.sh
```

**Append: resource tag**

Enforce a tag, **apply** if not specified.

```
cd ~/storage/speaking-engagements/talk-azure-governance/policy/tag-append
sh ./policyTagAppend.sh
```

**Audit:**

TODO - add policy that perhaps audits all resource group locations?

**Initiative:**

TODO - add CLI example for initiative.

## Azure Blueprints

**Manual Demo**

Create blueprint consisting of two of the above policies, and resource group, and Resource Manager template.

**Automation**

Currently no PowerShell or CLI support for Blueprints. I've included PowerShell scripts to demo the REST interface, they are rough. I've also configured a Azure DevOps pipeline to demonstrate CI/CD. If you would like access, let me know.

- [Blueprint](./blueprints/create-blueprint/blueprint-body.json)
- [Create Blueprint](./blueprints/create-blueprint/CreateUpdateBlueprint.ps1)
- [Assign Blueprint](./blueprints/assign-blueprint/AssignBlueprint.ps1)

**Rest Demo**

Create and Publish:

```
cd ~/storage/speaking-engagements/talk-azure-governance/blueprints/create-blueprint
pwsh ./CreateUpdateBlueprint.ps1
```

Assign:

```
cd ~/storage/speaking-engagements/talk-azure-governance/blueprints/assign-blueprint
pwsh ./AssignBlueprint.ps1
```

**Azure DevOps and Blueprints**

[![Build Status](https://nepeters-devops.visualstudio.com/azure-blueprints/_apis/build/status/azure-blueprints-CI?branchName=master)](https://nepeters-devops.visualstudio.com/azure-blueprints/_build/latest?definitionId=8?branchName=master)