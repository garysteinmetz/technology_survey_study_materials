#I Know How to Reserve a Domain in AWS and Create a Static Web Site Using S3

## What Is Cloud Computing?
Cloud computing is the concept of using (renting) publicly-available
computer services instead of purchasing, hosting, and maintaining
the necessary hardware and software one would normally need to host
web applications (and other software technology) by oneself.

### What Are the Advantages of Cloud Computing?
Cloud computing companies (like Amazon) make A Lot of money off of providing
this service. Intuition would suggest that it's better for a typical company
to just purchase and maintain its own computer hardware and software with
the added benefit of having full ownership over everything.

But typical companies actually want to use cloud computing for reasons including
the following -
  - Companies want to focus on what they're good at ('core competencies')
    and not be distracted by things they aren't necessarily proficient at.
    A bread company probably doesn't immediately know or care about Unix
    system administration; learning about Unix system administration would
    be a terrible distraction. It's better (and likely cheaper) to hire
    the experts than do it on one's own.
  - Cloud computing allows companies to instantaneously change the technologies
    and quantity of those technologies ('scale'). For accounting reasons,
    companies Hate acquiring fixed assets (like a computer) which are outside
    of the core business and which only depreciate (become less valuable)
    with time. Based on experience, it can even take several weeks for
    a company to get a new computer server following corporate procurement
    policies.

#### If Companies Like Cloud Computing, Why Do They Still Develop Their Own Software?

Companies don't always develop their own software and instead frequently pay
another company ('outsource') to develop and maintain the software instead.

But companies still frequently develop software on their own because
the software is either too close to the core function of the business
or a key representation of the brand of the business (like its web site).
In these cases, ownership and responsiveness to change are important.

## What Is AWS?
AWS stands for Amazon Web Services and it's Amazon's cloud computing platform.
As of late 2019, AWS is the most popular cloud computing platform
and produces the majority of profits for Amazon.

## Important Disclaimer - Using AWS Costs Money
In most cases, using AWS costs money although with vigilance total costs
to host a small web site should cost under $10 per month (in 2019).

Be careful when using AWS and stick to a budget.

## Logging into the AWS Console

The AWS console is the administrative web site for AWS which allows a user
to use its different and vast array of services.

  - Note that software projects generally use automated processes
    (by executing command line scripts and batch files) to perform
    repetitive actions like deploying an application to the cloud.
    For more mature software projects, using the AWS console is more
    of the exception than the rule.

### How to Login
Go to main AWS login page at https://aws.amazon.com/ , click the
'Sign In to the Console' button (on top-right), and login using the same
username/password combination used to order things from Amazon (like books).

  - Note that the members of more mature software projects generally
    do not use their personal AWS username/password to login
    into a project's AWS page. Instead, they use IAM (Identity
    and Access Management) systems, which still generally involve
    a user signing in with username/password but that username/password
    combination is different from the one used on the retail Amazon
    web site (e.g. where people have Prime membership and buy books
    or birthday presents).
  - Note that more advanced login procedures use something called
    Two-Factor Authentication (TFA) which typically involves not only
    logging in with a username/password combination, but following up
    that login by entering in a pass code received on one's cell phone.

### Select the Region to Work In

AWS hosts its services around the world in specific regions. Its important
to ensure that whatever set of services that are being used (like a web site
and its database) reside in the same region so that they can conveniently
communicate with one another.

Select the 'us-east-1' region by clicking the currently-selected region
in the top-right and selecting 'US East (N. Virginia)' .

#### Sometimes a Web Application Is Hosted in Multiple Regions

Some applications (especially more popular and more mature ones) are hosted
in multiple regions for reasons including the following.

  - Faster Response Times - Web pages load faster when the web server
    is nearer to the browser. In the US, it's common to host the same
    application on the west coast (for west coast users) and the east coast
    (for east coast users).
  - Resiliency - Each hosted region uses state-of-the-art facilities
    and technology, but in the off chance that a hosted region goes down
    the web application will still be available if it's hosted in another.

## Study the AWS Console
Click the 'Services' link in the top-left to reveal the dozens of different
AWS services. They come in different categories including the following.

  - Compute
  - Storage
  - Internet of Things
  - Database
  - Machine Learning

Note that for a generic web site, most of the topics in these
different categories won't be used. Here are some more commonly used
AWS services for a generic web site.

  - Route 53 - Register and configure domain names (e.g. mywebsite.com)
  - EC2/ECS - Host web servers (which serve content
    and perform server-side processing (like submitting an order for delivery))
  - AWS Cost Management - Determine money owed and where it's being spent

Here are other services that are frequently used.

  - Lambda - Perform server-side processing (including web services,
    which process commands from a browser, like submitting an order)
  - S3 - Store files and directories in a specific location ('bucket')
  - DynamoDB - Manage semi-structured data
  - API Gateway - Package and secure web services
  - SQS (Simple Queue Service) - Accumulate a pile of requests
    ('jobs' - like orders for delivery) which are then processed
    sometime later

