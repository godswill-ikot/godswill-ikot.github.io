---
title: 'Zabbix and web monitoring'
date: 2025-01-15
permalink: /posts/2025/15/Zabbix for monitoring a website
excerpt_separator: <!--more-->
toc: true
tags:
  - career
  - cyber security
  - zabbix
---
## Zabbix for web monitoring portfolio 3 discussion
Zabbix is an open-source monitoring software specially crafted and built for monitoring various IT infrastructure components, such as web-sites, servers, network devices, applications, and services. It provides a holistic and comprehensive suite of features for real-time monitoring, alerting, and visualization of system health and performance. Zabbix is particularly popular in enterprise environments due to its scalability, flexibility, and open-source nature, making it highly customizable and cost-effective.

#### Key Features of Zabbix <!--more-->
- Real-time Monitoring: For network devices (switches), servers (physical and virtual servers, etc), applications (Web applications, databases, email systems, etc.), cloud environments (AWS, Azure, Google Cloud, etc.), storage devices (Disk usage, file systems, etc.).
- Data Collection: it consists of Agent-based monitoring (Zabbix agents are installed on monitored machines) and, Agentless monitoring (For devices or systems where agent installation is not possible or desirable, Zabbix can collect data via protocols like SNMP (Simple Network Management Protocol), IPMI (Intelligent Platform Management Interface), or SSH (Secure Shell).
- Visualization: It provides dashboards with customizable, real-time visual representations of the system’s health, graphs, and charts, as well as trend analysis of performance metrics such as CPU usage, memory usage, and network throughput.
- #### Other features
- Scalability, Auto-discovery, Security, Alerts and Notifications

### Zabbix portfolio network segmentation (create a VM sandbox)
This a continuation and an extension from my [previous post](/posts/2023/03/nest-map) on 'A Basic Sandboxing Portfolio', we are going to consider an extended network segmentation for this portfolio study.
#### Zabbix network segmentation diagram

<img src="/images/posts/nest-map/p2.png" style="display: block; margin: auto;" /> 

#### Create an IP table for each machine on the network

| Device     | Role     | IP Address     | Subnet Mask     |
|--------------|--------------|--------------|--------------|
| Desktop 1 VM | Management and deployment | 192.168.200.9  | 255.255.255.0 |
| Desktop 2 as Wordpress server VM | Management and deployment | 192.168.200.5  | 255.255.255.0 |
| Gateway Router VM (enp0s3)  | Subnet 01 - Access to internet, Gateway and Desktop | 192.168.126.1  | 255.255.255.0 |
| Gateway Router VM (enp0s8)  | Subnet 02 - Access to internet and Gateway Desktop 1 and Desktop Wordpress server| 192.168.200.1  | 255.255.255.0 |
| Gateway Router VM (enp0s9)  |  Internet Access to Ubuntu Gateway  | 10.0.2.15  | 255.255.255.0 |
| Gateway Router VM (enp0s10)  | Subnet 03 - Access to internet, Gateway and Desktop | 192.168.26.1  | 255.255.255.0 |
| Application Server VM  | Server (Bitnami-Opencart)  | 192.168.26.2  | 255.255.255.0 |

- #### Desktop Configuration:
  - #### Desktop 1 for Management and deployment
Go to setting and then click NETWORK and set ADPATER 1 to INTERNAL NETWORK, then clicked OK and click START to bootup the machine on the VM.

<img src="/images/posts/nest-map/st1.PNG" style="display: block; margin: auto;" />

After starting up the machine, go to Settings and click on WIRED SETTINGS then click on IDENTITY to setup the MAC Address to (08:00:27:97:75:31 (enp0s3)) then click IPV4 and set to Manual to set the ADDRESS, NETMASK, GATEWAY AND DNS ADDRESS: 192.168.126.2	NETMASK: 255.255.255.0 GATEWAY: 192.168.126.1	and DNS: 8.8.8.8, 1.1.1.1 
Then click on APPLY and then DISCONNECT and RE-CONNECT the WIRED CONNECTION

<img src="/images/posts/nest-map/ubsp1.PNG" style="display: block; margin: auto;" />

Open a command line terminal using “Ctrl + alt + T” and type “ip a” to see if IP address is set, if IP address is set continue, else re-do the above step and restart the Ubuntu desktop machine. 

<img src="/images/posts/nest-map/ubip.PNG" style="display: block; margin: auto;" />

 - #### Desktop 2 for WORDPRESS maangement, installation and deployment
Go to setting and then click NETWORK and set ADPATER 1 to INTERNAL NETWORK, then clicked OK and click START to bootup the machine on the VM.

<img src="/images/posts/nest-map/st1.PNG" style="display: block; margin: auto;" />

After starting up the machine, go to Settings and click on WIRED SETTINGS then click on IDENTITY to setup the MAC Address to (08:00:27:97:75:31 (enp0s3)) then click IPV4 and set to Manual to set the ADDRESS, NETMASK, GATEWAY AND DNS ADDRESS: 192.168.126.2	NETMASK: 255.255.255.0 GATEWAY: 192.168.126.1	and DNS: 8.8.8.8, 1.1.1.1 
Then click on APPLY and then DISCONNECT and RE-CONNECT the WIRED CONNECTION

<img src="/images/posts/nest-map/ubsp1.PNG" style="display: block; margin: auto;" />

Open a command line terminal using “Ctrl + alt + T” and type “ip a” to see if IP address is set, if IP address is set continue, else re-do the above step and restart the Ubuntu desktop machine. 

<img src="/images/posts/nest-map/ubip.PNG" style="display: block; margin: auto;" />

- #### **Command codes for installation of ZABBIX-AGENT and WORDPRESS**
<div style="background-color: #f0f8ff; border-left: 5px solid #007acc; padding: 10px; margin: 25px 0; font-style: italic; font-weight: bold;">
<p style="color: #333; font-size: 13px; line-height: 1.5;">
1.    sudo apt update<br>
2.    sudo apt install -y zabbix-agent<br>
Enter the zabbix configuration file<br>
3.    sudo nano /etc/zabbix/zabbix_agentd.conf<br>
Search manually for Server, ServerActive and Hostname (insert the host IP on which the server is stored for monitoring)<br>
4.    Server=192.168.200.2<br>
5.    ServerActive=192.168.200.2<br>
6.    Hostname=Zabbix server <!-- Zabbix server --> <span style="color: #007acc;">[Zabbix server]</span><br>
7.    sudo systemctl enable zabbix-agent <!-- Enable from system start-up --> <span style="color: #007acc;">[Enable from system start-up]</span><br>
8.    sudo systemctl start zabbix-agent <!-- To start agent installed --> <span style="color: #007acc;">[To start agent installed] </span><br>
9.    sudo systemctl status zabbix-agent <!-- To start agent installed --> <span style="color: #007acc;">[To check agent availability if active or not] </span><br>
    <a href="https://example-link.com" style="color: #007acc;"></a>
</p>
</div>
- #### Prequisite and dependecies for WORDPRESS installation 
To install WORDPRESS you need Apache2, Mysql, and Php
- #### Steps to install Apache
<div style="background-color: #f0f8ff; border-left: 5px solid #007acc; padding: 10px; margin: 25px 0; font-style:     italic; font-weight: bold;">
<p style="color: #333; font-size: 13px; line-height: 1.5;">
1.    sudo apt update<br>
2.    sudo apt install apache2 -y<br>
3.    sudo systemctl restart apache2 <!-- To restart the apache2 --> <span style="color: #007acc;">[To restart the apache2]</span><br>
4.    sudo systemctl start apache2 <!-- To start apache installed --> <span style="color: #007acc;">[To start apache2 installed] </span><br>
5.    sudo systemctl enable apache2 <!-- To start apache from system-boot up --> <span style="color: #007acc;">[To start apache from system-boot up] </span><br>
6.    sudo systemctl status apache2 <!-- To check availability installed --> <span style="color: #007acc;">[To check apache2 availability if active or not] </span><br>
<a href="https://example-link.com" style="color: #007acc;"></a>
</p>
</div>
- #### Steps to install Mysql server for database management
<div style="background-color: #f0f8ff; border-left: 5px solid #007acc; padding: 10px; margin: 25px 0; font-style: italic; font-weight: bold;">
<p style="color: #333; font-size: 13px; line-height: 1.5;">
1.    sudo apt update<br>
2.    sudo apt install mysql-server<br>
3.    sudo systemctl restart mysql <!-- To restart the mysql --> <span style="color: #007acc;">[To restart the mysql]</span><br>
4.    sudo systemctl start mysql <!-- To start mysql installed --> <span style="color: #007acc;">[To start mysql installed] </span><br>
5.    sudo systemctl enable mysql <!-- To start apache from system-boot up --> <span style="color: #007acc;">[To start mysql from system-boot up] </span><br>
6.    sudo systemctl status mysql <!-- To check availability installed --> <span style="color: #007acc;">[To check mysql availability if active or not] </span><br>
7.    sudo mysql_secure_installation<!-- anwswer yes to all question in this section --> <span style="color: #007acc;">[anwswer yes to all question in this section] </span><br>
8.    sudo mysql -u root -p <!-- To enter mysql database interface --> <span style="color: #007acc;">[To enter mysql database interface ]</span><br>
9.    CREATE DATABASE wordpress; <!--In the mtsql enviroment enter this script to build wordpress database--> <span style="color: #007acc;">[in the mysql enviroment enter this script to build wordpress database] </span><br>
10.    CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'your_password';<!--To create user named 'wordpressuser' set your password --> <span style="color: #007acc;">[To create user named 'wordpressuser' and set your password] </span><br>
11.   GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';<!--granting privileges and access--> <span style="color: #007acc;">[granting privileges and access] </span><br>
12.    FLUSH PRIVILEGES;<!--make all changes permanent--> <span style="color: #007acc;">[make all changes permanent] </span><br>
13.   EXIT;<!--To quit or leave--> <span style="color: #007acc;">[To quit or leave] </span><br> <a href="https://example-link.com" style="color: #007acc;"></a>
</p>
</div>
- #### Steps to install PHP server for database management
<div style="background-color: #f0f8ff; border-left: 5px solid #007acc; padding: 10px; margin: 25px 0; font-style: italic; font-weight: bold;">
<p style="color: #333; font-size: 13px; line-height: 1.5;">
1.    sudo apt update<br>
2.    sudo apt sudo apt install php libapache2-mod-php php-mysql php-cli php-xml php-curl php-json php-mbstring php-zip php-gd php-intl<br><!-- php, libraries and other dependecies installation --> <span style="color: #007acc;">[php and other dependecies installation] </span><br>
3.    sudo sudo apt install php-bcmath php-soap php-ldap php-imagick php-xsl php-opcache php-sqlite3 php-memcached php-redis<br><!-- compactibility dependecies installation -->
4.    sudo apt install php-fpm <!--(Optional fpm-php for nginx)--> <span style="color: #007acc;">[Optional fpm-php for nginx] </span><br>
5.    php -v <!-- To verify php and its version --> <span style="color: #007acc;">[To verify] </span><br>
6.   sudo a2enmod php <!-- Configure apache to work with php --> <span style="color: #007acc;">[Configure apache to work with php] </span><br>
7.   sudo systemctl restart apache2 <!-- Restarting apache --> <span style="color: #007acc;">[Restarting apache] </span><br>
<a href="https://example-link.com" style="color: #007acc;"></a>
</p>
</div>
- #### Gateway(Router) Configuration:
  Go to settings and then click NETWORK and set ADAPTER 1 to NAT, ADAPTER 2 for (desktop) to INTERNAL NETWORK and ADAPTER 3 for (opencart) to INTERNAL NETWORK
<img src="/images/posts/nest-map/g1.PNG" style="display: block; margin: auto;" />
<img src="/images/posts/nest-map/g2.PNG" style="display: block; margin: auto;" />
<img src="/images/posts/nest-map/g3.PNG" style="display: block; margin: auto;" />

Then click OK and click START to bootup the machine on the VM  

After starting up the machine use:  

**student@router:~$   sudo nano /etc/netplan/00-installer-config.yaml**  
to enter the network interface to configure the ADDRESS, NETMASK, and GATEWAY for all three (3) ADAPTERS. 
<img src="/images/posts/nest-map/setup.PNG" style="display: block; margin: auto;" />
Then use: student@router:~$ **sudo netplan apply** 	       (to apply new configuration) 

Then use: student@router:~$ **ip a**				(to view all IPs) 
<img src="/images/posts/nest-map/g5.PNG" style="display: block; margin: auto;" />

- #### Bitnami Opencart Server Configuration:
  Go to settings and then click NETWORK and set ADPATER 1 to INTERNAL NETWORK, then click OK and click START to bootup the machine on the VM
<img src="/images/posts/nest-map/st2.PNG" style="display: block; margin: auto;"/>

After starting up the machine use:  
bitnami@debian:~$   **sudo nano /etc/network/interfaces**  
to enter the network interface to configure the ADDRESS, NETMASK, and GATEWAY.

ADDRESS: 192.168.26.2	NETMASK: 255.255.255.0	GATEWAY: 192.168.126.1

<img src="/images/posts/nest-map/opc1.PNG" style="display: block; margin: auto;"/>

Then use **Ctrl + X** to save by pressing Y when asked do you want to save settings? 
Use: bitnami@debian:~$  **sudo reboot now**  

After reboot use: bitnami@debian:~$ **ip a** 	to see if IP Address is set. 

<img src="/images/posts/nest-map/opcst.PNG" style="display: block; margin: auto;"/>             

<!--more-->

I'm drawing inferences from an *n* of one, so take anything I say with a hefty grain of salt.[^time] While I'm structuring this post largely as pieces of advice, keep in mind that these were things that worked for me, and may not generalize.[^negotiation]

[^time]: Three months is also [far too short a time](https://archive.org/details/Science_Fiction_Quarterly_New_Series_v04n05_1956-11_slpn/page/n5/mode/2up?view=theater) to reach a definitive conclusion on this topic.

[^negotiation]: Talking to other data scientists with similar backgrounds, which I discuss [below](#things-to-do), was useful because it gave me information and context that I was able to draw on when negotiating salary. However, an extensive [body](https://www.newyorker.com/science/maria-konnikova/lean-out-the-dangers-for-women-who-negotiate) [of](https://hbr.org/2014/06/why-women-dont-negotiate-their-job-offers) [research](https://www.npr.org/2007/08/06/12529237/for-women-pay-negotiations-can-bear-social-cost) finds that women are penalized for negotiating where men are rewarded for it. This is just one reminder of the fact that something that I found helpful may be less useful for you.

# Differences from the academic job market

Some important differences between the academic and nonacademic job markets that are useful to consider at the start:

- Timelines are faster than faculty searches, but they are far less consistent. One process took almost three months, while another took less than three weeks.
- Not a single employer asked for letters of recommendation. One contacted references.
- Who you talk to varies greatly. For some positions my first contact was an HR phone screen, for others it was a 30 minute initial interview with the hiring manager.
- Performance tasks, otherwise known as coding assignments (or, more accurately, unpaid work), are common. These are just a fact of life for data science jobs. They varied from straightforward problem sets to research design memos, but not every job I interviewed for required them.
- There will probably be a technical interview. As these were not software engineering jobs, most of the ones I encountered tried to assess whether you know the basics of analyzing data in your language of choice and to get some insight into your problem solving approaches.
- Job talks are much less common, but not unheard of. Only two of the positions I interviewed for required a technical presentation, and unlike in academia, there is absolutely zero stigma against presenting coauthored work.
- Based on some very informal reckoning, automated HR rejection emails seem to be about as common for nonacademic jobs as academic ones.[^rejections] When they do come, these emails are much faster than in academia: days or weeks instead of months.
- Get ready for a new world of terminology and titles. In the same way that the assistant $\rightarrow$ associate $\rightarrow$ full professor progression baffles many outside of academia, I felt very lost upon encountering ads for senior, principal, and lead data scientists, and especially so when I applied to one for a data science technical adviser.
- Similarly, get ready to navigate the variety of different jobs that can fall under the umbrella of data scientist. Does a job list SQL, Tableau, and Excel as the most important technical skills? That's probably more of a data analyst position. TensorFlow, Dask, and C++? That's likely more of machine learning engineer job. If you're anything like me, you want to aim for the middle ground between these two.

[^rejections]: This was a pleasant surprise for me, as I still have vivid memories of sending résumé after résumé out into the void as a fresh poli sci BA in 2012 and almost never hearing back.

# The nonacademic résumé

Probably the biggest transition when starting to apply for data science jobs was the shift from an academic CV to a nonacademic résumé. A CV lists functionally every major accomplishment you've achieved in your time in the field, while a résumé is highly targeted for a specific position. When applying to academic jobs, I wrote a (semi) customized cover letter for every job, and then included the relevant version of my CV (conflict, methods, or teaching). Each of these CVs contained the same information, just in a different order. In contrast, I significantly edited the skills section of most résumés I sent out based on the job listing. The [WashU career center](https://students.wustl.edu/career-center) has a [fantastic handout](https://students.wustl.edu/wp-content/uploads/2021/02/Resumes-and-CVs-2021-Final-1.pdf) on differences between the two documents and how to adapt a CV into a résumé that I drew on heavily in this process.

In my opinion, the conventional wisdom that a résumé can only ever be one page is an overcorrection from the never-ending academic CV. The résumé I used to apply for jobs was two pages: the first included work experience, education, and a list of technical skills, while the second was project-oriented, and covered two publications, a couple of blog posts, a Shiny dashboard, teaching materials for the grad stats lab I taught. You definitely want to include links here, not just to the final product, but also the code behind it where relevant (replication materials for publications, git repos for smaller projects). This is an excellent opportunity to showcase work that uses data science skills to show something interesting, but wouldn't be considered novel enough for publication in an academic journal. Here are some other points that may be helpful when writing a résumé:

- No one is likely to care that you wrote an undergraduate thesis or received a masters in passing (I did both, neither are on my résumé). An important exception to the latter point applies if you will be leaving your program without finishing your PhD; definitely list an in-passing masters in this case. Similarly, if you received a masters in a separate (more technical) program during your PhD, e.g., statistics or data science, be sure to list it as well.
- Social sciences can be a bit out of left field for data science hiring managers, so my résumé did include a "Concentrations: quantitative methodology and international relations" sub-bullet under my PhD in my education section.
- Paid research assistant jobs you had in grad school absolutely count as work experience and should be listed separately from your research and teaching if relevant to the types of jobs you're applying for. I listed my jobs ensuring the reproducibility of quantitative results for academic journals and supporting users of university high performance computing resources as there's a very short line between both of those job descriptions and many common data science tasks.
- If a job ad lists a skill and you have that skill, put it on your résumé, even if it's not one of your strongest skills. Your résumé will almost certainly be fed through an [applicant tracking system](https://en.wikipedia.org/wiki/Applicant_tracking_system), and the more matches the system finds, the higher the chance your résumé will end up in front of human eyes.
- I would take this a step further and do this in your cover letter as well. Does a job ad list a "solid understanding of relevant theories in machine learning, statistics, and probability theory" in the requirements? Then you'd better be prepared to talk about how you apply machine learning, statistics, and probability in your work. Does this feel a little like undergraduates trying to avoid plagiarism detection software by changing a few words here and there? Yes, but it's how hiring happens these days.

# Things to do

Below is a list of non-résumé-related things I did to prepare for and during my nonacademic job search that I found helpful:

- As someone who (hubristically) deleted theirs the second year of grad school, it pains me to say that the most important thing you can do here is get yourself a LinkedIn. Get it looking as professional as your academic website. The first thing is to set the headline directly below your name to the type of job you're looking for. Want to be a research manager? List yourself as one and then talk about all the research assistants you coordinated. You'll have to do some reframing and shortening, but you can largely transfer over content from your academic website. I added publications and blog posts to the publications and projects section at the bottom of my profile, and I also added them as media items under my postdoc and PhD experiences where appropriate. Add a link or two with high quality preview images to the featured section at the top of your page.
- If you're applying for jobs now and you've taught a quantitative methods course at any point, get ready to talk about this. Every single interview asked me about a time where I had to explain a technical concept or project to a nontechnical audience, and teaching quantitative methods is nothing but that, multiple times a week, for an entire semester. Teaching statistics and programming is hard, so you'll also have lots of anecdotes ready when the interviewer asks a followup question about a time where you had to change your approach midway through a project. If you haven't taught quantitative methods yet and you're not already applying for jobs, do so if at all possible.
- Use your resources. I was fortunate enough to do my postdoc at an institution with an excellent career center that had multiple staff members with experience helping PhD students and postdocs get nonacademic jobs. However, even if your career center is less prepared to help you get a nonacademic job, lots of career centers have publicly available [online resources](https://students.wustl.edu/graduate-student-postdoc-career-resources) that can be very helpful.
- Use your networks. I talked with *many* people who work in data science and do not have degrees in computer science or statistics. This included two people from my undergraduate institution (one PhD in psychology, one in physics), multiple political science PhDs I met through Twitter and LinkedIn, and people who did data science masters and nonacademic data science bootcamps. Their experience and advice were invaluable for me in my job search process.
- Research salaries in the field you're applying to. You can get a broad sense of this through sites like Glassdoor, but ask the people I mentioned above about their starting salaries as well. They likely came from a similar background to you, and this information can be very useful when negotiating salary. You don't want to undersell yourself when an interviewer asks you your salary range.

# Software skills

Social science PhD programs are good at teaching research design, formal modeling, and statistical methodology. They spend far less time on what I'll call more supporting technical skills. Here are some suggestions in this domain based on my observations so far:

- Don't try to learn everything there is to know about a cloud computing architecture. There are too many, and every company's implementation is subtly different. At my job, we use AWS, GCP, and Azure for various tasks, so learning one inside and out won't give you a huge advantage when applying. If you can generate SSH keys and copy them to a remote host, you're most of the way there.
- Learn some SQL, but don't worry about learning how to administer a database. If you can write queries that join multiple tables together and summarize by multiple groups, you're probably good. If you know the standard libraries for connecting to and querying a SQL database in Python and/or R, that's great. Again, depending on the individual database solution your job uses, you may have to use a very specific package to access it from your data science language. Mode has a free [tutorial](https://mode.com/sql-tutorial/introduction-to-sql) with an interactive interface that lets you write and run SQL queries in your browser that I found very helpful.
- Get some experience with shell scripting. I was first exposed to shell scripts because you had to write one to submit jobs on our university cluster in grad school. Data science often involves many moving parts, and being able to use some shell scripting to glue them all together can be incredibly useful. Software Carpentry has a pretty solid introductory [lesson](https://swcarpentry.github.io/shell-novice).
- I use git daily. While I rarely used git to manage collaboration with coauthors in academia, I used it to version control all of my solo-authored projects, and that provided a solid-enough background for my current level of usage.
- Automation is another important skill in the data science toolbox. Sometimes you'll have fancy GUI-based tools to set things up to run automatically, but other times it's faster and simpler to use a [cron jobs](https://en.wikipedia.org/wiki/Cron). I taught myself the basics of cron to keep the stats in my post [visualizing police militarization via the transfer of surplus armored vehicles to police departments](/posts/2020/06/visualizing-militarization/) automatically updated.

# The social science PhD comparative advantage

So far this post has mainly been oriented around a list of discrete things you can do to (potentially) improve your odds of securing a data science job as someone with a social science PhD. This last section reflects a perspective I developed throughout my job search process as I participated in more and more interviews, and I hope, will serve as a source of motivation for anyone pursuing a similar career transition.

The vast majority of quantitative social science PhDs (myself very much included) are never going to be machine learning engineers who run neural networks all day long. Instead, we're going to be working with those engineers, running our own analyses (which might include some deep learning models, but plenty of other types of models as well), and also working with with less-technical stakeholders.

Based on conversations with other data scientists and my experiences as a data scientist thus far, a large part of a data scientist's job is communicating the value of the work you and your more-technical team members have done to people with less technical training. Even if they have a strong background in statistics or research design more generally, they're still likely to be less familiar with your specific area of expertise. Communicating effectively in this situation requires distilling large amounts of information, drawing conclusions based on data, and then summarizing what you did, why you did it, and what you learned from doing it. To me, that sounds exactly like what social science PhD programs train their students to do.[^concrete]

[^concrete]: To make this even more concrete: being able to communicate effectively with software engineers means that they help make your models more efficient with less work from you; being able to communicate with stakeholders means that you are more likely to get recognition for the work you did.
