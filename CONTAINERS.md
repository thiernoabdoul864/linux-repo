# Configuring an Apache Container

```bash
# Step 1: Create a Directory 
mkdir /apache/html -p
chmod 777 -R /apache/html/
echo "This Is the website from our container" > /apache/html/index.html

# Step 2: Install Podman and Container-Tools, then Log in to Red Hat Registry
yum install podman container-tools -y
podman login registry.redhat.io
# Use your Red Hat credentials to log in

# Step 3: Search for the Given Image (httpd-24)
podman search httpd-24 | grep rhel8

# Step 4: Download the Image with the Tag Attached
podman pull registry.redhat.io/rhel8/httpd-24:1-105

# Step 5: Verify the Download and Build an Image
podman images
podman run -d --name website -p 8080:7070 -v /apache/html:/var/www/html 7e92f25a9468
# -d: Stands for detached mode
# --name: The name of the container being created
# -p: Port mapping
# -v: Local directory mapping (volume)
# 7e92f25a9488: The image ID

# Verify using:
podman ps

# Step 6: Generate the systemd Service Using the Image
mkdir -p /home/sams/.config/systemd/user
podman generate systemd --new website > /home/sams/.config/systemd/user/website.service
# --new: Ensures that the created service does not depend on the website container to run

# Note: Edit /home/sams/.config/systemd/user/website.service to ensure the last line is:
# Wants=default.service

# Step 7: Reload the Daemon, Enable, and Start the Service
systemctl --user daemon-reload
systemctl --user enable --now website.service
systemctl enable-linger website.service
# Note: This last line ensures that the service stays up and running even when user sams logs out.
