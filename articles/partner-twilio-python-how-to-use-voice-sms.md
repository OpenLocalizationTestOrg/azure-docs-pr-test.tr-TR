---
title: aaaHow tooUse Twilio ses ve SMS (Python) | Microsoft Docs
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. Kod örnekleri Python içinde yazılmış."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>Nasıl tooUse Twilio ses ve Python SMS özellikleri
Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir. Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir. Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.

## <a id="WhatIs"></a>Twilio nedir?
Twilio iş iletişimleri hello geleceği destekleyen, geliştiricilerin tooembed ses, VoIP, etkinleştirme ve uygulamalara Mesajlaşma. Bunlar hello Twilio iletişimleri API platformu ile gösterme bulut tabanlı, genel bir ortamda gerekli tüm altyapı sanallaştırın. Uygulamalardır basit toobuild ve ölçeklendirilebilir. Sizinle ödeme-olarak esnekliğinin fiyatlandırma gidin ve bulut güvenilirlik ' yararlanır.

**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar.
**Twilio SMS** metin iletileri almasına ve uygulama toosend sağlar.
**Twilio istemci** toomake VoIP çağrılarından herhangi telefon, tablet veya tarayıcı sağlar ve WebRTC destekler.

## <a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler
Azure müşterilerin alacak bir [özel teklif] [ special_offer] 10 Twilio Twilio hesabınızı yükseltirken kredisi. Bu Twilio kredi uygulanan tooany Twilio kullanım (1. 000'kadar SMS iletileri veya too1000 yukarı alma gelen telefon numarasını ve ileti veya çağrı hedef hello konumuna bağlı olarak sesli dakika başına 10 kredi eşdeğer toosending) olabilir. Bu kullanmak [Twilio kredi] [ special_offer] ve çalışmaya başlama.

Twilio Kullandıkça Ödeme tabanlı bir hizmettir. Hiçbir Kurulum ücretleri vardır ve herhangi bir zamanda hesabınızı kapatabilirsiniz. Daha fazla bilgi bulabilirsiniz [Twilio fiyatlandırma][twilio_pricing].

## <a id="Concepts"></a>Kavramları
Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır. İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].

Merhaba Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.

### <a id="Verbs"></a>Twilio fiiller
Merhaba API yapar Twilio kullanmak fiiller; Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.

Merhaba, Twilio fiillerin listesi verilmiştir. Bilgi hakkında hello diğer fiilleri ve yetenekleri aracılığıyla [Twilio biçimlendirme dili belgeleri][twiml].

* **&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.
* **&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.
* **&lt;Kapat&gt;**: bir aramasını sonlandırır.
* **&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.
* **&lt;Yürüt&gt;**: bir ses dosyası çalar.
* **&lt;Sıra&gt;**: Merhaba tooa arayanlar kuyruğunu ekleyin.
* **&lt;Kayıt&gt;**: hello arayanın hello sesli kayıtlar ve hello kaydı içeren bir dosyanın URL'sini döndürür.
* **&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.
* **&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın.
* **&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.
* **&lt;SMS&gt;**: SMS iletisi gönderir.

### <a id="TwiML"></a>TwiML
TwiML XML tabanlı yönergeleri nasıl Twilio bildirmek hello Twilio fiiller üzerinde temel kümesidir tooprocess çağrısı veya SMS.

Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Twilio API uygulaması çağrılarınızı Merhaba, hello API parametrelerden biri hello TwiML yanıt veren hello URL'dir. Geliştirme amaçlı sağlanan Twilio URL'leri tooprovide hello TwiML yanıtlarını uygulamalarınız tarafından kullanılan kullanabilirsiniz. Kendi URL'leri tooproduce hello TwiML yanıtları de barındırabilir ve başka bir seçeneği toouse hello `TwiMLResponse` nesnesi.

Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml]. Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Twilio hesabı oluşturma
Konumundaki hazır tooget Twilio hesabı olduğunda kaydolun [deneyin Twilio][try_twilio]. Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.

