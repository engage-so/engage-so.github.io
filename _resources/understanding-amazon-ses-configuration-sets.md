---
title: Understanding Amazon SES Configuration Sets and how Engage uses them
layout: resources
author_avi: kehers.jpg
author: Opeyemi Obembe
excerpt: Configuration Sets are settings for emails you send using Amazon SES. Here is what you need to know about them.
banner: config-set.svg
bg: '#e6e4ff'
---

Configuration Sets are settings for emails you send using Amazon SES. They are broadly used for [tracking email events](/resources/tracking-deliveries-opens-and-clicks-for-amazon-ses) and sending emails with dedicated IPs.

<!--more-->

![](/images/blog/130720/config-sets.png)

### How Engage uses configuration sets

Configuration Sets are how Engage is able to track your Amazon SES transactional emails and provide analytic reporting. When you add an SES domain to Engage, the application automatically creates a configuration set for you. To do this, we request your IAM credentials with Full SNS and SES access.

Here is the breakdown of the process in 4 steps.

1.  Engage creates a SNS Topic. This is named `engage_so` for easy identification.
2.  A subscription to the topic is created. The subscription points the topic to a webhook that handles messages to the SNS topic.
3.  Engage creates the configuration set. This is also named `engage_so`
4.  Engage creates the configuration set event destination. This involves 2 things: selecting the events to track and pointing the configuration set to the SNS topic created earlier. The events tracked are `reject`, `bounce`, `complaint`, `delivery`, `open` and `click`.

If you get an error when adding your domain, it’s most likely an issue with the access keys. Ensure they have full SNS and SES permissions.

### What the access keys are used for?

The SNS and SES permissions are used to created and manage the SNS topic, SNS topic subscription and SES configuration set. Engage lets you send email broadcasts and create email automations. The SES permission is used for this.

### Confirming proper setup

If for any reason you need to confirm your setup is rightly done, here is how to confirm everything has been properly set up.

1.  Go to SNS on your Amazon console. Click on **Topics**. You should see **engage_so** in the list of topics.
2.  Click on the mailintel topic. It should have an HTTPS subscription pointing to a URL similar to this `https://us-central1-suet-170506.cloudfunctions.net/ses-webhook`. The status should be **confirmed**.
3.  Go to SES on your Amazon console. Click on **Configuration Sets**. You should see **engage_so** in the list of configuration sets.
4.  Click on the engage_so configuration set. It should have the engage_so SNS topic as its destination and should have the event types _Bounce, Click, Complaint, Delivery, Open, Reject_.

### Updating the configuration set

_Do not do this unless you know what you are doing._

Now that we've established you understand what you are doing, you may need to update the configuration set for custom purposes; especially because you can only use one configuration set at a time when sending emails.

![Update configuration set](/images/blog/130720/edit-config-set.png)

1.  You can add additional destination to the configuration set by clicking on the engage_so configuration set and selecting a new option for **Add destination**
2.  You can add an IP pool by clicking the **Sending IP pool** tab
3.  You can update the tracked events, for example to disable open or click tracking. To do this, click on the edit (pencil icon) option on the configuration set page and uncheck the events you want to stop tracking. Engage doesn’t track `Send`, `Rendering Failure` and `Rendering Success` so don’t check those.
4.  You can also use a custom subdomain for your open and click tracking. This option is available on the same edit configuration set page above.

### Telling Amazon SES to use the configuration set

Using the configuration set is not automatic. You need to tell Amazon to use it anytime you send an email. Depending on how you are sending your email and what library you use, you just need to add the SMTP header: `X-SES-CONFIGURATION-SET: mailintel`.

If you use PHP Laravel for example, here is a short post on how to do this: [eoghanobrien.com/posts/laravel-smtp-ses-configuration-set](https://eoghanobrien.com/posts/laravel-smtp-ses-configuration-set)

If you use PHPMailer, it should be something like this

```php
// ...
$mail = new PHPMailer(true);
try {
    $mail->isSMTP();
    // ...
    $mail->addCustomHeader('X-SES-CONFIGURATION-SET', 'engage_so');  // <-- this
    // ...
    $mail->Send();
} catch (Exception $e) {
    echo "Email not sent. {$mail->ErrorInfo}";
}
```

If you use SwiftMailer:

```php
// ...
$mailer = new Swift_Mailer($transport);

$message = new Swift_Message('Wonderful Subject');
$headers = $message->getHeaders();
$headers->addTextHeader('X-SES-CONFIGURATION-SET', 'engage_so');  // <-- this
$message->setFrom(['john@doe.com' => 'John Doe'])
  ->setTo(['receiver@domain.org', 'other@domain.org' => 'A name'])
  ->setBody('Here is the message itself')
  ;

$result = $mailer->send($message);
```

In NodeMailer:

```js
const transporter = nodemailer.createTransport(transportObject);

await transporter.sendMail({
  from: '"Fred Foo 👻" <foo@example.com>',
  to: "bar@example.com, baz@example.com",
  subject: "Hello ✔",
  text: "Hello world?",
  html: "<b>Hello world?</b>",
  headers: {
      'X-SES-CONFIGURATION-SET': 'engage_so'  // <-- this
  },
});
```

AWS NodeJs library

```js
const ses = new AWS.SES({
  accessKeyId: process.env.ID,
  secretAccessKey: process.env.KEY,
  region: process.env.REGION
});
ses.sendEmail({
  Destination: {
    ToAddresses: ['yo@hey.com']
  },
  Message: {
    Body: {
    Html: {
      Charset: "UTF-8",
      Data: '<p>Yo. This is a test :)</p>'
    },
    Text: { Data: 'Yo. This is test :)' }
    },
    Subject: { Data: 'Hey' }
  },
  ConfigurationSetName: 'engage_so', // <-- this
  Source:  '"Heello" <hello@awesome.co>'
  }, (err, data) => {
  console.log(data, err);
  // ~
})
```

If you are sending your email via the [sendRawEmail](https://docs.aws.amazon.com/ses/latest/APIReference/API_SendRawEmail.html) or [SendEmail](https://docs.aws.amazon.com/ses/latest/APIReference/API_SendEmail.html) API, there is a `ConfigurationSetName` parameter you should set to `engage_so`
