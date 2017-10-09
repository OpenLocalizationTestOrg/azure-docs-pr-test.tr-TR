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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="899b1-104">Nasıl toouse Twilio ses ve azure'dan SMS özellikleri</span><span class="sxs-lookup"><span data-stu-id="899b1-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="899b1-105">Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir.</span><span class="sxs-lookup"><span data-stu-id="899b1-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="899b1-106">Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="899b1-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="899b1-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="899b1-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="899b1-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="899b1-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="899b1-109">Twilio iş iletişimleri hello geleceği destekleyen, geliştiricilerin tooembed ses, VoIP, etkinleştirme ve uygulamalara Mesajlaşma.</span><span class="sxs-lookup"><span data-stu-id="899b1-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="899b1-110">Bunlar hello Twilio iletişimleri API platformu ile gösterme bulut tabanlı, genel bir ortamda gerekli tüm altyapı sanallaştırın.</span><span class="sxs-lookup"><span data-stu-id="899b1-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="899b1-111">Uygulamalardır basit toobuild ve ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="899b1-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="899b1-112">Kullandıkça Öde fiyatlandırma ile esnekliğinin ve bulut güvenilirlik ' yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="899b1-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="899b1-113">**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="899b1-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="899b1-114">**Twilio SMS** SMS iletileri almasına ve uygulamaları toosend sağlar.</span><span class="sxs-lookup"><span data-stu-id="899b1-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="899b1-115">**Twilio istemci** toomake VoIP çağrılarından herhangi telefon, tablet veya tarayıcı sağlar ve WebRTC destekler.</span><span class="sxs-lookup"><span data-stu-id="899b1-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="899b1-116"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="899b1-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="899b1-117">Azure müşterilerin alacak bir [özel teklif](http://www.twilio.com/azure): 10 ücretsiz Twilio Twilio hesabınızı yükseltirken kredisi.</span><span class="sxs-lookup"><span data-stu-id="899b1-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="899b1-118">Bu Twilio kredi uygulanan tooany Twilio kullanım (1. 000'kadar SMS iletileri veya too1000 yukarı alma gelen telefon numarasını ve ileti veya çağrı hedef hello konumuna bağlı olarak sesli dakika başına 10 kredi eşdeğer toosending) olabilir.</span><span class="sxs-lookup"><span data-stu-id="899b1-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="899b1-119">Bu Twilio iade almak ve adresindeki başlama [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="899b1-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="899b1-120">Twilio Kullandıkça Ödeme tabanlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="899b1-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="899b1-121">Hiçbir Kurulum ücretleri vardır ve herhangi bir zamanda hesabınızı kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="899b1-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="899b1-122">Daha fazla bilgi bulabilirsiniz [Twilio fiyatlandırma](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="899b1-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="899b1-123"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="899b1-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="899b1-124">Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="899b1-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="899b1-125">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="899b1-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="899b1-126">Merhaba Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.</span><span class="sxs-lookup"><span data-stu-id="899b1-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="899b1-127"><a id="Verbs"></a>Twilio fiiller</span><span class="sxs-lookup"><span data-stu-id="899b1-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="899b1-128">Merhaba API yapar Twilio kullanmak fiiller; Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.</span><span class="sxs-lookup"><span data-stu-id="899b1-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="899b1-129">Merhaba, Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="899b1-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="899b1-130">Bilgi hakkında hello diğer fiilleri ve yetenekleri aracılığıyla [Twilio biçimlendirme dili belgeleri](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="899b1-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="899b1-131">**&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.</span><span class="sxs-lookup"><span data-stu-id="899b1-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="899b1-132">**&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="899b1-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="899b1-133">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="899b1-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="899b1-134">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="899b1-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="899b1-135">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="899b1-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="899b1-136">**&lt;Kayıt&gt;**: hello arayanın sesli kaydeder ve bir hello kaydı içeren bir dosyanın URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="899b1-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="899b1-137">**&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="899b1-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="899b1-138">**&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın</span><span class="sxs-lookup"><span data-stu-id="899b1-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="899b1-139">**&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="899b1-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="899b1-140">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="899b1-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="899b1-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="899b1-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="899b1-142">TwiML XML tabanlı yönergeleri nasıl Twilio bildirmek hello Twilio fiiller üzerinde temel kümesidir tooprocess çağrısı veya SMS.</span><span class="sxs-lookup"><span data-stu-id="899b1-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="899b1-143">Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="899b1-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="899b1-144">Twilio API uygulaması çağrılarınızı Merhaba, hello API parametrelerden biri hello TwiML yanıt veren hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="899b1-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="899b1-145">Geliştirme amaçlı sağlanan Twilio URL'leri tooprovide hello TwiML yanıtlarını uygulamalarınız tarafından kullanılan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="899b1-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="899b1-146">Kendi URL'leri tooproduce hello TwiML yanıtları de barındırabilir ve başka bir seçeneği toouse hello **TwiMLResponse** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="899b1-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="899b1-147">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="899b1-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="899b1-148">Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="899b1-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="899b1-149"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="899b1-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="899b1-150">Hazır tooget Twilio hesabı olduğunuzda, oturum açın [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="899b1-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="899b1-151">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="899b1-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="899b1-152">Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="899b1-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="899b1-153">Her ikisi de gerekli toomake Twilio API çağrıları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="899b1-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="899b1-154">tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="899b1-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="899b1-155">Hesap Kimliğini ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio hesap sayfası][twilio_account], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="899b1-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="899b1-156"><a id="create_app"></a>Azure uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="899b1-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="899b1-157">Etkin Twilio uygulamasını barındıran Azure uygulaması herhangi diğer Azure uygulamasından farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="899b1-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="899b1-158">Merhaba Twilio .NET kitaplığı ekleyip hello rol toouse hello Twilio .NET kitaplıklarına yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="899b1-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="899b1-159">İlk Azure projesi oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio ile bir Azure projesi oluşturma][vs_project].</span><span class="sxs-lookup"><span data-stu-id="899b1-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="899b1-160"><a id="configure_app"></a>Uygulamanızı toouse Twilio kitaplıklarını yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="899b1-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="899b1-161">Twilio toogenerate TwiML yanıtlar Twilio tooprovide basit ve kolay şekilde toointeract hello Twilio REST API ve Twilio istemci ile çeşitli yönlerini sarmalamak .NET Yardımcısı kitaplıkları kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="899b1-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="899b1-162">Twilio .NET geliştiricileri için beş kitaplıkları sağlar:</span><span class="sxs-lookup"><span data-stu-id="899b1-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="899b1-163">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="899b1-163">Library</span></span>|<span data-ttu-id="899b1-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="899b1-164">Description</span></span>
---|---
<span data-ttu-id="899b1-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="899b1-165">Twilio.API</span></span>|<span data-ttu-id="899b1-166">Merhaba Twilio REST API kolay .NET Kitaplığı'nda sarmalar hello çekirdek Twilio kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="899b1-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="899b1-167">Bu kitaplık, .NET, Silverlight ve Windows Phone 7 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="899b1-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="899b1-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="899b1-168">Twilio.TwiML</span></span>|<span data-ttu-id="899b1-169">Bir .NET kolay şekilde toogenerate TwiML biçimlendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="899b1-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="899b1-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="899b1-170">Twilio.MVC</span></span>|<span data-ttu-id="899b1-171">ASP.NET MVC kullanan geliştiriciler için bu kitaplığı TwilioController, TwiML ActionResult ve istek doğrulama özniteliği içerir.</span><span class="sxs-lookup"><span data-stu-id="899b1-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="899b1-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="899b1-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="899b1-173">Microsoft'un ücretsiz WebMatrix geliştirme aracını kullanarak geliştiriciler için bu kitaplık çeşitli Twilio eylemler için Razor sözdizimi Yardımcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="899b1-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="899b1-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="899b1-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="899b1-175">Merhaba yetenek belirteç Oluşturucu hello Twilio istemci JavaScript SDK'sı ile kullanılmak üzere içerir.</span><span class="sxs-lookup"><span data-stu-id="899b1-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="899b1-176">Tüm kitaplıkları .NET 3.5, Silverlight 4 veya Windows Phone 7 veya üzeri gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="899b1-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="899b1-177">Bu kılavuzda sağlanan hello örnekleri hello Twilio.API kitaplığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="899b1-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="899b1-178">Merhaba kitaplıkları olabilir [hello NuGet Paket Yöneticisi uzantısı kullanılarak yüklenen](http://www.twilio.com/docs/csharp/install) too2015 yukarı Visual Studio 2010 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="899b1-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="899b1-179">Merhaba kaynak kodu barındırılan [GitHub][twilio_github_repo], hello kitaplıklarını kullanma için kapsamlı belgeler içeren bir Wiki içerir.</span><span class="sxs-lookup"><span data-stu-id="899b1-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="899b1-180">Varsayılan olarak, Microsoft Visual Studio 2010 NuGet 1.2 sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="899b1-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="899b1-181">Merhaba Twilio kitaplıkları yükleme sürüm 1.6 NuGet veya üstü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="899b1-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="899b1-182">Yükleme veya NuGet güncelleştirme hakkında daha fazla bilgi için bkz: [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="899b1-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="899b1-183">tooinstall hello en son sürümünü NuGet, ilk hello Visual Studio Uzantı Yöneticisi'ni kullanarak hello yüklü sürümünü kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="899b1-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="899b1-184">toodo bu nedenle, Visual Studio Yönetici olarak çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="899b1-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="899b1-185">Aksi takdirde hello Kaldır düğmesi devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="899b1-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="899b1-186"><a id="use_nuget"></a>tooadd hello Twilio kitaplıkları tooyour Visual Studio projesi:</span><span class="sxs-lookup"><span data-stu-id="899b1-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="899b1-187">Çözümünüzü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="899b1-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="899b1-188">Sağ **başvurular**.</span><span class="sxs-lookup"><span data-stu-id="899b1-188">Right-click **References**.</span></span>
3. <span data-ttu-id="899b1-189">Tıklatın **NuGet paketlerini Yönet...**</span><span class="sxs-lookup"><span data-stu-id="899b1-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="899b1-190">Tıklatın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="899b1-190">Click **Online**.</span></span>
5. <span data-ttu-id="899b1-191">Merhaba arama çevrimiçi kutusuna *twilio*.</span><span class="sxs-lookup"><span data-stu-id="899b1-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="899b1-192">Tıklatın **yükleme** hello Twilio paketinizdeki.</span><span class="sxs-lookup"><span data-stu-id="899b1-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="899b1-193"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="899b1-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="899b1-194">Merhaba aşağıdaki giden toomake nasıl hello kullanarak Çağır gösterir **CallResource** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="899b1-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="899b1-195">Bu kod ayrıca Twilio tarafından sağlanan site tooreturn hello Twilio biçimlendirme dili (TwiML) yanıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="899b1-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="899b1-196">Kendi değerlerinizi hello yerine **için** ve **gelen** telefon numaraları ve hello doğrulayın olun **gelen** telefon numarası Twilio hesabınızın hello kod çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="899b1-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

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

