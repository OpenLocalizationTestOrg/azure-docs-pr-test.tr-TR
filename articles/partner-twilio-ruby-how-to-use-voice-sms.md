---
title: "Twilio ses ve SMS (Ruby) için nasıl kullanılacağı | Microsoft Docs"
description: "Bir telefon araması yapın ve Azure üzerinde Twilio API hizmetiyle SMS mesajı göndermek öğrenin. Ruby içinde yazılan kod örnekleri."
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
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="3a50d-104">Ses ve SMS özelliklerini Söyleniş için Twilio kullanma</span><span class="sxs-lookup"><span data-stu-id="3a50d-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="3a50d-105">Bu kılavuz, Azure üzerinde Twilio API hizmeti genel programlama görevleri gerçekleştirmek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="3a50d-106">Kapsamdaki senaryolar bir telefon araması yapmadan ve kısa ileti hizmeti (SMS) ileti gönderme içerir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="3a50d-107">Twilio ve ses ve SMS uygulamalarınızda kullanma hakkında daha fazla bilgi için bkz: [sonraki adımlar](#NextSteps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3a50d-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="3a50d-108"><a id="WhatIs"></a>Twilio nedir?</span><span class="sxs-lookup"><span data-stu-id="3a50d-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="3a50d-109">Twilio ses ve SMS uygulamaları oluşturmak için varolan web dilleri ve yetenekleri kullanmanıza olanak sağlayan bir telefon web hizmeti API'dir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="3a50d-110">Twilio, (olmayan bir Azure özelliğidir ve Microsoft Ürün) bir bir üçüncü taraf hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="3a50d-111">**Twilio sesli** yapmak ve telefon çağrılarını almak, uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a50d-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="3a50d-112">**Twilio SMS** yapmak ve SMS iletileri almak, uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a50d-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="3a50d-113">**Twilio istemci** mobil bağlantıları dahil olmak üzere var olan Internet bağlantıları kullanarak sesli iletişimi etkinleştirmek, uygulamalarınızın sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a50d-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="3a50d-114"><a id="Pricing"></a>Twilio fiyatlandırma ve özel teklifler</span><span class="sxs-lookup"><span data-stu-id="3a50d-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="3a50d-115">Twilio fiyatlandırma hakkında daha fazla bilgi şu adreste [Twilio fiyatlandırma][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="3a50d-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="3a50d-116">Azure müşterilerine alma bir [özel teklif][special_offer]: boş bir kredi 1000 metinlerinin veya 1000 dakika sayısı.</span><span class="sxs-lookup"><span data-stu-id="3a50d-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="3a50d-117">Bu teklif için kaydolun veya daha fazla bilgi edinmek için lütfen ziyaret [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="3a50d-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="3a50d-118"><a id="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="3a50d-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="3a50d-119">Twilio API uygulamaları için ses ve SMS işlevselliği sağlayan bir RESTful API'dır.</span><span class="sxs-lookup"><span data-stu-id="3a50d-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="3a50d-120">İstemci kitaplıkları, birden çok dilde kullanılabilir; bir listesi için bkz: [Twilio API kitaplıkları][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="3a50d-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="3a50d-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="3a50d-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="3a50d-122">TwiML bir çağrı işlemek nasıl Twilio veya SMS bildiren XML tabanlı yönergeleri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="3a50d-123">Örnek olarak, aşağıdaki TwiML metin dönüştürecektir **Hello World** konuşma için.</span><span class="sxs-lookup"><span data-stu-id="3a50d-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="3a50d-124">Tüm TwiML dosyalarınız `<Response>` kendi kök öğesi olarak.</span><span class="sxs-lookup"><span data-stu-id="3a50d-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="3a50d-125">Burada, uygulamanızın davranışını tanımlamak için Twilio fiilleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3a50d-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="3a50d-126"><a id="Verbs"></a>TwiML fiiller</span><span class="sxs-lookup"><span data-stu-id="3a50d-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="3a50d-127">Twilio fiiller olan Twilio ne söylemek XML etiketleri **yapmak**.</span><span class="sxs-lookup"><span data-stu-id="3a50d-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="3a50d-128">Örneğin,  **&lt;Say&gt;**  fiili kullanımı bir çağrıda bir ileti teslim Twilio bildirir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="3a50d-129">Twilio fiillerin listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="3a50d-130">**&lt;Arama&gt;**: başka bir telefon çağıran bağlanır.</span><span class="sxs-lookup"><span data-stu-id="3a50d-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="3a50d-131">**&lt;Toplama&gt;**: telefon tuş takımında girilen Sayısal basamaklar toplar.</span><span class="sxs-lookup"><span data-stu-id="3a50d-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="3a50d-132">**&lt;Kapat&gt;**: bir aramasını sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="3a50d-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="3a50d-133">**&lt;Yürüt&gt;**: bir ses dosyası çalar.</span><span class="sxs-lookup"><span data-stu-id="3a50d-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="3a50d-134">**&lt;Duraklatma&gt;**: sessizce belirtilen sayıda saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="3a50d-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="3a50d-135">**&lt;Kayıt&gt;**: arayanın sesli kayıtlar ve kayıt içeren bir dosyanın URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3a50d-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="3a50d-136">**&lt;Yeniden yönlendirme&gt;**: farklı bir URL'de TwiML çağrısı veya SMS denetim aktarır.</span><span class="sxs-lookup"><span data-stu-id="3a50d-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="3a50d-137">**&lt;Reddetme&gt;**: faturalama olmadan Twilio numaranızı için bir gelen çağrıyı reddeder</span><span class="sxs-lookup"><span data-stu-id="3a50d-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="3a50d-138">**&lt;Söyleyin&gt;**: dönüştürür metin bir çağrıda yapılan okuma.</span><span class="sxs-lookup"><span data-stu-id="3a50d-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="3a50d-139">**&lt;SMS&gt;**: SMS iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="3a50d-140">Twilio fiiller, öznitelikleri ve TwiML hakkında daha fazla bilgi için bkz: [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="3a50d-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="3a50d-141">Twilio API'si hakkında ek bilgi için bkz: [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="3a50d-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="3a50d-142"><a id="CreateAccount"></a>Twilio hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a50d-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="3a50d-143">Twilio hesap almak hazır olduğunuzda, oturum açın [deneyin Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="3a50d-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="3a50d-144">Ücretsiz bir hesap ile başlatın ve daha sonra hesabınızı yükseltin.</span><span class="sxs-lookup"><span data-stu-id="3a50d-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="3a50d-145">Twilio hesabı için kaydolduğunuzda, uygulamanız için bir ücretsiz telefon numarası elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="3a50d-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="3a50d-146">Ayrıca, bir hesap SID'si ve bir kimlik doğrulama belirteci alırsınız.</span><span class="sxs-lookup"><span data-stu-id="3a50d-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="3a50d-147">Her ikisi de Twilio API çağrıları yapmanız gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="3a50d-148">Hesabınıza yetkisiz erişimi önlemek için kimlik doğrulama belirteci güvenli tutun.</span><span class="sxs-lookup"><span data-stu-id="3a50d-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="3a50d-149">Hesabınızın SID ve kimlik doğrulama belirteci adresindeki görüntülenebilir [Twilio hesap sayfası][twilio_account], etiketli alanları **HESABININ SID** ve **kimlik doğrulama BELİRTECİ**, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="3a50d-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="3a50d-150"><a id="VerifyPhoneNumbers"></a>Telefon numaralarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="3a50d-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="3a50d-151">Yanı sıra numarası Twilio tarafından verilen de doğrulayabilirsiniz uygulamalarınızda kullanım için kontrol ettiğiniz (yani, cep telefonu veya ev telefon numarası) numaralandırır.</span><span class="sxs-lookup"><span data-stu-id="3a50d-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="3a50d-152">Bir telefon numarası doğrulama hakkında daha fazla bilgi için bkz: [yönetmek numaraları][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="3a50d-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="3a50d-153"><a id="create_app"></a>Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a50d-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="3a50d-154">Twilio hizmeti kullanır ve Azure üzerinde çalışan bir Ruby uygulaması Twilio hizmetini kullanan tüm diğer Söyleniş uygulamadan daha farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="3a50d-155">Twilio Hizmetleri RESTful ve Ruby çeşitli yollarla çağrılabilir olsa da, bu makalede Twilio Hizmetleri ile kullanmak üzere nasıl odaklanacaktır [Twilio yardımcı kitaplık Ruby için][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="3a50d-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="3a50d-156">İlk olarak, [Kurulum yeni bir Azure Linux VM] [ azure_vm_setup] yeni Söyleniş web uygulamanız için bir konak olarak hareket edecek.</span><span class="sxs-lookup"><span data-stu-id="3a50d-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="3a50d-157">Rayları uygulama, yalnızca Kurulum VM oluşturulmasını içeren adımları yoksayın.</span><span class="sxs-lookup"><span data-stu-id="3a50d-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="3a50d-158">Bir dış bağlantı noktası 80 ve 5000 iç bir bağlantı noktası ile bir uç nokta oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3a50d-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="3a50d-159">Aşağıdaki örneklerde, biz kullanacağınız [Sinatra][sinatra], Ruby için çok basit web çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="3a50d-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="3a50d-160">Ancak kesinlikle Twilio yardımcı kitaplık için Ruby Ruby rayları üzerinde de dahil olmak üzere tüm diğer web framework ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a50d-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="3a50d-161">Yeni VM'nin içine SSH ve yeni uygulamanız için bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a50d-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="3a50d-162">Bu dizin içinde Gemfile adlı bir dosya oluşturun ve içine aşağıdaki kodu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="3a50d-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="3a50d-163">Komut satırını Çalıştır üzerinde `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="3a50d-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="3a50d-164">Bu, yukarıdaki bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="3a50d-164">This will install the dependencies above.</span></span> <span data-ttu-id="3a50d-165">Sonraki adlı bir dosya oluşturun `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="3a50d-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="3a50d-166">Bu, web uygulamanız için kod nerede yaşıyor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3a50d-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="3a50d-167">Aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="3a50d-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="3a50d-168">Bu noktada görüyor olmalısınız komutunu çalıştırın `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="3a50d-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="3a50d-169">Bu dönüş-bağlantı noktası 5000 küçük web sunucusunda yukarı.</span><span class="sxs-lookup"><span data-stu-id="3a50d-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="3a50d-170">Tarayıcınız bu uygulama için URL'yi ziyaret ederek Kurulum Azure VM için göz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="3a50d-171">Web uygulamanızı tarayıcıda ulaştıktan sonra bir Twilio uygulaması oluşturmaya başlamak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="3a50d-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="3a50d-172"><a id="configure_app"></a>Uygulamanızı Twilio kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3a50d-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="3a50d-173">Web uygulamanızı güncelleştirerek Twilio kitaplığını kullanacak şekilde yapılandırabilirsiniz, `Gemfile` bu satır eklemek için:</span><span class="sxs-lookup"><span data-stu-id="3a50d-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="3a50d-174">Komut satırında çalıştırmak `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="3a50d-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="3a50d-175">Şimdi açmak `web.rb` ve bu satırı üst dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="3a50d-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="3a50d-176">Şimdi tüm web uygulamanız için Ruby Twilio yardımcı kitaplık kullanmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="3a50d-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="3a50d-177"><a id="howto_make_call"></a>Nasıl yapılır: giden bir çağrı yapın</span><span class="sxs-lookup"><span data-stu-id="3a50d-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="3a50d-178">Giden bir çağrı yapma gösterir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="3a50d-179">Temel kavramları Twilio yardımcı kitaplık Ruby için REST API çağrıları yapma kullanmayı ve TwiML işleme içerir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="3a50d-180">Kendi değerlerinizi yerleştirin **gelen** ve **için** telefon numaraları ve doğrulamanız olun **gelen** kod çalıştırılmadan önce Twilio hesabınız için telefon numarası.</span><span class="sxs-lookup"><span data-stu-id="3a50d-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="3a50d-181">Bu işlev eklemek `web.md`:</span><span class="sxs-lookup"><span data-stu-id="3a50d-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="3a50d-182">Açık yukarı ise `http://yourdomain.cloudapp.net/make_call` bir tarayıcıda, tetiklemek telefon araması yapmak için Twilio API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="3a50d-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="3a50d-183">İlk iki parametre `client.account.calls.create` oldukça kendinden açıklamalıdır: sayı çağrıdır `from` ve sayı çağrı `to`.</span><span class="sxs-lookup"><span data-stu-id="3a50d-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="3a50d-184">Üçüncü parametre (`url`) Twilio çağrı bağlandıktan sonra yapmanız gerekenler hakkında yönergeler almak için ister URL'dir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="3a50d-185">Bu durumda biz Kurulum bir URL (`http://yourdomain.cloudapp.net`), basit bir TwiML belge döndürür ve kullanır `<Say>` fiil bazı okuma yapmak ve çağrı alan kişiye "Merhaba Monkey" söyleyin.</span><span class="sxs-lookup"><span data-stu-id="3a50d-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="3a50d-186"><a id="howto_recieve_sms"></a>Nasıl yapılır: alma SMS iletisi</span><span class="sxs-lookup"><span data-stu-id="3a50d-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="3a50d-187">Önceki örnekte biz başlatılan bir **giden** telefon araması.</span><span class="sxs-lookup"><span data-stu-id="3a50d-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="3a50d-188">Bu kez, bize sırasında Twilio verdiği telefon numarasını kullanalım kaydolma işlemi için bir **gelen** SMS iletisi.</span><span class="sxs-lookup"><span data-stu-id="3a50d-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="3a50d-189">Birincisi, oturum açma için sizin [Twilio Pano][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="3a50d-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="3a50d-190">"Numaralarında" içinde üst gezinme ve size sağlanan Twilio sayısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3a50d-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="3a50d-191">Yapılandırabileceğiniz iki URL'leri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3a50d-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="3a50d-192">Sesli istek URL'si ve bir SMS istek URL'si.</span><span class="sxs-lookup"><span data-stu-id="3a50d-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="3a50d-193">Twilio numaranızı gönderilen bir SMS veya telefon görüşmesi yapılan her çağrı URL'leri bunlar.</span><span class="sxs-lookup"><span data-stu-id="3a50d-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="3a50d-194">URL'leri "web kancaları" da bilinir.</span><span class="sxs-lookup"><span data-stu-id="3a50d-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="3a50d-195">İsteriz gelen SMS iletileri işlemek için URL'ye sağlandığından güncelleştirme `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="3a50d-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="3a50d-196">Bir tane sayfanın sonundaki değişiklikleri Kaydet'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3a50d-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="3a50d-197">Şimdi, geri `web.rb` şimdi uygulamamız bu durumu çözmek için program:</span><span class="sxs-lookup"><span data-stu-id="3a50d-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="3a50d-198">Değişikliği yaptıktan sonra web uygulamanızı yeniden başlatmayı emin olun.</span><span class="sxs-lookup"><span data-stu-id="3a50d-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="3a50d-199">Şimdi telefonunuz alın ve Twilio numaranızı bir SMS gönder.</span><span class="sxs-lookup"><span data-stu-id="3a50d-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="3a50d-200">Derhal "Hey, ping işlemi için teşekkür ederiz! bildiren bir SMS yanıt almanız gerekir</span><span class="sxs-lookup"><span data-stu-id="3a50d-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="3a50d-201">Twilio ve Azure rock! ".</span><span class="sxs-lookup"><span data-stu-id="3a50d-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="3a50d-202"><a id="additional_services"></a>Nasıl yapılır: ek Twilio Hizmetleri kullanın</span><span class="sxs-lookup"><span data-stu-id="3a50d-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="3a50d-203">Burada gösterilen örnekler yanı sıra, Azure uygulamanız ek Twilio işlevinden yararlanmak için kullanabileceğiniz web tabanlı API'ler Twilio sunar.</span><span class="sxs-lookup"><span data-stu-id="3a50d-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="3a50d-204">Ayrıntılar için bkz: [Twilio API belgelerine][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="3a50d-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="3a50d-205"><a id="NextSteps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3a50d-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="3a50d-206">Twilio hizmetinin öğrendiğinize göre daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="3a50d-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="3a50d-207">[Twilio güvenlik yönergeleri][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="3a50d-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="3a50d-208">[Twilio HowTos ve örnek kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="3a50d-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="3a50d-209">[Twilio hızlı başlangıç öğreticileri][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="3a50d-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="3a50d-210">[Github'da Twilio][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="3a50d-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="3a50d-211">[Twilio desteklemek için konuşun][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="3a50d-211">[Talk to Twilio Support][twilio_support]</span></span>

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
