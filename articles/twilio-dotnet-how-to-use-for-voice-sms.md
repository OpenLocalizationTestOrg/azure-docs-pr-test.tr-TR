---
title: aaaHow tooUse Twilio ses ve SMS (.NET) | Microsoft Docs
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. .NET ile yazılan kod örnekleri."
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>Nasıl toouse Twilio ses ve azure'dan SMS özellikleri
Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir. Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir. Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.

## <a id="WhatIs"></a>Twilio nedir?
Twilio iş iletişimleri hello geleceği destekleyen, geliştiricilerin tooembed ses, VoIP, etkinleştirme ve uygulamalara Mesajlaşma. Bunlar hello Twilio iletişimleri API platformu ile gösterme bulut tabanlı, genel bir ortamda gerekli tüm altyapı sanallaştırın. Uygulamalardır basit toobuild ve ölçeklendirilebilir. Kullandıkça Öde fiyatlandırma ile esnekliğinin ve bulut güvenilirlik ' yararlanabilirsiniz.

**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar. **Twilio SMS** SMS iletileri almasına ve uygulamaları toosend sağlar. **Twilio istemci** toomake VoIP çağrılarından herhangi telefon, tablet veya tarayıcı sağlar ve WebRTC destekler.

## <a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler
Azure müşterilerin alacak bir [özel teklif](http://www.twilio.com/azure): 10 ücretsiz Twilio Twilio hesabınızı yükseltirken kredisi. Bu Twilio kredi uygulanan tooany Twilio kullanım (1. 000'kadar SMS iletileri veya too1000 yukarı alma gelen telefon numarasını ve ileti veya çağrı hedef hello konumuna bağlı olarak sesli dakika başına 10 kredi eşdeğer toosending) olabilir. Bu Twilio iade almak ve adresindeki başlama [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio Kullandıkça Ödeme tabanlı bir hizmettir. Hiçbir Kurulum ücretleri vardır ve herhangi bir zamanda hesabınızı kapatabilirsiniz. Daha fazla bilgi bulabilirsiniz [Twilio fiyatlandırma](http://www.twilio.com/voice/pricing).

## <a id="Concepts"></a>Kavramları
Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır. İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].

Merhaba Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.

### <a id="Verbs"></a>Twilio fiiller
Merhaba API yapar Twilio kullanmak fiiller; Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.

Merhaba, Twilio fiillerin listesi verilmiştir.  Bilgi hakkında hello diğer fiilleri ve yetenekleri aracılığıyla [Twilio biçimlendirme dili belgeleri](http://www.twilio.com/docs/api/twiml).

* **&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.
* **&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.
* **&lt;Kapat&gt;**: bir aramasını sonlandırır.
* **&lt;Yürüt&gt;**: bir ses dosyası çalar.
* **&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.
* **&lt;Kayıt&gt;**: hello arayanın sesli kaydeder ve bir hello kaydı içeren bir dosyanın URL'sini döndürür.
* **&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.
* **&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın
* **&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.
* **&lt;SMS&gt;**: SMS iletisi gönderir.

### <a id="TwiML"></a>TwiML
TwiML XML tabanlı yönergeleri nasıl Twilio bildirmek hello Twilio fiiller üzerinde temel kümesidir tooprocess çağrısı veya SMS.

Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Twilio API uygulaması çağrılarınızı Merhaba, hello API parametrelerden biri hello TwiML yanıt veren hello URL'dir. Geliştirme amaçlı sağlanan Twilio URL'leri tooprovide hello TwiML yanıtlarını uygulamalarınız tarafından kullanılan kullanabilirsiniz. Kendi URL'leri tooproduce hello TwiML yanıtları de barındırabilir ve başka bir seçeneği toouse hello **TwiMLResponse** nesnesi.

Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml]. Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Twilio hesabı oluşturma
Hazır tooget Twilio hesabı olduğunuzda, oturum açın [deneyin Twilio][try_twilio]. Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.

Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız. Her ikisi de gerekli toomake Twilio API çağrıları olacaktır. tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun. Hesap Kimliğini ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio hesap sayfası][twilio_account], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.

