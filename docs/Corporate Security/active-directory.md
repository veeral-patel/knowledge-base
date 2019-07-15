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

## AD Tree or Forest?

- use a forest if you need to use more than 1 namespace
- one namespace: corp.com = 1 domain

```
One Domain:
sales.corp.com - 1 OU
finance.corp.com - 1 OU
```

- multiple namespaces - `corp.com`, `newcorp.com` = domains grouped in 1 forest

```
One Forest:
sales.corp.com - 1 OU
sales.newcorp.com - 1 OU
```

## Domains in the same forest share

- the same schema
- the same configuration partition (?)
- 2-way Kerberos trust
- a common "Enterprise Administrators" group
  - only group allowed to make forest-wide changes, like adding/removing a domain
- same global catalog

## Organizing with OUs

- each OU is in exactly 1 domain
- an OU can't contain objects from other domains

### Patterns for organizing a domain's objects into OUs

- object-based. domain has OUs for users, printers, computers. most flexible
- administrative
- division/department
- can assign an administrator to an OU

## Stable Domains and Transient OUs

- domains should be stable - objects should not move frequently btwn domains
  - base domains on geography, not department/function/etc
- OUs are for transient groupings, like project

## Example: `flexport.com` [root domain]

```
- us.flexport.com [domain]
  - users.eng.us.flexport.com [ou]
  - printers.eng.us.flexport.com [ou]
  - fileshares.eng.us.flexport.com [ou]
- asia.flexport.com [domain]
- eu.flexport.com [domain]
```

- here, you have a tree of domains

- now, if Flexport buys foobar.com (but keeps it independent), then it'll have
  2 trees - `flexport.com` and `foobar.com`
- Flexport can then combine `flexport.com` and `foobar.com` into a forest - so 1
  central group can administer both, the trees share a schema, etc

## Physical AD layout

- can replicate your domain controllers (DCs)
- can select domain controllers to store global catalogs
- guideline - have a DC at each branch office with >= 50 people to speed up authentication requests
- have a DC at any office with applications running which require AD authentication

## Managing users and groups

### Creating user objects

Open AD Users and Groups (ADUC) application from Server Manager in Windows Server

LDIFDE = import objects from LDIF file
CSVDE = import objects from CSV file

### Types of groups

- Domain local groups = only valid within their local domain
- Global groups = valid within specified domains
- Universal groups = valid across all domains in a forest

#### Uses of groups

- Security - to restrict access to specific people. Can give 1 group read-only access, another write access too, etc
- Distribution - say you wanted to email all employees in California
