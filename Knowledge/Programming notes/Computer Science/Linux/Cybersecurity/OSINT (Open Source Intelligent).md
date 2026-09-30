### **What is OSINT (Open Source Intelligence)?**

**Open Source Intelligence (OSINT)** refers to the ==process of collecting and analyzing publicly available data== from various sources to gather valuable intelligence. 

This data can come from a wide range of ==publicly accessible channels such as websites, social media platforms, public records, news articles, forums, and even images or videos. ==

OSINT is widely ==used in cybersecurity, law enforcement, business intelligence, and even by journalists and researchers== to uncover information without violating privacy or using secret sources. It provides insights that can be critical for threat detection, risk assessment, and even investigative work.

---

### **Essential OSINT Websites:**

1. **Shodan**  
    **Website**: [shodan.io](https://www.shodan.io)  
    **Description**: A search engine for discovering internet-connected devices and identifying security vulnerabilities.

---
2. **Maltego**  
    **Website**: [maltego.com](https://www.maltego.com)  
    **Description**: A powerful OSINT tool for mapping relationships between people, companies, domains, and more to uncover hidden links.

---
3. **Censys**  
    **Website**: [censys.io](https://www.censys.io)  
    **Description**: Provides internet-wide scanning and data analysis to track devices, services, and vulnerabilities exposed to the internet.

---
4. **TheHarvester**  
    **Website**: [github.com/laramies/theHarvester](https://github.com/laramies/theHarvester)  
    **Description**: A tool for gathering information about email addresses, domains, and subdomains from public sources like search engines and social media.

---
5. **Social Search Engines (Pipl, Spokeo, etc.)**  
    **Website**: [pipl.com](https://pipl.com) 
    **Description**: Search engines that aggregate and index public data from social media, online profiles, and public records to find personal or business-related information.

---
6. **Spokeo**  
    **Website**: [spokeo.com ](https://spokeo.com)
    **Description**: A people search engine that aggregates data from public records and social media profiles.
---
7. **PimEyes**  
    **Website**: [pimeyes.com ](https://pimeyes.com) 
    **Description**: An advanced facial recognition search engine that allows users to find publicly available images of individuals online.
---
8. **OSINT Framework**  
    **Website**: [osintframework.com](https://osintframework.com)  
    **Description**: A comprehensive collection of OSINT tools and resources for gathering intelligence from various online platforms.
---
9. **Bing Search**  
    **Website**: [bing.com](https://www.bing.com)  
    **Description**: Although a basic search engine, Bing can be used for advanced queries, including reverse image searches and URL exploration for OSINT purposes.
---
10. **Clean up a picture, editing**
	 **Website**: [cleanup.pictures](https://cleanup.pictures/)
	 **Description:** Useful tool to remove background or exact objects from a picture. It's very essential to gather more information and separate non-important information. 

### **What is Google Dorking?**

**Google Dorking** involves ==using advanced search operators to search Google== in ways that reveal specific information that may not appear in standard search results. It is often used in cybersecurity for vulnerability scanning, information gathering, and penetration testing, but it can also be used for less ethical purposes, so it's important to be aware of legal and ethical boundaries when using these techniques.

==Google Dorks allow you to refine your searches to uncover exposed files, database errors, sensitive information, and more.== Here are some of the most useful Google Dorking techniques:

---

### **Common Google Dorking Techniques**

1. **Finding Specific File Types:**
    
    - **Example**: `filetype:pdf confidential`
	     > **Used with "OR" (e.g, filetype:pdf OR filetype:docs)**
	     >  **"Credentials" filetype:pdf OR filetype:xlsx OR filetype:docx**
        
    - **Description**: Search for specific file types (e.g., PDF, DOC, XLS) that contain certain keywords.
        
    - **Use Case**: To find exposed documents, reports, or files online that are publicly accessible.
        
2. **Finding Exposed Login Pages:**
    
    - **Example**: `intitle:"index of" admin`
        
    - **Description**: Searches for directories or pages with "index of" in the title, which may indicate an exposed admin panel.
        
    - **Use Case**: To locate admin login pages or control panels that might be publicly accessible.
        
3. **Searching for Exposed Databases:**
    
    - **Example**: `filetype:sql "password"`
        
    - **Description**: Looks for SQL dump files that may contain sensitive data, including passwords.
        
    - **Use Case**: To find databases that have been improperly exposed on the web.
        
4. **Finding Vulnerable Websites:**
    
    - **Example**: `inurl:/wp-login.php`
        
    - **Description**: Searches for WordPress login pages (`wp-login.php`), which can be vulnerable to brute-force attacks.
        
    - **Use Case**: To identify potential targets that use outdated or vulnerable WordPress installations.
        
5. **Finding Exposed Sensitive Data in URLs:**
    
    - **Example**: `inurl:"/wp-content/uploads/" filetype:pdf`
        
    - **Description**: Finds specific file types (e.g., PDFs) that are uploaded to certain directories in WordPress websites.
        
    - **Use Case**: To find sensitive documents or media files that may have been left publicly accessible.
        
6. **Locating Specific Web Servers or Technologies:**
    
    - **Example**: `intitle:"Apache2 Ubuntu Default Page"`
        
    - **Description**: Looks for servers that are running default Apache2 installation pages, which could be insecure if not properly configured.
        
    - **Use Case**: To identify web servers running specific technologies or configurations.
        
7. **Finding Directory Listings:**
    
    - **Example**: `intitle:"index of" "parent directory"`
        
    - **Description**: Finds open directories that may contain downloadable files.
        
    - **Use Case**: To locate websites that have not been configured to block directory listing.
        
8. **Finding Exposed User Files:**
    
    - **Example**: `inurl:/user/ filetype:txt`
        
    - **Description**: Looks for text files on web servers that may contain user data, like usernames or other personal information.
        
    - **Use Case**: To find user-specific files or data that may have been left exposed.
        
9. **Exposing Email Addresses:**
    
    - **Example**: `intext:"@gmail.com" filetype:xls`
        
    - **Description**: Searches for specific email addresses (e.g., Gmail) in spreadsheet files.
        
    - **Use Case**: To discover emails exposed in public files (useful in data scraping or lead generation).
        
10. **Finding Sensitive Information in Public PDFs:**
    
    - **Example**: `filetype:pdf "Confidential" "Financial Report"`
        
    - **Description**: Searches for PDFs that may contain sensitive information, such as financial reports or confidential documents.
        
    - **Use Case**: To uncover potentially exposed sensitive business or personal data in PDF files.
        
11. **Exposing Webcams or IoT Devices:**
    
    - **Example**: `inurl:"/view.shtml"`
        
    - **Description**: Finds URLs that lead to live webcam streams, which may be exposed due to insecure configurations.
        
    - **Use Case**: To locate webcams or IoT devices that have been left unsecured and exposed to the public.
        
12. **Finding Web Server Errors:**
    
    - **Example**: `intitle:"index of" "parent directory" "error.log"`
        
    - **Description**: Searches for log files (like error logs) that may be exposed on public servers.