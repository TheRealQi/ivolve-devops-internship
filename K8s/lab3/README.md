# Kubernetes Lab 3: Managing Configuration and Sensitive Data with ConfigMaps and Secrets

This lab demonstrates how to manage configurations and sensitive data using Kubernetes `ConfigMaps` and `Secrets`.

----------

## Tasks Overview

- Define a ConfigMap to store non-sensitive MySQL configuration variables:
	- DB_HOST – The hostname of the MySQL StatefulSet service.
	- DB_USER – The database user that the application will use to connect to the ivolve database.
- Define a Secret to store sensitive MySQL credentials securely:
	- DB_PASSWORD – The password for the DB_USER.
	- MYSQL_ROOT_PASSWORD – The root password for MySQL database.
- Use base64 encoding for the Secret data values
      
----------

## Steps and Screenshots

### 0. Prerequisites:
- Namespace `ivolve` exists, which is created in a previous Kubernetes lab.

### 1. Create the ConfigMap

Create a ConfigMap YAML file called `mysql-configmap.yaml` with the following content to include the DB host and user:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mysql-config
  namespace: ivolve
data:
  DB_HOST: mysql-service
  DB_USER: backend
```
----------

### 2. Create the Secret

#### 2.1 Encode the secrets with base64
Secrets in Kubernetes must be base64 encoded beforehand. 
To encode our secrets, we can use the `base64` command in Linux to do so:
```bash
echo -n 'backenddbuserpassword' | base 64
echo -n 'rootdbuserpassword' | base 64
```
![Encoding Secrets with base64](screenshots/1.png)

#### 2.2 YAML File
Create a YAML file `mysql-secret.yaml` with the following content to include the DB password and root password:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
  namespace: ivolve
type: Opaque
data:
  DB_PASSWORD: YmFja2VuZGRidXNlcnBhc3N3b3Jk
  MYSQL_ROOT_PASSWORD: cm9vdGRidXNlcnBhc3N3b3Jk
``` 

### 3. Apply & Verify
We apply the manifests through:
```bash
kubectl apply -f mysql-configmap.yaml
kubectl apply -f mysql-secret.yaml
```
![Applying the Manifests](screenshots/2.png)

Verify the `ConfigMap`:
```bash
kubectl get cm mysql-config -n ivolve
kubectl describe cm mysql-config -n ivolve
```
![](screenshots/3.png)
Verify the `Secret`:
```bash
kubectl get secrets mysql-secret -n ivolve
kubectl describe secrets mysql-secret -n ivolve
```
![](screenshots/4.png)
