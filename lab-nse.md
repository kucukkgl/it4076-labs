### **Nmap NSE Scripts Lab: Enumeration and Web Server Discovery**

#### **Objective:**
This lab focuses on using Nmap NSE (Nmap Scripting Engine) scripts for enumerating and discovering web server services, specifically targeting Apache web servers.

---

#### **Tasks:**

1. **Locate the `.nse` files in Kali Linux:**
   - Find the location of the `.nse` files on your Kali Linux system.

2. **Determine the number of NSE scripts related to the Apache web server:**
   - How many `.nse` scripts are available that relate to Apache web servers?

3. **Identify the Target Server IP:**
   - You need to determine the target server's IP address.
     - a. The regular way is to log in to the Metasploitable server and run `ifconfig`.
     - b. Alternatively, run the following Nmap command to identify the server:
       ```
       nmap -sV 192.168.2.1/27
       ```
     - c. One server will have many open ports with FTP on port 21. That’s your Metasploitable server.

4. **Identify the List of NSE Categories:**
   - Reach out to the list of NSE categories.  
   - Which category would you start with if you want to stay stealthy?

5. **Run the Nmap NSE Scripts Against Your Target:**
   - Start running a category script against your target. Compare the executed scripts with the list on [nmap.org](https://nmap.org).  
   - Some scripts may require user interaction.  
   - **Command:**
     ```
     nmap targethost --script <category> -oN filename.txt
     ```
   - Save the results in a `.txt` file.

6. **Identify Libraries in the `http-enum.nse` Script:**
   - Which libraries are being used in the `http-enum.nse` script?

7. **Use Shodan to Find Common Apache Web Server Ports:**
   - As part of the reconnaissance phase, use [shodan.io](https://shodan.io) to find the most common port numbers for Apache web servers.

8. **Enumerate Directories and Files on the HTTP Server:**
   - Your task is to enumerate directories and files on the HTTP server by performing basic directory brute-force and file discovery techniques.
   - Find the relevant NSE script for this task. 
   - Hint: Focus on the most famous Apache service port.  
   - **Command:**
     ```
     nmap -p <famous_port> <Metasploitable_IP> --script=http-enum.nse
     ```

9. **Access Found Directories Using `curl`:**
   - Once directories are discovered, use the `curl` command or a browser on your Kali Linux system to access those directories.
   - **Command:**
     ```
     curl <Metasploitable_IP>/directory/
     ```
