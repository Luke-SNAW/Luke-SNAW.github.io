
## Github

### Secret key

- S3_CODEDEPLOY\_\_AWS_SECRET_ACCESS_KEY

[https://docs.aws.amazon.com/codedeploy/latest/userguide/instances-ec2-configure.html](https://docs.aws.amazon.com/codedeploy/latest/userguide/instances-ec2-configure.html)

### Actions

```yaml
- name: Make zip file
  run: zip -qq -r ./$BRANCH.zip ./www-new ./code-deploy ./appspec.yml
  shell: bash
```

## Code Deploy Agent

### [설치](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ubuntu.html)

> wget https://aws-codedeploy-ap-northeast-1.s3.ap-northeast-1.amazonaws.com/latest/install
> chmod +x ./install

### 설정

> vi /etc/codedeploy-agent/conf/codedeploy.onpremises.yml

```yaml
aws_access_key_id: AKIASOOTGVZGPVLXFZWT
aws_secret_access_key: <Key>
iam_user_arn: arn:aws:iam::*:user/CodeDeployUser-Test
region: ap-northeast-1
```

### Service command

https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install.html

```shell
sudo service codedeploy-agent start
sudo service codedeploy-agent status
```

### Code Deploy와 연결(aws cli 설치)

```shell
aws deploy register-on-premises-instance --instance-name "[TEST] GP_WEB" --iam-user-arn arn:aws:iam::*:user/CodeDeployUser-Test --region ap-northeast-1

aws deploy register-on-premises-instance --instance-name GP_Renewal_TestServer --iam-user-arn arn:aws:iam::*:user/CodeDeployUser-Test --region ap-northeast-1

aws deploy add-tags-to-on-premises-instances --instance-names GP_Renewal_TestServer --tags Key=CodeDeploy,Value=Web-Test --region ap-northeast-1

aws deploy remove-tags-from-on-premises-instances --instance-names GP_Renewal_TestServer --tags Key=Name --region ap-northeast-1

aws deploy list-on-premises-instances --region ap-northeast-1
```
