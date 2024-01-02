# Architecture Best Practicies

## Secure access to public S3 buckets serving static content behind CloudFront to prevent DDos attack.

https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency/web-application-delivery-at-the-edge-bp1.html

If you’re using Amazon Simple Storage Service (Amazon S3) to serve static content on the internet, AWS recommends you use Amazon CloudFront to protect your bucket providing the following benefits:

* Restricts access to the Amazon S3 bucket so that it's not publicly accessible.
* Makes sure that viewers (users) can access the content in the bucket only through the specified CloudFront distribution—that is, prevents them from accessing the content directly from the bucket, or through an unintended CloudFront distribution.

To achieve this, configure CloudFront to send authenticated requests to Amazon S3, and configure Amazon S3 to only allow access to authenticated requests from CloudFront. CloudFront provides two ways to send authenticated requests to an Amazon S3 origin: origin access control (OAC) and origin access identity (OAI). We recommend using OAC.

