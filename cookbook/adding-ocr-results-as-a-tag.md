---
description: By Josh Slivken - Cloudinary Solutions Engineer
---

# Adding OCR results as a Tag



![Easily Capture Text from Images](../.gitbook/assets/ec18d5b63b46a112b486a97a9d8885d7.jpg)

Cloudinary ocr add-on allows you to easily capture text found in images.   This example shows you how to  captire the text and then update the images tags with the captured text.

```javascript

var url = "“https://res.cloudinary.com/demo-robert/image/upload/v1523390181/ec18d5b63b46a112b486a97a9d8885d7.jpg";
var options = {ocr: “adv_ocr” };
cloudinary.v2.uploader.upload(url,options, function(error,result){
     console.log(result);
     var ocrResult = result.info.ocr.adv_ocr.data[0].fullTextAnnotation.text || 0,
       publicId = result.public_id;
         if (ocrResult != 0){
             cloudinary.v2.uploader.add_tag(ocrResult, publicId,
             function(result) {
             console.log(result)
             });
           };
   });
```

{% hint style="success" %}
Want to try this out quickly?   Use a webtask FaaS.  Check out this article:

{% page-ref page="autotag\_faas/" %}
{% endhint %}



