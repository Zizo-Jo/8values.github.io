# 8values on AWS

This project deploys the 8values political quiz(https://github.com/8values/8values.github.io) website to AWS using Terraform. The infrastructure consists of an S3 bucket to host the static website content and a CloudFront distribution to serve the content globally with low latency.

## Infrastructure

The following resources are created by this Terraform configuration:

- **aws_s3_bucket**: An S3 bucket to store the static website files (HTML, CSS, JavaScript, images).
- **aws_cloudfront_origin_access_identity**: An Origin Access Identity (OAI) to restrict direct access to the S3 bucket, ensuring that users can only access the website through the CloudFront distribution.
- **aws_cloudfront_distribution**: A CloudFront distribution to cache the website content at edge locations around the world, providing low-latency access to users.
- **aws_s3_bucket_policy**: A bucket policy that grants the CloudFront OAI permission to read objects from the S3 bucket.

## Deployment

To deploy the 8values website to your AWS account, follow these steps:

1. **Clone this repository.**
2. **Configure your AWS credentials.** Make sure you have the AWS CLI installed and configured with your access key and secret key.
3. **Initialize Terraform.** Run `terraform init` to initialize the Terraform working directory.
4. **(Optional) Change the bucket name.** If you want to use a different name for the S3 bucket, modify the `bucket` argument in the `aws_s3_bucket` resource in `main.tf`.
5. **Deploy the infrastructure.** Run `terraform apply` to create the AWS resources.
6. **Upload the website files.** After the infrastructure is created, you need to upload the 8values website files to the S3 bucket. You can do this using the AWS Management Console or the AWS CLI. (Or sync by the terminal: aws s3 sync /your/local/path://your-s3-unique-name --delete)
7. **Access the website.** Once the files are uploaded, you can access the website through the CloudFront distribution's domain name. You can find this domain name in the `outputs.tf` file or in the AWS Management Console.

## Cleanup

To destroy the infrastructure created by this project, run `terraform destroy`.
