# Deploy an Ubuntu Virtual Machine on Microsoft Azure

A beginner-friendly Azure hands-on lab: provision an Ubuntu Server VM,
connect through SSH, install Nginx, and publish a simple HTML page over
HTTP.

## Lab objectives

By completing this lab, you will:

-   Create an Azure Resource Group and Ubuntu virtual machine.
-   Configure a public IP address and Network Security Group (NSG)
    rules.
-   Connect to Linux using SSH key authentication.
-   Update Ubuntu and install Nginx.
-   Host a custom HTML page.
-   Verify that the website is reachable from a browser.

## Architecture

``` text
                  HTTP (TCP/80)
Internet  ------------------------------+
                                         |
                                  Azure Public IP
                                         |
                                  Network Security
                                    Group (NSG)
                                         |
                                  Ubuntu 24.04 LTS
                                         |
                                      Nginx
                                         |
                                  /var/www/html
                                    index.html

Administrator -- SSH (TCP/22) ----------> Ubuntu VM
```

## Azure resources and configuration

  Setting                    Value used in this lab
  -------------------------- --------------------------------------------------------
  Subscription               Azure subscription
  Resource Group             `rg-azure-vm-lab`
  VM name shown in the lab   `azureuser`
  Operating system           Ubuntu Server 24.04 LTS
  VM size                    Standard D2alds_v7 (as shown in the deployment review)
  Region                     West US 2
  Authentication             SSH public key
  Username                   `azureuser`
  SSH key pair name          `azureuser_key`
  Inbound ports              HTTP (80), SSH (22)
  Web server                 Nginx
  Website directory          `/var/www/html`

> **Note:** VM size, region, and pricing depend on subscription
> availability and can change. Choose an appropriately sized VM for your
> own lab and review the estimated cost before deployment.

## 1. Create the virtual machine

