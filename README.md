# Sprint 9: Course Drop Impact

Suggested students not copy parts for coursework

## Initial Setup
Clone the files and run our install script, this will install nginx, nodejs, and npm if you don't already have it. It will also run npm install to install and setup our node dependencies.
```
git clone https://gitlab.socs.uoguelph.ca/cmifsud/w22_cis3760_team07.git
sudo ./install.sh
```

## Setting Up The Server
In order to set up flask we must run the following commands from the root directory

Create a Python Virtual Environment in the flask directory and download necessary dependencies:
```
cd flask
python3 -m venv venv
. venv/bin/activate
pip install -r requirements.txt
```

In order to run our NGINX server we need to put our react build files in a place where NGINX knows to look.

Before running this command, we need to make sure the `project.service` file located in the `nginxconfig` folder is updated with our information.
```
[Unit]
Description=uWSGI instance to serve project
After=network.target

[Service]
# ADD YOUR OWN USER INFO HERE
User=sysadmin
Group=www-data

# ADD YOUR OWN PATHS HERE
# include path to the flask directory
WorkingDirectory=/home/sysadmin/w22_cis3760_team07/flask
Environment="PATH=/home/sysadmin/w22_cis3760_team07/flask/venv/bin"
ExecStart=/home/sysadmin/w22_cis3760_team07/flask/venv/bin/uwsgi --ini wsgi.ini

[Install]
WantedBy=multi-user.target
```

From the root directory of the project folder, run this script:
```
./nginx_setup.sh
```

The NGINX server is now setup. 

Next we need to start the uWSGI server:
```
sudo systemctl start project
sudo systemctl enable project
```

The server should now be up and running.

## Website
Our website link: https://131.104.49.101/

## API Endpoints
To get all Guelph courses: https://131.104.49.101/api/courses/guelph

To get all Waterloo courses: https://131.104.49.101/api/courses/waterloo

To get all Caterloo courses: https://131.104.49.101/api/courses/carleton

Course search queries can be made here: 

https://131.104.49.101/api/course-search/guelph

https://131.104.49.101/api/course-search/waterloo

https://131.104.49.101/api/course-search/carleton

# Weights and Work Completed
The burndown and burnup charts for this week can be found here: [Burndown Chart](https://gitlab.socs.uoguelph.ca/cmifsud/w22_cis3760_team07/-/milestones/9#tab-issues)

For this sprint we had 3 meetings throughout the week:
- 2 hour initial meeting for sprint planning, discussion of programming process and creating issues.
- 1 hour mid-week meeting to discuss improvments on accessibility throughout the website
- 1 hour end-week meeting to finalize all changes, finish slide show presentation and complete final website adjustments
