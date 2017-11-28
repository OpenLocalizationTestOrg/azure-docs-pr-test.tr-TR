---
title: aaaHow tooUse Twilio ses ve SMS (PHP) | Microsoft Docs
description: "Nasıl azure'da hello Twilio API hizmetiyle toomake telefon ve SMS iletisi öğrenin. PHP ile yazılan kod örnekleri."
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
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="d58cc-104">Nasıl tooUse Twilio ses ve PHP SMS özellikleri</span><span class="sxs-lookup"><span data-stu-id="d58cc-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="d58cc-105">Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="d58cc-106">Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="d58cc-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d58cc-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="d58cc-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="d58cc-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="d58cc-109">Twilio iş iletişimleri hello geleceği destekleyen, geliştiricilerin tooembed ses, VoIP, etkinleştirme ve uygulamalara Mesajlaşma.</span><span class="sxs-lookup"><span data-stu-id="d58cc-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="d58cc-110">Bunlar hello Twilio iletişimleri API platformu ile gösterme bulut tabanlı, genel bir ortamda gerekli tüm altyapı sanallaştırın.</span><span class="sxs-lookup"><span data-stu-id="d58cc-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="d58cc-111">Uygulamalardır basit toobuild ve ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="d58cc-112">Sizinle ödeme-olarak esnekliğinin fiyatlandırma gidin ve bulut güvenilirlik ' yararlanır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="d58cc-113">**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="d58cc-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="d58cc-114">**Twilio SMS** metin iletileri almasına ve uygulama toosend sağlar.</span><span class="sxs-lookup"><span data-stu-id="d58cc-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="d58cc-115">**Twilio istemci** toomake VoIP çağrılarından herhangi telefon, tablet veya tarayıcı sağlar ve WebRTC destekler.</span><span class="sxs-lookup"><span data-stu-id="d58cc-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="d58cc-116"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="d58cc-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="d58cc-117">Azure müşterilerin alacak bir [özel teklif](http://www.twilio.com/azure): 10 ücretsiz Twilio Twilio hesabınızı yükseltirken kredisi.</span><span class="sxs-lookup"><span data-stu-id="d58cc-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="d58cc-118">Bu Twilio kredi uygulanan tooany Twilio kullanım (1. 000'kadar SMS iletileri veya too1000 yukarı alma gelen telefon numarasını ve ileti veya çağrı hedef hello konumuna bağlı olarak sesli dakika başına 10 kredi eşdeğer toosending) olabilir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="d58cc-119">Bu Twilio iade almak ve adresindeki kullanmaya başlama: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="d58cc-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="d58cc-120">Twilio Kullandıkça Ödeme tabanlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="d58cc-121">Hiçbir Kurulum ücretleri vardır ve herhangi bir zamanda hesabınızı kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d58cc-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="d58cc-122">Daha fazla bilgi bulabilirsiniz [Twilio fiyatlandırma][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="d58cc-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="d58cc-123"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="d58cc-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="d58cc-124">Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="d58cc-125">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="d58cc-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="d58cc-126">Merhaba Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="d58cc-127"><a id="Verbs"></a>Twilio fiiller</span><span class="sxs-lookup"><span data-stu-id="d58cc-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="d58cc-128">Merhaba API yapar Twilio kullanmak fiiller; Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="d58cc-129">Merhaba, Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="d58cc-130">Bilgi hakkında hello diğer fiilleri ve yetenekleri aracılığıyla [Twilio biçimlendirme dili belgeleri](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="d58cc-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="d58cc-131">**&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="d58cc-132">**&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="d58cc-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="d58cc-133">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="d58cc-134">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="d58cc-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="d58cc-135">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="d58cc-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="d58cc-136">**&lt;Kayıt&gt;**: hello arayanın sesli kayıtlar ve hello kaydı içeren bir dosyanın URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="d58cc-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="d58cc-137">**&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="d58cc-138">**&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın</span><span class="sxs-lookup"><span data-stu-id="d58cc-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="d58cc-139">**&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="d58cc-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="d58cc-140">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="d58cc-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="d58cc-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="d58cc-142">TwiML XML tabanlı yönergeleri nasıl Twilio bildirmek hello Twilio fiiller üzerinde temel kümesidir tooprocess çağrısı veya SMS.</span><span class="sxs-lookup"><span data-stu-id="d58cc-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="d58cc-143">Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="d58cc-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="d58cc-144">Twilio API uygulaması çağrılarınızı Merhaba, hello API parametrelerden biri hello TwiML yanıt veren hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="d58cc-145">Geliştirme amaçlı sağlanan Twilio URL'leri tooprovide hello TwiML yanıtlarını uygulamalarınız tarafından kullanılan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d58cc-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="d58cc-146">Kendi URL'leri tooproduce hello TwiML yanıtları de barındırabilir ve başka bir seçeneği toouse hello **TwiMLResponse** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d58cc-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="d58cc-147">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="d58cc-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="d58cc-148">Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="d58cc-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="d58cc-149"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d58cc-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="d58cc-150">Hazır tooget Twilio hesabı olduğunuzda, oturum açın [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="d58cc-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="d58cc-151">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="d58cc-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="d58cc-152">Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d58cc-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="d58cc-153">Her ikisi de gerekli toomake Twilio API çağrıları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="d58cc-154">tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="d58cc-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="d58cc-155">Hesap Kimliğini ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio hesap sayfası][twilio_account], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="d58cc-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="d58cc-156"><a id="create_app"></a>PHP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d58cc-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="d58cc-157">Merhaba Twilio hizmeti kullanır ve Azure üzerinde çalışan bir PHP uygulamasının hello Twilio hizmetini kullanan tüm diğer PHP uygulaması farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="d58cc-158">Twilio Hizmetleri REST tabanlı ve PHP'nin çeşitli yollarla çağrılabilir olsa da, bu makalede toouse Twilio ile hizmetleri nasıl üzerine odaklanacaktır [GitHub PHP'nin Twilio kitaplığının][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="d58cc-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="d58cc-159">PHP için hello Twilio kitaplığını kullanma hakkında daha fazla bilgi için bkz: [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="d58cc-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="d58cc-160">Oluşturma ve Twilio/PHP uygulama tooAzure dağıtma hakkında ayrıntılı yönergeler şurada bulunabilir [nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir PHP uygulamasının içinde][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="d58cc-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="d58cc-161"><a id="configure_app"></a>Uygulamanızı tooUse Twilio kitaplıklarını yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="d58cc-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="d58cc-162">PHP için uygulama toouse hello Twilio kitaplığınızın iki yolla yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d58cc-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="d58cc-163">Merhaba Twilio kitaplığı PHP github'dan indirin ([https://github.com/twilio/twilio-php][twilio_php]) ve hello ekleyin **Hizmetleri** directory tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="d58cc-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="d58cc-164">-VEYA-</span><span class="sxs-lookup"><span data-stu-id="d58cc-164">-OR-</span></span>
2. <span data-ttu-id="d58cc-165">Merhaba Twilio kitaplığı için PHP ARMUTLU paket olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d58cc-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="d58cc-166">Aşağıdaki komutları hello ile yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="d58cc-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="d58cc-167">PHP için hello Twilio kitaplığı yükledikten sonra daha sonra ekleyebilirsiniz bir **require_once** deyimi, PHP hello üstündeki dosyaları tooreference hello kitaplığı:</span><span class="sxs-lookup"><span data-stu-id="d58cc-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="d58cc-168">Daha fazla bilgi için bkz: [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="d58cc-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="d58cc-169"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="d58cc-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="d58cc-170">Merhaba aşağıdaki giden toomake nasıl hello kullanarak Çağır gösterir **Services_Twilio** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d58cc-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="d58cc-171">Bu kod ayrıca Twilio tarafından sağlanan site tooreturn hello Twilio biçimlendirme dili (TwiML) yanıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="d58cc-172">Kendi değerlerinizi hello yerine **gelen** ve **için** telefon numaraları ve hello doğruladığınızdan emin olun **gelen** Twilio hesabı önceki toorunning hello kodunuz için telefon numarası.</span><span class="sxs-lookup"><span data-stu-id="d58cc-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
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

<span data-ttu-id="d58cc-173">Belirtildiği gibi bu kodu bir Twilio tarafından sağlanan site tooreturn hello TwiML yanıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="d58cc-174">Bunun yerine, kendi site tooprovide hello TwiML yanıt kullanabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooProvide TwiML yanıtları bilgisayarınızı kendi Web sitesinden](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="d58cc-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="d58cc-175">**Not**: tootroubleshoot SSL sertifika doğrulama hataları, bkz: [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="d58cc-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="d58cc-176"><a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin</span><span class="sxs-lookup"><span data-stu-id="d58cc-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="d58cc-177">Merhaba aşağıdakileri nasıl bir SMS iletisini kullanarak toosend hello gösterir **Services_Twilio** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d58cc-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="d58cc-178">Merhaba **gelen** SMS iletileri toosend deneme hesapları için numarası Twilio tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="d58cc-179">Merhaba **için** Twilio hesap önceki toorunning hello kodu için sayı doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="d58cc-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="d58cc-180"><a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar</span><span class="sxs-lookup"><span data-stu-id="d58cc-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="d58cc-181">Uygulamanızı bir çağrı toohello Twilio API başlattığında Twilio olduğundan isteği tooa URL'nizi tooreturn TwiML yanıt beklenen gönderir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="d58cc-182">Hello yukarıdaki örnekte hello Twilio tarafından sağlanan URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="d58cc-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="d58cc-183">(TwiML Twilio tarafından kullanılmak üzere tasarlandığından, görüntüleyebileceğiniz tarayıcınızda hello.</span><span class="sxs-lookup"><span data-stu-id="d58cc-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="d58cc-184">Örneğin, [http://twimlets.com/message] [ twimlet_message_url] toosee boş bir `<Response>` öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message? İleti % 5B0 %5 D Hello % 20World =] [ twimlet_message_url_hello_world] toosee bir `<Response>` içeren öğe bir `<Say>` öğesi.)</span><span class="sxs-lookup"><span data-stu-id="d58cc-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="d58cc-185">Merhaba Twilio tarafından sağlanan URL güvenmek yerine, HTTP yanıtlarını döndürür, kendi site oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d58cc-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="d58cc-186">XML yanıtlarını döndürür herhangi bir dilde hello sitesi oluşturabilirsiniz; Bu konu, PHP toocreate hello TwiML kullanan varsaymaktadır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="d58cc-187">PHP sayfa sonuçlarını bildiren bir TwiML yanıt aşağıdaki hello **Hello World** hello çağrıda.</span><span class="sxs-lookup"><span data-stu-id="d58cc-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="d58cc-188">Yukarıdaki hello örnekte görebildiğiniz gibi hello TwiML yanıt basitçe bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="d58cc-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="d58cc-189">PHP için Hello Twilio kitaplığı TwiML oluşturacaktır sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="d58cc-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="d58cc-190">Aşağıdaki Hello örnek yukarıda gösterildiği gibi hello eşdeğer yanıt oluşturur, ancak kullanır hello **Hizmetleri\_Twilio\_Twiml** sınıfı PHP hello Twilio Kitaplığı'nda:</span><span class="sxs-lookup"><span data-stu-id="d58cc-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="d58cc-191">TwiML hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="d58cc-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="d58cc-192">Tooprovide TwiML yanıtları ayarlayın, PHP sayfanızı oluşturduktan sonra hello geçirilen URL hello gibi hello hello PHP sayfanın URL'sini kullanın `Services_Twilio->account->calls->create` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d58cc-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="d58cc-193">Adlı bir Web uygulaması varsa, örneğin, **MyTwiML** dağıtılan tooan Azure barındırılan hizmeti ve hello PHP sayfa hello adıdır **mytwiml.php**, URL çok geçirilebilir hello **Services_ Twilio -> Hesap çağrıları -> -> oluşturma** hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="d58cc-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
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

<span data-ttu-id="d58cc-194">PHP ile azure'da Twilio kullanma hakkında ek bilgi için bkz: [nasıl tooMake kullanarak bir telefon araması Twilio Azure üzerinde bir PHP uygulamasının içinde][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="d58cc-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="d58cc-195"><a id="AdditionalServices"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="d58cc-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="d58cc-196">Ayrıca, web tabanlı API'ler Twilio sunar buradaki toohello örnekler Azure uygulamanızı tooleverage ek Twilio işlevini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d58cc-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="d58cc-197">Tüm Ayrıntılar için bkz: hello [Twilio API belgelerine][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="d58cc-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="d58cc-198"><a id="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d58cc-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="d58cc-199">Merhaba Twilio hizmet hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="d58cc-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="d58cc-200">[Twilio güvenlik yönergeleri][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="d58cc-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="d58cc-201">[Twilio nasıl ın yapılır ve örnek kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="d58cc-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="d58cc-202">[Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="d58cc-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="d58cc-203">[Github'da Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="d58cc-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="d58cc-204">[Konuşma tooTwilio desteği][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="d58cc-204">[Talk tooTwilio Support][twilio_support]</span></span>

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
