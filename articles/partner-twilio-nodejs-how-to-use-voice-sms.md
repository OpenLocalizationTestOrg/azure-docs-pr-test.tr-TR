---
title: "aaaUsing Twilio ses, VoIP ve SMS Mesajlaşma Azure"
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. Node.js içinde yazılan kod örnekleri."
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
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="9b4e0-104">Ses, VoIP ve Azure'da SMS Mesajlaşma Twilio kullanma</span><span class="sxs-lookup"><span data-stu-id="9b4e0-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="9b4e0-105">Bu kılavuz gösterir toobuild uygulamalar, nasıl iletişim Twilio ve azure'da node.js kurar.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="9b4e0-106">Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="9b4e0-106">What is Twilio?</span></span>
<span data-ttu-id="9b4e0-107">Twilio, geliştiricilerin toomake kolaylaştırır ve telefon çağrılarını almak, Gönder ve metin iletileri almasına ve tarayıcı tabanlı ve yerel mobil uygulamalara VoIP arama katıştırmak bir API platformudur.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="9b4e0-108">Şimdi bunun girmeden önce işleyişi kısaca gidin.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="9b4e0-109">Aramaları ve metin iletileri alma</span><span class="sxs-lookup"><span data-stu-id="9b4e0-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="9b4e0-110">Twilio sağlayan geliştiriciler çok[programlanabilir telefon numaralarını satın] [ purchase_phone] kullanılan tooboth olabilen gönderip çağrıları ve metin iletileri.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="9b4e0-111">Twilio sayıyı bir gelen arama veya metin aldığında, Twilio web uygulamanızı bir HTTP POST veya GET isteğini nasıl toohandle hello üzerinde arama veya kısa mesaj yönergeler için isteyen gönderir.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="9b4e0-112">Sunucunuz tooTwilio'nın HTTP isteğiyle yanıtlar [TwiML][twiml], yönergeler içeren XML etiketleri basit bir dizi toohandle arama veya metin.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="9b4e0-113">Yalnızca bir dakika içinde TwiML örneklerde göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="9b4e0-114">Çağrıları yapma ve metin iletileri gönderme</span><span class="sxs-lookup"><span data-stu-id="9b4e0-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="9b4e0-115">Geliştiriciler, HTTP isteklerini toohello Twilio web hizmeti API'sine yaparak, kısa mesaj göndermek veya giden telefon aramaları başlatın.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="9b4e0-116">Giden çağrıları için hello Geliştirici de toohandle hello giden nasıl çağrısı, bağlı olduğu bir kez TwiML yönergeler döndüren bir URL belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="9b4e0-117">UI kodunda (JavaScript, iOS veya Android) VoIP yetenekleri katıştırma</span><span class="sxs-lookup"><span data-stu-id="9b4e0-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="9b4e0-118">Twilio tüm masaüstü web tarayıcısı, iOS uygulaması ya da Android uygulaması VoIP telefon kapatabilirsiniz bir istemci-tarafı SDK sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="9b4e0-119">Bu makalede, sizi nasıl odaklanacaktır toouse VoIP hello tarayıcıda çağırma.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="9b4e0-120">Toplama toohello içinde *Twilio JavaScript SDK'sı* hello tarayıcıda çalışan, bir sunucu-tarafı uygulaması (node.js uygulamamız) kullanılan tooissue "özelliği belirteci" toohello JavaScript istemci olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="9b4e0-121">Daha fazla bilgiyi VoIP node.js ile kullanma hakkında [hello Twilio geliştirme blogunda][voipnode].</span><span class="sxs-lookup"><span data-stu-id="9b4e0-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="9b4e0-122">Twilio (Microsoft iskonto) için kaydolun</span><span class="sxs-lookup"><span data-stu-id="9b4e0-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="9b4e0-123">Twilio hizmetlerini kullanmadan önce öncelikle [bir hesap için kaydolabilirsiniz][signup].</span><span class="sxs-lookup"><span data-stu-id="9b4e0-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="9b4e0-124">Microsoft Azure müşterilerin alma özel bir indirim - [burada yukarı emin toosign olması][signup]!</span><span class="sxs-lookup"><span data-stu-id="9b4e0-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="9b4e0-125">Oluşturma ve bir node.js Azure Web sitesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="9b4e0-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="9b4e0-126">Ardından, Azure üzerinde çalışan bir node.js Web sitesi toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="9b4e0-127">[Bunu yapmak için resmi belge hello bulunduğu burada][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="9b4e0-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="9b4e0-128">Yüksek bir düzeyde hello aşağıdakileri yaparak:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="9b4e0-129">Zaten yoksa, bir Azure hesabı için kaydolma</span><span class="sxs-lookup"><span data-stu-id="9b4e0-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="9b4e0-130">Hello Azure Yönetici Konsolu toocreate yeni bir Web sitesi kullanma</span><span class="sxs-lookup"><span data-stu-id="9b4e0-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="9b4e0-131">Kaynak denetimi desteği (git kullanılan varsayacağız) ekleme</span><span class="sxs-lookup"><span data-stu-id="9b4e0-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="9b4e0-132">Bir dosya oluşturulurken `server.js` basit bir node.js web uygulaması ile</span><span class="sxs-lookup"><span data-stu-id="9b4e0-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="9b4e0-133">Bu basit uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="9b4e0-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="9b4e0-134">Merhaba Twilio modülü Yapılandır</span><span class="sxs-lookup"><span data-stu-id="9b4e0-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="9b4e0-135">Ardından, biz olmasını sağlayan bir basit bir node.js uygulaması kullanmak Twilio API Merhaba toowrite başlar.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="9b4e0-136">Başlamadan önce bizim Twilio hesap kimlik bilgilerini tooconfigure ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="9b4e0-137">Sistem ortam değişkenleri Twilio kimlik bilgilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b4e0-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="9b4e0-138">Sipariş kimliği doğrulanmış toomake isteklerinde hello Twilio arka uç karşı bizim hesap SID'si ve kimlik doğrulama belirteci, hangi işlev hello kullanıcı adı ve parola bizim Twilio hesabı için ayarlanan olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="9b4e0-139">Bunlar azure'da hello düğümü modülü ile kullanılmak üzere olan doğrudan hello Azure Yönetici konsolunda ayarlanan sistem ortam değişkenlerini aracılığıyla en güvenli yolu tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="9b4e0-140">Node.js Web sitenizi seçin ve hello "Yapılandırma" bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="9b4e0-141">Bir bit kaydırın, uygulamanız için yapılandırma özelliklerini ayarlayabileceğiniz bir alan görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="9b4e0-142">Twilio hesabı kimlik bilgilerinizi girin ([Twilio konsolunuzdan bulunan][twilio_console]) gösterildiği gibi - emin tooname olun bunları `TWILIO_ACCOUNT_SID` ve `TWILIO_AUTH_TOKEN`sırasıyla:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Azure Yönetim Konsolu][azure-admin-console]

