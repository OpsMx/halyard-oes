FROM quay.io/opsmxpublic/ubifips:8.7
MAINTAINER sig-platform@spinnaker.io
LABEL name='halyard'
LABEL maintainer='info@opsmx.io'
LABEL release=1
LABEL version='1.28.4'
LABEL summary='Red Hat certified Open Enterprise Spinnaker ubi8 container image for clouddriver'
LABEL description='Certified Open Enterprise Spinnaker is an Enterprise grade, Red Hat certified and OpsMx supported release of the popular and critically acclaimed Continuous Delivery platform Spinnaker'
LABEL vendor='OpsMx'
COPY halyard-web/build/install/halyard /opt/halyard

ENV KUBECTL_VERSION v1.22.0


#ENV KUBECTL_RELEASE=1.15.10
#ENV AWS_BINARY_RELEASE_DATE=2020-02-22
#ENV AWS_CLI_VERSION=1.18.18

#RUN apk --no-cache add --update \
#      bash \
#      curl \
#      openjdk11-jre \
#      openssl \
#      py-pip \
#      python \
#  && pip install --upgrade awscli==${AWS_CLI_VERSION} \
#  && apk --purge del \
#       py-pip \
#  && rm -rf /var/cache/apk

RUN yum -y install bash unzip wget unzip procps java-17-openjdk-devel python2 vim  net-tools curl git
RUN yum -y update



RUN echo '#!/usr/bin/env bash' > /usr/local/bin/hal && \
  echo '/opt/halyard/bin/hal "$@"' >> /usr/local/bin/hal && \
  chmod +x /usr/local/bin/hal



#RUN curl -f -LO --retry 3 --retry-delay 3 https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_RELEASE}/bin/linux/${TARGETARCH}/kubectl && \
#    chmod +x ./kubectl && \
#    mv ./kubectl /usr/local/bin/kubectl

RUN wget https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl && \
  chmod +x kubectl && \
  mv ./kubectl /usr/local/bin/kubectl
  
  
RUN adduser spinnaker
USER spinnaker

CMD ["/opt/halyard/bin/halyard"]
  
  
