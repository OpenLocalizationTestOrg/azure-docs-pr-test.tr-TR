---
title: aaaHow tooUse Twilio ses ve SMS (Ruby) | Microsoft Docs
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. Ruby içinde yazılan kod örnekleri."
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>Nasıl tooUse Twilio ses ve SMS özelliklerini Söyleniş için
Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir. Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir. Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.

## <a id="WhatIs"></a>Twilio nedir?
Twilio varolan web dilleri ve yetenekleri toobuild ses ve SMS uygulamaları kullanmanıza olanak sağlayan bir telefon web hizmeti API'dir. Twilio, (olmayan bir Azure özelliğidir ve Microsoft Ürün) bir bir üçüncü taraf hizmetidir.

**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar. **Twilio SMS** SMS iletileri almasına ve uygulamaları toomake sağlar. **Twilio istemci** uygulamalarınızın mobil bağlantıları dahil olmak üzere var olan Internet bağlantıları kullanarak tooenable sesli iletişime olanak sağlar.

## <a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler
Twilio fiyatlandırma hakkında daha fazla bilgi şu adreste [Twilio fiyatlandırma][twilio_pricing]. Azure müşterilerine alma bir [özel teklif][special_offer]: boş bir kredi 1000 metinlerinin veya 1000 dakika sayısı. Bu kaydınızı toosign sunmak veya daha fazla bilgi almak, lütfen şu adresi ziyaret [http://ahoy.twilio.com/azure][special_offer].  

## <a id="Concepts"></a>Kavramları
Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır. İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].

### <a id="TwiML"></a>TwiML
TwiML nasıl Twilio bildiren XML tabanlı yönergeleri kümesidir tooprocess çağrısı veya SMS.

Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Tüm TwiML dosyalarınız `<Response>` kendi kök öğesi olarak. Burada, uygulamanızın Twilio fiiller toodefine hello davranışını kullanın.

### <a id="Verbs"></a>TwiML fiiller
Twilio fiiller olan Twilio çok ne yapacağımı XML etiketleri**yapmak**. Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir. 

Merhaba, Twilio fiillerin listesi verilmiştir.

* **&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.
* **&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.
* **&lt;Kapat&gt;**: bir aramasını sonlandırır.
* **&lt;Yürüt&gt;**: bir ses dosyası çalar.
* **&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.
* **&lt;Kayıt&gt;**: hello arayanın sesli kayıtlar ve hello kaydı içeren bir dosyanın URL'sini döndürür.
* **&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.
* **&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın
* **&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.
* **&lt;SMS&gt;**: SMS iletisi gönderir.

Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml]. Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Twilio hesabı oluşturma
Hazır tooget Twilio hesabı olduğunuzda, oturum açın [deneyin Twilio][try_twilio]. Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.

Twilio hesabı için kaydolduğunuzda, uygulamanız için bir ücretsiz telefon numarası elde edersiniz. Ayrıca, bir hesap SID'si ve bir kimlik doğrulama belirteci alırsınız. Her ikisi de gerekli toomake Twilio API çağrıları olacaktır. tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun. Hesabınızın SID ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio hesap sayfası][twilio_account], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ** , sırasıyla.

### <a id="VerifyPhoneNumbers"></a>Telefon numaralarını doğrulayın
Ekleme toohello numarası Twilio tarafından verilen uygulamalarınızda kullanım için (örneğin, cep telefonu veya ev telefon numarası) kontrol sayılar da doğrulayabilirsiniz. 

Hakkında bilgi için bir telefon numarası tooverify bkz [yönetmek numaraları][verify_phone].

## <a id="create_app"></a>Ruby uygulaması oluşturma
Merhaba Twilio hizmeti kullanır ve Azure üzerinde çalışan bir Ruby uygulaması hello Twilio hizmetini kullanan tüm diğer Söyleniş uygulamadan daha farklı değildir. Twilio Hizmetleri RESTful ve Ruby çeşitli yollarla çağrılabilir olsa da, bu makalede toouse Twilio ile hizmetleri nasıl üzerine odaklanacaktır [Twilio yardımcı kitaplık Ruby için][twilio_ruby].

İlk olarak, [Kurulum yeni bir Azure Linux VM] [ azure_vm_setup] tooact yeni Söyleniş web uygulamanız için bir konak olarak. Merhaba adımları rayları uygulama, yalnızca Kurulum hello VM Hello oluşturulmasını içeren yoksay. Bir dış bağlantı noktası 80 ve 5000 iç bir bağlantı noktası ile bir uç nokta oluşturduğunuzdan emin olun.

Merhaba aşağıdaki örnekte, biz kullanacağınız [Sinatra][sinatra], Ruby için çok basit web çerçevesi. Ancak kesinlikle hello Twilio yardımcı kitaplık için Ruby Ruby rayları üzerinde de dahil olmak üzere tüm diğer web framework ile kullanabilirsiniz.

Yeni VM'nin içine SSH ve yeni uygulamanız için bir dizin oluşturun. Bu dizini içinde kod içine aşağıdaki Gemfile ve kopyalama hello adlı bir dosya oluşturun:

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