## <a id="create_app"></a>Azure uygulama oluşturma
Etkin Twilio uygulamasını barındıran Azure uygulaması herhangi diğer Azure uygulamasından farklı değildir. Merhaba Twilio .NET kitaplığı ekleyip hello rol toouse hello Twilio .NET kitaplıklarına yapılandırabilirsiniz.
İlk Azure projesi oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio ile bir Azure projesi oluşturma][vs_project].

## <a id="configure_app"></a>Uygulamanızı toouse Twilio kitaplıklarını yapılandırmak
Twilio toogenerate TwiML yanıtlar Twilio tooprovide basit ve kolay şekilde toointeract hello Twilio REST API ve Twilio istemci ile çeşitli yönlerini sarmalamak .NET Yardımcısı kitaplıkları kümesi sağlar.

Twilio .NET geliştiricileri için beş kitaplıkları sağlar:
Kitaplık|Açıklama
---|---
Twilio.API|Merhaba Twilio REST API kolay .NET Kitaplığı'nda sarmalar hello çekirdek Twilio kitaplığı. Bu kitaplık, .NET, Silverlight ve Windows Phone 7 için kullanılabilir.
Twilio.TwiML|Bir .NET kolay şekilde toogenerate TwiML biçimlendirme sağlar.
Twilio.MVC|ASP.NET MVC kullanan geliştiriciler için bu kitaplığı TwilioController, TwiML ActionResult ve istek doğrulama özniteliği içerir.
Twilio.WebMatrix|Microsoft'un ücretsiz WebMatrix geliştirme aracını kullanarak geliştiriciler için bu kitaplık çeşitli Twilio eylemler için Razor sözdizimi Yardımcıları içerir.
Twilio.Client.Capability|Merhaba yetenek belirteç Oluşturucu hello Twilio istemci JavaScript SDK'sı ile kullanılmak üzere içerir.

Tüm kitaplıkları .NET 3.5, Silverlight 4 veya Windows Phone 7 veya üzeri gerektiğini unutmayın.

Bu kılavuzda sağlanan hello örnekleri hello Twilio.API kitaplığını kullanın.

