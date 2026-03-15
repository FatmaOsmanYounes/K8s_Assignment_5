# Kubernetes ConfigMap & Secret Lab

## Student Information

**Name:** Fatma Osman Mahmoud

---

# Lab Overview

This lab demonstrates how to manage application configuration in Kubernetes using **ConfigMaps** and **Secrets**.

The lab focuses on:

* Creating ConfigMaps using the imperative method
* Injecting ConfigMap values into Pods
* Selective environment variable injection
* Creating and inspecting Kubernetes Secrets
* Injecting Secrets into containers
* Combining ConfigMaps and Secrets
* Using configuration in a scaled Deployment

These techniques are essential for separating **application configuration** from **container images**, which is a best practice in Kubernetes and modern DevOps environments.

---

# Technologies Used

* Kubernetes
* kubectl
* YAML configuration files
* BusyBox container image

---

# Repository Structure

To complete this lab, the repository is organized as follows:

```
├── cm-env.yaml        # Task 2: Inject all ConfigMap keys as environment variables
├── cm-sel.yaml        # Task 3: Selective ConfigMap injection
├── secret-env.yaml    # Task 5: Secret injection as environment variables
├── cmsec.yaml         # Task 6: Combined ConfigMap and Secret pattern
├── deploy-config.yaml # Task 7: Deployment using ConfigMap and Secret
```

Each file represents a specific Kubernetes configuration scenario related to environment variable management.

---

# Tasks Explanation

## Task 1 — Create ConfigMap

A ConfigMap named **app-config** was created using the imperative kubectl command.

The ConfigMap stores the following configuration values:

* APP_ENV
* APP_PORT
* APP_COLOR
* MAX_CONNECTIONS

This separates configuration from the container image.

---

## Task 2 — Inject ConfigMap as Environment Variables

File: **cm-env.yaml**

A Pod named **env-pod** loads all ConfigMap values using:

```
envFrom → configMapRef
```

This method automatically injects all keys as environment variables inside the container.

---

## Task 3 — Selective ConfigMap Injection

File: **cm-sel.yaml**

A Pod named **selective-pod** injects only specific keys from the ConfigMap.

Example mapping:

* APP_COLOR → COLOR
* APP_PORT → PORT

This method is useful when only specific configuration values are required.

---

## Task 4 — Create Secret

A Secret named **db-secret** was created to store database credentials:

* DB_USER
* DB_PASSWORD
* DB_NAME

Kubernetes stores Secret values encoded using **Base64**.

---

## Task 5 — Inject Secret as Environment Variables

File: **secret-env.yaml**

A Pod named **db-pod** loads Secret values using:

```
envFrom → secretRef
```

The container automatically receives decoded values as environment variables.

---

## Task 6 — Combined ConfigMap and Secret

File: **cmsec.yaml**

A Pod named **fullapp-pod** loads both:

* ConfigMap → application configuration
* Secret → database credentials

This pattern is commonly used in real production applications.

---

## Task 7 — Deployment Using ConfigMap and Secret

File: **deploy-config.yaml**

A Deployment named **webapp-configured** creates **3 replicas** of a Pod.

Each Pod receives configuration values from:

* ConfigMap → APP_ENV
* Secret → DB_USER and DB_PASSWORD

This ensures that all Pods share the same configuration automatically.

---

# Key Learnings

From this lab, the following Kubernetes concepts were practiced:

* Configuration management using ConfigMaps
* Secure credential storage using Secrets
* Environment variable injection
* Selective configuration usage
* Combining configuration sources
* Using configuration with Deployments
* Scaling applications with consistent configuration

---

# Conclusion

Using ConfigMaps and Secrets improves Kubernetes application design by separating configuration from application code.

This approach enables:

* Easier configuration updates
* Better security for sensitive data
* Consistent configuration across multiple Pods
* More flexible and maintainable deployments

---

**End of Lab**
