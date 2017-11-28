---
title: "Twilio ses ve SMS (.NET) için nasıl kullanılacağı | Microsoft Docs"
description: "Bir telefon araması yapın ve Azure üzerinde Twilio API hizmetiyle SMS mesajı göndermek öğrenin. .NET ile yazılan kod örnekleri."
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
ms.openlocfilehash: 1442e3af26ae87e645cf207228ed1197b2afdd4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="af69c-104">Twilio ses ve Azure SMS özelliklerini kullanma</span><span class="sxs-lookup"><span data-stu-id="af69c-104">How to use Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="af69c-105">Bu kılavuz, Azure üzerinde Twilio API hizmeti genel programlama görevleri gerçekleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="af69c-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="af69c-106">Kapsamdaki senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="af69c-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="af69c-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="af69c-107">For more information on Twilio and using voice and SMS in your applications, see the [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="af69c-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="af69c-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="af69c-109">Twilio iş iletişimleri, ses, VoIP ve uygulamalara Mesajlaşma geliştiricilerin etkinleştirme geleceği destekleyen.</span><span class="sxs-lookup"><span data-stu-id="af69c-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="af69c-110">Bunlar Twilio iletişim API platformu gösterme bulut tabanlı, genel bir ortamda gerekli tüm altyapı sanallaştırın.</span><span class="sxs-lookup"><span data-stu-id="af69c-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="af69c-111">Uygulamaları oluşturmak basit ve ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="af69c-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="af69c-112">Kullandıkça Öde fiyatlandırma ile esnekliğinin ve bulut güvenilirlik ' yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af69c-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="af69c-113">**Twilio sesli** yapmak ve telefon çağrılarını almak, uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="af69c-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="af69c-114">**Twilio SMS** SMS iletileri göndermek ve almak için uygulamalarınızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="af69c-114">**Twilio SMS** enables your applications to send and receive SMS messages.</span></span> <span data-ttu-id="af69c-115">**Twilio istemci** VoIP çağrıları herhangi telefon, tablet ya da tarayıcı yapmanızı sağlar ve WebRTC destekler.</span><span class="sxs-lookup"><span data-stu-id="af69c-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="af69c-116"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="af69c-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="af69c-117">Azure müşterilerin alacak bir [özel teklif](http://www.twilio.com/azure): 10 ücretsiz Twilio Twilio hesabınızı yükseltirken kredisi.</span><span class="sxs-lookup"><span data-stu-id="af69c-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="af69c-118">Bu Twilio kredi varsa Twilio kullanımını ($10 alacak kadar 1.000 SMS iletileri göndermek ya da telefon numarası ve ileti veya çağrı hedef konumuna bağlı olarak en fazla 1000 gelen sesli dakika alırken eşdeğerdir) uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="af69c-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="af69c-119">Bu Twilio iade almak ve adresindeki başlama [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="af69c-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="af69c-120">Twilio Kullandıkça Ödeme tabanlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="af69c-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="af69c-121">Hiçbir Kurulum ücretleri vardır ve herhangi bir zamanda hesabınızı kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af69c-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="af69c-122">Daha fazla bilgi bulabilirsiniz [Twilio fiyatlandırma](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="af69c-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="af69c-123"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="af69c-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="af69c-124">Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="af69c-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="af69c-125">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="af69c-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="af69c-126">Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.</span><span class="sxs-lookup"><span data-stu-id="af69c-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="af69c-127"><a id="Verbs"></a>Twilio fiiller</span><span class="sxs-lookup"><span data-stu-id="af69c-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="af69c-128">API Twilio yararlanır fiiller; Örneğin,  **&lt;Say&gt;**  fiili kullanımı bir çağrıda bir ileti teslim Twilio bildirir.</span><span class="sxs-lookup"><span data-stu-id="af69c-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="af69c-129">Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="af69c-129">The following is a list of Twilio verbs.</span></span>  <span data-ttu-id="af69c-130">Diğer fiilleri ve aracılığıyla özellikleri hakkında bilgi edinin [Twilio biçimlendirme dili belgeleri](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="af69c-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="af69c-131">**&lt;Arama&gt;**: başka bir telefon çağıran bağlanır.</span><span class="sxs-lookup"><span data-stu-id="af69c-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="af69c-132">**&lt;Toplama&gt;**: telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="af69c-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="af69c-133">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="af69c-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="af69c-134">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="af69c-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="af69c-135">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="af69c-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="af69c-136">**&lt;Kayıt&gt;**: arayanın sesli kayıtlar ve kayıt içeren bir dosyayı bir URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="af69c-136">**&lt;Record&gt;**: Records the caller's voice and returns an URL of a file that contains the recording.</span></span>
* <span data-ttu-id="af69c-137">**&lt;Yeniden yönlendirme&gt;**: farklı bir URL'de TwiML çağrısı veya SMS denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="af69c-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="af69c-138">**&lt;Reddetme&gt;**: faturalama olmadan Twilio numaranızı için bir gelen çağrıyı reddeder</span><span class="sxs-lookup"><span data-stu-id="af69c-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="af69c-139">**&lt;Söyleyin&gt;**: dönüştürür metin bir çağrıda yapılan okuma.</span><span class="sxs-lookup"><span data-stu-id="af69c-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="af69c-140">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="af69c-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="af69c-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="af69c-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="af69c-142">TwiML bir çağrı işlemek nasıl Twilio veya SMS bildiren Twilio fiilleri dayalı XML tabanlı yönergeleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="af69c-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="af69c-143">Örnek olarak, aşağıdaki TwiML metin dönüştürecektir **Hello World** konuşma için.</span><span class="sxs-lookup"><span data-stu-id="af69c-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="af69c-144">Uygulamanız Twilio API çağırdığında API parametrelerden biri TwiML yanıt veren URL'dir.</span><span class="sxs-lookup"><span data-stu-id="af69c-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="af69c-145">Geliştirme amaçlı uygulamalarınız tarafından kullanılan TwiML yanıt sağlamanız için sağlanan Twilio URL'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af69c-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="af69c-146">TwiML yanıtları oluşturmak üzere kendi URL'leri de barındırabilir ve başka bir seçenek kullanmaktır **TwiMLResponse** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="af69c-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="af69c-147">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="af69c-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="af69c-148">Twilio API'si hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="af69c-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="af69c-149"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="af69c-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="af69c-150">Twilio hesap almak hazır olduğunuzda, oturum açın [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="af69c-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="af69c-151">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="af69c-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="af69c-152">Twilio hesabı için kaydolduğunuzda, hesap Kimliğini ve kimlik doğrulama belirtecini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="af69c-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="af69c-153">Her ikisi de Twilio API çağrıları yapmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="af69c-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="af69c-154">Hesabınıza yetkisiz erişimi önlemek için kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="af69c-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="af69c-155">Hesap Kimliğini ve kimlik doğrulama belirteci adresindeki görüntülenebilir [Twilio hesap sayfası][twilio_account], etiketli alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="af69c-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="af69c-156"><a id="create_app"></a>Azure uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="af69c-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="af69c-157">Etkin Twilio uygulamasını barındıran Azure uygulaması herhangi diğer Azure uygulamasından farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="af69c-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="af69c-158">Twilio .NET kitaplığı ekleyip Twilio .NET kitaplıklarına kullanmak için rol yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af69c-158">You add the Twilio .NET library and configure the role to use the Twilio .NET libraries.</span></span>
<span data-ttu-id="af69c-159">İlk Azure projesi oluşturma hakkında daha fazla bilgi için bkz: [Visual Studio ile bir Azure projesi oluşturma][vs_project].</span><span class="sxs-lookup"><span data-stu-id="af69c-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="af69c-160"><a id="configure_app"></a>Twilio kitaplıkları kullanmak için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="af69c-160"><a id="configure_app"></a>Configure Your Application to use Twilio Libraries</span></span>
<span data-ttu-id="af69c-161">Twilio Twilio TwiML yanıtları oluşturmak Twilio REST API ve Twilio istemci ile etkileşim kurmak için basit ve kolay yollar sağlamak için çeşitli yönlerini sarmalamak .NET Yardımcısı kitaplıkları kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="af69c-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio to provide simple and easy ways to interact with the Twilio REST API and Twilio Client to generate TwiML responses.</span></span>