<span data-ttu-id="9b4e0-144">Bu değişkenler yapılandırdıktan sonra uygulamanızı hello Azure konsolunda yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="9b4e0-145">Merhaba Twilio package.json modülünde bildirme</span><span class="sxs-lookup"><span data-stu-id="9b4e0-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="9b4e0-146">Toocreate package.json toomanage bizim düğümü modülü bağımlılıkları aracılığıyla daha ihtiyacımız [npm].</span><span class="sxs-lookup"><span data-stu-id="9b4e0-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="9b4e0-147">Merhaba aynı hello düzey `server.js` hello oluşturulan dosya *Azure/node.js* öğretici, adlı bir dosya oluşturun `package.json`.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="9b4e0-148">Bu dosya içinde hello aşağıdaki koyun:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-148">Inside this file, place hello following:</span></span>

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

<span data-ttu-id="9b4e0-149">Bu hello twilio modülü bir bağımlılık yanı sıra hello popüler bildirir [Express web çerçevesi] [ express] ve hello EJS şablon motoru.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="9b4e0-150">Tamam, biz başlamaya artık hazırsınız - biraz kod yazalım!</span><span class="sxs-lookup"><span data-stu-id="9b4e0-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="9b4e0-151">Giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="9b4e0-151">Make an Outbound Call</span></span>
<span data-ttu-id="9b4e0-152">Burada bir çağrı tooa sayısı yerleştirir basit bir form oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="9b4e0-153">Açık `server.js`ve hello aşağıdaki kodu girin.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="9b4e0-154">Burada "CHANGE_ME" Merhaba azure Web sitenizin adı var. put - diyor dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

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

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
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

<span data-ttu-id="9b4e0-155">Ardından, adlı bir dizin oluşturun `views` - bu dizin içinde adlı bir dosya oluşturun `index.ejs` içeriği aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

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
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="9b4e0-156">Şimdi, Web sitesi tooAzure dağıtmak ve ev açın.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="9b4e0-157">Telefon numaranız hello metin alanında mümkün tooenter olması ve Twilio numarasından bir arama alırsınız!</span><span class="sxs-lookup"><span data-stu-id="9b4e0-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="9b4e0-158">SMS iletisi gönder</span><span class="sxs-lookup"><span data-stu-id="9b4e0-158">Send an SMS Message</span></span>
<span data-ttu-id="9b4e0-159">Şimdi, bir kullanıcı arabirimi ve mantığı toosend işleme formunu bir kısa mesaj şimdi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="9b4e0-160">Açık `server.js`ve hello son çağrısından sonra çok koddan hello ekleyin`app.post`:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="9b4e0-161">İçinde `views/index.ejs`, başka bir form hello ilk toosubmit altında bir sayı ve kısa mesaj ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="9b4e0-162">Uygulama tooAzure yeniden dağıtın ve form ve kendiniz (veya en yakın arkadaşlarınızın hiçbirini) SMS mesajı gönderecek mümkün toosubmit şimdi olmalıdır!</span><span class="sxs-lookup"><span data-stu-id="9b4e0-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="9b4e0-163">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9b4e0-163">Next Steps</span></span>
<span data-ttu-id="9b4e0-164">Artık, node.js ve iletişim Twilio toobuild uygulamaları kullanma temelleri hello öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="9b4e0-165">Ancak bu örnekler Twilio ve node.js ile olası nedir, hello yüzeyini neredeyse hiç boş.</span><span class="sxs-lookup"><span data-stu-id="9b4e0-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="9b4e0-166">Node.js ile Twilio kullanarak daha fazla bilgi için kaynakları aşağıdaki hello denetleyin:</span><span class="sxs-lookup"><span data-stu-id="9b4e0-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="9b4e0-167">[Resmi modülü belgeleri][docs]</span><span class="sxs-lookup"><span data-stu-id="9b4e0-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="9b4e0-168">[Node.js uygulamaları ile VoIP öğretici][voipnode]</span><span class="sxs-lookup"><span data-stu-id="9b4e0-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="9b4e0-169">[Votr - uygulama node.js ve CouchDB (üç bölümden) ile oylama gerçek zamanlı bir SMS][votr]</span><span class="sxs-lookup"><span data-stu-id="9b4e0-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="9b4e0-170">[Node.js ile Merhaba tarayıcıda çifti programlama][pair]</span><span class="sxs-lookup"><span data-stu-id="9b4e0-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="9b4e0-171">Azure'da node.js ve Twilio korsan memnuniyet umuyoruz!</span><span class="sxs-lookup"><span data-stu-id="9b4e0-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