### SQS Is for Asynchronous Processing

Novices to the computing world may tend to expect that computer applications
give an immediate response. But since computer applications model real-world
situations, just like the real world there are situations where a request
to complete an action is submitted but that action won't be completed
immediately. SQS is a technology that can be used in those case.

Pizza ordering and delivery is one such process. No one calls in an order
for pizza and then remains on the phone until the pizza is delivered. Instead,
the order is recorded (like being 'enqueued' (added) to SQS) then later
prepared/delivered (like being 'dequeued' (removed) from SQS).

In fact, pizza ordering and delivery may actually consist of two (or more)
queues. The first queue is for taking the orders which the cook processes.
The second queue is for delivering the orders which the cook processes.

## Exercise - Use S3 and Route 53 to Create a Static Web Site

### What's a Static Web Site?
A static web site is one where the web server just sends a file
to the browser without editing it - all browsers receive the exact
same file for a given URL and the server doesn't take any other action
(like submitting an order).

### Register a Domain

  - Go to the AWS console main page, click the 'Services' link (top-left).
  - Scroll down to the 'Networking & Content Delivery' section
    and click the 'Route 53' link.
  - Click the 'Registered domains' link (left) then click
    the 'Register Domain' button.
  - Enter the desired domain name (without the 'www.' prefix) in the text box
    under 'Choose a domain name', leave '.com' selected, then click
    the 'Check' button.
  - If an "Availability for '<whatever_domain_name_was_entered>'" section
    appears with the submitted domain name, click the 'Add to cart' button
    to its right, then scroll down and click the 'Continue' button.
  - On the next page, review and (as needed) edit the contact information
    then scroll down and click the 'Continue' button.
  - Scroll down to the checkbox to the immediate left of the
    'I have read and agree to the AWS Domain Name Registration Agreement'
    statement. Determine whether to 'Enable' or 'Disable'
    the 'Do you want to automatically renew your domain?' option
    (keeping at 'Enable' will mean that the account will be charged
    annually to continue registering the domain name). Then click
    the 'Complete Order' button.

Note that whatever contact information was entered during this domain
registration might be publicly available.

### Create an S3 Bucket

  - Go to the AWS console main page, click the 'Services' link (top-left).
  - Scroll down to the 'Networking & Content Delivery' section
    and click the 'S3' link.
  - Click the 'Create bucket' button, (important) correctly enter the domain
    name in the 'Bucket name' field (it should exactly match), make sure
    the region is 'US East (N. Virginia)', then click the 'Next' button.
  - Accept the defaults of the next page and click the 'Next' button.
  - Uncheck the 'Block all public access' check box then click
    the 'Next' button.
  - Finally, create the 'Create bucket' button.

### Align the Domain with the S3 Bucket

  - Go to the AWS console main page, click the 'Services' link (top-left).
  - Scroll down to the 'Networking & Content Delivery' section
    and click the 'Route 53' link.
  - Click the 'Hosted zones' link then click the 'Create Hosted Zone' button.
  - Correctly enter the domain name into the 'Domain Name' field,
    leave the 'Type' as 'Public Hosted Zone', then click the 'Create' button.
  - Click the link for the hosted zone then click
    the 'Create Record Set' button.
  - In the 'Create Record Set' form, leave the 'Name' field blank,
    select 'Yes' for the 'Alias' value, click the 'Alias Target' field
    and select the S3 bucket under the '-- S3 website endpoints --',
    then click the 'Create' button.
  - Repeat the previous step but this time use 'www' for the 'Name' field.

Note that the name of this hosted zone will have a period '.'
at the end of it.

### Upload Project Files to the S3 Bucket

  - Go to the AWS console main page, click the 'Services' link (top-left).
  - Scroll down to the 'Networking & Content Delivery' section
    and click the 'S3' link.
  - Click the name of the bucket then click the 'Upload' button.
  - Click the 'Add files' button, select the files to publish,
    then click the 'Next' button.
  - Under 'Manage public permissions', select
    'Grant public read access to this object(s)', then click the 'Next'
    button.
  - Again click the 'Next' button then click the 'Upload' button.
  - Select the files and directories to upload, then click the 'Next' button.

Note that, when a user just enters the domain name into the browser,
by convention web browser first searches for the 'index.html'
web page. Make sure this file is present in the S3 bucket.

### Confirm
Open a web browser and enter the domain name into the address bar.

### Analysis

Note the following
  - To update the content on this web site, just re-follow the steps
    under the 'Upload Project Files to the S3 Bucket' section.
  - Observe how this process of creating even this simple web site
    was lengthy and error-prone. As web applications mature, it becomes
    increasingly imperative to automate the (build and) deployment process
    to save time and reduce errors.