<span data-ttu-id="af69c-162">Twilio .NET geliştiricileri için beş kitaplıkları sağlar:</span><span class="sxs-lookup"><span data-stu-id="af69c-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="af69c-163">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="af69c-163">Library</span></span>|<span data-ttu-id="af69c-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="af69c-164">Description</span></span>
---|---
<span data-ttu-id="af69c-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="af69c-165">Twilio.API</span></span>|<span data-ttu-id="af69c-166">Twilio REST API kolay .NET Kitaplığı'nda sarmalar çekirdek Twilio kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="af69c-166">The core Twilio library that wraps the Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="af69c-167">Bu kitaplık, .NET, Silverlight ve Windows Phone 7 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="af69c-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="af69c-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="af69c-168">Twilio.TwiML</span></span>|<span data-ttu-id="af69c-169">TwiML biçimlendirme oluşturmak için bir .NET kolay yolunu sunar.</span><span class="sxs-lookup"><span data-stu-id="af69c-169">Provides a .NET friendly way to generate TwiML markup.</span></span>
<span data-ttu-id="af69c-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="af69c-170">Twilio.MVC</span></span>|<span data-ttu-id="af69c-171">ASP.NET MVC kullanan geliştiriciler için bu kitaplığı TwilioController, TwiML ActionResult ve istek doğrulama özniteliği içerir.</span><span class="sxs-lookup"><span data-stu-id="af69c-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="af69c-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="af69c-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="af69c-173">Microsoft'un ücretsiz WebMatrix geliştirme aracını kullanarak geliştiriciler için bu kitaplık çeşitli Twilio eylemler için Razor sözdizimi Yardımcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="af69c-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="af69c-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="af69c-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="af69c-175">Twilio istemci JavaScript SDK'sı ile kullanılmak üzere yetenek belirteç Oluşturucu içerir.</span><span class="sxs-lookup"><span data-stu-id="af69c-175">Contains the Capability token generator for use with the Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="af69c-176">Tüm kitaplıkları .NET 3.5, Silverlight 4 veya Windows Phone 7 veya üzeri gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="af69c-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="af69c-177">Bu kılavuzda sağlanan örnekleri Twilio.API kitaplığını kullanın.</span><span class="sxs-lookup"><span data-stu-id="af69c-177">The samples provided in this guide use the Twilio.API library.</span></span>