Twilio hesabı için kaydolduğunuzda, SID bir hesap ve kimlik doğrulama belirtecini alır. Her ikisi de gerekli toomake Twilio API çağrıları olacaktır. tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun. Hesabınızın SID ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio konsol][twilio_console], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.

## <a id="create_app"></a>Python uygulaması oluşturma
Merhaba Twilio hizmeti kullanır ve Azure üzerinde çalışan bir Python uygulaması hello Twilio hizmetini kullanan tüm diğer Python uygulamadan daha farklı değildir. Twilio Hizmetleri REST tabanlı ve Python çeşitli yollarla çağrılabilir olsa da, bu makalede toouse Twilio ile hizmetleri nasıl üzerine odaklanacaktır [github'dan Python için Twilio Kitaplığı][twilio_python]. Python için hello Twilio kitaplığını kullanma hakkında daha fazla bilgi için bkz: [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].

İlk olarak, [Kurulum yeni bir Azure Linux VM] [azure_vm_setup] tooact yeni Python web uygulamanız için bir konak olarak. Merhaba sanal makine çalışmaya başladıktan sonra aşağıda açıklandığı gibi tooexpose genel bir bağlantı noktası uygulamanız gerekir.

### <a name="add-an-incoming-rule"></a>Bir gelen kuralı ekleyin
  1. [Ağ güvenlik grubu] [azure_nsg] toohello Git sayfası.
  2. Ağ güvenlik grubu, sanal makineyle karşılık gelen Hello seçin.
  3. Ekleme ve **giden kuralı** için **bağlantı noktası 80**. Herhangi bir adresinden gelen emin tooallow.

### <a name="set-hello-dns-name-label"></a>Merhaba DNS ad etiketi ayarlayın
  1. Toohello [hello ortak IP adresi] Git [azure_ips] sayfası.
  2. Merhaba, sanal makineyle genel IP bu correspends seçin.
  3. Set hello **DNS ad etiketi** hello içinde **yapılandırma** bölümü. Bu örnek Hello durumda aşağıdakine benzer görünecektir *etki alanı etiketi bilgisayarınızı*. centralus.cloudapp.azure.com

Mümkün olduğunda tooconnect SSH toohello sanal makine yükleyebilirsiniz aracılığıyla hello tercih ettiğiniz Web çerçevesi (en iyi Python olan bilinen iki hello [Flask](http://flask.pocoo.org/) ve [Django](https://www.djangoproject.com)). Bunlardan birini hello çalıştırarak yükleyin `pip install` komutu.

Biz yalnızca bağlantı noktası 80 üzerinde hello sanal makine tooallow trafiği yapılandırılmış olduğunu aklınızda bulundurun. Bu nedenle bu bağlantı noktası emin tooconfigure hello uygulama toouse olun.

## <a id="configure_app"></a>Uygulamanızı tooUse Twilio kitaplıklarını yapılandırmak
Python için uygulama toouse hello Twilio kitaplığınızın iki yolla yapılandırabilirsiniz:

* Merhaba Twilio kitaplığı Python için PIP paket olarak yükleyin. Aşağıdaki komutları hello ile yüklenebilir:
   
        $ pip install twilio

    -VEYA-

* Merhaba Twilio kitaplığı Python github'dan indirin ([https://github.com/twilio/twilio-python][twilio_python]) ve aşağıdaki gibi yükleyin:

        $ python setup.py install

Python için hello Twilio kitaplığı yükledikten sonra böylece `import` Python dosyalarınızı içinde:

        import twilio

Daha fazla bilgi için bkz: [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın
Aşağıdaki hello nasıl giden toomake çağrısı gösterir. Bu kod ayrıca Twilio tarafından sağlanan site tooreturn hello Twilio biçimlendirme dili (TwiML) yanıt kullanır. Kendi değerlerinizi hello yerine **from_number** ve **to_number** telefon numaraları ve hello doğrulandıktan olun **from_number** Twilio hesabınız için telefon numarası önce çalışan hello kodu.

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

Belirtildiği gibi bu kodu bir Twilio tarafından sağlanan site tooreturn hello TwiML yanıt kullanır. Bunun yerine, kendi site tooprovide hello TwiML yanıt kullanabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooProvide TwiML yanıtları bilgisayarınızı kendi Web sitesinden](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin
Merhaba aşağıdakileri nasıl bir SMS iletisini kullanarak toosend hello gösterir `TwilioRestClient` sınıfı. Merhaba **from_number** SMS iletileri toosend deneme hesapları için numarası Twilio tarafından sağlanır. Merhaba **to_number** numarası gerekir doğrulandı Twilio hesabınız için hello kod çalıştırmadan önce.

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar
Uygulamanızı bir çağrı toohello Twilio API başlattığında Twilio olduğundan isteği tooa URL'nizi tooreturn TwiML yanıt beklenen gönderir. Hello yukarıdaki örnekte hello Twilio tarafından sağlanan URL [http://twimlets.com/message][twimlet_message_url]. (TwiML Twilio tarafından kullanılmak üzere tasarlandığından, tarayıcınızda görüntüleyebilirsiniz. Örneğin, [http://twimlets.com/message] [ twimlet_message_url] toosee boş bir `<Response>` öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message? İleti % 5B0 %5 D Hello % 20World =] [ twimlet_message_url_hello_world] toosee bir `<Response>` içeren öğe bir `<Say>` öğesi.)

Merhaba Twilio tarafından sağlanan URL güvenmek yerine, HTTP yanıtlarını döndürür, kendi site oluşturabilirsiniz. XML yanıtlarını döndürür herhangi bir dilde hello sitesi oluşturabilirsiniz; Bu konu Python toocreate hello TwiML kullanan varsaymaktadır.

Merhaba aşağıdaki örneklerde bildiren TwiML yanıt çıkış **Hello World** hello çağrıda.

Flask ile:

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

Django ile:

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

Yukarıdaki hello örnekte görebildiğiniz gibi hello TwiML yanıt basitçe bir XML dosyasıdır. Python için Hello Twilio kitaplığı TwiML oluşturacaktır sınıfları içerir. Merhaba aşağıdaki örnek yukarıda gösterildiği gibi hello eşdeğer yanıt oluşturur, ancak kullanır hello `twiml` modülü Python hello Twilio Kitaplığı'nda:

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

TwiML hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/twiml][twiml_reference].

Python uygulamanızı tooprovide TwiML yanıtları ayarlayın sahip olduktan sonra hello uygulamasının hello URL'si hello geçirilen URL hello gibi kullanın `client.calls.create` yöntemi. Adlı bir Web uygulaması varsa, örneğin, **MyTwiML** dağıtılan tooan Azure barındırılan hizmeti, kendi url hello aşağıdaki örnekte gösterildiği gibi Web kancası kullanabilirsiniz:

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <a id="AdditionalServices"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın
Ayrıca, web tabanlı API'ler Twilio sunar buradaki toohello örnekler Azure uygulamanızı tooleverage ek Twilio işlevini kullanabilirsiniz. Tüm Ayrıntılar için bkz: hello [Twilio API belgelerine][twilio_api].

## <a id="NextSteps"></a>Sonraki Adımlar
Merhaba Twilio hizmet hello temel bilgileri öğrendiniz, daha fazla bu bağlantılar toolearn izleyin:

* [Twilio güvenlik yönergeleri][twilio_security_guidelines]
* [Twilio nasıl yapılır kılavuzları ve örnek kod][twilio_howtos]
* [Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]
* [Github'da Twilio][twilio_on_github]
* [Konuşma tooTwilio desteği][twilio_support]

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
