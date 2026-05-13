
# 🗂️ Polystack IronCore – Glance Image Service & Custom Image Storage Configuration

---

## 1. 🔎 Introduction

**Polystack IronCore OpenStack** includes a fully integrated **Glance Image Service**, which enables users to discover, upload, and manage virtual machine images used across the platform. Glance serves as the centralized repository for VM images and plays a vital role in compute provisioning by supplying images to **Nova** during instance creation.

The Glance service is designed to support a variety of backend storage options, ensuring flexibility and scalability for diverse customer environments.

---

## 2. 🧱 Architecture Overview

### 🔹 Image Service Architecture

1. **Users upload images** via Horizon UI, OpenStack CLI, or API.
2. **Glance stores image data** using the selected backend (e.g., local FS, Swift, Ceph, etc.).
3. **Nova retrieves images** from Glance when provisioning new VMs.
4. **Glance APIs** manage image metadata, formats, versioning, and access policies.
5. **Multiple backends** can be configured simultaneously and selected per image.

---

## 3. ✨ Supported Storage Backends

| Backend Type               | Description                                                                          |
| -------------------------- | ------------------------------------------------------------------------------------ |
| **Local File System**      | Stores image files on the Glance host's disk. Ideal for simple deployments.          |
| **Object Storage (Swift)** | Uses OpenStack Swift for scalable and distributed image storage.                     |
| **Ceph RBD**               | Stores images in Ceph's RADOS Block Device; supports native sharing across services. |
| **Amazon S3**              | S3-compatible support exists but is deprecated in most production cases.             |
| **VMware Datastore**       | Allows storing images directly in vSphere environments (for VMware integration).     |

> 📌 Polystack IronCore can operate multiple backends concurrently and assign them dynamically per image upload.

---

## 4. 🧰 Use Case: Custom Local Directory for Image Storage

In some deployments, administrators may want to store image files in a **custom local directory** (e.g., on dedicated volumes or bind-mounted storage). Polystack IronCore supports this through configuration overrides.

### ✅ Example: Configure a Custom Directory

1. **Create Override Configuration Path**
   On the control node:

   ```bash
   mkdir -p /etc/ironcore/config/glance
   ```

2. **Define the Custom Image Path**
   Example override snippet:

   ```ini
   [glance_store]
   default_backend = file
   filesystem_store_datadir = /mnt/glance_images/
   ```

3. **Prepare the Host Storage Path**

   ```bash
   sudo mkdir -p /mnt/glance_images/
   sudo chown 42424:42424 /mnt/glance_images/
   ```

   * `42424` is the default UID/GID for Glance in Polystack IronCore (adjust if needed).

4. **Apply the Configuration**
   Deploy configuration changes with:

   ```bash
   ironcore reconfigure -t glance
   ```

---

## 5. 🤖 Automation and Operational Fit

* **Terraform-Compatible**: Glance image upload actions can be embedded in Terraform workflows.
* **Ansible Integration**: Image uploads and directory permissions can be managed via Ansible tasks.
* **Multi-Store Support**: Admins can register multiple backends and select which one to use per image.
* **Secure Access Control**: Role-based visibility and image access policies applied at the project/tenant level.

---

## 6. ✅ Summary & Positioning

The **Polystack IronCore Glance Image Service** provides robust and flexible image management for virtual machine provisioning. With multi-backend support and customizable local directory storage, Glance ensures:

* Consistent image availability across compute nodes
* Scalable image distribution and replication
* Seamless integration with object storage, Ceph, or local disks
* Secure, tenant-aware image operations

> 🟢 **Customer Experience:** Upload your images via UI, CLI, or API—our platform manages where and how they are stored based on your configuration or policy.

---
