<link href="/images/images.css" rel="stylesheet"></link>
<div>
  <style>
    img[alt=small] {
      width: 300px;
    }
  </style>
</div>
# Cloud Computing

## What is cloud computing?
Cloud computing is the on-demand availability of computer system resources, especially data storage and computing power, without direct active management by the user. Large clouds often have functions distributed over multiple locations, each of which is a data center.

## Serverful Models
![small](images/IaaS_PaaS_SaaS.jpg)
### Software as a Service (SaaS)
 - Cloud provider gives access to applications on a subscription basis
### Platform as a Service (PaaS)
 - Cloud provider gives access to servers with operating systems and tools
### Infrastructure as a Service (IaaS)
 - Cloud providergives access to bare servers
## Why should you use cloud computing and its benefits

### Flexibility
  1. Scalability: Cloud infrastructure scales on demand to support fluctuating workloads.
  2. Storage options: Users can choose public, private, or hybrid storage offerings, depending on security needs and other considerations.
  3. Control choices: Organizations can determine their level of control with as-a-service options. These include software as a service (SaaS), platform as a service (PaaS), and infrastructure as a service (IaaS).
  4. Tool selection: Users can select from a menu of prebuilt tools and features to build a solution that fits their specific needs.
  5. Security features: Virtual private cloud, encryption, and API keys help keep data secure.

### Efficiency

 1. Accessibility: Cloud-based applications and data are accessible from virtually any internet-connected device.
 2. Speed to market: Developing in the cloud enables users to get their applications to market quickly.
 3. Data security: Hardware failures do not result in data loss because of networked backups.
 4. Savings on equipment: Cloud computing uses remote resources, saving organizations the cost of servers and other equipment.
 5. Pay structure: A “utility” pay structure means users only pay for the resources they use.

### Strategic value
 1. Streamlined work: Cloud service providers (CSPs) manage underlying infrastructure, enabling organizations to focus on application development and other priorities.
 2. Regular updates: Service providers regularly update offerings to give users the most up-to-date technology.
 Collaboration: Worldwide access means teams can collaborate from widespread locations.
 1. Competitive edge: Organizations can move more nimbly than competitors who must devote IT resources to managing infrastructure.


## Who is AWS?
Amazon Web Services provides on-demand cloud computing platforms and APIs to individuals, companies, and governments, on a metered pay-as-you-go basis. These cloud computing web services provide distributed computing processing capacity and software tools via AWS server farms.

Some companies who use AWS:
 - Adobe
 - Docker
 - Netflix
 - Ubisoft
 - UCAS
 - Spotify
 - Sony

## Cap-ex vs Op-ex

 - Capital expenditures (CapEx) are major purchases a company makes that are designed to be used over the long term. 
   - buildings 
   - equipment 
   - machinery
   - vehicles
 - Operating expenses (OpEx) are the day-to-day expenses a company incurs to keep its business operational.
   - utilities
   - property taxes
   - cost of goods sold (COGS)

## Setup VM instance on AWS

1. Go to the EC2 page on AWS and click on this button (labeled in red)

![ec2 large](images/EC2_home_page.png)

2. Provide all information asked (apart from Advanced at the bottom, unless needed)
  1. Ensure you select the appropriate operating system and plan so you don't get charged
  2. Select key pair if you have it, if not create a new one
  3. Select your network security group (create a new one if you don't have one)
  4. Allow http trafic if you need to host website
      1. Not https as you probably do not have the required key
  5. If you want to enable SSH connection make sure you use your IP instead of the default `0.0.0.0/0` 
  6. You can use a different amount of storage if you want but 8GiB should be enough
3. Click on `Launch Instance` if ready
4. If you recieve any errors try to fix them and try again
5. Go to the Instances tab on the left and click it, you should see your instance running or initialising

## Editing incoming rules for network security
1. Head to your instace tab (code with letters and numbers that has a typical hyperlink look)
2. Go to the Security tab and click on the hyperlinked security group code
3. From there at the bottom right you should see "Edit inbound rules"
   1. Go in there and create any rule for any port you want 

## Setup reverse proxy with `nginx`
# How to set up reverse proxy with nginx / #

1. Go to your home location (default location, no folders)
2. `cd /etc/nginx/sites-available`
3. `sudo nano default` - ensure you use sudo, otherwise you wont be able to edit
4. look for the server block
5. within server, look for location block
6. write the following commands (ensure any other lines are deleted from that block):

    ```
        location / {
                proxy_pass http://localhost:8080;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
            }
    ```

7. replace "8080" with whatever port you need
8. Press Ctrl + x to begin exit
9. Press Y to agree to changes
10. Press Enter to save and exit
11. sudo nginx -t
    1. testing the syntax
12. sudo systemctl restart nginx
13. npm start
14. You are good to go

## Providing SSH key

1. Locate your `.pem` file containing the key
2. **Move** it to the `.ssh` folder (so C:Users/name/.ssh)