

### Git Commands

1. How do you set up a script to run every time a repository receives new commits through push? <br>

This can be achieve by Git-hooks.
In any repo we have ~/.git/hooks folder we can have shell scripts to apply any kind of the actions while committing the changes
<br>

    git help hooks



2. How do you find a list of files that have changed in a particular commit? <br>

We can find the changed files by simply running below command

    git show <git_commit_hash>

In Git CLI we can find git commit message by running below command in repo
<br>

    git log


### Docker

Below Dockerfile could used to create node.js application with IST time zone and runnng the app as non-root user

```

# Dockerfile 

FROM node:current-alpine


# Set the time zone
ENV TZ="Asia/Calcutta"
RUN date


# 8877 is the user id for non-root user

RUN useradd -u 8877 om
# Change to non-root privilege user
USER om

```


Steps to build and run docker image
```
# Build docker image from Dockerfile
docker build -t node:0.1.0 .

# Mounting host volume with image volume
docker run -d --memory="16g" --restart=on-failure -p 8080:8080 -v /root/app/src:/root/app/src  -it node:v0.1.0

Note: Assuming system max memory in 16GB

```

<br>


### Security

<br>

1. How to block the ports oon Ubuntu server

Command to install firewalld

```
apt-get install firewalld
```

Command to block port number

```
sudo firewall-cmd --remove-port=22/tcp --permanent
```

2. Steps to setup port forwarding on linux VM

```
sudo apt-get update
sudo apt-get install nginx
sudo nano /etc/nginx/sites-enabled/default


#Update above default file as below
server {
    listen 10.10.123.1232:80 default_server; # random IP
}
```
```
# To verify we can run curl command

curl -k -vvv 10.10.123.1232

```

### Network
<br>
1. Show list of process using the network

```
netstat -punta | awk {'print $5, $7'}
```

2. Show the list of IPs a process is connected

```
ss -tun state connected
```

3. Show how to list open files and kill process tied to a user

```
# To list open files tied to root
lsof -u username

# To kill the process tied to user
kill -9 $(lsof -t -u username)
```


<br>

### Code

<br>

```

class Demo:

    def __init__(self, min_range, max_range):
        self.min_range = min_range
        self.max_range = max_range

    def print_manager(self):

        for x in range (self.min_range, self.max_range + 1):

            if x % 3 == 0 and x % 5 == 0: # If the number are multiple of 3 and 5 both
                print('AVAAMO', x)
            elif x % 5 == 0: # if number are multiple of only 5
                print('AMO', x)
            elif x % 3 == 0: # if number are multiple of only 3
                print('AVO', x)
            else:  # else continue to next number
                continue

# define min and max range
MIN_RANGE = 1
MAX_RANGE = 100

obj1 = Demo(MIN_RANGE, MAX_RANGE)
obj1.print_manager()

```