<span data-ttu-id="899b1-197">Toohello içinde geçirilen hello parametreler hakkında daha fazla bilgi için **CallResource.Create** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="899b1-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="899b1-198">Belirtildiği gibi bu kodu bir Twilio tarafından sağlanan site tooreturn hello TwiML yanıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="899b1-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="899b1-199">Bunun yerine, kendi site tooprovide hello TwiML yanıt kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="899b1-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="899b1-200">Daha fazla bilgi için bkz: [nasıl yapılır: sağlamak TwiML yanıtları kendi Web sitesinden](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="899b1-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="899b1-201"><a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin</span><span class="sxs-lookup"><span data-stu-id="899b1-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="899b1-202">Merhaba aşağıdaki ekran görüntüsü bir SMS iletisini kullanarak toosend nasıl hello gösterir **MessageResource** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="899b1-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="899b1-203">Merhaba **gelen** SMS iletileri toosend deneme hesapları için numarası Twilio tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="899b1-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="899b1-204">Merhaba **için** numarası gerekir doğrulandı Twilio hesabınız için hello kodu çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="899b1-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

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

## <span data-ttu-id="899b1-205"><a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar</span><span class="sxs-lookup"><span data-stu-id="899b1-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="899b1-206">Ne zaman uygulamanızı başlatır çağrısı toohello Twilio API - Örneğin, hello **CallResource.Create** yöntemi - Twilio beklenen tooreturn, istek tooan URL bir TwiML yanıtını gönderir.</span><span class="sxs-lookup"><span data-stu-id="899b1-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="899b1-207">Merhaba örnekte [nasıl yapılır: giden bir çağrı yapmak](#howto_make_call) kullanır hello Twilio tarafından sağlanan URL [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello yanıt.</span><span class="sxs-lookup"><span data-stu-id="899b1-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="899b1-208">TwiML web hizmetleri tarafından kullanılmak üzere tasarlandığından, hello TwiML tarayıcınızda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="899b1-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="899b1-209">Örneğin, [http://twimlets.com/message] [ twimlet_message_url] toosee boş bir &lt;yanıt&gt; öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message ? İleti % 5B0 %5 D Hello % 20World =](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee bir &lt;yanıt&gt; içeren öğe bir &lt;Say&gt; öğesi.</span><span class="sxs-lookup"><span data-stu-id="899b1-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="899b1-210">Merhaba Twilio tarafından sağlanan URL güvenmek yerine, HTTP yanıtlarını döndürür kendi URL sitesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="899b1-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="899b1-211">HTTP yanıt veren herhangi bir dilde hello sitesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="899b1-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="899b1-212">Bu konu, bir ASP.NET genel işleyici hello URL'den barındırma varsayar.</span><span class="sxs-lookup"><span data-stu-id="899b1-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="899b1-213">ASP.NET işleyicisi aşağıdaki hello işler bildiren TwiML yanıt **Hello World** hello çağrıda.</span><span class="sxs-lookup"><span data-stu-id="899b1-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

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
    
