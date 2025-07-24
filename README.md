# 📦 AWS S3 Static Website Hosting Guide

This document outlines steps to host a static website using **Amazon S3**, including uploading files, setting permissions, and enabling website hosting.

---

## ✅ 1. Create an S3 Bucket

```bash
aws s3api create-bucket \
  --bucket mybucketatulkamble \
  --region us-east-1
```

> ⚠️ Bucket name must be **globally unique**.

---

## 📤 2. Upload an Object (`cat.jpg`)

```bash
aws s3 cp cat.jpg s3://mybucketatulkamble/
```

You can also upload manually using the AWS Console:

* Open S3 → Your Bucket → **Upload** → Choose File → Upload.

---

## 🔐 3. Update Bucket Policy (Make Objects Public)

Update the **bucket policy** to allow public read access for all objects:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::mybucketatulkamble/*"
    }
  ]
}
```

To apply:

* Go to S3 Console → Your Bucket → **Permissions** tab → **Bucket Policy** → Paste and Save.

---

## 🌐 4. Upload `index.html`

### `index.html` Example:

```html
<html>
<head>
    <title>My Static Website</title>
</head>
<body>
    <h1 style="text-align: center;">Welcome to My Static Website!</h1>

    <div style="text-align: center;">
        <img src="https://mybucketatulkamble.s3.us-east-1.amazonaws.com/cat.jpg" alt="Cat">
    </div>
</body>
</html>
```

### Upload via AWS CLI:

```bash
aws s3 cp index.html s3://mybucketatulkamble/
```

---

## ⚙️ 5. Enable Static Website Hosting

1. Go to S3 Console → Your Bucket → **Properties** tab.
2. Scroll to **Static website hosting**.
3. Click **Edit**, then:

   * Enable Static Website Hosting
   * Index document: `index.html`
4. Save changes.

---

## 🔍 Final Check

Open your website in the browser:

```
http://mybucketatulkamble.s3-website-us-east-1.amazonaws.com
```

> ✅ You should see your static webpage with the centered cat image.