1.  Sign in to the [Azure Portal](https://portal.azure.com/).
2.  Search for **Virtual machines**.
3.  Select **Create → Azure virtual machine**.
4.  On the **Basics** tab, select your subscription and create or select
    the Resource Group `rg-azure-vm-lab`.
5.  Set the operating system image to **Ubuntu Server 24.04 LTS**.
6.  Choose a suitable VM size.
7.  Under **Administrator account**, select **SSH public key**
    authentication.
8.  Enter the username `azureuser`.
9.  Generate a new SSH key pair and download the private key. Store it
    securely.
10. On the **Networking** tab, configure a Virtual Network, subnet, and
    public IP.
11. Allow inbound HTTP (TCP/80). Allow SSH (TCP/22) only from your own
    public IP address where possible.
12. Review the configuration and select **Create**.

Screenshots: - [VM deployment review](screenshots/01-vm-review.png) -
[VM deployment configuration
details](screenshots/02-vm-review-details.png)

## 2. Find the VM public IP address

After deployment:

1.  Open the virtual machine in the Azure Portal.
2.  On the **Overview** page, locate the public IP address.
3.  Copy it; you will use it to connect over SSH and test the website.

The lab screenshot shows the public IP resource. The address has been
masked in the repository copy.

-   [Public IP resource](screenshots/03-public-ip-resource.png)

## 3. Connect to Ubuntu using SSH

On Windows, open PowerShell and run the SSH command using the path to
the downloaded private key:

``` powershell
ssh -i "C:\path\to\azureuser_key.pem" azureuser@YOUR_PUBLIC_IP
```

Replace `C:\path\to\azureuser_key.pem` with the actual private-key path
and `YOUR_PUBLIC_IP` with the VM's public IP.

If prompted to trust the host fingerprint, verify that you are
connecting to your VM, then accept the prompt.

A successful login displays the Ubuntu welcome message and a shell
prompt similar to:

``` text
azureuser@azureuser:~$
```

-   [Successful SSH connection](screenshots/04-ssh-connection.png)

### SSH security

-   Never upload your private `.pem` key to GitHub or share it.
-   Restrict inbound SSH (TCP/22) to your current public IP instead of
    allowing access from `Any` or `0.0.0.0/0`.
-   Keep the private key in a secure location and use appropriate file
    permissions.

## 4. Update Ubuntu packages

Inside the SSH session, refresh the package index:

``` bash
sudo apt update
```

Optionally install available package upgrades:

``` bash
sudo apt upgrade -y
```

The `apt update` command refreshes the local package metadata; it does
not itself upgrade installed packages.

-   [Package index update](screenshots/05-apt-update.png)

## 5. Install and start Nginx

Install Nginx:

``` bash
sudo apt install nginx -y
```

Start the service:

``` bash
sudo systemctl start nginx
```

Enable Nginx to start automatically after a reboot:

``` bash
sudo systemctl enable nginx
```

Check its current status:

``` bash
sudo systemctl status nginx
```

The expected status is:

``` text
Active: active (running)
```

-   [Nginx installation](screenshots/06-nginx-installation.png)
-   [Nginx service status](screenshots/07-nginx-service-status.png)

## 6. Create a custom HTML page

Nginx serves the default website from `/var/www/html` on this Ubuntu
installation.

Open the default index file:

``` bash
sudo nano /var/www/html/index.html
```

Replace its content with:

``` html
<!DOCTYPE html>
<html>
<head>
    <title>My First Azure VM</title>
</head>
<body>
    <h1>Hello from Microsoft Azure!</h1>
    <h2>My First Ubuntu Virtual Machine</h2>
    <p>This website is hosted using Nginx.</p>
    <p>Learning Azure Cloud and DevOps.</p>
</body>
</html>
```

Save and exit Nano:

-   Press `Ctrl + O`, then `Enter` to save.

-   Press `Ctrl + X` to exit.

-   [Custom HTML source](screenshots/08-custom-html-page-source.png)

## 7. Test the website

Open a browser and navigate to:

``` text
http://YOUR_PUBLIC_IP
```

You should see the custom page with the heading **Hello from Microsoft
Azure!**

-   [Website successfully served by
    Nginx](screenshots/09-live-website.png)

## 8. Troubleshooting

If the website does not load, check the following from the VM:

``` bash
# Check whether Nginx is running
sudo systemctl status nginx

# Check whether a process is listening on TCP port 80
sudo ss -tlnp | grep ':80'

# Check Nginx configuration syntax
sudo nginx -t

# View recent Nginx error log entries
sudo tail -n 30 /var/log/nginx/error.log

# Test the web server locally from the VM
curl -I http://localhost
```

Also verify in Azure:

-   The VM is running and has the expected public IP.
-   The NSG attached to the VM's network interface or subnet allows
    inbound TCP/80.
-   The rule has an appropriate priority and is not overridden by a
    higher-priority deny rule.
-   If Ubuntu's UFW firewall is enabled, it allows Nginx HTTP traffic.

## 9. Clean up Azure resources

When you finish the lab, delete the Resource Group if you no longer need
its resources:

1.  Open **Resource groups** in the Azure Portal.
2.  Select `rg-azure-vm-lab`.   
3.  Select **Delete resource group**.
4.  Confirm the Resource Group name and deletion.

Deleting the Resource Group removes the resources contained in it.
Confirm that it contains only resources you intend to delete.

> **Cost reminder:** A stopped VM may still incur charges for attached
> resources such as managed disks and certain IP/network resources.
> Review the subscription's pricing and billing details, and delete the
> lab resources when finished.

## What I learned

-   Provisioning an Ubuntu Linux VM in Azure.
-   Basic Azure networking: Virtual Networks, public IP addresses, and
    NSGs.
-   Remote Linux administration using SSH key authentication.
-   Managing Linux services with `systemctl`.
-   Installing software with Ubuntu's `apt` package manager.
-   Hosting a static HTML page with Nginx.
-   Testing public HTTP connectivity.

