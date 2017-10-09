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
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>Ses, VoIP ve Azure'da SMS Mesajlaşma Twilio kullanma
Bu kılavuz gösterir toobuild uygulamalar, nasıl iletişim Twilio ve azure'da node.js kurar.

<a id="whatis"/>

## <a name="what-is-twilio"></a>Twilio nedir?
Twilio, geliştiricilerin toomake kolaylaştırır ve telefon çağrılarını almak, Gönder ve metin iletileri almasına ve tarayıcı tabanlı ve yerel mobil uygulamalara VoIP arama katıştırmak bir API platformudur. Şimdi bunun girmeden önce işleyişi kısaca gidin.

### <a name="receiving-calls-and-text-messages"></a>Aramaları ve metin iletileri alma
Twilio sağlayan geliştiriciler çok[programlanabilir telefon numaralarını satın] [ purchase_phone] kullanılan tooboth olabilen gönderip çağrıları ve metin iletileri. Twilio sayıyı bir gelen arama veya metin aldığında, Twilio web uygulamanızı bir HTTP POST veya GET isteğini nasıl toohandle hello üzerinde arama veya kısa mesaj yönergeler için isteyen gönderir. Sunucunuz tooTwilio'nın HTTP isteğiyle yanıtlar [TwiML][twiml], yönergeler içeren XML etiketleri basit bir dizi toohandle arama veya metin. Yalnızca bir dakika içinde TwiML örneklerde göreceğiz.

### <a name="making-calls-and-sending-text-messages"></a>Çağrıları yapma ve metin iletileri gönderme
Geliştiriciler, HTTP isteklerini toohello Twilio web hizmeti API'sine yaparak, kısa mesaj göndermek veya giden telefon aramaları başlatın. Giden çağrıları için hello Geliştirici de toohandle hello giden nasıl çağrısı, bağlı olduğu bir kez TwiML yönergeler döndüren bir URL belirtmeniz gerekir.

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>UI kodunda (JavaScript, iOS veya Android) VoIP yetenekleri katıştırma
Twilio tüm masaüstü web tarayıcısı, iOS uygulaması ya da Android uygulaması VoIP telefon kapatabilirsiniz bir istemci-tarafı SDK sağlar. Bu makalede, sizi nasıl odaklanacaktır toouse VoIP hello tarayıcıda çağırma. Toplama toohello içinde *Twilio JavaScript SDK'sı* hello tarayıcıda çalışan, bir sunucu-tarafı uygulaması (node.js uygulamamız) kullanılan tooissue "özelliği belirteci" toohello JavaScript istemci olması gerekir. Daha fazla bilgiyi VoIP node.js ile kullanma hakkında [hello Twilio geliştirme blogunda][voipnode].

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>Twilio (Microsoft iskonto) için kaydolun
Twilio hizmetlerini kullanmadan önce öncelikle [bir hesap için kaydolabilirsiniz][signup]. Microsoft Azure müşterilerin alma özel bir indirim - [burada yukarı emin toosign olması][signup]!

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>Oluşturma ve bir node.js Azure Web sitesi dağıtma
Ardından, Azure üzerinde çalışan bir node.js Web sitesi toocreate gerekir. [Bunu yapmak için resmi belge hello bulunduğu burada][azure_new_site]. Yüksek bir düzeyde hello aşağıdakileri yaparak:

* Zaten yoksa, bir Azure hesabı için kaydolma
* Hello Azure Yönetici Konsolu toocreate yeni bir Web sitesi kullanma
* Kaynak denetimi desteği (git kullanılan varsayacağız) ekleme
* Bir dosya oluşturulurken `server.js` basit bir node.js web uygulaması ile
* Bu basit uygulama tooAzure dağıtma

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>Merhaba Twilio modülü Yapılandır
Ardından, biz olmasını sağlayan bir basit bir node.js uygulaması kullanmak Twilio API Merhaba toowrite başlar. Başlamadan önce bizim Twilio hesap kimlik bilgilerini tooconfigure ihtiyacımız var.

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>Sistem ortam değişkenleri Twilio kimlik bilgilerini yapılandırma
Sipariş kimliği doğrulanmış toomake isteklerinde hello Twilio arka uç karşı bizim hesap SID'si ve kimlik doğrulama belirteci, hangi işlev hello kullanıcı adı ve parola bizim Twilio hesabı için ayarlanan olarak gerekir. Bunlar azure'da hello düğümü modülü ile kullanılmak üzere olan doğrudan hello Azure Yönetici konsolunda ayarlanan sistem ortam değişkenlerini aracılığıyla en güvenli yolu tooconfigure hello.

