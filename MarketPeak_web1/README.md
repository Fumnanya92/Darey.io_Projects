# MarketPeak_Ecommerce2


## 1.	Git Version Control setup
Step 1: Opening a project Directory on my terminal
I opened my mobaxterm terminal and navigated to the directory git-project [cd /home/mobaxterm/Desktop/Darey.io/git-project], I created another folder named MarketPeak_Ecommerce2/
Using [mkdir MarketPeak_Ecommerce2]. 
Cd MarketPeak_Ecommerce2
## Step 2. Prepare an Ecommerce website
I downloaded a copy of an Ecommerce website template from tooplate.com. Then extracted the folder into MarketPeak_Ecommerce2 directory 
## Step 3. Stage and commit the website templete to Git. 
I logged into my Github account, I created a remote repository with title MarketPeak_Ecommerce2, without initializing a README.md, gitognor or licences
echo "# MarketPeak_Ecommerce3" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Fumnanya92/MarketPeak_Ecommerce2.git
git push -u origin main
I use git add. To track the templete, the I commit again with git commit -m main and finally push 
With git push origin main.

2.	Aws Development 
a.	Ec2 instance setup:
Once I logged into my Aws account I navigated to the EC2 Dashboard.  I click on the "Launch Instance" button to start the instance creation process. Choose an Amazon Machine Image (AMI)" Search and "Amazon Linux 2023" in the search bar. 
I created my pem key saved in the Capstone/ directory, proceeded to configure Instance details. I left most on default settings except I selected the “Allow HTTP traffic from the internet” option. 
Review all the details of your instance to ensure everything is correct. I Launched the instance. Navigated back to the EC2 Dashboard.

3.	Cloning the repository on the linux server(Https)
First I used [yum install git] to install Git to my linux server. 
I navigated to my repository on Github, copied the Https link from the ‘code’ dropdown.
Navigated back to my terminal where git had finished installing and then pasted it to clone  my repository in on linux.
git clone  https://github.com/Fumnanya92/MarketPeak_Ecommerce2.git

4.	Installing web server httpd[Apache]
I ran 
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd

to install the latest update of Apache to my server and to enable the webserver on my Ec2 instance

5.	Configure httpd for website
I used [sudo rm -rf /var/www/html/*] to clear the default httpd web directory and then I used [sudo cp -r ~/MarketPeak_Ecommerce2/* /var/www/html/] to move my templete into Apache directory /var/www/html/MarketPeak_web1. Then I used sudo system reload httpd to reload Apache.

6.	Accessing the website 
I navigate back to my ec2 dashboard and copy the running ec2 public Ip address. Opened a fresh browser and paste http://44.206.236.195/MarketPeak_web1/

7.	Continuous integration and Continuous Development [CI/CD] 
I created a development branch on git with the command [git branch development]
I entered the development “workspace” with [git checkout development]. 
I edited the index.html file with [vim index.html], [git add .] to track the file, [git commit -m “new text added”]. I [git push origin development].
I used git checkout main to move into the main branch ‘workspace’, and the [git merge development] to merge changes to  the main branch. Finally I [git push main] to push update to remote repository. 
I reloaded httpd with [sudo systemctl reload httpd]. It works

Challenges
Cloning the repository on the linux server: I tried cloning the git repository in my Ec2 instance as instructed with Https or Ssh, but this didn’t work. So, I did a little research online and saw that I needed to first install git on my Linux. I used [yum install git] to achieve this.






