

##

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
                sh 'rm -rf terraformsingleinstance'
                sh 'git clone -b Jenkins3-DP https://github.com/Shiva-Juturi/Jenkins3-DP.git'
                sh 'ls -al'
            }
        }

        stage('Terraform Plan') {
             when {
                    expression {
                        params.PLAN == 'NO'
                    }
                }
            steps {
                dir('Jenkins3-DP') {
                    sh 'terraform init'
                    sh 'terraform plan'
                }
            }
        }
        stage('Terraform Apply') {
             when {
                    expression {
                        params.APPLY == 'NO'
                    }
                }
            steps {
                dir('Jenkins3-DP') {
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
                dir('Jenkins3-DP') {
                    sh 'terraform init'
                    sh 'terraform destroy --auto-approve'
                }
            }
        }
    }
}

```
