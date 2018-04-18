---
description: Use Cloudinary and Auth0 Webtask to Auto tag with multiple add-ons.
---

# Auto Tagging Images with Fans

## Setup Cloudinary

First things, first,  sign up for [Cloudinary](https://cloudinary.com/signup?utm_source=Emerge_Americas&utm_medium=Gitbook&utm_campaign=Evangelism&utm_term=Hackathon&utm_content=Signup_EA)

{% hint style="info" %}
TIP: During the sign up process, make sure you create a memerable cloud name for your cloudinary account.   Hacking Teams will want to create one account and name their cloud name after their team.
{% endhint %}

## Sign up for Auth0 Webtask

Next [sign up](https://webtask.io/make) for webtask and follow these steps to create an empty function:

### Install the Cli

The recommended way of using webtask is through the `wt `command line interface.

> [Install the CLI](https://webtask.io/cli)

Once you set it up, here are some common examples of usage.

Auto Tagging example:

```javascript
const public_id = "car.jpg";
const options = { categorization: "google_tagging,imagga_tagging,aws_rek_tagging", auto_tagging: 0.6 };
cloudinary.uploader.upload(public_id, options, function(error, result) { 
console.log(result); 
});
```

{% hint style="warning" %}
Note:  First param can be a public\_id of an asset on cloudinary or a publically accessable URL. 
{% endhint %}

Let's move the code example into the webtask:

```javascript
function labelImage(context, cb){

const public_id = context.query.url ||  "car.jpg";  
const options = { categorization: "google_tagging,imagga_tagging,aws_rek_tagging", 
auto_tagging: 0.6 };

cloudinary.uploader.upload(public_id, options, function(error, result) { 
if(error){
  cb(error);
}
  console.log(result); 
  cb(null, result)
});

}

module.exports = function(context, cb) {
  
   cloudinary.config({
      "cloud_name":  context.secrets.cloud_name,
      "api_key": context.secrets.api_key,
      "api_secret":  context.secrets.api_secret
    });
    
    labelImage(context, cb);
};
```

{% hint style="warning" %}
We created a function passing in the context and callback as params. This allows us to complete the callback \(cb\) when Cloudinary's api returns either an error or result.
{% endhint %}

{% code-tabs %}
{% code-tabs-item title="JSON Results" %}
```text


```
{% endcode-tabs-item %}
{% endcode-tabs %}

