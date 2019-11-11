FROM docker.pkg.github.com/ksivamuthu/cei-k8s-ops/k8s-ops:latest

ENV AWS_CLI_VERSION=1.16.277
RUN curl -o aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/aws-iam-authenticator
RUN chmod +x aws-iam-authenticator && mv aws-iam-authenticator /usr/local/bin

RUN pip3 install --no-cache-dir awscli==${AWS_CLI_VERSION}
