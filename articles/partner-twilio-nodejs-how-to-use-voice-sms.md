---
title: "Ses, VoIP ve Azure'da SMS Mesajlaşma Twilio kullanma"
description: "Bir telefon araması yapın ve Azure üzerinde Twilio API hizmetiyle SMS mesajı göndermek öğrenin. Node.js içinde yazılan kod örnekleri."
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 44ec97812130d41d75be98fc8e2d846b7cb5c913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="a304f-104">Ses, VoIP ve Azure'da SMS Mesajlaşma Twilio kullanma</span><span class="sxs-lookup"><span data-stu-id="a304f-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="a304f-105">Bu kılavuz, iletişim Twilio ve azure'da node.js uygulamaları geliştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a304f-105">This guide demonstrates how to build apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="a304f-106">Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="a304f-106">What is Twilio?</span></span>
<span data-ttu-id="a304f-107">Twilio yapmak ve telefon çağrılarını almak, Gönder ve metin iletileri almasına ve tarayıcı tabanlı ve yerel mobil uygulamalara VoIP arama katıştırmak geliştiriciler için kolaylaştıran bir API platformudur.</span><span class="sxs-lookup"><span data-stu-id="a304f-107">Twilio is an API platform that makes it easy for developers to make and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="a304f-108">Şimdi bunun girmeden önce işleyişi kısaca gidin.</span><span class="sxs-lookup"><span data-stu-id="a304f-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="a304f-109">Aramaları ve metin iletileri alma</span><span class="sxs-lookup"><span data-stu-id="a304f-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="a304f-110">Twilio geliştiricilerine verir [programlanabilir telefon numaralarını satın] [ purchase_phone] hem göndermek ve çağrıları ve metin iletileri almak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a304f-110">Twilio allows developers to [purchase programmable phone numbers][purchase_phone] which can be used to both send and receive calls and text messages.</span></span> <span data-ttu-id="a304f-111">Twilio sayıyı bir gelen arama veya metin aldığında, Twilio web uygulamanızı bir HTTP POST veya GET isteğini nasıl arama veya kısa mesaj yönetileceğine ilişkin yönergeler için isteyen gönderir.</span><span class="sxs-lookup"><span data-stu-id="a304f-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how to handle the call or text.</span></span> <span data-ttu-id="a304f-112">Sunucunuz Twilio'nın HTTP isteğiyle yanıtlar [TwiML][twiml], arama veya kısa mesaj işlemek yönergeler içeren XML etiketleri basit bir dizi.</span><span class="sxs-lookup"><span data-stu-id="a304f-112">Your server will respond to Twilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how to handle a call or text.</span></span> <span data-ttu-id="a304f-113">Yalnızca bir dakika içinde TwiML örneklerde göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="a304f-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="a304f-114">Çağrıları yapma ve metin iletileri gönderme</span><span class="sxs-lookup"><span data-stu-id="a304f-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="a304f-115">Geliştiriciler, Twilio web hizmeti API'sine HTTP isteklerini yaparak, kısa mesaj göndermek veya giden telefon aramaları başlatın.</span><span class="sxs-lookup"><span data-stu-id="a304f-115">By making HTTP requests to the Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="a304f-116">Giden çağrıları için Geliştirici de onu bağlandıktan sonra giden çağrısını işlemek nasıl TwiML yönergeler döndüren bir URL belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a304f-116">For outbound calls, the developer must also specify a URL that returns TwiML instructions for how to handle the outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="a304f-117">UI kodunda (JavaScript, iOS veya Android) VoIP yetenekleri katıştırma</span><span class="sxs-lookup"><span data-stu-id="a304f-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="a304f-118">Twilio tüm masaüstü web tarayıcısı, iOS uygulaması ya da Android uygulaması VoIP telefon kapatabilirsiniz bir istemci-tarafı SDK sağlar.</span><span class="sxs-lookup"><span data-stu-id="a304f-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="a304f-119">Bu makalede, biz tarayıcıda çağırma VoIP kullanma hakkında odaklanır.</span><span class="sxs-lookup"><span data-stu-id="a304f-119">In this article, we will focus on how to use VoIP calling in the browser.</span></span> <span data-ttu-id="a304f-120">Ek olarak *Twilio JavaScript SDK'sı* tarayıcıda çalışan, bir sunucu-tarafı uygulaması (node.js uygulamamız) bir "özelliği" JavaScript istemciye belirteç için kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a304f-120">In addition to the *Twilio JavaScript SDK* running in the browser, a server-side application (our node.js application) must be used to issue a "capability token" to the JavaScript client.</span></span> <span data-ttu-id="a304f-121">Daha fazla bilgiyi VoIP node.js ile kullanma hakkında [Twilio geliştirme blogunda][voipnode].</span><span class="sxs-lookup"><span data-stu-id="a304f-121">You can read more about using VoIP with node.js [on the Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="a304f-122">Twilio (Microsoft iskonto) için kaydolun</span><span class="sxs-lookup"><span data-stu-id="a304f-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="a304f-123">Twilio hizmetlerini kullanmadan önce öncelikle [bir hesap için kaydolabilirsiniz][signup].</span><span class="sxs-lookup"><span data-stu-id="a304f-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="a304f-124">Microsoft Azure müşterilerin alma özel bir indirim - [burada oturum özen][signup]!</span><span class="sxs-lookup"><span data-stu-id="a304f-124">Microsoft Azure customers receive a special discount - [be sure to sign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="a304f-125">Oluşturma ve bir node.js Azure Web sitesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="a304f-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="a304f-126">Ardından, Azure üzerinde çalışan bir node.js Web sitesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a304f-126">Next, you will need to create a node.js website running on Azure.</span></span> <span data-ttu-id="a304f-127">[Bunu yapmak için resmi belge burada bulunduğu][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="a304f-127">[The official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="a304f-128">Yüksek bir düzeyde, aşağıdakileri yaparak:</span><span class="sxs-lookup"><span data-stu-id="a304f-128">At a high level, you will be doing the following:</span></span>

* <span data-ttu-id="a304f-129">Zaten yoksa, bir Azure hesabı için kaydolma</span><span class="sxs-lookup"><span data-stu-id="a304f-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="a304f-130">Yeni bir Web sitesi oluşturmak için Azure yönetim konsolunu kullanarak</span><span class="sxs-lookup"><span data-stu-id="a304f-130">Using the Azure admin console to create a new website</span></span>
* <span data-ttu-id="a304f-131">Kaynak denetimi desteği (git kullanılan varsayacağız) ekleme</span><span class="sxs-lookup"><span data-stu-id="a304f-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="a304f-132">Bir dosya oluşturulurken `server.js` basit bir node.js web uygulaması ile</span><span class="sxs-lookup"><span data-stu-id="a304f-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="a304f-133">Bu basit uygulamayı Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="a304f-133">Deploying this simple application to Azure</span></span>

<a id="twiliomodule"/>

## <a name="configure-the-twilio-module"></a><span data-ttu-id="a304f-134">Twilio modülü Yapılandır</span><span class="sxs-lookup"><span data-stu-id="a304f-134">Configure the Twilio Module</span></span>
<span data-ttu-id="a304f-135">Ardından, biz Twilio API'si kullanmak olmasını sağlayan bir basit bir node.js uygulaması yazma başlar.</span><span class="sxs-lookup"><span data-stu-id="a304f-135">Next, we will begin to write a simple node.js application which makes use of the Twilio API.</span></span> <span data-ttu-id="a304f-136">Başlamadan önce bizim Twilio hesap kimlik bilgilerini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a304f-136">Before we begin, we need to configure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="a304f-137">Sistem ortam değişkenleri Twilio kimlik bilgilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a304f-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="a304f-138">Kimliği doğrulanmış istekler Twilio arka uç yapmak için hesap SID'si ve kimlik doğrulama belirteci, kullanıcı adı ve parola bizim Twilio hesabı için ayarlanan hangi işlevi ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="a304f-138">In order to make authenticated requests against the Twilio back end, we need our account SID and auth token, which function as the username and password set for our Twilio account.</span></span> <span data-ttu-id="a304f-139">Bunlar kullanmak için Azure düğümü modülünde ile yapılandırmak için en güvenli aracılığıyla doğrudan Azure Yönetici konsolunda ayarlayabilirsiniz sistem ortam değişkenlerini yoludur.</span><span class="sxs-lookup"><span data-stu-id="a304f-139">The most secure way to configure these for use with the node module in Azure is via system environment variables, which you can set directly in the Azure admin console.</span></span>

<span data-ttu-id="a304f-140">Node.js Web sitenizi seçin ve "Yapılandırma" bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a304f-140">Select your node.js website, and click the "CONFIGURE" link.</span></span>  <span data-ttu-id="a304f-141">Bir bit kaydırın, uygulamanız için yapılandırma özelliklerini ayarlayabileceğiniz bir alan görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a304f-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="a304f-142">Twilio hesabı kimlik bilgilerinizi girin ([Twilio konsolunuzdan bulunan][twilio_console]) gösterildiği gibi - bunları ad verdiğinizden emin olun `TWILIO_ACCOUNT_SID` ve `TWILIO_AUTH_TOKEN`sırasıyla:</span><span class="sxs-lookup"><span data-stu-id="a304f-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure to name them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Azure Yönetim Konsolu][azure-admin-console]

<span data-ttu-id="a304f-144">Bu değişkenler yapılandırdıktan sonra uygulamanızı Azure konsolunda yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a304f-144">Once you have configured these variables, restart your application in the Azure console.</span></span>

### <a name="declaring-the-twilio-module-in-packagejson"></a><span data-ttu-id="a304f-145">Package.json Twilio modülünde bildirme</span><span class="sxs-lookup"><span data-stu-id="a304f-145">Declaring the Twilio module in package.json</span></span>
<span data-ttu-id="a304f-146">Ardından, bizim düğümü modülü bağımlılıkları aracılığıyla yönetmek için bir package.json oluşturmak ihtiyacımız [npm].</span><span class="sxs-lookup"><span data-stu-id="a304f-146">Next, we need to create a package.json to manage our node module dependencies via [npm].</span></span> <span data-ttu-id="a304f-147">Aynı düzeyde `server.js` içinde oluşturduğunuz dosya *Azure/node.js* öğretici adlı bir dosya oluşturun `package.json`.</span><span class="sxs-lookup"><span data-stu-id="a304f-147">At the same level as the `server.js` file you created in the *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="a304f-148">Bu dosya içinde aşağıdaki koyun:</span><span class="sxs-lookup"><span data-stu-id="a304f-148">Inside this file, place the following:</span></span>

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

<span data-ttu-id="a304f-149">Bu bağımlılık yanı sıra popüler twilio modülü bildirir [Express web çerçevesi] [ express] ve EJS şablon motoru.</span><span class="sxs-lookup"><span data-stu-id="a304f-149">This declares the twilio module as a dependency, as well as the popular [Express web framework][express] and the EJS template engine.</span></span>  <span data-ttu-id="a304f-150">Tamam, biz başlamaya artık hazırsınız - biraz kod yazalım!</span><span class="sxs-lookup"><span data-stu-id="a304f-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="a304f-151">Giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="a304f-151">Make an Outbound Call</span></span>
<span data-ttu-id="a304f-152">Burada birkaç çağrı yerleştirir basit bir form oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="a304f-152">Let's create a simple form that will place a call to a number we choose.</span></span> <span data-ttu-id="a304f-153">Açık `server.js`ve aşağıdaki kodu girin.</span><span class="sxs-lookup"><span data-stu-id="a304f-153">Open up `server.js`, and enter the following code.</span></span> <span data-ttu-id="a304f-154">Burada "CHANGE_ME" azure Web sitenizin adı var. put - diyor dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="a304f-154">Note where it says "CHANGE_ME" - put the name of your azure website there:</span></span>

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for the application's home page
app.get('/', (request, response) => response.render('index'));

// Handle the form POST to place a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call to this number
    to:request.body.number,

    // Change to a Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" to your app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});

// Generate TwiML to handle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message to the call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

<span data-ttu-id="a304f-155">Ardından, adlı bir dizin oluşturun `views` - bu dizin içinde adlı bir dosya oluşturun `index.ejs` aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="a304f-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with the following contents:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call the number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="a304f-156">Şimdi, Azure için Web sitenizi dağıtmak ve ev açın.</span><span class="sxs-lookup"><span data-stu-id="a304f-156">Now, deploy your website to Azure and open your home.</span></span> <span data-ttu-id="a304f-157">Metin alanına telefon numaranızı girin ve bir çağrı Twilio numarasından almak mümkün olmalıdır!</span><span class="sxs-lookup"><span data-stu-id="a304f-157">You should be able to enter your phone number in the text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="a304f-158">SMS iletisi gönder</span><span class="sxs-lookup"><span data-stu-id="a304f-158">Send an SMS Message</span></span>
<span data-ttu-id="a304f-159">Şimdi, şimdi kısa mesaj göndermek için bir kullanıcı arabirimi ve mantığı işleme formunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a304f-159">Now, let's set up a user interface and form handling logic to send a text message.</span></span> <span data-ttu-id="a304f-160">Açık `server.js`ve son çağrısından sonra aşağıdaki kodu ekleyin `app.post`:</span><span class="sxs-lookup"><span data-stu-id="a304f-160">Open up `server.js`, and add the following code after the last call to `app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text to this number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // The body of the text message
      body: request.body.message

  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="a304f-161">İçinde `views/index.ejs`, başka bir formu bir sayı ve kısa mesaj göndermek için birinci altında ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a304f-161">In `views/index.ejs`, add another form under the first one to submit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message to send" name="message"/>
  <br/>
  <input type="submit" value="Send text to the number above"/>
</form>
```

<span data-ttu-id="a304f-162">Azure uygulamanızı yeniden dağıtmanıza ve şimdi, form ve kendiniz (veya en yakın arkadaşlarınızın hiçbirini) SMS mesajı gönderecek gönderemeyecek olmalıdır!</span><span class="sxs-lookup"><span data-stu-id="a304f-162">Re-deploy your application to Azure, and you should now be able to submit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="a304f-163">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a304f-163">Next Steps</span></span>
<span data-ttu-id="a304f-164">Artık, node.js ve Twilio iletişim uygulamalar oluşturmak için kullanma temelleri öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="a304f-164">You have now learned the basics of using node.js and Twilio to build apps that communicate.</span></span> <span data-ttu-id="a304f-165">Ancak bu örnekler Twilio ve node.js ile olası nedir yüzeyine neredeyse hiç boş.</span><span class="sxs-lookup"><span data-stu-id="a304f-165">But these examples barely scratch the surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="a304f-166">Node.js ile Twilio kullanarak daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="a304f-166">For more information using Twilio with node.js, check out the following resources:</span></span>

* <span data-ttu-id="a304f-167">[Resmi modülü belgeleri][docs]</span><span class="sxs-lookup"><span data-stu-id="a304f-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="a304f-168">[Node.js uygulamaları ile VoIP öğretici][voipnode]</span><span class="sxs-lookup"><span data-stu-id="a304f-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="a304f-169">[Votr - uygulama node.js ve CouchDB (üç bölümden) ile oylama gerçek zamanlı bir SMS][votr]</span><span class="sxs-lookup"><span data-stu-id="a304f-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="a304f-170">[Node.js ile tarayıcıda çifti programlama][pair]</span><span class="sxs-lookup"><span data-stu-id="a304f-170">[Pair programming in the browser with node.js][pair]</span></span>

<span data-ttu-id="a304f-171">Azure'da node.js ve Twilio korsan memnuniyet umuyoruz!</span><span class="sxs-lookup"><span data-stu-id="a304f-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
<span data-ttu-id="a304f-172">[npm]: http://npmjs.org</span><span class="sxs-lookup"><span data-stu-id="a304f-172">[npm]: http://npmjs.org</span></span>
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
