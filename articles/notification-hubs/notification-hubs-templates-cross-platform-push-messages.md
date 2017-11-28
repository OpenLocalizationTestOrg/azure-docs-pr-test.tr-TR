---
title: "Şablonlar"
description: "Bu konu, şablonları Azure bildirim hub'ları için açıklar."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 1ca24a4bf08ecdbe1c1e47a931613144309a04a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="templates"></a><span data-ttu-id="83af9-103">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="83af9-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="83af9-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="83af9-104">Overview</span></span>
<span data-ttu-id="83af9-105">Şablonları almak istediği bildirim tam biçimini belirtmek bir istemci uygulaması etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="83af9-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="83af9-106">Şablonları kullanarak bir uygulama aşağıdakiler de dahil olmak üzere birkaç farklı faydaları hayata geçirmek:</span><span class="sxs-lookup"><span data-stu-id="83af9-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="83af9-107">Platform belirsiz arka uç</span><span class="sxs-lookup"><span data-stu-id="83af9-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="83af9-108">Kişiselleştirilmiş bildirimler</span><span class="sxs-lookup"><span data-stu-id="83af9-108">Personalized notifications</span></span>
* <span data-ttu-id="83af9-109">İstemci sürümü bağımsızlığı</span><span class="sxs-lookup"><span data-stu-id="83af9-109">Client-version independence</span></span>
* <span data-ttu-id="83af9-110">Kolay yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="83af9-110">Easy localization</span></span>

