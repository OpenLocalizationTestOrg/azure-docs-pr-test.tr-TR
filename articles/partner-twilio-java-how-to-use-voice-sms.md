---
title: aaaHow tooUse Twilio ses ve SMS (Java) | Microsoft Docs
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. Java dilinde yazılan kod örnekleri."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="f1b0e-104">Nasıl tooUse Twilio ses ve Java SMS özellikleri</span><span class="sxs-lookup"><span data-stu-id="f1b0e-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="f1b0e-105">Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="f1b0e-106">Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="f1b0e-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="f1b0e-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="f1b0e-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="f1b0e-109">Twilio varolan web dilleri ve yetenekleri toobuild ses ve SMS uygulamaları kullanmanıza olanak sağlayan bir telefon web hizmeti API'dir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="f1b0e-110">Twilio, (olmayan bir Azure özelliğidir ve Microsoft Ürün) bir bir üçüncü taraf hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="f1b0e-111">**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="f1b0e-112">**Twilio SMS** SMS iletileri almasına ve uygulamaları toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="f1b0e-113">**Twilio istemci** uygulamalarınızın mobil bağlantıları dahil olmak üzere var olan Internet bağlantıları kullanarak tooenable sesli iletişime olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="f1b0e-114"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="f1b0e-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="f1b0e-115">Twilio fiyatlandırma hakkında daha fazla bilgi şu adreste [Twilio fiyatlandırma][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="f1b0e-116">Azure müşterilerine alma bir [özel teklif][special_offer]: boş bir kredi 1000 metinlerinin veya 1000 dakika sayısı.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="f1b0e-117">Bu kaydınızı toosign sunmak veya daha fazla bilgi almak, lütfen şu adresi ziyaret [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="f1b0e-118"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="f1b0e-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="f1b0e-119">Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="f1b0e-120">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="f1b0e-121">Merhaba Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="f1b0e-122"><a id="Verbs"></a>Twilio fiiller</span><span class="sxs-lookup"><span data-stu-id="f1b0e-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="f1b0e-123">Merhaba API yapar Twilio kullanmak fiiller; Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="f1b0e-124">Merhaba, Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="f1b0e-125">**&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="f1b0e-126">**&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="f1b0e-127">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="f1b0e-128">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="f1b0e-129">**&lt;Sıra&gt;**: Merhaba tooa arayanlar kuyruğunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="f1b0e-130">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="f1b0e-131">**&lt;Kayıt&gt;**: hello arayanın sesli kayıtlar ve hello kaydı içeren bir dosyanın URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="f1b0e-132">**&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="f1b0e-133">**&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="f1b0e-134">**&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="f1b0e-135">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="f1b0e-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="f1b0e-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="f1b0e-137">TwiML XML tabanlı yönergeleri nasıl Twilio bildirmek hello Twilio fiiller üzerinde temel kümesidir tooprocess çağrısı veya SMS.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="f1b0e-138">Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="f1b0e-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="f1b0e-139">toospeech.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="f1b0e-140">Twilio API uygulaması çağrılarınızı Merhaba, hello API parametrelerden biri hello TwiML yanıt veren hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="f1b0e-141">Geliştirme amaçlı sağlanan Twilio URL'leri tooprovide hello TwiML yanıtlarını uygulamalarınız tarafından kullanılan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="f1b0e-142">Kendi URL'leri tooproduce hello TwiML yanıtları de barındırabilir ve başka bir seçeneği toouse hello **TwiMLResponse** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="f1b0e-143">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="f1b0e-144">Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="f1b0e-145"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1b0e-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="f1b0e-146">Hazır tooget Twilio hesabı olduğunuzda, oturum açın [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="f1b0e-147">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="f1b0e-148">Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="f1b0e-149">Her ikisi de gerekli toomake Twilio API çağrıları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="f1b0e-150">tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="f1b0e-151">Hesap Kimliğini ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio konsol][twilio_console], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="f1b0e-152"><a id="create_app"></a>Bir Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1b0e-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="f1b0e-153">Merhaba Twilio JAR almak ve Java derleme yolu ve WAR dağıtım derlemenizi tooyour ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="f1b0e-154">Konumundaki [https://github.com/twilio/twilio-java][twilio_java], hello GitHub kaynakları indirmek ve kendi JAR oluşturabilir veya önceden oluşturulmuş bir JAR (veya ile bağımlılıklar olmadan) yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="f1b0e-155">JDK's olun **cacerts** anahtar deposu hello Equifax güvenli sertifika yetkilisi sertifikası MD5 parmak izi 67:CB:9 D ile içerir: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (Merhaba seri numarası olan 35:DE:F4:CF ve hello SHA1 parmak izi olan D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="f1b0e-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="f1b0e-156">Merhaba sertifika yetkilisi (CA) sertifikası hello için budur [https://api.twilio.com] [ twilio_api_service] Twilio API'leri kullandığınızda çağrılan hizmet.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="f1b0e-157">JDK's sağlama hakkında bilgi için **cacerts** anahtar deposu hello doğru CA sertifikası varsa, bkz: [sertifika toohello Java CA sertifika deposuna ekleme][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="f1b0e-158">Java için hello Twilio istemci kitaplığı kullanılarak ayrıntılı yönergeler şurada bulunabilir [nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir Java uygulamasında][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="f1b0e-159"><a id="configure_app"></a>Uygulamanızı tooUse Twilio kitaplıklarını yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="f1b0e-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="f1b0e-160">Kodunuzu içinde ekleyebileceğiniz **alma** deyimleri Twilio paketleri veya, sınıfları hello için Kaynak dosyalarınız hello üstündeki istediğiniz uygulamanızda toouse.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="f1b0e-161">Java kaynak dosyalar için:</span><span class="sxs-lookup"><span data-stu-id="f1b0e-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="f1b0e-162">Kaynak dosyaları Java sunucu sayfası (JSP):</span><span class="sxs-lookup"><span data-stu-id="f1b0e-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="f1b0e-163">Toouse, istediğiniz hangi Twilio paketleri ya da sınıfları bağlı olarak, **alma** deyimleri farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="f1b0e-164"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="f1b0e-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="f1b0e-165">Merhaba aşağıdaki giden toomake nasıl hello kullanarak Çağır gösterir **çağrısı** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="f1b0e-166">Bu kod ayrıca Twilio tarafından sağlanan site tooreturn hello Twilio biçimlendirme dili (TwiML) yanıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="f1b0e-167">Kendi değerlerinizi hello yerine **gelen** ve **için** telefon numaraları ve hello doğruladığınızdan emin olun **gelen** Twilio hesabı önceki toorunning hello kodunuz için telefon numarası.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="f1b0e-168">Toohello içinde geçirilen hello parametreler hakkında daha fazla bilgi için **Call.creator** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="f1b0e-169">Belirtildiği gibi bu kodu bir Twilio tarafından sağlanan site tooreturn hello TwiML yanıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="f1b0e-170">Bunun yerine, kendi site tooprovide hello TwiML yanıt kullanabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooProvide TwiML yanıtları Azure üzerinde bir Java uygulamasında](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="f1b0e-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="f1b0e-171"><a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin</span><span class="sxs-lookup"><span data-stu-id="f1b0e-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="f1b0e-172">Merhaba aşağıdakileri nasıl bir SMS iletisini kullanarak toosend hello gösterir **ileti** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="f1b0e-173">Merhaba **gelen** numarası **4155992671**, SMS iletileri toosend deneme hesapları için Twilio tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="f1b0e-174">Merhaba **için** Twilio hesap önceki toorunning hello kodu için sayı doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="f1b0e-175">Toohello içinde geçirilen hello parametreler hakkında daha fazla bilgi için **Message.creator** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="f1b0e-176"><a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar</span><span class="sxs-lookup"><span data-stu-id="f1b0e-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="f1b0e-177">Olduğunda, uygulamanızın başlatır örneğin hello aracılığıyla çağrı toohello Twilio API **CallCreator.create** yöntemi, Twilio gönderecek beklenen tooreturn olduğundan isteği tooa URL'nizi TwiML yanıt.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="f1b0e-178">Hello yukarıdaki örnekte hello Twilio tarafından sağlanan URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="f1b0e-179">(TwiML Web Hizmetleri tarafından kullanılmak üzere tasarlandığından, hello TwiML tarayıcınızda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="f1b0e-180">Örneğin, [http://twimlets.com/message] [ twimlet_message_url] toosee boş bir  **&lt;yanıt&gt;**  öğesi; başka bir örnek olarak, 'ıtıklatın.[http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee bir  **&lt;yanıt&gt;**  içeren öğe bir  **&lt;Say &gt;**  öğesi.)</span><span class="sxs-lookup"><span data-stu-id="f1b0e-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="f1b0e-181">Merhaba Twilio tarafından sağlanan URL güvenmek yerine, HTTP yanıtlarını döndürür kendi URL sitesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="f1b0e-182">HTTP yanıt veren herhangi bir dilde hello sitesi oluşturabilirsiniz; Bu konu, bir JSP sayfasında hello URL barındırma varsayar.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="f1b0e-183">JSP sayfa sonuçlarını bildiren bir TwiML yanıt aşağıdaki hello **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="f1b0e-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="f1b0e-184">Merhaba çağrıda.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="f1b0e-185">JSP sayfa bazı metinleri bildiren TwiML yanıt sonuçlarında aşağıdaki hello birkaç duraklatır var ve hello Twilio API sürümü ve hello Azure rol adı hakkında bilgi söyler.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="f1b0e-186">Merhaba **ApiVersion** parametredir Twilio sesli istekler (SMS istek değil) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="f1b0e-187">toosee hello kullanılabilir İstek parametreleri Twilio ses ve SMS istekleri için bkz: <https://www.twilio.com/docs/api/twiml/twilio_request> ve <https://www.twilio.com/docs/api/twiml/sms/twilio_request >sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="f1b0e-188">Merhaba **RoleName** ortam değişkeni kullanılabilir Azure dağıtımın bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="f1b0e-189">(Bunlar gelen çekilmesi şekilde tooadd özel ortam değişkenleri istiyorsanız **System.getenv**, hello ortam değişkenleri kısmına bakın [çeşitli rol yapılandırma ayarları] [misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="f1b0e-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="f1b0e-190">JSP sayfanızı tooprovide TwiML yanıtları ayarlayın olduktan sonra hello geçirilen URL hello gibi hello hello JSP sayfasının URL'sini kullanın **Call.creator** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="f1b0e-191">Örneğin, bir Web uygulaması varsa, dağıtılan MyTwiML tooan adlı Azure hizmeti, barındırılan ve hello JSP sayfasının hello adı mytwiml.jsp, hello URL çok geçirilebilir**Call.creator** hello aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f1b0e-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="f1b0e-192">Merhaba TwiML ile yanıt için başka bir seçenek olan **VoiceResponse** hello kullanılabilir sınıfı **com.twilio.twiml** paket.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="f1b0e-193">Java ile Azure Twilio kullanma hakkında ek bilgi için bkz: [nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir Java uygulamasında][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="f1b0e-194"><a id="AdditionalServices"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="f1b0e-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="f1b0e-195">Ayrıca, web tabanlı API'ler Twilio sunar buradaki toohello örnekler Azure uygulamanızı tooleverage ek Twilio işlevini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1b0e-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="f1b0e-196">Tüm Ayrıntılar için bkz: hello [Twilio API belgelerine][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="f1b0e-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="f1b0e-197"><a id="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f1b0e-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="f1b0e-198">Merhaba Twilio hizmet hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="f1b0e-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="f1b0e-199">[Twilio güvenlik yönergeleri][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="f1b0e-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="f1b0e-200">[Twilio nasıl ın yapılır ve örnek kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="f1b0e-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="f1b0e-201">[Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="f1b0e-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="f1b0e-202">[Github'da Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="f1b0e-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="f1b0e-203">[Konuşma tooTwilio desteği][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="f1b0e-203">[Talk tooTwilio Support][twilio_support]</span></span>

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
