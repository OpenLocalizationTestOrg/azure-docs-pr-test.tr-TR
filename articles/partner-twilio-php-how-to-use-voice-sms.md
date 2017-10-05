---
title: "Twilio ses ve SMS (PHP) için nasıl kullanılacağı | Microsoft Docs"
description: "Bir telefon araması yapın ve Azure üzerinde Twilio API hizmetiyle SMS mesajı göndermek öğrenin. PHP ile yazılan kod örnekleri."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="3d709-104">Ses ve PHP SMS özelliklerini için Twilio kullanma</span><span class="sxs-lookup"><span data-stu-id="3d709-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="3d709-105">Bu kılavuz, Azure üzerinde Twilio API hizmeti genel programlama görevleri gerçekleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3d709-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="3d709-106">Kapsamdaki senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="3d709-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="3d709-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3d709-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="3d709-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="3d709-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="3d709-109">Twilio iş iletişimleri, ses, VoIP ve uygulamalara Mesajlaşma geliştiricilerin etkinleştirme geleceği destekleyen.</span><span class="sxs-lookup"><span data-stu-id="3d709-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="3d709-110">Bunlar Twilio iletişim API platformu gösterme bulut tabanlı, genel bir ortamda gerekli tüm altyapı sanallaştırın.</span><span class="sxs-lookup"><span data-stu-id="3d709-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="3d709-111">Uygulamaları oluşturmak basit ve ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3d709-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="3d709-112">Sizinle ödeme-olarak esnekliğinin fiyatlandırma gidin ve bulut güvenilirlik ' yararlanır.</span><span class="sxs-lookup"><span data-stu-id="3d709-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="3d709-113">**Twilio sesli** yapmak ve telefon çağrılarını almak, uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d709-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="3d709-114">**Twilio SMS** metin ileti gönderme ve alma için uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="3d709-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="3d709-115">**Twilio istemci** VoIP çağrıları herhangi telefon, tablet ya da tarayıcı yapmanızı sağlar ve WebRTC destekler.</span><span class="sxs-lookup"><span data-stu-id="3d709-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="3d709-116"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="3d709-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="3d709-117">Azure müşterilerin alacak bir [özel teklif](http://www.twilio.com/azure): 10 ücretsiz Twilio Twilio hesabınızı yükseltirken kredisi.</span><span class="sxs-lookup"><span data-stu-id="3d709-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="3d709-118">Bu Twilio kredi varsa Twilio kullanımını ($10 alacak kadar 1.000 SMS iletileri göndermek ya da telefon numarası ve ileti veya çağrı hedef konumuna bağlı olarak en fazla 1000 gelen sesli dakika alırken eşdeğerdir) uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="3d709-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="3d709-119">Bu Twilio iade almak ve adresindeki kullanmaya başlama: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="3d709-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="3d709-120">Twilio Kullandıkça Ödeme tabanlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="3d709-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="3d709-121">Hiçbir Kurulum ücretleri vardır ve herhangi bir zamanda hesabınızı kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d709-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="3d709-122">Daha fazla bilgi bulabilirsiniz [Twilio fiyatlandırma][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="3d709-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="3d709-123"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="3d709-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="3d709-124">Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="3d709-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="3d709-125">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="3d709-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="3d709-126">Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.</span><span class="sxs-lookup"><span data-stu-id="3d709-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="3d709-127"><a id="Verbs"></a>Twilio fiiller</span><span class="sxs-lookup"><span data-stu-id="3d709-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="3d709-128">API Twilio yararlanır fiiller; Örneğin,  **&lt;Say&gt;**  fiili kullanımı bir çağrıda bir ileti teslim Twilio bildirir.</span><span class="sxs-lookup"><span data-stu-id="3d709-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="3d709-129">Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3d709-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="3d709-130">Diğer fiilleri ve aracılığıyla özellikleri hakkında bilgi edinin [Twilio biçimlendirme dili belgeleri](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="3d709-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="3d709-131">**&lt;Arama&gt;**: başka bir telefon çağıran bağlanır.</span><span class="sxs-lookup"><span data-stu-id="3d709-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="3d709-132">**&lt;Toplama&gt;**: telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="3d709-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="3d709-133">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="3d709-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="3d709-134">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="3d709-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="3d709-135">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="3d709-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="3d709-136">**&lt;Kayıt&gt;**: arayanın sesli kayıtlar ve kayıt içeren bir dosyanın URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d709-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="3d709-137">**&lt;Yeniden yönlendirme&gt;**: farklı bir URL'de TwiML çağrısı veya SMS denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="3d709-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="3d709-138">**&lt;Reddetme&gt;**: faturalama olmadan Twilio numaranızı için bir gelen çağrıyı reddeder</span><span class="sxs-lookup"><span data-stu-id="3d709-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="3d709-139">**&lt;Söyleyin&gt;**: dönüştürür metin bir çağrıda yapılan okuma.</span><span class="sxs-lookup"><span data-stu-id="3d709-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="3d709-140">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3d709-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="3d709-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="3d709-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="3d709-142">TwiML bir çağrı işlemek nasıl Twilio veya SMS bildiren Twilio fiilleri dayalı XML tabanlı yönergeleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="3d709-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="3d709-143">Örnek olarak, aşağıdaki TwiML metin dönüştürecektir **Hello World** konuşma için.</span><span class="sxs-lookup"><span data-stu-id="3d709-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="3d709-144">Uygulamanız Twilio API çağırdığında API parametrelerden biri TwiML yanıt veren URL'dir.</span><span class="sxs-lookup"><span data-stu-id="3d709-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="3d709-145">Geliştirme amaçlı uygulamalarınız tarafından kullanılan TwiML yanıt sağlamanız için sağlanan Twilio URL'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d709-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="3d709-146">TwiML yanıtları oluşturmak üzere kendi URL'leri de barındırabilir ve başka bir seçenek kullanmaktır **TwiMLResponse** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3d709-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="3d709-147">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="3d709-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="3d709-148">Twilio API'si hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3d709-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="3d709-149"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d709-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="3d709-150">Twilio hesap almak hazır olduğunuzda, oturum açın [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="3d709-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="3d709-151">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="3d709-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="3d709-152">Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3d709-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="3d709-153">Her ikisi de Twilio API çağrıları yapmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="3d709-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="3d709-154">Hesabınıza yetkisiz erişimi önlemek için kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="3d709-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="3d709-155">Hesap Kimliğini ve kimlik doğrulama belirteci adresindeki görüntülenebilir [Twilio hesap sayfası][twilio_account], etiketli alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="3d709-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="3d709-156"><a id="create_app"></a>PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d709-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="3d709-157">Twilio hizmeti kullanır ve Azure üzerinde çalışan bir PHP uygulaması Twilio hizmetini kullanan tüm diğer PHP uygulaması farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="3d709-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="3d709-158">Twilio Hizmetleri REST tabanlı ve PHP'nin çeşitli yollarla çağrılabilir olsa da, bu makalede Twilio Hizmetleri ile kullanmak üzere nasıl odaklanacaktır [GitHub PHP'nin Twilio kitaplığının][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="3d709-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="3d709-159">PHP için Twilio kitaplığını kullanma hakkında daha fazla bilgi için bkz: [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="3d709-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="3d709-160">Oluşturma ve azure'a Twilio/PHP uygulaması dağıtma hakkında ayrıntılı yönergeler şurada bulunabilir [Azure üzerinde bir PHP uygulamasının içinde kullanarak bir telefon araması Twilio nasıl][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="3d709-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="3d709-161"><a id="configure_app"></a>Uygulamanızı Twilio kitaplıkları kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3d709-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="3d709-162">Uygulamanızı Twilio kitaplığı PHP için iki yolla kullanacak şekilde yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3d709-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="3d709-163">Twilio kitaplığı PHP github'dan indirin ([https://github.com/twilio/twilio-php][twilio_php]) ve ekleme **Hizmetleri** uygulamanıza dizin.</span><span class="sxs-lookup"><span data-stu-id="3d709-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="3d709-164">-VEYA-</span><span class="sxs-lookup"><span data-stu-id="3d709-164">-OR-</span></span>
2. <span data-ttu-id="3d709-165">Twilio kitaplığı için PHP ARMUTLU paket olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3d709-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="3d709-166">Aşağıdaki komutlarla yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="3d709-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="3d709-167">PHP için Twilio kitaplığı yükledikten sonra daha sonra ekleyebilirsiniz bir **require_once** kitaplığı başvurmak için PHP dosyalarınızı üstündeki deyimi:</span><span class="sxs-lookup"><span data-stu-id="3d709-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="3d709-168">Daha fazla bilgi için bkz: [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="3d709-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="3d709-169"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="3d709-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="3d709-170">Aşağıdaki çağrıda giden yapılacağını gösterir **Services_Twilio** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3d709-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="3d709-171">Bu kod bir Twilio tarafından sağlanan site Twilio biçimlendirme dili (TwiML) yanıt döndürmek için de kullanır.</span><span class="sxs-lookup"><span data-stu-id="3d709-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="3d709-172">Kendi değerlerinizi yerleştirin **gelen** ve **için** telefon numaraları ve doğrulamanız olun **gelen** kod çalıştırılmadan önce Twilio hesabınız için telefon numarası.</span><span class="sxs-lookup"><span data-stu-id="3d709-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

<span data-ttu-id="3d709-173">Belirtildiği gibi bu kod bir Twilio tarafından sağlanan site TwiML yanıt döndürmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="3d709-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="3d709-174">Bunun yerine, kendi site TwiML yanıt sağlamak için de kullanabilirsiniz; Daha fazla bilgi için bkz: [nasıl TwiML yanıtlar sağlayan bilgisayarınızı kendi Web sitesinden](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="3d709-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="3d709-175">**Not**: SSL sertifikası doğrulama hatalarını gidermek için bkz: [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="3d709-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="3d709-176"><a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin</span><span class="sxs-lookup"><span data-stu-id="3d709-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="3d709-177">Aşağıdaki bir SMS kullanarak ileti gönder gösterilmektedir **Services_Twilio** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3d709-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="3d709-178">**Gelen** numarası SMS iletileri göndermek için tarafından deneme hesapları için Twilio sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3d709-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="3d709-179">**İçin** sayı doğrulandı, kod çalıştırılmadan önce Twilio hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="3d709-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="3d709-180"><a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar</span><span class="sxs-lookup"><span data-stu-id="3d709-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="3d709-181">Uygulamanızı Twilio API çağrısı başlattığında Twilio TwiML yanıt döndürmek için beklenen bir URL isteğinizi gönderin.</span><span class="sxs-lookup"><span data-stu-id="3d709-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="3d709-182">Yukarıdaki örnekte Twilio tarafından sağlanan URL'yi kullanır [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="3d709-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="3d709-183">(TwiML Twilio tarafından kullanılmak üzere tasarlandığından, BT tarayıcınızda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d709-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="3d709-184">For example, tıklatın [http://twimlets.com/message] [ twimlet_message_url] boş bir görmek için `<Response>` öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message?Message%5B0%5D=Hello%20World] [ twimlet_message_url_hello_world] görmek için bir `<Response>` içeren öğe bir `<Say>` öğesi.)</span><span class="sxs-lookup"><span data-stu-id="3d709-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="3d709-185">Twilio tarafından sağlanan URL üzerinde güvenmek yerine, HTTP yanıtlarını döndürür, kendi site oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d709-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="3d709-186">XML yanıtlarını döndürür herhangi bir dilde site oluşturabilirsiniz; Bu konu, PHP TwiML oluşturmak için kullanmaya başlayacağınız varsayar.</span><span class="sxs-lookup"><span data-stu-id="3d709-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="3d709-187">Aşağıdaki PHP sayfasını sonuçlarını bildiren bir TwiML yanıtına **Hello World** çağrısında.</span><span class="sxs-lookup"><span data-stu-id="3d709-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="3d709-188">Yukarıdaki örnekte görüldüğü gibi TwiML yanıt basitçe bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="3d709-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="3d709-189">PHP için Twilio kitaplığı TwiML oluşturacaktır sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="3d709-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="3d709-190">Aşağıdaki örnek, yukarıda gösterildiği gibi eşdeğer yanıt verir, ancak kullanır **Hizmetleri\_Twilio\_Twiml** sınıfı PHP Twilio Kitaplığı'nda:</span><span class="sxs-lookup"><span data-stu-id="3d709-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="3d709-191">TwiML hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="3d709-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="3d709-192">TwiML yanıt sağlamanız için ayarlamanız PHP sayfanızı oluşturduktan sonra içine URL geçti olarak PHP sayfasının URL'sini kullanmak `Services_Twilio->account->calls->create` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3d709-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="3d709-193">Adlı bir Web uygulaması varsa, örneğin, **MyTwiML** dağıtılan Azure barındırılan hizmeti ve PHP sayfanın adıdır **mytwiml.php**, URL için geçirilebilir **Services_Twilio -> Hesap çağrıları -> -> oluşturma** aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="3d709-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

<span data-ttu-id="3d709-194">PHP ile azure'da Twilio kullanma hakkında ek bilgi için bkz: [Azure üzerinde bir PHP uygulamasının içinde kullanarak bir telefon araması Twilio nasıl][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="3d709-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="3d709-195"><a id="AdditionalServices"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="3d709-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="3d709-196">Burada gösterilen örnekler yanı sıra, Azure uygulamanız ek Twilio işlevinden yararlanmak için kullanabileceğiniz web tabanlı API'ler Twilio sunar.</span><span class="sxs-lookup"><span data-stu-id="3d709-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="3d709-197">Ayrıntılar için bkz: [Twilio API belgelerine][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="3d709-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="3d709-198"><a id="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3d709-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="3d709-199">Twilio hizmetinin öğrendiğinize göre daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3d709-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="3d709-200">[Twilio güvenlik yönergeleri][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="3d709-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="3d709-201">[Twilio nasıl ın yapılır ve örnek kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="3d709-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="3d709-202">[Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="3d709-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="3d709-203">[Github'da Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="3d709-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="3d709-204">[Twilio desteklemek için konuşun][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="3d709-204">[Talk to Twilio Support][twilio_support]</span></span>

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
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