Merhaba komut satırını Çalıştır üzerinde `bundle install`. Bu, yukarıdaki hello bağımlılıkları yükler. Sonraki adlı bir dosya oluşturun `web.rb`. Bu, web uygulamanız için hello kodu nerede yaşıyor olacaktır. Kod içine aşağıdaki hello yapıştırın:

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

Bu noktada çalıştırmak mümkün hello hello komutu olmalıdır `ruby web.rb -p 5000`. Bu dönüş-bağlantı noktası 5000 küçük web sunucusunda yukarı. Merhaba URL adresini ziyaret ederek tarayıcınızda mümkün toobrowse toothis uygulama olmalıdır, Kurulum, Azure VM için. Web uygulamanızı hello tarayıcıda ulaştıktan sonra bir Twilio uygulaması oluşturmaya hazır toostart demektir.

## <a id="configure_app"></a>Uygulamanızı tooUse Twilio yapılandırın
Web uygulaması toouse hello Twilio kitaplığınızın güncelleştirerek yapılandırabilirsiniz, `Gemfile` tooinclude bu satırı:

    gem 'twilio-ruby'

Merhaba komut satırında çalıştırmak `bundle install`. Şimdi açmak `web.rb` ve bu satırı hello üstünde dahil olmak üzere:

    require 'twilio-ruby'

Web uygulamanız için Ruby toouse hello Twilio yardımcı kitaplık ayarlamak artık olduğunuz.

## <a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın
Aşağıdaki hello nasıl giden toomake çağrısı gösterir. Temel kavramları hello Twilio yardımcı kitaplık Söyleniş toomake REST API çağrıları için kullanarak ve TwiML işleme içerir. Kendi değerlerinizi hello yerine **gelen** ve **için** telefon numaraları ve hello doğruladığınızdan emin olun **gelen** Twilio hesabı önceki toorunning hello kodunuz için telefon numarası.

Bu işlev çok eklemek`web.md`:

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

Açık yukarı ise `http://yourdomain.cloudapp.net/make_call` bir tarayıcıda, tetiklemek hello çağrısı toohello Twilio API toomake hello telefon araması. ilk iki parametrelerinde hello `client.account.calls.create` oldukça kendinden açıklamalıdır: hello sayı hello çağrısı `from` ve hello sayı hello çağrısı `to`. 

Üçüncü parametre hello (`url`) hello çağrısı bağlandıktan sonra Twilio hangi toodo tooget yönergeler istekleri hello URL'dir. Bu durumda biz Kurulum bir URL (`http://yourdomain.cloudapp.net`), basit bir TwiML belge döndürür ve kullandığı hello `<Say>` bazı okuma ve deyin alma "Merhaba Monkey" toohello kişi hello fiil toodo çağırın.

## <a id="howto_recieve_sms"></a>Nasıl yapılır: alma SMS iletisi
Merhaba önceki örnekte biz başlatılan bir **giden** telefon araması. Bu kez, Twilio sırasında kaydolma tooprocess bize verdiğiniz hello telefon numarası kullanalım bir **gelen** SMS iletisi.

Birincisi, oturum açma tooyour [Twilio Pano][twilio_account]. "Numaralarında" Merhaba üst nav uygulamasında tıklayın ve Twilio sayısı, sağlanan üzerinde hello'ye tıklayın. Yapılandırabileceğiniz iki URL'leri görürsünüz. Sesli istek URL'si ve bir SMS istek URL'si. Twilio çağrıları bir telefon araması her yapıldığında hello URL'leri bunlar veya SMS tooyour numarası gönderilir. Merhaba URL'leri "web kancaları" da bilinir.

Biz ister tooprocess gelen SMS iletileri sağlandığından güncelleştirme hello URL çok`http://yourdomain.cloudapp.net/sms_url`. Bir tane hello sayfanın hello Değişiklikleri Kaydet'ı tıklatın. Şimdi, geri `web.rb` şimdi bizim uygulama toohandle bu programı:

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

Hello değişiklik yaptıktan sonra web uygulamanızı emin toore başlangıç yapın. Şimdi telefonunuz alın ve SMS tooyour Twilio numarası gönderin. Derhal "Hey, hello ping için teşekkür ederiz! bildiren bir SMS yanıt almanız gerekir Twilio ve Azure rock! ".

## <a id="additional_services"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın
Ayrıca, web tabanlı API'ler Twilio sunar buradaki toohello örnekler Azure uygulamanızı tooleverage ek Twilio işlevini kullanabilirsiniz. Tüm Ayrıntılar için bkz: hello [Twilio API belgelerine][twilio_api_documentation].

### <a id="NextSteps"></a>Sonraki Adımlar
Merhaba Twilio hizmet hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin:

* [Twilio güvenlik yönergeleri][twilio_security_guidelines]
* [Twilio HowTos ve örnek kod][twilio_howtos]
* [Twilio hızlı başlangıç öğreticileri][twilio_quickstarts] 
* [Github'da Twilio][twilio_on_github]
* [Konuşma tooTwilio desteği][twilio_support]

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
