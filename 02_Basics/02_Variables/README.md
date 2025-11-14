# 📘 Ansible Inventory

## 📌 What Is an Inventory?

The **Ansible inventory** is a list of systems that Ansible automates. It can contain:

* One or many hosts
* Multiple groups
* Group variables
* Host-specific variables

Inventories are usually file-based but can also come from **dynamic inventory sources**.

---

## 📄 Example Inventory (INI Format)

```ini
[myservers]
10.42.0.2
appserver01
appserver02
node1[1:20]
10.42.0.[100:130]
host1.saleh.miri
```

### This example includes:

* IP addresses
* Hostnames
* Range patterns
* Mixed host types in one group

---

## 📂 Inventory Format Types

Ansible supports multiple file formats for inventories. The two most common are:

---

## 1️⃣ INI Format

**Best for:**

* Small teams or startups
* Simple environments
* Easy-to-write static inventories

### Example:

```ini
[web]
web01
web02
```

---

## 2️⃣ YAML Format

**Best for:**

* Large enterprises
* Production-grade automated environments
* Complex structures with variables

### Example:

```yaml
all:
  children:
    web:
      hosts:
        web01:
        web02:
    db:
      hosts:
        db01:
```
