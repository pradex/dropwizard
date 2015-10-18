FROM gcr.io/oauth-1710/oracle8u60

RUN mkdir dropwizard

COPY dropwiz-exp.zip dropwizard/

#Installing ca-certificates is a must to verify googleapis.com
RUN sudo apt-get update && sudo apt-get install -y unzip && sudo apt-get install -y ca-certificates

WORKDIR dropwizard/

RUN unzip dropwiz-exp.zip

WORKDIR dropwizard-example/

#Execution Command along with agent information for cloud debugging
CMD java -jar target/dropwizard-example-0.9.0-rc4-SNAPSHOT.jar db migrate example.yml && java $( wget --no-check-certificate -q -O - https://storage.googleapis.com/cloud-debugger/compute-java/format_env_gce.sh | \
  sudo bash -- /dev/stdin --app_class_path=target/dropwizard-example-0.9.0-rc4-SNAPSHOT.jar --version=1.0.0 \
  --enable_service_account_auth --verbose --project_id=oauth-1710 \
--project_number=364426739259 --service_account_email=364426739259-opjf8ghcov7iutcr3dvmhmrgrufpqc0g@developer.gserviceaccount.com \
--service_account_p12_file=oauth-project-e9b592592ac8.p12 ) -jar target/dropwizard-example-0.9.0-rc4-SNAPSHOT.jar server example.yml
