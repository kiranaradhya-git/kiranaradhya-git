# To **extend `/dev/xvda1` (your root partition) on AWS EC2**, follow these steps:

---

### 1. **Increase EBS Volume Size in AWS Console**
- Go to **EC2 > Volumes**.
- Select the volume attached to your instance (usually `/dev/xvda`).
- Click **Actions > Modify Volume**.
- Enter the new, larger size (e.g., 16 GiB).
- Click **Modify** and confirm.

---

### 2. **Extend the Partition on the Instance**

SSH into your EC2 instance and run:

```sh
# Install growpart if not present
sudo yum install cloud-utils-growpart -y   # Amazon Linux/CentOS
# or
sudo apt-get install cloud-guest-utils -y  # Ubuntu/Debian

# Extend the partition (usually partition 1)
sudo growpart /dev/xvda 1
```

---

### 3. **Resize the Filesystem**

- For **ext4** (most common):
    ```sh
    sudo resize2fs /dev/xvda1
    ```
- For **xfs**:
    ```sh
    sudo xfs_growfs /
    ```

---

### 4. **Verify**

```sh
df -h
```

You should now see the increased space available on `/`.

---

**Note:**  
- No reboot is required for these steps.
- Replace `/dev/xvda1` with your root partition if different.  
- Always back up important data before resizing disks.
