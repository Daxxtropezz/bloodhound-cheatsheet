# BloodHound Queries Cheatsheet

A simple and organized list of commonly used BloodHound queries for Active Directory analysis.

---

## 📌 Shortest Path Queries

### **Find Shortest Path to Domain Admins**

```
MATCH p=shortestPath(
  (n:User {name:$USER})-[*1..]->(m:Group {name:"DOMAIN ADMINS@DOMAIN.LOCAL"})
)
RETURN p
```

### **Find Shortest Path to Enterprise Admins**

```
MATCH p=shortestPath(
  (n:User {name:$USER})-[*1..]->(m:Group {name:"ENTERPRISE ADMINS@DOMAIN.LOCAL"})
)
RETURN p
```

---

## 📌 Kerberoasting Queries

### **List All Kerberoastable Users**

```
MATCH (u:User)
WHERE u.hasspn=true
RETURN u.name AS KerberoastableUsers
```

### **Kerberoastable Accounts with Admin Rights**

```
MATCH (u:User)-[:MemberOf]->(g:Group)
WHERE u.hasspn=true AND g.name CONTAINS "ADMIN"
RETURN u.name, g.name
```

---

## 📌 AS-REP Roasting Queries

### **Users with "Do Not Require Pre-Auth" Enabled**

```
MATCH (u:User)
WHERE u.donotreqpreauth=true
RETURN u.name AS ASREP_RoastableUsers
```

---

## 📌 Local Admin Rights Queries

### **Users With Local Admin Rights on Any Machine**

```
MATCH (n:User)-[:AdminTo]->(c:Computer)
RETURN n.name AS User, c.name AS Computer
```

### **Groups With Local Admin Rights**

```
MATCH (g:Group)-[:AdminTo]->(c:Computer)
RETURN g.name AS Group, c.name AS Computer
```

---

## 📌 Lateral Movement Queries

### **Users With RDP Rights**

```
MATCH (n)-[:CanRDP]->(c:Computer)
RETURN n.name AS Principal, c.name AS Computer
```

### **Users With DCOM Access**

```
MATCH (n)-[:ExecuteDCOM]->(c:Computer)
RETURN n.name AS Principal, c.name AS Computer
```

### **Users Who Can Perform PSRemoting**

```
MATCH (n)-[:CanPSRemote]->(c:Computer)
RETURN n.name AS Principal, c.name AS Computer
```

---

## 📌 Privilege Escalation Queries

### **Users Eligible for Resource-Based Constrained Delegation (RBCD)**

```
MATCH (c:Computer)-[:AllowedToActOnBehalfOf]->(u:User)
RETURN c.name AS VulnerableComputer, u.name AS ControlledUser
```

### **Unconstrained Delegation Machines**

```
MATCH (c:Computer)
WHERE c.unconstraineddelegation=true
RETURN c.name AS UnconstrainedDelegationHosts
```

### **Users with Constrained Delegation Rights**

```
MATCH (u:User)-[:AllowedToDelegate]->(s:Computer)
RETURN u.name AS User, s.name AS Service
```

---

## 📌 Domain Trust Queries

### **Inbound Domain Trusts**

```
MATCH (d:Domain)-[:TrustedBy]->(t:Domain)
RETURN d.name AS Domain, t.name AS TrustedBy
```

### **Outbound Domain Trusts**

```
MATCH (d:Domain)-[:Trusts]->(t:Domain)
RETURN d.name AS Domain, t.name AS Trusts
```

---

## 📌 Group Membership Queries

### **List All Members of Domain Admins**

```
MATCH (u)-[:MemberOf*1..]->(g:Group {name:"DOMAIN ADMINS@DOMAIN.LOCAL"})
RETURN u.name AS Members
```

### **Users in High-Value Groups**

```
MATCH (u)-[:MemberOf*1..]->(g:Group)
WHERE g.highvalue=true
RETURN u.name AS User, g.name AS HighValueGroup
```

---

## 📌 High Value Targets

### **Show All High Value Objects**

```
MATCH (n)
WHERE n.highvalue = true
RETURN n.name AS HighValueObject, labels(n) AS Type
```

---

If you want, I can generate:

* A more advanced query set
* Separate files (beginner / intermediate / advanced)
* A visual graph map of recommended queries
* Color-coded categories for GitHub formatting
