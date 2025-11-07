

# Stackstore - Decentralized Cloud Storage (Clarity Smart Contract)

A decentralized file metadata management system built on the **Stacks blockchain** using the **Clarity smart contract language**.
This contract allows users to **upload, update, delete, transfer, and manage permissions** for file metadata in a secure and trustless way — representing a simplified decentralized cloud storage registry.

---

## 🚀 Features

* **File Uploading** — Users can register new files with metadata (name, size, timestamp).
* **File Updating** — Owners can rename or resize existing file entries.
* **File Deletion** — Owners can delete their uploaded files.
* **Ownership Transfer** — Transfer file ownership to another Stacks address.
* **Access Control** — Owners can grant or revoke access permissions to other users.
* **Read-Only Queries** — Anyone can fetch file information and total file counts.

---

## 🧩 Data Structures

### Variables & Maps

| Name               | Type                                                          | Description                                                |
| ------------------ | ------------------------------------------------------------- | ---------------------------------------------------------- |
| `total-files`      | `uint`                                                        | Keeps count of total uploaded files.                       |
| `files`            | map `{ file-id: uint }` → `{ owner, name, size, created-at }` | Stores metadata of each file.                              |
| `file-permissions` | map `{ file-id, user }` → `{ permission: bool }`              | Tracks which users have permission to access a given file. |

---

## ⚙️ Public Functions

| Function                                          | Description                                                             |
| ------------------------------------------------- | ----------------------------------------------------------------------- |
| `(upload-file name size)`                         | Uploads a new file with a given name and size. Returns a new `file-id`. |
| `(update-file file-id new-name new-size)`         | Updates file metadata. Only callable by the file owner.                 |
| `(delete-file file-id)`                           | Deletes a file. Only the owner can perform this.                        |
| `(transfer-file-ownership file-id new-owner)`     | Transfers ownership of a file to another principal.                     |
| `(grant-permission file-id permission recipient)` | Grants or removes a permission flag for another user.                   |
| `(revoke-permission file-id user)`                | Revokes a user’s access permission.                                     |
| `(get-total-files)`                               | Returns the total number of files in the system.                        |
| `(get-file-info file-id)`                         | Returns file details (owner, name, size, created-at).                   |

---

## 🧠 Error Codes

| Error Code | Description           |
| ---------- | --------------------- |
| `err u100` | Owner-only operation. |
| `err u101` | File not found.       |
| `err u102` | File already exists.  |
| `err u103` | Invalid file name.    |
| `err u104` | Invalid file size.    |
| `err u105` | Unauthorized access.  |
| `err u106` | Invalid recipient.    |

---

## 📜 Example Usage

### Upload a File

```clarity
(contract-call? .decentralized-cloud-storage upload-file "my-photo.jpg" u204800)
;; Returns (ok u1)
```

### Update File Metadata

```clarity
(contract-call? .decentralized-cloud-storage update-file u1 "photo-updated.jpg" u205000)
;; Returns (ok true)
```

### Grant Access to Another User

```clarity
(contract-call? .decentralized-cloud-storage grant-permission u1 true 'SP3FBR2AGK7...)
;; Returns (ok true)
```

### Fetch File Info

```clarity
(contract-call? .decentralized-cloud-storage get-file-info u1)
;; Returns (ok { owner: ..., name: ..., size: ..., created-at: ... })
```

---

## 🔒 Security Considerations

* Only file owners can modify or delete their files.
* Permissions cannot be granted to the owner themselves.
* The contract enforces validation on file name length and file size (max 1 GB).
* Access control is explicit — unauthorized users cannot modify or access file details.

---

## 🏗️ Future Improvements

* File encryption metadata support (hash or CID storage).
* Integration with IPFS or Gaia for decentralized file content.
* Batch permission management.
* Enhanced event logging for UI integrations.
* Versioning system for file updates.

---

## 🧾 License

This project is open-source under the **MIT License**.

---



