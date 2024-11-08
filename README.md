
# PollyNarrator

## Project Description
The **PollyNarrator** project leverages AWS services to convert text files (such as random text files,blog posts, articles, newsletters) into speech. This is particularly useful for creating audio versions of written content, making it accessible to a wider audience, including those who prefer listening over reading.

## Use Cases
- **Content Accessibility**: Provides audio versions of written content for visually impaired users.
- **Learning**: Enables users to listen to educational materials, enhancing learning experiences.
- **Content Distribution**: Offers an additional medium for content consumption, increasing engagement.
- **Convenience**: Allows users to listen to articles or books while multitasking, such as during commutes or workouts.

## Project Architecture
The system is built around AWS services such as S3 (Simple Storage Service), Lambda, and Polly, and follows a serverless architecture. The process flow is as follows:
1. A `.txt` file is uploaded to the source S3 bucket.
2. The Lambda function is triggered by an event notification from S3.
3. The text is processed by AWS Polly to convert it into an audio file.
4. The resulting `.mp3` file is stored in the destination S3 bucket, ready for download.

---

## Steps to Build the Project

### Step 1: Set Up an AWS Account
Create an AWS account if you don't have one and set up billing information.

### Step 2: Create Two S3 Buckets
- **Source S3 Bucket Name**: `amc-polly-source-bucket`
- **Destination S3 Bucket Name**: `amc-polly-destination-bucket`

### Step 3: Create an IAM Policy
Create an IAM policy that allows access to S3 and Polly services.

**IAM Policy Name**: `amc-polly-lambda-policy`

**Policy Definition**:
```json
{
  "Version": "2012-10-17",
  "Statement": [
      {
          "Effect": "Allow",
          "Action": [
              "s3:GetObject",
              "s3:PutObject"
          ],
          "Resource": [
              "arn:aws:s3:::amc-polly-source-bucket/*",
              "arn:aws:s3:::amc-polly-destination-bucket/*"
          ]
      },
      {
          "Effect": "Allow",
          "Action": [
              "polly:SynthesizeSpeech"
          ],
          "Resource": "*"
      }
  ]
}
