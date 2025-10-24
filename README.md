# Project: Static Website Hosting on RHEL 10 + AWS

Is project ka goal ek RHEL 10 server ko AWS EC2 par launch karke, use ek basic Apache web server mein badalna tha.

**Technologies Used:** AWS EC2, RHEL 10, Apache (httpd), FirewallD.

---

### Process / Steps:

1.  **Launch EC2 Instance:**
    * AWS Management Console se ek EC2 instance launch kiya.
    * AMI (Amazon Machine Image): **RHEL 10** select kiya.
    * Instance Type: `t2.micro` (Free tier).
    * Security Group: Port 22 (SSH) aur Port 80 (HTTP) ko allow kiya.

2.  **Install Apache:**
    * Instance mein SSH se connect kiya.
    * Apache package install kiya:
        ```bash
        sudo dnf install httpd -y
        ```

3.  **Start and Enable Apache Service:**
    * Service ko start kiya aur boot par enable kiya:
        ```bash
        sudo systemctl start httpd
        sudo systemctl enable httpd
        ```

4.  **Configure Firewall (FirewallD):**
    * RHEL ke built-in firewall mein HTTP traffic ko permanently allow kiya:
        ```bash
        sudo firewall-cmd --permanent --add-service=http
        sudo firewall-cmd --reload
        ```

5.  **Deploy Website:**
    * Is repository mein jo `index.html` file hai, use web directory (`/var/www/html/`) mein copy kiya.
        ```bash
        sudo cp index.html /var/www/html/index.html
        ```
    * **Result:** Instance ki Public IP ko browser mein open karke website live ho gayi.
