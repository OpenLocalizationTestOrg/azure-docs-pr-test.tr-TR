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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="c28e3-104">Nasıl tooUse Twilio ses ve SMS özelliklerini Söyleniş için</span><span class="sxs-lookup"><span data-stu-id="c28e3-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="c28e3-105">Bu kılavuz, nasıl tooperform genel programlama görevleri hello Twilio API ile Azure üzerinde hizmet gösterir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="c28e3-106">Kapsanan hello senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="c28e3-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c28e3-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="c28e3-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="c28e3-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="c28e3-109">Twilio varolan web dilleri ve yetenekleri toobuild ses ve SMS uygulamaları kullanmanıza olanak sağlayan bir telefon web hizmeti API'dir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="c28e3-110">Twilio, (olmayan bir Azure özelliğidir ve Microsoft Ürün) bir bir üçüncü taraf hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="c28e3-111">**Twilio sesli** telefon çağrılarını almak ve uygulamaları toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="c28e3-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="c28e3-112">**Twilio SMS** SMS iletileri almasına ve uygulamaları toomake sağlar.</span><span class="sxs-lookup"><span data-stu-id="c28e3-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="c28e3-113">**Twilio istemci** uygulamalarınızın mobil bağlantıları dahil olmak üzere var olan Internet bağlantıları kullanarak tooenable sesli iletişime olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c28e3-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="c28e3-114"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="c28e3-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="c28e3-115">Twilio fiyatlandırma hakkında daha fazla bilgi şu adreste [Twilio fiyatlandırma][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="c28e3-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="c28e3-116">Azure müşterilerine alma bir [özel teklif][special_offer]: boş bir kredi 1000 metinlerinin veya 1000 dakika sayısı.</span><span class="sxs-lookup"><span data-stu-id="c28e3-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="c28e3-117">Bu kaydınızı toosign sunmak veya daha fazla bilgi almak, lütfen şu adresi ziyaret [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="c28e3-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="c28e3-118"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="c28e3-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="c28e3-119">Merhaba Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="c28e3-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="c28e3-120">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="c28e3-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="c28e3-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="c28e3-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="c28e3-122">TwiML nasıl Twilio bildiren XML tabanlı yönergeleri kümesidir tooprocess çağrısı veya SMS.</span><span class="sxs-lookup"><span data-stu-id="c28e3-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="c28e3-123">Örnek olarak, TwiML aşağıdaki hello hello metin dönüştürecektir **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="c28e3-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="c28e3-124">Tüm TwiML dosyalarınız `<Response>` kendi kök öğesi olarak.</span><span class="sxs-lookup"><span data-stu-id="c28e3-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="c28e3-125">Burada, uygulamanızın Twilio fiiller toodefine hello davranışını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c28e3-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="c28e3-126"><a id="Verbs"></a>TwiML fiiller</span><span class="sxs-lookup"><span data-stu-id="c28e3-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="c28e3-127">Twilio fiiller olan Twilio çok ne yapacağımı XML etiketleri**yapmak**.</span><span class="sxs-lookup"><span data-stu-id="c28e3-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="c28e3-128">Örneğin, hello  **&lt;Say&gt;**  fiil aramasında bir ileti Twilio tooaudibly teslim bildirir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="c28e3-129">Merhaba, Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="c28e3-130">**&lt;Arama&gt;**: hello arayan tooanother telefon bağlanır.</span><span class="sxs-lookup"><span data-stu-id="c28e3-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="c28e3-131">**&lt;Toplama&gt;**: hello telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="c28e3-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="c28e3-132">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="c28e3-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="c28e3-133">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="c28e3-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="c28e3-134">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="c28e3-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="c28e3-135">**&lt;Kayıt&gt;**: hello arayanın sesli kayıtlar ve hello kaydı içeren bir dosyanın URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="c28e3-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="c28e3-136">**&lt;Yeniden yönlendirme&gt;**: çağrısı veya SMS toohello TwiML farklı bir URL'de denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="c28e3-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="c28e3-137">**&lt;Reddetme&gt;**: reddeder gelen bir faturalama olmadan tooyour Twilio numarasını arayın</span><span class="sxs-lookup"><span data-stu-id="c28e3-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="c28e3-138">**&lt;Söyleyin&gt;**: üzerinde bir çağrı yapılır metin toospeech dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="c28e3-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="c28e3-139">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="c28e3-140">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="c28e3-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="c28e3-141">Merhaba Twilio API hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="c28e3-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="c28e3-142"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c28e3-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="c28e3-143">Hazır tooget Twilio hesabı olduğunuzda, oturum açın [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="c28e3-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="c28e3-144">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="c28e3-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="c28e3-145">Twilio hesabı için kaydolduğunuzda, uygulamanız için bir ücretsiz telefon numarası elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="c28e3-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="c28e3-146">Ayrıca, bir hesap SID'si ve bir kimlik doğrulama belirteci alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c28e3-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="c28e3-147">Her ikisi de gerekli toomake Twilio API çağrıları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c28e3-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="c28e3-148">tooprevent yetkisiz erişim tooyour hesabı, kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="c28e3-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="c28e3-149">Hesabınızın SID ve kimlik doğrulama belirteci hello görüntülenebilir [Twilio hesap sayfası][twilio_account], hello olarak etiketlenen alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ** , sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="c28e3-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="c28e3-150"><a id="VerifyPhoneNumbers"></a>Telefon numaralarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="c28e3-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="c28e3-151">Ekleme toohello numarası Twilio tarafından verilen uygulamalarınızda kullanım için (örneğin, cep telefonu veya ev telefon numarası) kontrol sayılar da doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c28e3-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="c28e3-152">Hakkında bilgi için bir telefon numarası tooverify bkz [yönetmek numaraları][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="c28e3-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="c28e3-153"><a id="create_app"></a>Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c28e3-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="c28e3-154">Merhaba Twilio hizmeti kullanır ve Azure üzerinde çalışan bir Ruby uygulaması hello Twilio hizmetini kullanan tüm diğer Söyleniş uygulamadan daha farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="c28e3-155">Twilio Hizmetleri RESTful ve Ruby çeşitli yollarla çağrılabilir olsa da, bu makalede toouse Twilio ile hizmetleri nasıl üzerine odaklanacaktır [Twilio yardımcı kitaplık Ruby için][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="c28e3-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="c28e3-156">İlk olarak, [Kurulum yeni bir Azure Linux VM] [ azure_vm_setup] tooact yeni Söyleniş web uygulamanız için bir konak olarak.</span><span class="sxs-lookup"><span data-stu-id="c28e3-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="c28e3-157">Merhaba adımları rayları uygulama, yalnızca Kurulum hello VM Hello oluşturulmasını içeren yoksay.</span><span class="sxs-lookup"><span data-stu-id="c28e3-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="c28e3-158">Bir dış bağlantı noktası 80 ve 5000 iç bir bağlantı noktası ile bir uç nokta oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c28e3-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="c28e3-159">Merhaba aşağıdaki örnekte, biz kullanacağınız [Sinatra][sinatra], Ruby için çok basit web çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="c28e3-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="c28e3-160">Ancak kesinlikle hello Twilio yardımcı kitaplık için Ruby Ruby rayları üzerinde de dahil olmak üzere tüm diğer web framework ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c28e3-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="c28e3-161">Yeni VM'nin içine SSH ve yeni uygulamanız için bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c28e3-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="c28e3-162">Bu dizini içinde kod içine aşağıdaki Gemfile ve kopyalama hello adlı bir dosya oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c28e3-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="c28e3-163">Merhaba komut satırını Çalıştır üzerinde `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="c28e3-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="c28e3-164">Bu, yukarıdaki hello bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="c28e3-164">This will install hello dependencies above.</span></span> <span data-ttu-id="c28e3-165">Sonraki adlı bir dosya oluşturun `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="c28e3-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="c28e3-166">Bu, web uygulamanız için hello kodu nerede yaşıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c28e3-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="c28e3-167">Kod içine aşağıdaki hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="c28e3-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="c28e3-168">Bu noktada çalıştırmak mümkün hello hello komutu olmalıdır `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="c28e3-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="c28e3-169">Bu dönüş-bağlantı noktası 5000 küçük web sunucusunda yukarı.</span><span class="sxs-lookup"><span data-stu-id="c28e3-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="c28e3-170">Merhaba URL adresini ziyaret ederek tarayıcınızda mümkün toobrowse toothis uygulama olmalıdır, Kurulum, Azure VM için.</span><span class="sxs-lookup"><span data-stu-id="c28e3-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="c28e3-171">Web uygulamanızı hello tarayıcıda ulaştıktan sonra bir Twilio uygulaması oluşturmaya hazır toostart demektir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="c28e3-172"><a id="configure_app"></a>Uygulamanızı tooUse Twilio yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c28e3-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="c28e3-173">Web uygulaması toouse hello Twilio kitaplığınızın güncelleştirerek yapılandırabilirsiniz, `Gemfile` tooinclude bu satırı:</span><span class="sxs-lookup"><span data-stu-id="c28e3-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="c28e3-174">Merhaba komut satırında çalıştırmak `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="c28e3-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="c28e3-175">Şimdi açmak `web.rb` ve bu satırı hello üstünde dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="c28e3-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="c28e3-176">Web uygulamanız için Ruby toouse hello Twilio yardımcı kitaplık ayarlamak artık olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="c28e3-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="c28e3-177"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="c28e3-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="c28e3-178">Aşağıdaki hello nasıl giden toomake çağrısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="c28e3-179">Temel kavramları hello Twilio yardımcı kitaplık Söyleniş toomake REST API çağrıları için kullanarak ve TwiML işleme içerir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="c28e3-180">Kendi değerlerinizi hello yerine **gelen** ve **için** telefon numaraları ve hello doğruladığınızdan emin olun **gelen** Twilio hesabı önceki toorunning hello kodunuz için telefon numarası.</span><span class="sxs-lookup"><span data-stu-id="c28e3-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="c28e3-181">Bu işlev çok eklemek`web.md`:</span><span class="sxs-lookup"><span data-stu-id="c28e3-181">Add this function too`web.md`:</span></span>

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

