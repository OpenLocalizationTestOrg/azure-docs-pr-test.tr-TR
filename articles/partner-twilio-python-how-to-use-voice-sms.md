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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="24c73-104">Nasıl tooUse Twilio ses ve Python SMS özellikleri</span><span class="sxs-lookup"><span data-stu-id="24c73-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="24c73-105">Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir.</span><span class="sxs-lookup"><span data-stu-id="24c73-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="24c73-106">Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="24c73-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="24c73-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="24c73-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="24c73-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="24c73-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="24c73-109">Twilio iş iletişimleri hello geleceği destekleyen, geliştiricilerin tooembed ses, VoIP, etkinleştirme ve uygulamalara Mesajlaşma.</span><span class="sxs-lookup"><span data-stu-id="24c73-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="24c73-110">Bunlar hello Twilio iletişimleri API platformu ile gösterme bulut tabanlı, genel bir ortamda gerekli tüm altyapı sanallaştırın.</span><span class="sxs-lookup"><span data-stu-id="24c73-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="24c73-111">Uygulamalardır basit toobuild ve ölçeklendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="24c73-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="24c73-112">Sizinle ödeme-olarak esnekliğinin fiyatlandırma gidin ve bulut güvenilirlik ' yararlanır.</span><span class="sxs-lookup"><span data-stu-id="24c73-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="24c73-113">**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="24c73-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="24c73-114">**Twilio SMS** metin iletileri almasına ve uygulama toosend sağlar.</span><span class="sxs-lookup"><span data-stu-id="24c73-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="24c73-115">**Twilio istemci** toomake VoIP çağrılarından herhangi telefon, tablet veya tarayıcı sağlar ve WebRTC destekler.</span><span class="sxs-lookup"><span data-stu-id="24c73-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="24c73-116"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="24c73-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="24c73-117">Azure müşterilerin alacak bir [özel teklif] [ special_offer] 10 Twilio Twilio hesabınızı yükseltirken kredisi.</span><span class="sxs-lookup"><span data-stu-id="24c73-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="24c73-118">Bu Twilio kredi uygulanan tooany Twilio kullanım (1. 000'kadar SMS iletileri veya too1000 yukarı alma gelen telefon numarasını ve ileti veya çağrı hedef hello konumuna bağlı olarak sesli dakika başına 10 kredi eşdeğer toosending) olabilir.</span><span class="sxs-lookup"><span data-stu-id="24c73-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="24c73-119">Bu kullanmak [Twilio kredi] [ special_offer] ve çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="24c73-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="24c73-120">Twilio Kullandıkça Ödeme tabanlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="24c73-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="24c73-121">Hiçbir Kurulum ücretleri vardır ve herhangi bir zamanda hesabınızı kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24c73-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="24c73-122">Daha fazla bilgi bulabilirsiniz [Twilio fiyatlandırma][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="24c73-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="24c73-123"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="24c73-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="24c73-124">Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="24c73-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="24c73-125">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="24c73-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="24c73-126">Merhaba Twilio API anahtar yönlerini Twilio fiilleri ve Twilio biçimlendirme dili (TwiML) ' dir.</span><span class="sxs-lookup"><span data-stu-id="24c73-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="24c73-127"><a id="Verbs"></a>Twilio fiiller</span><span class="sxs-lookup"><span data-stu-id="24c73-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="24c73-128">Merhaba API yapar Twilio kullanmak fiiller; Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.</span><span class="sxs-lookup"><span data-stu-id="24c73-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="24c73-129">Merhaba, Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="24c73-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="24c73-130">Bilgi hakkında hello diğer fiilleri ve yetenekleri aracılığıyla [Twilio biçimlendirme dili belgeleri][twiml].</span><span class="sxs-lookup"><span data-stu-id="24c73-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="24c73-131">**&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.</span><span class="sxs-lookup"><span data-stu-id="24c73-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="24c73-132">**&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="24c73-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="24c73-133">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="24c73-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="24c73-134">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="24c73-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="24c73-135">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="24c73-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="24c73-136">**&lt;Sıra&gt;**: Merhaba tooa arayanlar kuyruğunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="24c73-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="24c73-137">**&lt;Kayıt&gt;**: hello arayanın hello sesli kayıtlar ve hello kaydı içeren bir dosyanın URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="24c73-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="24c73-138">**&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="24c73-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="24c73-139">**&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın.</span><span class="sxs-lookup"><span data-stu-id="24c73-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="24c73-140">**&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="24c73-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="24c73-141">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="24c73-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="24c73-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="24c73-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="24c73-143">TwiML XML tabanlı yönergeleri nasıl Twilio bildirmek hello Twilio fiiller üzerinde temel kümesidir tooprocess çağrısı veya SMS.</span><span class="sxs-lookup"><span data-stu-id="24c73-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="24c73-144">Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="24c73-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="24c73-145">Twilio API uygulaması çağrılarınızı Merhaba, hello API parametrelerden biri hello TwiML yanıt veren hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="24c73-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="24c73-146">Geliştirme amaçlı sağlanan Twilio URL'leri tooprovide hello TwiML yanıtlarını uygulamalarınız tarafından kullanılan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24c73-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="24c73-147">Kendi URL'leri tooproduce hello TwiML yanıtları de barındırabilir ve başka bir seçeneği toouse hello `TwiMLResponse` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="24c73-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="24c73-148">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="24c73-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="24c73-149">Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="24c73-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="24c73-150"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="24c73-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="24c73-151">Konumundaki hazır tooget Twilio hesabı olduğunda kaydolun [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="24c73-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="24c73-152">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="24c73-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="24c73-153">Twilio hesabı için kaydolduğunuzda, SID bir hesap ve kimlik doğrulama belirtecini alır.</span><span class="sxs-lookup"><span data-stu-id="24c73-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="24c73-154">Her ikisi de gerekli toomake Twilio API çağrıları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="24c73-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="24c73-155">tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="24c73-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="24c73-156">Hesabınızın SID ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio konsol][twilio_console], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="24c73-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="24c73-157"><a id="create_app"></a>Python uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="24c73-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="24c73-158">Merhaba Twilio hizmeti kullanır ve Azure üzerinde çalışan bir Python uygulaması hello Twilio hizmetini kullanan tüm diğer Python uygulamadan daha farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="24c73-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="24c73-159">Twilio Hizmetleri REST tabanlı ve Python çeşitli yollarla çağrılabilir olsa da, bu makalede toouse Twilio ile hizmetleri nasıl üzerine odaklanacaktır [github'dan Python için Twilio Kitaplığı][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="24c73-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="24c73-160">Python için hello Twilio kitaplığını kullanma hakkında daha fazla bilgi için bkz: [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="24c73-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="24c73-161">İlk olarak, [Kurulum yeni bir Azure Linux VM] [azure_vm_setup] tooact yeni Python web uygulamanız için bir konak olarak.</span><span class="sxs-lookup"><span data-stu-id="24c73-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="24c73-162">Merhaba sanal makine çalışmaya başladıktan sonra aşağıda açıklandığı gibi tooexpose genel bir bağlantı noktası uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="24c73-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="24c73-163">Bir gelen kuralı ekleyin</span><span class="sxs-lookup"><span data-stu-id="24c73-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="24c73-164">[Ağ güvenlik grubu] [azure_nsg] toohello Git sayfası.</span><span class="sxs-lookup"><span data-stu-id="24c73-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="24c73-165">Ağ güvenlik grubu, sanal makineyle karşılık gelen Hello seçin.</span><span class="sxs-lookup"><span data-stu-id="24c73-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="24c73-166">Ekleme ve **giden kuralı** için **bağlantı noktası 80**.</span><span class="sxs-lookup"><span data-stu-id="24c73-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="24c73-167">Herhangi bir adresinden gelen emin tooallow.</span><span class="sxs-lookup"><span data-stu-id="24c73-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="24c73-168">Merhaba DNS ad etiketi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="24c73-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="24c73-169">Toohello [hello ortak IP adresi] Git [azure_ips] sayfası.</span><span class="sxs-lookup"><span data-stu-id="24c73-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="24c73-170">Merhaba, sanal makineyle genel IP bu correspends seçin.</span><span class="sxs-lookup"><span data-stu-id="24c73-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="24c73-171">Set hello **DNS ad etiketi** hello içinde **yapılandırma** bölümü.</span><span class="sxs-lookup"><span data-stu-id="24c73-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="24c73-172">Bu örnek Hello durumda aşağıdakine benzer görünecektir *etki alanı etiketi bilgisayarınızı*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="24c73-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="24c73-173">Mümkün olduğunda tooconnect SSH toohello sanal makine yükleyebilirsiniz aracılığıyla hello tercih ettiğiniz Web çerçevesi (en iyi Python olan bilinen iki hello [Flask](http://flask.pocoo.org/) ve [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="24c73-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="24c73-174">Bunlardan birini hello çalıştırarak yükleyin `pip install` komutu.</span><span class="sxs-lookup"><span data-stu-id="24c73-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="24c73-175">Biz yalnızca bağlantı noktası 80 üzerinde hello sanal makine tooallow trafiği yapılandırılmış olduğunu aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="24c73-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="24c73-176">Bu nedenle bu bağlantı noktası emin tooconfigure hello uygulama toouse olun.</span><span class="sxs-lookup"><span data-stu-id="24c73-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="24c73-177"><a id="configure_app"></a>Uygulamanızı tooUse Twilio kitaplıklarını yapılandırmak</span><span class="sxs-lookup"><span data-stu-id="24c73-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="24c73-178">Python için uygulama toouse hello Twilio kitaplığınızın iki yolla yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="24c73-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="24c73-179">Merhaba Twilio kitaplığı Python için PIP paket olarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="24c73-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="24c73-180">Aşağıdaki komutları hello ile yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="24c73-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="24c73-181">-VEYA-</span><span class="sxs-lookup"><span data-stu-id="24c73-181">-OR-</span></span>

* <span data-ttu-id="24c73-182">Merhaba Twilio kitaplığı Python github'dan indirin ([https://github.com/twilio/twilio-python][twilio_python]) ve aşağıdaki gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="24c73-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="24c73-183">Python için hello Twilio kitaplığı yükledikten sonra böylece `import` Python dosyalarınızı içinde:</span><span class="sxs-lookup"><span data-stu-id="24c73-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="24c73-184">Daha fazla bilgi için bkz: [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="24c73-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="24c73-185"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="24c73-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="24c73-186">Aşağıdaki hello nasıl giden toomake çağrısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="24c73-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="24c73-187">Bu kod ayrıca Twilio tarafından sağlanan site tooreturn hello Twilio biçimlendirme dili (TwiML) yanıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="24c73-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="24c73-188">Kendi değerlerinizi hello yerine **from_number** ve **to_number** telefon numaraları ve hello doğrulandıktan olun **from_number** Twilio hesabınız için telefon numarası önce çalışan hello kodu.</span><span class="sxs-lookup"><span data-stu-id="24c73-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

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

<span data-ttu-id="24c73-189">Belirtildiği gibi bu kodu bir Twilio tarafından sağlanan site tooreturn hello TwiML yanıt kullanır.</span><span class="sxs-lookup"><span data-stu-id="24c73-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="24c73-190">Bunun yerine, kendi site tooprovide hello TwiML yanıt kullanabilirsiniz; Daha fazla bilgi için bkz: [nasıl tooProvide TwiML yanıtları bilgisayarınızı kendi Web sitesinden](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="24c73-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="24c73-191"><a id="howto_send_sms"></a>Nasıl yapılır: bir SMS iletisi gönderin</span><span class="sxs-lookup"><span data-stu-id="24c73-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="24c73-192">Merhaba aşağıdakileri nasıl bir SMS iletisini kullanarak toosend hello gösterir `TwilioRestClient` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="24c73-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="24c73-193">Merhaba **from_number** SMS iletileri toosend deneme hesapları için numarası Twilio tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="24c73-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="24c73-194">Merhaba **to_number** numarası gerekir doğrulandı Twilio hesabınız için hello kod çalıştırmadan önce.</span><span class="sxs-lookup"><span data-stu-id="24c73-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

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

## <span data-ttu-id="24c73-195"><a id="howto_provide_twiml_responses"></a>Nasıl yapılır: kendi Web sitesinden TwiML yanıtlarını sağlar</span><span class="sxs-lookup"><span data-stu-id="24c73-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="24c73-196">Uygulamanızı bir çağrı toohello Twilio API başlattığında Twilio olduğundan isteği tooa URL'nizi tooreturn TwiML yanıt beklenen gönderir.</span><span class="sxs-lookup"><span data-stu-id="24c73-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="24c73-197">Hello yukarıdaki örnekte hello Twilio tarafından sağlanan URL [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="24c73-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="24c73-198">(TwiML Twilio tarafından kullanılmak üzere tasarlandığından, tarayıcınızda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24c73-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="24c73-199">Örneğin, [http://twimlets.com/message] [ twimlet_message_url] toosee boş bir `<Response>` öğesi; başka bir örnek olarak, tıklatın [http://twimlets.com/message? İleti % 5B0 %5 D Hello % 20World =] [ twimlet_message_url_hello_world] toosee bir `<Response>` içeren öğe bir `<Say>` öğesi.)</span><span class="sxs-lookup"><span data-stu-id="24c73-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="24c73-200">Merhaba Twilio tarafından sağlanan URL güvenmek yerine, HTTP yanıtlarını döndürür, kendi site oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24c73-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="24c73-201">XML yanıtlarını döndürür herhangi bir dilde hello sitesi oluşturabilirsiniz; Bu konu Python toocreate hello TwiML kullanan varsaymaktadır.</span><span class="sxs-lookup"><span data-stu-id="24c73-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="24c73-202">Merhaba aşağıdaki örneklerde bildiren TwiML yanıt çıkış **Hello World** hello çağrıda.</span><span class="sxs-lookup"><span data-stu-id="24c73-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="24c73-203">Flask ile:</span><span class="sxs-lookup"><span data-stu-id="24c73-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="24c73-204">Django ile:</span><span class="sxs-lookup"><span data-stu-id="24c73-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="24c73-205">Yukarıdaki hello örnekte görebildiğiniz gibi hello TwiML yanıt basitçe bir XML dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="24c73-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="24c73-206">Python için Hello Twilio kitaplığı TwiML oluşturacaktır sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="24c73-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="24c73-207">Merhaba aşağıdaki örnek yukarıda gösterildiği gibi hello eşdeğer yanıt oluşturur, ancak kullanır hello `twiml` modülü Python hello Twilio Kitaplığı'nda:</span><span class="sxs-lookup"><span data-stu-id="24c73-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="24c73-208">TwiML hakkında daha fazla bilgi için bkz: [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="24c73-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="24c73-209">Python uygulamanızı tooprovide TwiML yanıtları ayarlayın sahip olduktan sonra hello uygulamasının hello URL'si hello geçirilen URL hello gibi kullanın `client.calls.create` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="24c73-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="24c73-210">Adlı bir Web uygulaması varsa, örneğin, **MyTwiML** dağıtılan tooan Azure barındırılan hizmeti, kendi url hello aşağıdaki örnekte gösterildiği gibi Web kancası kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="24c73-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

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

## <span data-ttu-id="24c73-211"><a id="AdditionalServices"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="24c73-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="24c73-212">Ayrıca, web tabanlı API'ler Twilio sunar buradaki toohello örnekler Azure uygulamanızı tooleverage ek Twilio işlevini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24c73-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="24c73-213">Tüm Ayrıntılar için bkz: hello [Twilio API belgelerine][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="24c73-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="24c73-214"><a id="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="24c73-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="24c73-215">Merhaba Twilio hizmet hello temel bilgileri öğrendiniz, daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="24c73-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="24c73-216">[Twilio güvenlik yönergeleri][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="24c73-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="24c73-217">[Twilio nasıl yapılır kılavuzları ve örnek kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="24c73-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="24c73-218">[Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="24c73-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="24c73-219">[Github'da Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="24c73-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="24c73-220">[Konuşma tooTwilio desteği][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="24c73-220">[Talk tooTwilio Support][twilio_support]</span></span>

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
