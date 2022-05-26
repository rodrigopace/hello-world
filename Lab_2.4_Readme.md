**Lambda and image clean-up lab**

Today all pictures come with metadata like GPS info, camera, etc. Here is a useful function to clean-up it and keep some of our privacy.

1. Download the lab files from this repository:

[https://github.com/Resistor52/hitc-dev/blob/main/lab2.4/lambda\_function.zip](https://github.com/Resistor52/hitc-dev/blob/main/lab2.4/lambda_function.zip)

![](https://github.com/rodrigopace/hello-world/blob/master/images/Img_01_Lab_2.4.png)

1. From AWS Management Console, time to create the buckets that will be used for our function. Create one called &quot;input-image-\&lt;myPhoneNumber\&gt;&quot; and another called &quot;output-image-\&lt;myPhoneNumber\&gt;&quot; using the procedure below.

Important - The buckets should start with the requested names, otherwise the clean up script will not work.

![](RackMultipart20220526-1-grk0zj_html_e69672f80632b72d.png)

![](RackMultipart20220526-1-grk0zj_html_9e64bcfc687b353b.png)

![](RackMultipart20220526-1-grk0zj_html_7719d602a23339ed.png)

Enable encryption by default and click in Create Bucket.

![](RackMultipart20220526-1-grk0zj_html_def2a673213210be.png)

Repeat this step for output bucket.

![](RackMultipart20220526-1-grk0zj_html_da12ca72bc24fa2.png)

Info - As S3 uses the global unique bucket, two students can&#39;t use the same bucket name.

1. Create a custom policy available in https://github.com/Resistor52/hitc-dev/blob/main/lab2.4/s3\_policy.json to add necessary permissions for the file transformation lambda function..

![](RackMultipart20220526-1-grk0zj_html_e95ed360cc6f13d3.png)

Select Policies

![](RackMultipart20220526-1-grk0zj_html_bdfc4f3542ce75fd.png)

Select Create policy

![](RackMultipart20220526-1-grk0zj_html_35285f43e1e5765e.png)

Click in JSON file and paste the file content available in the json file previously downloaded.

![](RackMultipart20220526-1-grk0zj_html_1de22d2cc202f500.png)

Click in Next review

![](RackMultipart20220526-1-grk0zj_html_622e87869272da8c.png)

Type the policy name and click in Create policy

![](RackMultipart20220526-1-grk0zj_html_5f1706451e20ebdf.png)

1. Create the lambda function that will be used to clean up the image when it is uploaded:

![](RackMultipart20220526-1-grk0zj_html_49ce555d7813f4e6.png)

![](RackMultipart20220526-1-grk0zj_html_2db4afb5d15d5253.png)

Select Use a blueprint and type s3-get-object-python.

![](RackMultipart20220526-1-grk0zj_html_acb22f72dd82ae87.png)

Select the available blueprint and click in configure.

![](RackMultipart20220526-1-grk0zj_html_e7c44444fd015d8.png)

Add a function name and select Create a new role with basic Lambda permissions

![](RackMultipart20220526-1-grk0zj_html_145b7940cc6bbade.png)

Scroll down and select Create function

![](RackMultipart20220526-1-grk0zj_html_dc6856c671f4401b.png)

Now click in the function to configure it.

![](RackMultipart20220526-1-grk0zj_html_b56f2fd87ca9f81e.png)

Select Add trigger

![](RackMultipart20220526-1-grk0zj_html_2436bd9fb5062145.png)

Select S3 as trigger, choosing the input bucket as source and keep All object create event.

![](RackMultipart20220526-1-grk0zj_html_fad7b6b4bff29e1a.png)

Acknowledge the potential recursive S3 action and click in Add

![](RackMultipart20220526-1-grk0zj_html_a98b487be448d121.png)

Time to upload the code. Click in Code tab, Upload from and .zip file.

![](RackMultipart20220526-1-grk0zj_html_aedb38eca53a3579.png)

Click in Upload button.

![](RackMultipart20220526-1-grk0zj_html_ba98486b734acb6.png)

Select the lambda\_function.zip file downloaded previously and hit OK

![](RackMultipart20220526-1-grk0zj_html_de6fc87503505c3b.png)

![](RackMultipart20220526-1-grk0zj_html_7b722fa45558cfb0.png)

Now it&#39;s time to edit the IAM role, adding the missing permissions

![](RackMultipart20220526-1-grk0zj_html_90a2e0e6ae003801.png)

Select Add permissions and Add policies.

![](RackMultipart20220526-1-grk0zj_html_140fbe948a3ad2f2.png)

Attach the previous policy created before and click in Attach policy

![](RackMultipart20220526-1-grk0zj_html_17dfce3d172dbfc5.png)

1. Now it&#39;s time to test the function. You can use a sample file available here: . Open the S3 console and add the file to the input bucket.

![](RackMultipart20220526-1-grk0zj_html_f0f0f87df3f7217d.png)

Open the input bucket

![](RackMultipart20220526-1-grk0zj_html_7ce07a0196f1c272.png)

Click in the Upload button

![](RackMultipart20220526-1-grk0zj_html_19c57bcf5c17d279.png)

Click in Add file and select a camera image

![](RackMultipart20220526-1-grk0zj_html_d62f5c1d95c117f9.png)

![](RackMultipart20220526-1-grk0zj_html_14e34a4e9a0ce08b.png)

Click in Upload

![](RackMultipart20220526-1-grk0zj_html_bc6c2f5b843c2bad.png)

After a minute, you can check the output bucket that a file started with &quot;clean…&quot; will be in there.

![](RackMultipart20220526-1-grk0zj_html_8d6c18dabea7de2d.png)

You can download this file and compare the results with the initial image with the previous one using [https://jimpl.com/](https://jimpl.com/)

1. The function logs can be checked here

![](RackMultipart20220526-1-grk0zj_html_8f09a009819b92d5.png)

![](RackMultipart20220526-1-grk0zj_html_9904656311056c74.png)

![](RackMultipart20220526-1-grk0zj_html_591f2f8a92d3926d.png)

![](RackMultipart20220526-1-grk0zj_html_2b817b82aa9f0bd.png)