<span data-ttu-id="c28e3-182">Açık yukarı ise `http://yourdomain.cloudapp.net/make_call` bir tarayıcıda, tetiklemek hello çağrısı toohello Twilio API toomake hello telefon araması.</span><span class="sxs-lookup"><span data-stu-id="c28e3-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="c28e3-183">ilk iki parametrelerinde hello `client.account.calls.create` oldukça kendinden açıklamalıdır: hello sayı hello çağrısı `from` ve hello sayı hello çağrısı `to`.</span><span class="sxs-lookup"><span data-stu-id="c28e3-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="c28e3-184">Üçüncü parametre hello (`url`) hello çağrısı bağlandıktan sonra Twilio hangi toodo tooget yönergeler istekleri hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="c28e3-185">Bu durumda biz Kurulum bir URL (`http://yourdomain.cloudapp.net`), basit bir TwiML belge döndürür ve kullandığı hello `<Say>` bazı okuma ve deyin alma "Merhaba Monkey" toohello kişi hello fiil toodo çağırın.</span><span class="sxs-lookup"><span data-stu-id="c28e3-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="c28e3-186"><a id="howto_recieve_sms"></a>Nasıl yapılır: alma SMS iletisi</span><span class="sxs-lookup"><span data-stu-id="c28e3-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="c28e3-187">Merhaba önceki örnekte biz başlatılan bir **giden** telefon araması.</span><span class="sxs-lookup"><span data-stu-id="c28e3-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="c28e3-188">Bu kez, Twilio sırasında kaydolma tooprocess bize verdiğiniz hello telefon numarası kullanalım bir **gelen** SMS iletisi.</span><span class="sxs-lookup"><span data-stu-id="c28e3-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="c28e3-189">Birincisi, oturum açma tooyour [Twilio Pano][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="c28e3-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="c28e3-190">"Numaralarında" Merhaba üst nav uygulamasında tıklayın ve Twilio sayısı, sağlanan üzerinde hello'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c28e3-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="c28e3-191">Yapılandırabileceğiniz iki URL'leri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c28e3-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="c28e3-192">Sesli istek URL'si ve bir SMS istek URL'si.</span><span class="sxs-lookup"><span data-stu-id="c28e3-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="c28e3-193">Twilio çağrıları bir telefon araması her yapıldığında hello URL'leri bunlar veya SMS tooyour numarası gönderilir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="c28e3-194">Merhaba URL'leri "web kancaları" da bilinir.</span><span class="sxs-lookup"><span data-stu-id="c28e3-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="c28e3-195">Biz ister tooprocess gelen SMS iletileri sağlandığından güncelleştirme hello URL çok`http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="c28e3-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="c28e3-196">Bir tane hello sayfanın hello Değişiklikleri Kaydet'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c28e3-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="c28e3-197">Şimdi, geri `web.rb` şimdi bizim uygulama toohandle bu programı:</span><span class="sxs-lookup"><span data-stu-id="c28e3-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="c28e3-198">Hello değişiklik yaptıktan sonra web uygulamanızı emin toore başlangıç yapın.</span><span class="sxs-lookup"><span data-stu-id="c28e3-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="c28e3-199">Şimdi telefonunuz alın ve SMS tooyour Twilio numarası gönderin.</span><span class="sxs-lookup"><span data-stu-id="c28e3-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="c28e3-200">Derhal "Hey, hello ping için teşekkür ederiz! bildiren bir SMS yanıt almanız gerekir</span><span class="sxs-lookup"><span data-stu-id="c28e3-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="c28e3-201">Twilio ve Azure rock! ".</span><span class="sxs-lookup"><span data-stu-id="c28e3-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="c28e3-202"><a id="additional_services"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="c28e3-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="c28e3-203">Ayrıca, web tabanlı API'ler Twilio sunar buradaki toohello örnekler Azure uygulamanızı tooleverage ek Twilio işlevini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c28e3-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="c28e3-204">Tüm Ayrıntılar için bkz: hello [Twilio API belgelerine][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="c28e3-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="c28e3-205"><a id="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c28e3-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="c28e3-206">Merhaba Twilio hizmet hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="c28e3-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="c28e3-207">[Twilio güvenlik yönergeleri][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="c28e3-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="c28e3-208">[Twilio HowTos ve örnek kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="c28e3-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="c28e3-209">[Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="c28e3-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="c28e3-210">[Github'da Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="c28e3-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="c28e3-211">[Konuşma tooTwilio desteği][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="c28e3-211">[Talk tooTwilio Support][twilio_support]</span></span>

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
