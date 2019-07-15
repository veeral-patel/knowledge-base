# Active Directory

From [Active Directory for Dummies](https://www.amazon.com/Active-Directory-Dummies-Steve-Clines/dp/0470287209)

## Physical vs logical parts of AD

- Physical part = domain controllers AD runs on
- Logical part = modelling your org with AD

## Services in the AD Umbrella

1. AD Domain Services (ADDS)
2. AD LDAP - ADDS with fewer features
3. AD Federation Services - SSO service
4. AD Certificate Services - create CAs, renew/revoke public key certs
5. AD Rights Management Services - create policies like user can't email doc to unauthorized ppl

## Components of AD

### Domain

- has at least 1 domain controller
- directory database - replicated btwn all DCs
- can create child domains to form a tree of domains

### Forest

- a forest is a group of trees that share the same schema and global catalog

### OUs and Objects

- OUs = "folders". for example - "west", "east"
- Objects - have an object class and attributes

### Schema

- lists object classes available
- for each object class, you must specify name, Object Identifier, required attributes, optional attributes
- AD installed with a base schema by default

### Global Catalog

- indexes all the objects in a forest so they're searchable
- but only indexes attributes you specify in the schema
