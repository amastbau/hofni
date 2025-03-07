# Classifier Reference Documentation

## Overview
This document provides a structured reference for classifying logs related to Velero, OADP, and related applications. Each classifier includes example logs and notable keywords for easier identification.

---

## Classifiers

### 1. vsl-missing
- **Text Example:**
  ```
  VSL spec is empty
      {
          s: "VSL spec is empty",
      }
  ```
- **Notables:**
  - "VSL spec is empty"

---

### 2. must-gather-failed
- **Text Example:**
  ```
  TEP: Find must-gather folder and rename it to a shorter more readable name
  2025/02/16 17:52:43 Failed to find must-gather folder
  rename logs/.../must-gather: no such file or directory
  [FAILED] Unexpected error:
  ```
- **Notables:**
  - "Failed to find must-gather folder"
  - "rename logs/.../must-gather: no such file or directory"

---

### 3. backup-partiallyfailed
- **Text Example:**
  ```
  Expected
      <v1.BackupPhase>: PartiallyFailed
  to equal
      <v1.BackupPhase>: Completed
  ```
- **Notables:**
  - "BackupPhase: PartiallyFailed" (Actual Phase)
  - "BackupPhase: Completed" (Expected Phase)

---

### 4. internal-registry-error
- **Text Example:**
  ```
  velero container contains "level=error" msg="Error backing up item"
  error="error executing custom action (groupResource=imagestreams.image.openshift.io, namespace=test-oadp, name=django-psql-persistent):
  rpc error: code = Unknown desc = writing blob: initiating layer upload to /v2/test-oadp/django-psql-persistent/blobs/uploads/
  in registry-1.docker.io: received unexpected HTTP status: 500 Internal Server Error"
  ```
- **Notables:**
  - "Error backing up item"
  - "rpc error: code = Unknown"
  - "writing blob"
  - "500 Internal Server Error"
  - "imagestreams.image.openshift.io"

---

### 5. unknown
- **Text Example:**
  ```
  2025/02/16 19:10:22 pod: velero-67c98477b5-mgp9m is not yet running with status: {Pending}
  2025/02/16 19:14:27 Timed out after 180.001s.
  Expected
      : cat: /tmp/credentials/.../cloud-credentials-gcp-cloud: No such file or directory
  to equal
      : Secret was mounted into the velero pod
  ```
- **Notables:**
  - "pod: velero-... is not yet running with status: {Pending}"
  - "Timed out after 180.001s"
  - "Secret was mounted into the velero pod"

---

### 6. application-validation
- **Text Example:**
  ```
  Command executed: ansible-playbook --extra-vars {"namespace":"test-oadp-417","use_role":"ocp-mssql","with_validate":true}
  ```
- **Notables:**
  - "ansible-playbook error"
  - "one or more hosts failed"
  - "with_validate":true

---

### 7. restic-command-failed
- **Text Example:**
  ```
  Restic command fail with ExitCode: 1
  ```
- **Notables:**
  - "Restic command fail with ExitCode: 1"

---

### 8. podvolumebackup-number
- **Text Example:**
  ```
  podVolumeBackup count is not matching with expectedVolumeBackupCount: 2 and No. of PodVolumeBackup are: 0
  ```
- **Notables:**
  - "podVolumeBackup count is not matching with expectedVolumeBackupCount"
  - "No. of PodVolumeBackup are: 0"

---

### 9. backup-failed
- **Text Example:**
  ```
  backup phase: Failed
  ```
- **Notables:**
  - "backup phase: Failed"

---

### 10. ocp-app-role (Dynamic)
- **Text Pattern:**
  ```
  ansible/roles/<app-name>
  ```
- **Notables:**
  - "ansible/roles/<app-name>" (Dynamically Extracted)
  - Example: "ansible/roles/ocp-todolist-mongodb-block"

---

### 11. todo-app-ready
- **Text Example:**
  ```
  applications/ocpdeployer/ansible/roles/ocp-todolist-mongodb-block : Wait until todoapp is ready] *
  ```
- **Notables:**
  - "Wait until todoapp is ready"
  - "server selection timeout"
  - "connection() error occurred during connection handshake"

---

### 12. <image-name>-pull-err (Dynamic)
- **Text Pattern:**
  ```
  Failed to pull image "<image-name>"
  ```
- **Notables:**
  - "ErrImagePull"
  - "ImagePullBackOff"
  - "unauthorized: The client does not have permission"
  - Example: "mongo-pull-err", "redis-pull-err"

---

### 13. <app-name>-deploy (Dynamic)
- **Text Pattern:**
  ```
  Command executed: ansible-playbook --extra-vars {"namespace":"test-oadp-492","use_role":"/ansible/roles/<app-name>","with_deploy":true}
  ```
- **Notables:**
  - "with_deploy"
  - "ansible/roles/<app-name>" (Dynamically Extracted)
  - Example: "ocp-todolist-mongodb-block-deploy"

---

## Conclusion
This document serves as a **reference guide** for understanding how different logs are classified in Velero/OADP testing. It ensures consistency in log analysis and helps with automation efforts.