Node.js Web sitenizi seçin ve hello "Yapılandırma" bağlantısını tıklatın.  Bir bit kaydırın, uygulamanız için yapılandırma özelliklerini ayarlayabileceğiniz bir alan görürsünüz.  Twilio hesabı kimlik bilgilerinizi girin ([Twilio konsolunuzdan bulunan][twilio_console]) gösterildiği gibi - emin tooname olun bunları `TWILIO_ACCOUNT_SID` ve `TWILIO_AUTH_TOKEN`sırasıyla:

![Azure Yönetim Konsolu][azure-admin-console]

Bu değişkenler yapılandırdıktan sonra uygulamanızı hello Azure konsolunda yeniden başlatın.

### <a name="declaring-hello-twilio-module-in-packagejson"></a>Merhaba Twilio package.json modülünde bildirme
Toocreate package.json toomanage bizim düğümü modülü bağımlılıkları aracılığıyla daha ihtiyacımız [npm]. Merhaba aynı hello düzey `server.js` hello oluşturulan dosya *Azure/node.js* öğretici, adlı bir dosya oluşturun `package.json`.  Bu dosya içinde hello aşağıdaki koyun:

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

Bu hello twilio modülü bir bağımlılık yanı sıra hello popüler bildirir [Express web çerçevesi] [ express] ve hello EJS şablon motoru.  Tamam, biz başlamaya artık hazırsınız - biraz kod yazalım!

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>Giden bir çağrı yapın
Burada bir çağrı tooa sayısı yerleştirir basit bir form oluşturalım. Açık `server.js`ve hello aşağıdaki kodu girin. Burada "CHANGE_ME" Merhaba azure Web sitenizin adı var. put - diyor dikkat edin:

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

Ardından, adlı bir dizin oluşturun `views` - bu dizin içinde adlı bir dosya oluşturun `index.ejs` içeriği aşağıdaki hello ile:

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

Şimdi, Web sitesi tooAzure dağıtmak ve ev açın. Telefon numaranız hello metin alanında mümkün tooenter olması ve Twilio numarasından bir arama alırsınız!

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>SMS iletisi gönder
Şimdi, bir kullanıcı arabirimi ve mantığı toosend işleme formunu bir kısa mesaj şimdi ayarlayın. Açık `server.js`ve hello son çağrısından sonra çok koddan hello ekleyin`app.post`:

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

İçinde `views/index.ejs`, başka bir form hello ilk toosubmit altında bir sayı ve kısa mesaj ekleyin:

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

Uygulama tooAzure yeniden dağıtın ve form ve kendiniz (veya en yakın arkadaşlarınızın hiçbirini) SMS mesajı gönderecek mümkün toosubmit şimdi olmalıdır!

<a id="nextsteps"/>

## <a name="next-steps"></a>Sonraki Adımlar
Artık, node.js ve iletişim Twilio toobuild uygulamaları kullanma temelleri hello öğrendiniz. Ancak bu örnekler Twilio ve node.js ile olası nedir, hello yüzeyini neredeyse hiç boş. Node.js ile Twilio kullanarak daha fazla bilgi için kaynakları aşağıdaki hello denetleyin:

* [Resmi modülü belgeleri][docs]
* [Node.js uygulamaları ile VoIP öğretici][voipnode]
* [Votr - uygulama node.js ve CouchDB (üç bölümden) ile oylama gerçek zamanlı bir SMS][votr]
* [Node.js ile Merhaba tarayıcıda çifti programlama][pair]

Azure'da node.js ve Twilio korsan memnuniyet umuyoruz!

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