<span data-ttu-id="af69c-178">Kitaplıkları olabilir [NuGet Paket Yöneticisi uzantısı kullanılarak yüklenen](http://www.twilio.com/docs/csharp/install) 2015 kadar Visual Studio 2010 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="af69c-178">The libraries can be [installed using the NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up to 2015.</span></span>  <span data-ttu-id="af69c-179">Kaynak kodu barındırılan [GitHub][twilio_github_repo], kitaplıklarını kullanma için kapsamlı belgeler içeren bir Wiki içerir.</span><span class="sxs-lookup"><span data-stu-id="af69c-179">The source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using the libraries.</span></span>

<span data-ttu-id="af69c-180">Varsayılan olarak, Microsoft Visual Studio 2010 NuGet 1.2 sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="af69c-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="af69c-181">Twilio kitaplıkları yükleme sürüm 1.6 NuGet veya üstü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="af69c-181">Installing the Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="af69c-182">Yükleme veya NuGet güncelleştirme hakkında daha fazla bilgi için bkz: [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="af69c-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="af69c-183">NuGet'ın en son sürümünü yüklemek için önce Visual Studio Uzantı Yöneticisi'ni kullanarak yüklenen sürümü kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="af69c-183">To install the latest version of NuGet, you must first uninstall the loaded version using the Visual Studio Extension Manager.</span></span> <span data-ttu-id="af69c-184">Bunu yapmak için Visual Studio'yu yönetici olarak çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="af69c-184">To do so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="af69c-185">Aksi takdirde kaldırma düğmesi devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="af69c-185">Otherwise, the Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="af69c-186"><a id="use_nuget"></a>Twilio kitaplıkları Visual Studio projenize eklemek için:</span><span class="sxs-lookup"><span data-stu-id="af69c-186"><a id="use_nuget"></a>To add the Twilio libraries to your Visual Studio project:</span></span>
1. <span data-ttu-id="af69c-187">Çözümünüzü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="af69c-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="af69c-188">Sağ **başvurular**.</span><span class="sxs-lookup"><span data-stu-id="af69c-188">Right-click **References**.</span></span>
3. <span data-ttu-id="af69c-189">Tıklatın **NuGet paketlerini Yönet...**</span><span class="sxs-lookup"><span data-stu-id="af69c-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="af69c-190">Tıklatın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="af69c-190">Click **Online**.</span></span>
5. <span data-ttu-id="af69c-191">Arama çevrimiçi kutuya yazın *twilio*.</span><span class="sxs-lookup"><span data-stu-id="af69c-191">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="af69c-192">Tıklatın **yükleme** Twilio paketinizdeki.</span><span class="sxs-lookup"><span data-stu-id="af69c-192">Click **Install** on the Twilio package.</span></span>

## <span data-ttu-id="af69c-193"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="af69c-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="af69c-194">Aşağıdaki çağrıda giden yapılacağını gösterir **CallResource** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="af69c-194">The following shows how to make an outgoing call using the **CallResource** class.</span></span> <span data-ttu-id="af69c-195">Bu kod bir Twilio tarafından sağlanan site Twilio biçimlendirme dili (TwiML) yanıt döndürmek için de kullanır.</span><span class="sxs-lookup"><span data-stu-id="af69c-195">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="af69c-196">Kendi değerlerinizi yerleştirin **için** ve **gelen** telefon numaraları ve doğrulamanız olun **gelen** telefon numarası Twilio hesabınız için kod çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="af69c-196">Substitute your values for the **to** and **from** phone numbers, and ensure that you verify the **from** phone number for your Twilio account before running the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set the call From, To, and URL values to use for the call.
    // This sample uses the sandbox number provided by
    // Twilio to make the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="af69c-197">İçin geçirilen parametreler hakkında daha fazla bilgi için **CallResource.Create** yöntemi, bkz: [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="af69c-197">For more information about the parameters passed in to the **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="af69c-198">Belirtildiği gibi bu kod bir Twilio tarafından sağlanan site TwiML yanıt döndürmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="af69c-198">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="af69c-199">Bunun yerine, kendi site TwiML yanıt sağlamak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af69c-199">You could instead use your own site to provide the TwiML response.</span></span> <span data-ttu-id="af69c-200">Daha fazla bilgi için bkz: [nasıl yapılır: sağlamak TwiML yanıtları kendi Web sitesinden](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="af69c-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="af69c-201"><a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin</span><span class="sxs-lookup"><span data-stu-id="af69c-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="af69c-202">Aşağıdaki ekran görüntüsü kullanarak bir SMS iletisi göndermek nasıl gösterir **MessageResource** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="af69c-202">The following screenshot shows how to send an SMS message using the **MessageResource**  class.</span></span> <span data-ttu-id="af69c-203">**Gelen** numarası SMS iletileri göndermek için tarafından deneme hesapları için Twilio sağlanır.</span><span class="sxs-lookup"><span data-stu-id="af69c-203">The **from** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="af69c-204">**İçin** numarası gerekir doğrulandı Twilio hesabınız için kod çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="af69c-204">The **to** number must be verified for your Twilio account before you run the code.</span></span>

    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize the TwilioClient.
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
        // An exception occurred making the REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="af69c-205"><a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar</span><span class="sxs-lookup"><span data-stu-id="af69c-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="af69c-206">Olduğunda, uygulamanızın başlatır - Örneğin, Twilio API çağrısı aracılığıyla **CallResource.Create** yöntemi - Twilio gönderir isteğiniz TwiML yanıt döndürmek için beklenen bir URL.</span><span class="sxs-lookup"><span data-stu-id="af69c-206">When your application initiates a call to the Twilio API - for example, via the **CallResource.Create** method - Twilio sends your request to an URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="af69c-207">Örnekte [nasıl yapılır: giden bir çağrı yapmak](#howto_make_call) Twilio tarafından sağlanan URL'yi kullanır [http://twimlets.com/message] [ twimlet_message_url] yanıt dönün.</span><span class="sxs-lookup"><span data-stu-id="af69c-207">The example in [How to: Make an outgoing call](#howto_make_call) uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] to return the response.</span></span>

> [!NOTE]
> <span data-ttu-id="af69c-208">TwiML web hizmetleri tarafından kullanılmak üzere tasarlandığından, TwiML tarayıcınızda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af69c-208">While TwiML is designed for use by web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="af69c-209">Örneğin, [http://twimlets.com/message] [ twimlet_message_url] boş bir görmek için &lt;yanıt&gt; öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) görmek için bir &lt;yanıt&gt; içeren öğe bir &lt;Say&gt; öğesi.</span><span class="sxs-lookup"><span data-stu-id="af69c-209">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) to see a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="af69c-210">Twilio tarafından sağlanan URL üzerinde güvenmek yerine, HTTP yanıtlarını döndürür kendi URL sitesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af69c-210">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="af69c-211">HTTP yanıt veren herhangi bir dilde sitesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af69c-211">You can create the site in any language that returns HTTP responses.</span></span> <span data-ttu-id="af69c-212">Bu konu, bir ASP.NET genel işleyici URL'den barındırma varsayar.</span><span class="sxs-lookup"><span data-stu-id="af69c-212">This topic assumes you'll be hosting the URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="af69c-213">Aşağıdaki ASP.NET işleyicisi bildiren TwiML yanıt işler **Hello World** çağrısında.</span><span class="sxs-lookup"><span data-stu-id="af69c-213">The following ASP.NET Handler crafts a TwiML response that says **Hello World** on the call.</span></span>

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
    
<span data-ttu-id="af69c-214">Yukarıdaki örnekte görüldüğü gibi TwiML yanıt basitçe bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="af69c-214">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="af69c-215">Twilio.TwiML kitaplığı TwiML oluşturacaktır sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="af69c-215">The Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="af69c-216">Aşağıdaki örnek, yukarıda gösterildiği gibi eşdeğer yanıt verir, ancak kullanır **VoiceResponse** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="af69c-216">The example below produces the equivalent response as shown above, but uses the **VoiceResponse** class.</span></span>

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

<span data-ttu-id="af69c-217">TwiML hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="af69c-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="af69c-218">TwiML yanıtları sağlamanın bir yolu ayarladıktan sonra bu URL'ye geçirebilirsiniz **CallResource.Create** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="af69c-218">Once you have set up a way to provide TwiML responses, you can pass that URL to the **CallResource.Create** method.</span></span> <span data-ttu-id="af69c-219">Örneğin, bir Azure bulut hizmeti dağıtılmış MyTwiML adlı bir web uygulaması varsa ve ASP.NET işleyicinizi mytwiml.ashx adıdır, URL için geçirilebilir **CallResource.Create** aşağıdaki kod örneğinde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="af69c-219">For example, if you have a web application named MyTwiML deployed to an Azure cloud service, and the name of your ASP.NET Handler is mytwiml.ashx, the URL can be passed to **CallResource.Create** as shown in the following code sample:</span></span>

    // This sample uses the sandbox number provided by Twilio to make the call.
    // Place the call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="af69c-220">ASP.NET ile azure'da Twilio kullanma hakkında ek bilgi için bkz: [Twilio Azure üzerinde bir web rolü kullanılarak bir telefon araması yapmak nasıl][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="af69c-220">For additional information about using Twilio on Azure with ASP.NET, see [How to make a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

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