<span data-ttu-id="83af9-111">Bu bölümde platformlar genelinde tüm aygıtlarınızın hedefleme platform belirsiz bildirimleri göndermek için ve her aygıt için yayın bildirim kişiselleştirmek için şablonları kullanma iki ayrıntılı örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="83af9-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="83af9-112">Şablonları platformlar arası kullanma</span><span class="sxs-lookup"><span data-stu-id="83af9-112">Using templates cross-platform</span></span>
<span data-ttu-id="83af9-113">Anında iletme bildirimleri göndermek için standart gönderilmesi için belirli bir yükü platform Bildirim Hizmetleri (WNS, APNS) için her bir bildirim göndermek için yoludur.</span><span class="sxs-lookup"><span data-stu-id="83af9-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="83af9-114">Örneğin, APNS için bir uyarı göndermek için aşağıdaki biçimde bir Json nesnesi yükü şöyledir:</span><span class="sxs-lookup"><span data-stu-id="83af9-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="83af9-115">Bir Windows mağazası uygulaması benzer bir bildirim iletisi göndermek için bir XML yükü aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="83af9-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="83af9-116">MPNS (Windows Phone) ve GCM (Android) platformlar için benzer yükü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83af9-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="83af9-117">Bu gereksinim, her platform için farklı yüklerini üretmek için uygulama arka ucu zorlar ve etkili bir şekilde arka uç uygulamasının sunu katmanı parçası sorumlu yapar.</span><span class="sxs-lookup"><span data-stu-id="83af9-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="83af9-118">Bazı sorunları yerelleştirme ve grafik düzenleri (döşeme çeşitli türleri için bildirimleri içeren özellikle Windows mağazası uygulamaları için) içerir.</span><span class="sxs-lookup"><span data-stu-id="83af9-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="83af9-119">Bildirim hub'ları şablon özelliği, bir şablon etiketleri kümesi yanı sıra içerir şablon kayıtlar adlı özel kayıtları oluşturmak için bir istemci uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="83af9-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="83af9-120">Bildirim hub'ları şablon özelliği (tercih edilen) yüklemeleri veya kayıtlar ile çalışıyorsanız olup olmadığını aygıtları şablonları ile ilişkilendirmek için bir istemci uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="83af9-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="83af9-121">Önceki bir yükü örnekler verildiğinde, platformdan bağımsız olarak yalnızca gerçek uyarı iletisi (Merhaba!) bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="83af9-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="83af9-122">Bir şablonu, bu özel istemci uygulaması kaydını platformdan bağımsız iletiyi biçimlendirmek nasıl bildirim hub'ına yönelik yönergeler kümesidir.</span><span class="sxs-lookup"><span data-stu-id="83af9-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="83af9-123">Önceki örnekte platform bağımsız tek bir özellik iletisidir: **ileti Hello =!**.</span><span class="sxs-lookup"><span data-stu-id="83af9-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="83af9-124">Aşağıdaki resimde, yukarıdaki işlemi gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="83af9-124">The following picture illustrates the above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="83af9-125">İOS istemci uygulamasını kaydı için şablonu aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="83af9-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="83af9-126">Windows mağazası istemci uygulaması için karşılık gelen şablon şöyledir:</span><span class="sxs-lookup"><span data-stu-id="83af9-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="83af9-127">Gerçek ileti geçmesidir olduğunu ifade $(ileti) dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="83af9-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="83af9-128">Bu ifade ve ortak değeri anahtarları izleyen bir ileti oluşturmak için bu belirli kayıt bir ileti gönderir her bildirim hub'ı bildirir.</span><span class="sxs-lookup"><span data-stu-id="83af9-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="83af9-129">Yükleme modeliyle çalışıyorsanız, birden çok şablonlarının JSON yükleme "Şablon" anahtarı saklar.</span><span class="sxs-lookup"><span data-stu-id="83af9-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="83af9-130">Kayıt modeliyle çalışıyorsanız, istemci uygulaması birden fazla şablon kullanmak için birden çok kayıt oluşturabilir; Örneğin, uyarı iletileri için bir şablon ve bölme için bir şablon güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="83af9-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="83af9-131">İstemci uygulamaları, yerel kayıtları (kayıtlar herhangi bir şablon ile) ve şablon kayıtlar de karıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83af9-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="83af9-132">Bildirim hub'ı aynı istemci uygulamasına ait düşünmeden her şablon için bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="83af9-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="83af9-133">Bu davranış, daha fazla bildirimleri platformdan bağımsız bildirimlerini çevirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="83af9-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="83af9-134">Örneğin, aynı platform bağımsız iletiyi bildirim hub'ına sorunsuz bir bildirim uyarı ve döşeme Güncelleştirmesi'nde bu durumdan haberdar olmasını arka uç gerek kalmadan çevrilebilir.</span><span class="sxs-lookup"><span data-stu-id="83af9-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="83af9-135">Kısa bir süre içinde gönderirse bazı platformlar (örneğin, iOS) birden fazla bildirim aynı cihaza Daralt olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="83af9-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="83af9-136">Kişiselleştirme için şablonları kullanma</span><span class="sxs-lookup"><span data-stu-id="83af9-136">Using templates for personalization</span></span>
<span data-ttu-id="83af9-137">Şablonları kullanarak başka bir avantajı kayıt başına kişiselleştirme bildirimler gerçekleştirmek için Notification Hubs'ı kullanma becerisini ' dir.</span><span class="sxs-lookup"><span data-stu-id="83af9-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="83af9-138">Örneğin, belirli bir konumda hava koşulları içeren bir kutucuk görüntüleyen bir hava durumu uygulama göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="83af9-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="83af9-139">Bir kullanıcı derece veya Fahrenhayt derece ve tek veya beş günlük bir tahmini arasında seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83af9-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="83af9-140">Şablonları kullanarak her bir istemci uygulama yükleme için gereken biçimi kaydedebilirsiniz (1 gün Celsius, 1 gün Fahrenhayt, 5 gün derece, 5 gün Fahrenhayt), ve bu şablonları doldurmak için gerekli tüm bilgileri içeren tek bir ileti gönderme arka uç (örneğin, bir beş derece ve Fahrenhayt derece ile tahmin gün).</span><span class="sxs-lookup"><span data-stu-id="83af9-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="83af9-141">Şablon için bir günlük tahmin etme ile derece şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="83af9-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="83af9-142">Bildirim Hub'ına gönderilen ileti aşağıdaki özellikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="83af9-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="83af9-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="83af9-143">day1_image</span></span></td><td><span data-ttu-id="83af9-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="83af9-144">day2_image</span></span></td><td><span data-ttu-id="83af9-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="83af9-145">day3_image</span></span></td><td><span data-ttu-id="83af9-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="83af9-146">day4_image</span></span></td><td><span data-ttu-id="83af9-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="83af9-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="83af9-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="83af9-148">day1_tempC</span></span></td><td><span data-ttu-id="83af9-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="83af9-149">day2_tempC</span></span></td><td><span data-ttu-id="83af9-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="83af9-150">day3_tempC</span></span></td><td><span data-ttu-id="83af9-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="83af9-151">day4_tempC</span></span></td><td><span data-ttu-id="83af9-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="83af9-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="83af9-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="83af9-153">day1_tempF</span></span></td><td><span data-ttu-id="83af9-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="83af9-154">day2_tempF</span></span></td><td><span data-ttu-id="83af9-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="83af9-155">day3_tempF</span></span></td><td><span data-ttu-id="83af9-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="83af9-156">day4_tempF</span></span></td><td><span data-ttu-id="83af9-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="83af9-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="83af9-158">Bu yöntemi kullanarak, arka uç yalnızca tek bir ileti uygulama kullanıcılar için belirli kişiselleştirme seçenekleri depolamak zorunda kalmadan gönderir.</span><span class="sxs-lookup"><span data-stu-id="83af9-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="83af9-159">Aşağıdaki resimde bu senaryo gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="83af9-159">The following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="83af9-160">Şablonları kaydetme</span><span class="sxs-lookup"><span data-stu-id="83af9-160">How to register templates</span></span>
<span data-ttu-id="83af9-161">(Tercih edilen) yükleme modeli veya kayıt modelini kullanarak şablonları ile kaydetmek için bkz: [kayıt yönetimi](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="83af9-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="83af9-162">Şablon ifade dili</span><span class="sxs-lookup"><span data-stu-id="83af9-162">Template expression language</span></span>
<span data-ttu-id="83af9-163">Şablonlar, XML veya JSON belge biçimlerine sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="83af9-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="83af9-164">Ayrıca, belirli yerlerde ifadeleri yalnızca koyabilirsiniz; örnek, düğüm öznitelikleri veya XML değerleri için özellik değerleri için JSON dizesi.</span><span class="sxs-lookup"><span data-stu-id="83af9-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="83af9-165">Aşağıdaki tabloda şablonlarında izin dil gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="83af9-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="83af9-166">ifade</span><span class="sxs-lookup"><span data-stu-id="83af9-166">Expression</span></span> | <span data-ttu-id="83af9-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="83af9-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="83af9-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="83af9-168">$(prop)</span></span> |<span data-ttu-id="83af9-169">Verilen ada sahip bir olay özellik referansı.</span><span class="sxs-lookup"><span data-stu-id="83af9-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="83af9-170">Özellik adları büyük küçük harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="83af9-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="83af9-171">Özellik mevcut değilse bu ifade özelliğin metin değeri veya boş bir dize çözümler.</span><span class="sxs-lookup"><span data-stu-id="83af9-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="83af9-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="83af9-172">$(prop, n)</span></span> |<span data-ttu-id="83af9-173">Yukarıdaki gibi ancak açıkça metindir n karakter kırpılmış, örneğin $(başlık, 20) title özelliğini içeriğini 20 karakter kırpar.</span><span class="sxs-lookup"><span data-stu-id="83af9-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="83af9-174">. (prop, n)</span><span class="sxs-lookup"><span data-stu-id="83af9-174">.(prop, n)</span></span> |<span data-ttu-id="83af9-175">Yukarıdaki gibi ancak bunu kırpılmış gibi metin ile üç noktaya sonekine.</span><span class="sxs-lookup"><span data-stu-id="83af9-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="83af9-176">Kırpılmış dize ve sonek toplam boyutu n karakteri aşmayan.</span><span class="sxs-lookup"><span data-stu-id="83af9-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="83af9-177">. (başlık, 20) "Bu başlık satırıdır" sonuçlarında bir giriş özelliğiyle **başlığı budur...**</span><span class="sxs-lookup"><span data-stu-id="83af9-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="83af9-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="83af9-178">%(prop)</span></span> |<span data-ttu-id="83af9-179">Benzer şekilde $(name) çıkış URI kodlanır dışında.</span><span class="sxs-lookup"><span data-stu-id="83af9-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="83af9-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="83af9-180">#(prop)</span></span> |<span data-ttu-id="83af9-181">JSON şablonları (örneğin, iOS ve Android şablonları için) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="83af9-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="83af9-182">Bu işlev tam olarak aynı daha önce JSON şablonları (örneğin, Apple Şablonları) kullanılması dışında belirtilen $(prop) çalışır.</span><span class="sxs-lookup"><span data-stu-id="83af9-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="83af9-183">Bu işlev tarafından çevrelenen değil, bu durumda, "{','}" (örneğin, 'myJsonProperty': '#(ad)'), ve onu, Javascript biçiminde bir sayı Örneğin, regexp değerlendirir: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, sonra da çıktıyı JSON bir sayıdır.</span><span class="sxs-lookup"><span data-stu-id="83af9-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="83af9-184">Örneğin, ' rozet: '#(ad)' hale 'göstergeye': 40 (ve değil '40').</span><span class="sxs-lookup"><span data-stu-id="83af9-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="83af9-185">'text' veya "metin"</span><span class="sxs-lookup"><span data-stu-id="83af9-185">‘text’ or “text”</span></span> |<span data-ttu-id="83af9-186">Bir hazır değer.</span><span class="sxs-lookup"><span data-stu-id="83af9-186">A literal.</span></span> <span data-ttu-id="83af9-187">Değişmez değerler tek veya çift tırnak içine alınmış rastgele metin içerir.</span><span class="sxs-lookup"><span data-stu-id="83af9-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="83af9-188">Expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="83af9-188">expr1 + expr2</span></span> |<span data-ttu-id="83af9-189">Tek bir dize iki ifadelere birleştirme birleştirme işleci.</span><span class="sxs-lookup"><span data-stu-id="83af9-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="83af9-190">Deyimler önceki biçimlerden birini olabilir.</span><span class="sxs-lookup"><span data-stu-id="83af9-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="83af9-191">Birleştirme kullanırken, tüm deyimin alınmalıdır {} ile.</span><span class="sxs-lookup"><span data-stu-id="83af9-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="83af9-192">Örneğin, {$(prop) + '-' + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="83af9-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="83af9-193">Örneğin, aşağıdaki geçerli bir XML şablon değil:</span><span class="sxs-lookup"><span data-stu-id="83af9-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="83af9-194">Olarak yukarıda anlatıldığı, birleştirme, kullanırken ifadeleri süslü parantez içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="83af9-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="83af9-195">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="83af9-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

