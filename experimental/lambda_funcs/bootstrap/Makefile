all: package-bootstrap

help:
	@echo "Please use \`make <target>' where <target> is one of"
	@echo "  package-bootstrap      to package the lambda function"
	@echo "  update-bootstrap       to update the lambda function in AWS. 


vpx-1nic-bootstrap.zip: bootstrap.py 
	zip  -r9 vpx-1nic-bootstrap.zip bootstrap.py 

package-bootstrap: vpx-1nic-bootstrap.zip
	@echo "create/update lambda deployment package (vpx-bootstrap.zip)"

update-bootstrap:  package-bootstrap
	@echo "Copying lambda deployment package to region-specific buckets"
	for r in "us-east-1" "us-east-2" "us-west-1" "us-west-2" "eu-west-1" "eu-west-2" "eu-central-1" "ca-central-1" "ap-south-1" "ap-northeast-2" "ap-southeast-1" "ap-southeast-2" "ap-northeast-1" "sa-east-1" ; do \
	    aws s3 cp ${PWD}/vpx-1nic-bootstrap.zip s3://netscaler-cft-fn-$$r ; \
	    aws --region=$$r s3api put-object-acl --acl public-read --bucket netscaler-cft-fn-$$r --key vpx-1nic-bootstrap.zip ;\
	done

