# Amazon S3 Static Website Hosting Mini Project

Hey there! This is a straightforward, responsive static website built specifically for hosting on Amazon S3. It comes with a clean homepage and a custom 404 error page, showing off the basics of static site hosting on AWS with solid error handling. Perfect for anyone dipping their toes into cloud hosting.

## What's Inside

- **Responsive Design**: Looks great on phones, tablets, and desktops without any fuss.
- **Custom Error Page**: A friendly 404 page that keeps the AWS vibe going.
- **AWS Ready**: Tailored for S3 static website hosting right out of the box.
- **Lightweight**: Just HTML and CSS—no JavaScript needed, so it loads super fast.
- **Performance Focused**: Keeps things simple for quick, reliable performance.

## Project Layout

```
base-index-error-html/
├── index.html          # Your main landing page
├── error.html          # The custom 404 page
└── README.md           # This guide you're reading
```

## What You'll Need

- An AWS account with the right permissions to mess around with S3.
- AWS CLI set up (handy for automated stuff, but not mandatory).
- A bit of familiarity with AWS S3 and static websites—nothing too crazy.

## Getting Started

### Step 1: Grab the Code

```bash
git clone <repository-url>
cd base-index-error-html
```

### Step 2: Test It Locally

Just open `index.html` in your browser to see how it looks. Easy peasy!

### Step 3: Get It Live on S3

#### Option 1: Manual Upload via AWS Console

1. **Set Up Your S3 Bucket**:
   - Head over to the AWS S3 Console.
   - Make a new bucket (something like `my-static-website-bucket`).
   - Turn on public access and static website hosting.

2. **Upload Your Files**:
   - Drop `index.html` and `error.html` into the bucket.
   - Point to `index.html` as your index document.
   - Set `error.html` as the error document.

3. **Sort Out Permissions**:
   Slap this bucket policy on to let everyone read your files:

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "PublicReadGetObject",
               "Effect": "Allow",
               "Principal": "*",
               "Action": "s3:GetObject",
               "Resource": "arn:aws:s3:::my-static-website-bucket/*"
           }
       ]
   }
   ```

4. **Check It Out**:
   Your site should be live at: `http://my-static-website-bucket.s3-website-region.amazonaws.com`

#### Option 2: Automated with AWS CLI

```bash
# Make the bucket
aws s3 mb s3://my-static-website-bucket --region us-east-1

# Turn on static hosting
aws s3 website s3://my-static-website-bucket --index-document index.html --error-document error.html

# Upload the files
aws s3 cp index.html s3://my-static-website-bucket/index.html --acl public-read
aws s3 cp error.html s3://my-static-website-bucket/error.html --acl public-read

# Apply the public policy
aws s3api put-bucket-policy --bucket my-static-website-bucket --policy file://bucket-policy.json
```

## Making It Your Own

### Tweak the Look
- Play around with the CSS inside the `<style>` tags in both HTML files.
- It uses the Amazon Ember font to match AWS's style—feel free to swap it out.
- Colors, spacing, everything's up for grabs.

### Change the Content
- Edit the text in `index.html` and `error.html` to say what you want.
- Add more pages by making new HTML files.
- Just remember to use relative paths for any links between pages.

## A Word on Security

- Right now, this lets anyone read your S3 bucket publicly.
- For real-world use, think about adding CloudFront with a custom domain and SSL for that extra layer.
- Keep an eye on your bucket policies and update them as needed.
- Turn on versioning and logging to keep tabs on things.

## When Things Go Wrong

### Common Headaches

1. **403 Forbidden**:
   - Double-check your bucket policy for public reads.
   - Make sure the files are set to public.

2. **404 Everywhere**:
   - Confirm static website hosting is switched on.
   - Verify the index and error docs are set correctly.

3. **Styles Not Showing**:
   - Ensure those external font links are working.
   - Check that your CSS is embedded properly.

## Want to Contribute?

1. Fork the repo.
2. Branch out with `git checkout -b feature/your-awesome-idea`.
3. Make your changes and commit with `git commit -m 'Added something cool'`.
4. Push it up with `git push origin feature/your-awesome-idea`.
5. Send a pull request our way!

## License

This project's under the MIT License—check out the [LICENSE](LICENSE) file for the nitty-gritty.

## Helpful Links

- [AWS S3 Static Website Docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
- [AWS CLI S3 Commands](https://docs.aws.amazon.com/cli/latest/reference/s3/index.html)
- [S3 Best Practices](https://aws.amazon.com/s3/best-practices/)

---

**Just a heads up**: This is more of a demo setup. For a full-blown site, you'd want CloudFront for CDN, custom domains, and beefed-up security.
