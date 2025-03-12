### **Lab-nmap**

1. **Explain the usage of `-T4` with its overall name in this command:**
   ```
   nmap -A -T4 scanme.nmap.org
   ```
   - **Question:** What does the `-T4` option do in this command, and what is its overall purpose in Nmap scanning?

2. **Perform a "no scan" with Nmap on 30 hosts:**
   - **Question:** Follow the rule of staying as stealthy as possible in penetration testing. Perform a "no scan" on 30 hosts in your network using the following Nmap command with CIDR and netmasking:
     ```
     nmap -sn <CIDR> 
     ```
     Explain your approach and the result of the scan.

3. **Perform a SYN scan on your target host:**
   - **Question:** Conduct a **SYN scan** on your target host using Nmap.  
     - How does a **SYN scan** work?  
     - Provide a **screenshot** of the scan output.

4. **Perform a service and version scan on your target host:**
   - **Question:** Run a **service and version scan** on your target host to gather details about the services running.  
     - What services are listening on the first 3 open ports?  
     - Provide a **screenshot** of the scan output.

5. **Perform an operating system scan on 6 hosts in your network:**
   - **Question:** Conduct an **operating system scan** on 6 hosts in your network using **subnetting and CIDR**.  
     - Are there any servers with Windows OS?  
     - Write down the information you have gathered about the Windows servers.  
     - Provide **screenshots** of the scan results.