Merhaba kitaplıkları olabilir [hello NuGet Paket Yöneticisi uzantısı kullanılarak yüklenen](http://www.twilio.com/docs/csharp/install) too2015 yukarı Visual Studio 2010 için kullanılabilir.  Merhaba kaynak kodu barındırılan [GitHub][twilio_github_repo], hello kitaplıklarını kullanma için kapsamlı belgeler içeren bir Wiki içerir.

Varsayılan olarak, Microsoft Visual Studio 2010 NuGet 1.2 sürümünü yükler. Merhaba Twilio kitaplıkları yükleme sürüm 1.6 NuGet veya üstü gerektirir. Yükleme veya NuGet güncelleştirme hakkında daha fazla bilgi için bkz: [http://nuget.org/][nuget].

> [!NOTE]
> tooinstall hello en son sürümünü NuGet, ilk hello Visual Studio Uzantı Yöneticisi'ni kullanarak hello yüklü sürümünü kaldırmanız gerekir. toodo bu nedenle, Visual Studio Yönetici olarak çalıştırmanız gerekir. Aksi takdirde hello Kaldır düğmesi devre dışıdır.
>
>

### <a id="use_nuget"></a>tooadd hello Twilio kitaplıkları tooyour Visual Studio projesi:
1. Çözümünüzü Visual Studio'da açın.
2. Sağ **başvurular**.
3. Tıklatın **NuGet paketlerini Yönet...**
4. Tıklatın **çevrimiçi**.
5. Merhaba arama çevrimiçi kutusuna *twilio*.
6. Tıklatın **yükleme** hello Twilio paketinizdeki.

## <a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın
Merhaba aşağıdaki giden toomake nasıl hello kullanarak Çağır gösterir **CallResource** sınıfı. Bu kod ayrıca Twilio tarafından sağlanan site tooreturn hello Twilio biçimlendirme dili (TwiML) yanıt kullanır. Kendi değerlerinizi hello yerine **için** ve **gelen** telefon numaraları ve hello doğrulayın olun **gelen** telefon numarası Twilio hesabınızın hello kod çalıştırmadan önce.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

Toohello içinde geçirilen hello parametreler hakkında daha fazla bilgi için **CallResource.Create** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Belirtildiği gibi bu kodu bir Twilio tarafından sağlanan site tooreturn hello TwiML yanıt kullanır. Bunun yerine, kendi site tooprovide hello TwiML yanıt kullanabilirsiniz. Daha fazla bilgi için bkz: [nasıl yapılır: sağlamak TwiML yanıtları kendi Web sitesinden](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin
Merhaba aşağıdaki ekran görüntüsü bir SMS iletisini kullanarak toosend nasıl hello gösterir **MessageResource** sınıfı. Merhaba **gelen** SMS iletileri toosend deneme hesapları için numarası Twilio tarafından sağlanır. Merhaba **için** numarası gerekir doğrulandı Twilio hesabınız için hello kodu çalıştırmadan önce.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar
Ne zaman uygulamanızı başlatır çağrısı toohello Twilio API - Örneğin, hello **CallResource.Create** yöntemi - Twilio beklenen tooreturn, istek tooan URL bir TwiML yanıtını gönderir. Merhaba örnekte [nasıl yapılır: giden bir çağrı yapmak](#howto_make_call) kullanır hello Twilio tarafından sağlanan URL [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello yanıt.

> [!NOTE]
> TwiML web hizmetleri tarafından kullanılmak üzere tasarlandığından, hello TwiML tarayıcınızda görüntüleyebilirsiniz. Örneğin, [http://twimlets.com/message] [ twimlet_message_url] toosee boş bir &lt;yanıt&gt; öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message ? İleti % 5B0 %5 D Hello % 20World =](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee bir &lt;yanıt&gt; içeren öğe bir &lt;Say&gt; öğesi.
>
>

Merhaba Twilio tarafından sağlanan URL güvenmek yerine, HTTP yanıtlarını döndürür kendi URL sitesi oluşturabilirsiniz. HTTP yanıt veren herhangi bir dilde hello sitesi oluşturabilirsiniz. Bu konu, bir ASP.NET genel işleyici hello URL'den barındırma varsayar.

ASP.NET işleyicisi aşağıdaki hello işler bildiren TwiML yanıt **Hello World** hello çağrıda.

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
Yukarıdaki hello örnekte görebildiğiniz gibi hello TwiML yanıt basitçe bir XML dosyasıdır. Merhaba Twilio.TwiML kitaplığı TwiML oluşturacaktır sınıfları içerir. Merhaba aşağıdaki örnek yukarıda gösterildiği gibi hello eşdeğer yanıt oluşturur, ancak kullanır hello **VoiceResponse** sınıfı.

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

TwiML hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).

Bir şekilde tooprovide TwiML yanıtları ayarladıktan sonra bu URL toohello geçirebilirsiniz **CallResource.Create** yöntemi. Örneğin, dağıtılan MyTwiML tooan Azure bulut hizmeti adlı bir web uygulaması varsa ve hello ASP.NET işleyicinizi adıdır mytwiml.ashx hello URL çok geçirilebilir**CallResource.Create** hello kod aşağıdaki gösterildiği gibi Örnek:

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

ASP.NET ile azure'da Twilio kullanma hakkında ek bilgi için bkz: [nasıl toomake bir telefon görüşmesi Twilio Azure üzerinde bir web rolü kullanılarak][howto_phonecall_dotnet].

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