<span data-ttu-id="899b1-214">Yukarıdaki hello örnekte görebildiğiniz gibi hello TwiML yanıt basitçe bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="899b1-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="899b1-215">Merhaba Twilio.TwiML kitaplığı TwiML oluşturacaktır sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="899b1-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="899b1-216">Merhaba aşağıdaki örnek yukarıda gösterildiği gibi hello eşdeğer yanıt oluşturur, ancak kullanır hello **VoiceResponse** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="899b1-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

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

<span data-ttu-id="899b1-217">TwiML hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="899b1-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="899b1-218">Bir şekilde tooprovide TwiML yanıtları ayarladıktan sonra bu URL toohello geçirebilirsiniz **CallResource.Create** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="899b1-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="899b1-219">Örneğin, dağıtılan MyTwiML tooan Azure bulut hizmeti adlı bir web uygulaması varsa ve hello ASP.NET işleyicinizi adıdır mytwiml.ashx hello URL çok geçirilebilir**CallResource.Create** hello kod aşağıdaki gösterildiği gibi Örnek:</span><span class="sxs-lookup"><span data-stu-id="899b1-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="899b1-220">ASP.NET ile azure'da Twilio kullanma hakkında ek bilgi için bkz: [nasıl toomake bir telefon görüşmesi Twilio Azure üzerinde bir web rolü kullanılarak][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="899b1-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

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
