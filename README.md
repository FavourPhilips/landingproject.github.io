# Landing Page Deployment

## Overview
This project demonstrates how to provision a Linux server on AWS, install a web server (Apache), deploy a simple HTML page, and configure networking so that the page is accessible from the web.

---

## Steps to Reproduce

### 1. Provision the Server (AWS EC2)

To get started, we need to create a virtual machine (VM) on AWS, called an **EC2 instance**, which will host our web page.

#### Step-by-Step Process:

1. **Log into AWS Management Console**  
   Go to the [AWS Management Console](https://aws.amazon.com/console/) and log in with your credentials.

2. **Launch an EC2 Instance**  
   - In the AWS dashboard, search for **EC2** and click on **Launch Instance**.
   - Choose an **Ubuntu 22.04** image (or whichever Linux distribution you prefer).
   - Select a **t2.micro** instance (this is free-tier eligible if you're using AWS's free tier).
   - Configure your instance settings (leave the default settings for now).
   
3. **Set Up Security Group**  
   - When prompted for security groups, make sure to allow **HTTP** (port 80) and **SSH** (port 22) access. This ensures we can access the server via a browser and SSH into it.
   
4. **Download the Key Pair**  
   - Create a new SSH key pair to access the server and download the `.pem` file. Keep it safe.
   
5. **Launch the Instance**  
   - Click **Launch** to start your EC2 instance.
   - Once the instance is running, go to **Instances** on the EC2 dashboard and note the **Public IP Address** of your instance (e.g., `3.25.45.150`).

---

### 2. Install the Web Server (Apache)

Next, we’ll install **Apache**, which is another popular web server, on our EC2 instance.

#### Step-by-Step Process:

1. **SSH into the EC2 Instance**  
   - Open a terminal and navigate to the folder where your `.pem` key file is located.  
   - Connect to your EC2 instance using the following command (replace `your-key.pem` and `<public-ip-address>` with your actual values):
     ```bash
     ssh -i your-key.pem ubuntu@<public-ip-address>
     ```
   - Example:
     ```bash
     ssh -i my-key.pem ubuntu@3.25.45.150
     ```

2. **Update the Server**  
   - Once you’re connected, update the package lists:
     ```bash
     sudo apt update
     ```

3. **Install Apache**  
   - Install the Apache web server:
     ```bash
     sudo apt install apache2 -y
     ```

4. **Start the Apache Service**  
   - Start the Apache service and enable it to start automatically on boot:
     ```bash
     sudo systemctl start apache2
     sudo systemctl enable apache2
     ```

5. **Check if Apache is Running**  
   - Open your browser and enter the **public IP address** of your EC2 instance (e.g., `http://3.25.45.150`).
  
---

### 3. Deploy the HTML Page

Now we will create a simple HTML landing page and deploy it to the web server.

#### Step-by-Step Process:

1. **Navigate to the Web Directory**  
   - The default web folder for Apache is located at `/var/www/html`. Go to this directory:
     ```bash
     cd /var/www/html
     ```

2. **Create the HTML File**  
   - Delete the default `index.html` file:
     ```bash
     sudo rm index.html
     ```
   - Create a new `index.html` file using `nano` or any text editor:
     ```bash
     sudo nano index.html
     ```
   - Add your HTML content. Here’s a simple example:
     ```html
     <!DOCTYPE html>
     <html>
     <head><title>Welcome to My Landing Page</title></head>
     <body>
         <h1>Welcome to My Landing Page</h1>
         <p>Hi, I'm Favour, a Cloud Engineering student. This is my first project hosted on AWS.</p>
     </body>
     </html>
     ```
   - Save the file by pressing `CTRL + O`, then press `Enter`, and exit by pressing `CTRL + X`.

3. **Verify the Deployment**  
   - Go back to your browser and type your server’s **public IP** (example: `http://3.25.45.150`).
   - Your new landing page should be visible.

---

### 4. Configure Networking

To make sure your server can be accessed via a web browser, we need to configure the **security group** in AWS and ensure HTTP traffic is allowed.

#### Step-by-Step Process:

1. **Configure Security Group for HTTP Traffic**  
   - Go to your **EC2 Dashboard** in AWS.
   - Under **Instances**, click on your EC2 instance.
   - In the **Security Group** section, click on the **Security Group ID**.
   - In the security group settings, ensure **HTTP (Port 80)** is allowed for inbound traffic. If not, add a new rule:
     - **Type**: HTTP
     - **Protocol**: TCP
     - **Port**: 80
     - **Source**: Anywhere (0.0.0.0/0)
   
2. **Test the Page**  
   - Open your browser and enter your **public IP address** (e.g., `http://3.25.45.150`).
   - Your landing page should now load, confirming that the networking is properly set up.

---

## Final Thoughts  
Now that you have a running server on AWS, with a simple HTML page deployed and accessible through the web, you can expand this project to include more complex applications in the future.

---

## Screenshot  
- Include a screenshot of your landing page loaded in the browser here.

---

## Tools and Technologies Used  
- **AWS EC2** for provisioning the server  
- **Ubuntu 22.04** as the operating system  
- **Apache** as the web server  
- **Basic HTML** for the landing page  

---

### Conclusion  
This project demonstrates the basics of deploying a web server on AWS and serving a simple HTML page. You can expand this by adding more advanced features such as database connections, dynamic pages, or integrating SSL certificates for HTTPS.
