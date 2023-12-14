---
layout: post
title: AWS S3 Credentials for Discourse
date: 2023-12-13
categories: ['AWS']
tags: ['IAM', 'S3', 'Discourse']
---

## Setting Up AWS S3 Credentials for Discourse

As a senior engineer and tech enthusiast, I'm always excited to share insights into configuring and optimizing tech platforms. Today, I'm delving into the process of generating AWS S3 credentials specifically for Discourse, a popular open-source discussion platform.

### Step-by-Step Guide

1. **Log in to AWS Management Console**: Access your AWS account and go to the IAM dashboard.

2. **Create a New IAM User**:
   - Enter a user name, such as `DiscourseS3User`.
   - Choose "Programmatic access" to receive an access key ID and secret access key.

3. **Set Permissions**:
   - It's crucial to assign appropriate permissions. For Discourse, you generally need access to a specific S3 bucket. I recommend a more restrictive policy than `AmazonS3FullAccess` for enhanced security.

4. **Review and Create User**:
   - After reviewing your settings, create the user.

5. **Save the Credentials**:
   - Carefully save the provided access key ID and secret access key. They are critical for the next steps and won't be shown again.

6. **Configure Discourse**:
   - In your Discourse settings, enter these credentials under the file upload or S3 settings section.

### Security and Management Tips

It's essential to practice the principle of least privilege in permission assignment. Regularly reviewing and rotating IAM credentials is also a wise security measure.

I hope this guide assists you in securely integrating AWS S3 with Discourse. Stay tuned for more tech tips and insights!
