

## Jenkins File For Declarative Syntax for CI/CD of  Terraform  

- Current url is  http://ec2-54-157-255-249.compute-1.amazonaws.com:8080/
-  i  want to change port
###  Re-directing Port  via iptables
```

sudo iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 9001 -j REDIRECT --to-port 8080
sudo sh -c "iptables-save > /etc/iptables.rules"
```
- now both urls are working

```
below both url are working

root@ip-192-168-0-252:~#
root@ip-192-168-0-252:~# sudo iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 9001 -j REDIRECT --to-port 8080
root@ip-192-168-0-252:~# sudo sh -c "iptables-save > /etc/iptables.rules"
root@ip-192-168-0-252:~#

http://ec2-54-157-255-249.compute-1.amazonaws.com:9001
http://ec2-54-157-255-249.compute-1.amazonaws.com:8080
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  samba



```

- Jenkinsfile
```
/*Jenkins File For Declarative Syntax for CI/CD of Git Packer Terraform */
pipeline {
    agent any

    stages {
        stage('Clone Git Repo') {

            steps {
                sh 'rm -rf Jenkins31-DP'
                sh 'git clone -b Jenkins31-DP  https://github.com/Shiva-Juturi/Jenkinsday3-DP.git  Jenkins31-DP'
                sh 'ls -al'
            }
        }

        stage('Terraform Plan') {
             when {
                    expression {
                        params.PLAN == 'YES'
                    }
                }
            steps {
                dir('Jenkins31-DP/Jenkins3-DP') {
                    sh 'terraform init'
                    sh 'terraform plan'
                }
            }
        }
        stage('Terraform Apply') {
             when {
                    expression {
                        params.APPLY == 'YES'
                    }
                }
            steps {
                dir('Jenkins31-DP/Jenkins3-DP') {
                    sh 'terraform init'
                    sh 'terraform apply --auto-approve'
                }
            }
        }
        stage('Terraform Destroy') {
            when {
                    expression {
                        params.DESTROY == 'YES'
                    }
                }
            steps {
                dir('Jenkins31-DP/Jenkins3-DP') {
                    sh 'terraform init'
                    sh 'terraform destroy --auto-approve'
                }
            }
        }
    }
}


```

```
root@ip-192-168-0-252:~# git clone https://github.com/Shiva-Juturi/Jenkins3-DP.git
Cloning into 'Jenkins3-DP'...
Username for 'https://github.com': shiva2cloud.juturi@gmail.com
Password for 'https://shiva2cloud.juturi@gmail.com@github.com':
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 9 (delta 1), reused 9 (delta 1), pack-reused 0
Unpacking objects: 100% (9/9), 954.58 KiB | 12.73 MiB/s, done.
root@ip-192-168-0-252:~#

```
- i need to set these in windows
```

git config --global user.name "XXXXX"
git config --global user.email "XXXXXXX"
git config --global user.password "XXXXX"
git config --global credential.helper store
git config --list --show-origin

```


- i have repository (https://github.com/Shiva-Juturi/Jenkinsday3-DP.git) it has main and  Jenkins31-DP  branches
- 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

# Jenkins Config Backup
- for this we can see the

```
In fact you have just to use this url to reactivate your deleted job : http://[url_of_jenkins]/jobConfigHistory/?filter=deleted


Download Plugin Job Config History

Download steps:- Manage Jenkins -> Manage Plugin -> Available -> JobConfigHistory Download and install

After Installation step:- Jenkins -> Job Config History -> Show deleted jobs only and restore the jobs
http://[url_of_jenkins]/jobConfigHistory/?filter=deleted

http://ec2-54-157-255-249.compute-1.amazonaws.com:8080/jobConfigHistory/?filter=deleted




```

# RBAC

- Role-based Authorization Strategy
