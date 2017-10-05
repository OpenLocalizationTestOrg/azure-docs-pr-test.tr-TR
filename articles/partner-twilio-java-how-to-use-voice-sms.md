---
title: "Twilio ses ve SMS (Java) için nasıl kullanılacağı | Microsoft Docs"
description: "Bir telefon araması yapın ve Azure üzerinde Twilio API hizmetiyle SMS mesajı göndermek öğrenin. Java dilinde yazılan kod örnekleri."
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
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="e881d-104">Ses ve Java SMS yetenekler için Twilio kullanma</span><span class="sxs-lookup"><span data-stu-id="e881d-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="e881d-105">Bu kılavuz, Azure üzerinde Twilio API hizmeti genel programlama görevleri gerçekleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e881d-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="e881d-106">Kapsamdaki senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="e881d-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="e881d-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e881d-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="e881d-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="e881d-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="e881d-109">Twilio ses ve SMS uygulamaları oluşturmak için varolan web dilleri ve yetenekleri kullanmanıza olanak sağlayan bir telefon web hizmeti API'dir.</span><span class="sxs-lookup"><span data-stu-id="e881d-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="e881d-110">Twilio, (olmayan bir Azure özelliğidir ve Microsoft Ürün) bir bir üçüncü taraf hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e881d-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="e881d-111">**Twilio sesli** yapmak ve telefon çağrılarını almak, uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="e881d-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="e881d-112">**Twilio SMS** yapmak ve SMS iletileri almak, uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="e881d-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="e881d-113">**Twilio istemci** mobil bağlantıları dahil olmak üzere var olan Internet bağlantıları kullanarak sesli iletişimi etkinleştirmek, uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="e881d-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="e881d-114"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="e881d-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="e881d-115">Twilio fiyatlandırma hakkında daha fazla bilgi şu adreste [Twilio fiyatlandırma][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="e881d-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="e881d-116">Azure müşterilerine alma bir [özel teklif][special_offer]: boş bir kredi 1000 metinlerinin veya 1000 dakika sayısı.</span><span class="sxs-lookup"><span data-stu-id="e881d-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="e881d-117">Bu teklif için kaydolun veya daha fazla bilgi edinmek için lütfen ziyaret [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="e881d-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="e881d-118"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="e881d-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="e881d-119">Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="e881d-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="e881d-120">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="e881d-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="e881d-121">Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.</span><span class="sxs-lookup"><span data-stu-id="e881d-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="e881d-122"><a id="Verbs"></a>Twilio fiiller</span><span class="sxs-lookup"><span data-stu-id="e881d-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="e881d-123">API Twilio yararlanır fiiller; Örneğin,  **&lt;Say&gt;**  fiili kullanımı bir çağrıda bir ileti teslim Twilio bildirir.</span><span class="sxs-lookup"><span data-stu-id="e881d-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="e881d-124">Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e881d-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="e881d-125">**&lt;Arama&gt;**: başka bir telefon çağıran bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e881d-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="e881d-126">**&lt;Toplama&gt;**: telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="e881d-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="e881d-127">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="e881d-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="e881d-128">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="e881d-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="e881d-129">**&lt;Sıra&gt;**: ekleme arayanlar sırasına.</span><span class="sxs-lookup"><span data-stu-id="e881d-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="e881d-130">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="e881d-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="e881d-131">**&lt;Kayıt&gt;**: arayanın sesli kayıtlar ve kayıt içeren bir dosyanın URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="e881d-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="e881d-132">**&lt;Yeniden yönlendirme&gt;**: farklı bir URL'de TwiML çağrısı veya SMS denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="e881d-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="e881d-133">**&lt;Reddetme&gt;**: faturalama olmadan Twilio numaranızı için bir gelen çağrıyı reddeder.</span><span class="sxs-lookup"><span data-stu-id="e881d-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="e881d-134">**&lt;Söyleyin&gt;**: dönüştürür metin bir çağrıda yapılan okuma.</span><span class="sxs-lookup"><span data-stu-id="e881d-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="e881d-135">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="e881d-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="e881d-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="e881d-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="e881d-137">TwiML bir çağrı işlemek nasıl Twilio veya SMS bildiren Twilio fiilleri dayalı XML tabanlı yönergeleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="e881d-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="e881d-138">Örnek olarak, aşağıdaki TwiML metin dönüştürecektir **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="e881d-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="e881d-139">Konuşma.</span><span class="sxs-lookup"><span data-stu-id="e881d-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="e881d-140">Uygulamanız Twilio API çağırdığında API parametrelerden biri TwiML yanıt veren URL'dir.</span><span class="sxs-lookup"><span data-stu-id="e881d-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="e881d-141">Geliştirme amaçlı uygulamalarınız tarafından kullanılan TwiML yanıt sağlamanız için sağlanan Twilio URL'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e881d-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="e881d-142">TwiML yanıtları oluşturmak üzere kendi URL'leri de barındırabilir ve başka bir seçenek kullanmaktır **TwiMLResponse** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="e881d-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="e881d-143">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="e881d-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="e881d-144">Twilio API'si hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="e881d-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="e881d-145"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e881d-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="e881d-146">Twilio hesap almak hazır olduğunuzda, oturum açın [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="e881d-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="e881d-147">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="e881d-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="e881d-148">Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e881d-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="e881d-149">Her ikisi de Twilio API çağrıları yapmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="e881d-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="e881d-150">Hesabınıza yetkisiz erişimi önlemek için kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="e881d-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="e881d-151">Hesap Kimliğini ve kimlik doğrulama belirteci adresindeki görüntülenebilir [Twilio konsol][twilio_console], etiketli alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="e881d-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="e881d-152"><a id="create_app"></a>Bir Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e881d-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="e881d-153">Twilio JAR edinin ve Java derleme yolu ve WAR dağıtım derleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e881d-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="e881d-154">Konumundaki [https://github.com/twilio/twilio-java][twilio_java], GitHub kaynakları indirmek ve kendi JAR oluşturabilir veya önceden oluşturulmuş bir JAR (veya ile bağımlılıklar olmadan) yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e881d-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="e881d-155">JDK's olun **cacerts** anahtar deposu MD5 parmak izi 67:CB:9 D Equifax güvenli sertifika yetkilisi sertifikayla içerir: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (seri numarasını 35:DE:F4:CF ve SHA1 parmak izi D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="e881d-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="e881d-156">Sertifika yetkilisi (CA) sertifikası budur [https://api.twilio.com] [ twilio_api_service] Twilio API'leri kullandığınızda çağrılan hizmet.</span><span class="sxs-lookup"><span data-stu-id="e881d-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="e881d-157">JDK's sağlama hakkında bilgi için **cacerts** anahtar deposu doğru CA sertifikası varsa, bkz: [Java CA sertifika deposuna sertifika ekleme][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="e881d-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="e881d-158">Java için Twilio istemci kitaplığı kullanılarak ayrıntılı yönergeler şurada bulunabilir [Azure üzerinde bir Java uygulamasında kullanarak bir telefon araması Twilio nasıl][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="e881d-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="e881d-159"><a id="configure_app"></a>Uygulamanızı Twilio kitaplıkları kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e881d-159"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="e881d-160">Kodunuzu içinde ekleyebileceğiniz **alma** deyimleri Twilio paketleri veya uygulamanızda kullanmak istediğiniz sınıfları için Kaynak dosyalarınız üstündeki.</span><span class="sxs-lookup"><span data-stu-id="e881d-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="e881d-161">Java kaynak dosyalar için:</span><span class="sxs-lookup"><span data-stu-id="e881d-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="e881d-162">Kaynak dosyaları Java sunucu sayfası (JSP):</span><span class="sxs-lookup"><span data-stu-id="e881d-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="e881d-163">Hangi Twilio paketleri veya sınıfları bağlı olarak, kullanmak istediğiniz, **alma** deyimleri farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e881d-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <span data-ttu-id="e881d-164"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="e881d-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="e881d-165">Aşağıdaki çağrıda giden yapılacağını gösterir **çağrısı** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="e881d-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="e881d-166">Bu kod bir Twilio tarafından sağlanan site Twilio biçimlendirme dili (TwiML) yanıt döndürmek için de kullanır.</span><span class="sxs-lookup"><span data-stu-id="e881d-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="e881d-167">Kendi değerlerinizi yerleştirin **gelen** ve **için** telefon numaraları ve doğrulamanız olun **gelen** kod çalıştırılmadan önce Twilio hesabınız için telefon numarası.</span><span class="sxs-lookup"><span data-stu-id="e881d-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="e881d-168">İçin geçirilen parametreler hakkında daha fazla bilgi için **Call.creator** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="e881d-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="e881d-169">Belirtildiği gibi bu kod bir Twilio tarafından sağlanan site TwiML yanıt döndürmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="e881d-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="e881d-170">Bunun yerine, kendi site TwiML yanıt sağlamak için de kullanabilirsiniz; Daha fazla bilgi için bkz: [TwiML yanıtlarında sağlayan Azure üzerinde bir Java uygulamasının nasıl](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="e881d-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="e881d-171"><a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin</span><span class="sxs-lookup"><span data-stu-id="e881d-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="e881d-172">Aşağıdaki bir SMS kullanarak ileti gönder gösterilmektedir **ileti** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="e881d-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="e881d-173">**Gelen** numarası **4155992671**, SMS iletileri göndermek için tarafından deneme hesapları için Twilio sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e881d-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="e881d-174">**İçin** sayı doğrulandı, kod çalıştırılmadan önce Twilio hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="e881d-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="e881d-175">İçin geçirilen parametreler hakkında daha fazla bilgi için **Message.creator** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="e881d-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="e881d-176"><a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar</span><span class="sxs-lookup"><span data-stu-id="e881d-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="e881d-177">Olduğunda, uygulamanızın başlatır Twilio API çağrısı örneğin aracılığıyla **CallCreator.create** yöntemi, Twilio gönderecek isteğiniz TwiML yanıt döndürmek için beklenen bir URL.</span><span class="sxs-lookup"><span data-stu-id="e881d-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="e881d-178">Yukarıdaki örnekte Twilio tarafından sağlanan URL'yi kullanır [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="e881d-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="e881d-179">(TwiML Web Hizmetleri tarafından kullanılmak üzere tasarlandığından, TwiML tarayıcınızda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e881d-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="e881d-180">For example, tıklatın [http://twimlets.com/message] [ twimlet_message_url] boş bir görmek için  **&lt;yanıt&gt;**  öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] görmek için bir  **&lt;yanıt&gt;**  içeren öğe bir  **&lt;Say&gt;**  öğesi.)</span><span class="sxs-lookup"><span data-stu-id="e881d-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="e881d-181">Twilio tarafından sağlanan URL üzerinde güvenmek yerine, HTTP yanıtlarını döndürür kendi URL sitesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e881d-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="e881d-182">HTTP yanıt veren herhangi bir dilde site oluşturabilirsiniz; Bu konu, bir JSP sayfa URL'SİNDE barındırma varsayar.</span><span class="sxs-lookup"><span data-stu-id="e881d-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="e881d-183">Aşağıdaki JSP sayfasını sonuçlarını bildiren bir TwiML yanıtına **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="e881d-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="e881d-184">arama üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e881d-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="e881d-185">Aşağıdaki JSP sayfası, bazı metinleri diyor, birkaç duraklatır olan ve Twilio API sürümü ve Azure rol adı hakkında bilgi belirten bir TwiML yanıt sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="e881d-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="e881d-186">**ApiVersion** parametredir Twilio sesli istekler (SMS istek değil) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e881d-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="e881d-187">Twilio ses ve SMS istekleri kullanılabilir istek parametrelerini görmek için bkz: <https://www.twilio.com/docs/api/twiml/twilio_request> ve <https://www.twilio.com/docs/api/twiml/sms/twilio_request>sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="e881d-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="e881d-188">**RoleName** ortam değişkeni kullanılabilir Azure dağıtımın bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="e881d-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="e881d-189">(Bunlar gelen çekilmesi şekilde özel ortam değişkenleri eklemek istiyorsanız **System.getenv**, ortam değişkenleri bölümüne adresindeki bakın [çeşitli rol yapılandırma ayarları][misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="e881d-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="e881d-190">TwiML yanıt sağlamanız için ayarlamanız JSP sayfanızı oluşturduktan sonra içine URL geçti olarak JSP sayfasının URL'sini kullanmak **Call.creator** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e881d-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="e881d-191">Örneğin, adlandırılan bir Web uygulaması varsa bir Azure dağıtılan MyTwiML barındırılan hizmeti ve mytwiml.jsp JSP sayfanın adıdır, URL için geçirilebilir **Call.creator** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="e881d-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="e881d-192">Aracılığıyla TwiML ile yanıt için başka bir seçenek olan **VoiceResponse** kullanılabilir sınıfı **com.twilio.twiml** paket.</span><span class="sxs-lookup"><span data-stu-id="e881d-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="e881d-193">Java ile Azure Twilio kullanma hakkında ek bilgi için bkz: [Azure üzerinde bir Java uygulamasında kullanarak bir telefon araması Twilio nasıl][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="e881d-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="e881d-194"><a id="AdditionalServices"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="e881d-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="e881d-195">Burada gösterilen örnekler yanı sıra, Azure uygulamanız ek Twilio işlevinden yararlanmak için kullanabileceğiniz web tabanlı API'ler Twilio sunar.</span><span class="sxs-lookup"><span data-stu-id="e881d-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="e881d-196">Ayrıntılar için bkz: [Twilio API belgelerine][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="e881d-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="e881d-197"><a id="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e881d-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="e881d-198">Twilio hizmetinin öğrendiğinize göre daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e881d-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="e881d-199">[Twilio güvenlik yönergeleri][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="e881d-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="e881d-200">[Twilio nasıl ın yapılır ve örnek kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="e881d-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="e881d-201">[Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="e881d-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="e881d-202">[Github'da Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="e881d-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="e881d-203">[Twilio desteklemek için konuşun][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="e881d-203">[Talk to Twilio Support][twilio_support]</span></span>

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
