---
title: aaaTemplates
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
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="f88ce-103">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="f88ce-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="f88ce-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f88ce-104">Overview</span></span>
<span data-ttu-id="f88ce-105">Şablonlar, bir istemci uygulama toospecify hello tam biçim tooreceive istediği hello bildirimleri etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="f88ce-106">Şablonları kullanarak bir uygulama hello aşağıdakileri içeren birkaç farklı faydaları hayata geçirmek:</span><span class="sxs-lookup"><span data-stu-id="f88ce-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="f88ce-107">Platform belirsiz arka uç</span><span class="sxs-lookup"><span data-stu-id="f88ce-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="f88ce-108">Kişiselleştirilmiş bildirimler</span><span class="sxs-lookup"><span data-stu-id="f88ce-108">Personalized notifications</span></span>
* <span data-ttu-id="f88ce-109">İstemci sürümü bağımsızlığı</span><span class="sxs-lookup"><span data-stu-id="f88ce-109">Client-version independence</span></span>
* <span data-ttu-id="f88ce-110">Kolay yerelleştirme</span><span class="sxs-lookup"><span data-stu-id="f88ce-110">Easy localization</span></span>

<span data-ttu-id="f88ce-111">Bu bölümde nasıl bildirim tooeach cihaz platformları ve toopersonalize tüm aygıtlarınızın hedefleme toouse şablonları toosend platform belirsiz bildirimleri yayını iki ayrıntılı örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="f88ce-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="f88ce-112">Şablonları platformlar arası kullanma</span><span class="sxs-lookup"><span data-stu-id="f88ce-112">Using templates cross-platform</span></span>
<span data-ttu-id="f88ce-113">Merhaba standart yol toosend anında iletme bildirimleri gönderilen toobe olan her bir bildirim için belirli yükü tooplatform Bildirim Hizmetleri (WNS, APNS) toosend olur.</span><span class="sxs-lookup"><span data-stu-id="f88ce-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="f88ce-114">Örneğin, bir uyarı tooAPNS toosend hello form aşağıdaki Json nesnesinin hello yükü olduğu:</span><span class="sxs-lookup"><span data-stu-id="f88ce-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="f88ce-115">bir Windows mağazası uygulaması üzerinde benzer bir bildirim iletisi toosend hello XML yükü aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f88ce-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="f88ce-116">MPNS (Windows Phone) ve GCM (Android) platformlar için benzer yükü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f88ce-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="f88ce-117">Bu gereksinim hello uygulama arka uç tooproduce farklı yüklerini her platform için zorlar ve etkili bir şekilde hello arka uç hello sunu katmanı hello uygulamanın parçası sorumlu hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="f88ce-118">Bazı sorunları yerelleştirme ve grafik düzenleri (döşeme çeşitli türleri için bildirimleri içeren özellikle Windows mağazası uygulamaları için) içerir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="f88ce-119">Ayrıca etiketler, bir şablon toohello kümesi içerir şablon kayıtlar adlı bir istemci uygulama toocreate özel kayıtları Hello bildirim hub'ları şablon özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="f88ce-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="f88ce-120">(tercih edilen) yüklemeleri veya kayıtlar ile çalışıyorsanız olup olmadığını şablonları ile bir istemci uygulama tooassociate cihazları hello bildirim hub'ları şablon özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="f88ce-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="f88ce-121">Yükü örnekler önceki hello verildiğinde, hello yalnızca platformdan bağımsız hello gerçek uyarı iletisi (Merhaba!) bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="f88ce-122">Şablon yönergeleri için nasıl tooformat platformdan bağımsız ileti bu belirli istemci uygulama hello kaydı için bildirim hub'ı hello kümesidir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="f88ce-123">Örnek önceki hello hello platform bağımsız tek bir özellik iletisidir: **ileti Hello =!**.</span><span class="sxs-lookup"><span data-stu-id="f88ce-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="f88ce-124">Resim aşağıdaki hello işlem yukarıda hello gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="f88ce-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="f88ce-125">Merhaba şablonu hello iOS istemci uygulamasını kaydı için aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f88ce-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="f88ce-126">Merhaba Windows mağazası istemci uygulaması için karşılık gelen şablon Hello şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f88ce-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="f88ce-127">Gerçek ileti hello bildirimi hello ifade $(ileti) konur.</span><span class="sxs-lookup"><span data-stu-id="f88ce-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="f88ce-128">Bir ileti toothis belirli kayıt, toobuild ve hello ortak değeri anahtarları izleyen bir ileti gönderir olduğunda bu ifade hello bildirim hub'ı bildirir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="f88ce-129">Yükleme modeliyle çalışıyorsanız, birden çok şablonlarının JSON hello yükleme "Şablon" anahtarı saklar.</span><span class="sxs-lookup"><span data-stu-id="f88ce-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="f88ce-130">Kayıt modeliyle çalışıyorsanız, birden fazla şablon Merhaba istemci uygulaması birden çok kayıtlar sipariş toouse oluşturabilirsiniz; Örneğin, uyarı iletileri için bir şablon ve bölme için bir şablon güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="f88ce-131">İstemci uygulamaları, yerel kayıtları (kayıtlar herhangi bir şablon ile) ve şablon kayıtlar de karıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f88ce-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="f88ce-132">Merhaba bildirim hub'ı toohello ait düşünmeden her şablon için bir bildirim gönderir aynı istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="f88ce-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="f88ce-133">Bu davranış, daha fazla bildirimleri kullanılan tootranslate platformdan bağımsız bildirimlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="f88ce-134">Örneğin, aynı platform bağımsız ileti toohello bildirim hub'ı sorunsuz bir bildirim uyarı ve döşeme Güncelleştirmesi'nde hello arka uç toobe bu durumdan haberdar gerek kalmadan çevrilebilir hello.</span><span class="sxs-lookup"><span data-stu-id="f88ce-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="f88ce-135">Bazı platformlar (örneğin, iOS) birden çok bildirimleri toohello Daralt Not kısa bir süre içinde gönderirse aynı aygıt.</span><span class="sxs-lookup"><span data-stu-id="f88ce-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="f88ce-136">Kişiselleştirme için şablonları kullanma</span><span class="sxs-lookup"><span data-stu-id="f88ce-136">Using templates for personalization</span></span>
<span data-ttu-id="f88ce-137">Başka bir avantajı toousing şablonları hello özelliği toouse bildirim hub'ları tooperform kayıt başına kişiselleştirme bildirimler olur.</span><span class="sxs-lookup"><span data-stu-id="f88ce-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="f88ce-138">Örneğin, belirli bir konumda hello hava koşulları içeren bir kutucuk görüntüleyen bir hava durumu uygulama göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="f88ce-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="f88ce-139">Bir kullanıcı derece veya Fahrenhayt derece ve tek veya beş günlük bir tahmini arasında seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f88ce-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="f88ce-140">Şablonları kullanarak her bir istemci uygulama yükleme için gerekli hello biçimi kaydedebilirsiniz (1 gün Celsius, 1 gün Fahrenhayt, 5 gün derece, 5 gün Fahrenhayt), ve hello arka uç tüm hello bilgileri içeren tek bir ileti gereken toofill olanlar Gönder Şablonlar (örneğin, bir beş derece ve Fahrenhayt derece ile tahmin gün).</span><span class="sxs-lookup"><span data-stu-id="f88ce-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="f88ce-141">Merhaba şablonu ile derece tahmin hello bir gün için etme aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f88ce-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="f88ce-142">Merhaba gönderilen ileti toohello bildirim hub'ı aşağıdaki özelliklere tüm hello içerir:</span><span class="sxs-lookup"><span data-stu-id="f88ce-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="f88ce-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="f88ce-143">day1_image</span></span></td><td><span data-ttu-id="f88ce-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="f88ce-144">day2_image</span></span></td><td><span data-ttu-id="f88ce-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="f88ce-145">day3_image</span></span></td><td><span data-ttu-id="f88ce-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="f88ce-146">day4_image</span></span></td><td><span data-ttu-id="f88ce-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="f88ce-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="f88ce-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="f88ce-148">day1_tempC</span></span></td><td><span data-ttu-id="f88ce-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="f88ce-149">day2_tempC</span></span></td><td><span data-ttu-id="f88ce-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="f88ce-150">day3_tempC</span></span></td><td><span data-ttu-id="f88ce-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="f88ce-151">day4_tempC</span></span></td><td><span data-ttu-id="f88ce-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="f88ce-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="f88ce-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="f88ce-153">day1_tempF</span></span></td><td><span data-ttu-id="f88ce-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="f88ce-154">day2_tempF</span></span></td><td><span data-ttu-id="f88ce-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="f88ce-155">day3_tempF</span></span></td><td><span data-ttu-id="f88ce-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="f88ce-156">day4_tempF</span></span></td><td><span data-ttu-id="f88ce-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="f88ce-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="f88ce-158">Bu yöntemi kullanarak hello arka uç yalnızca tek bir ileti toostore belirli kişiselleştirme seçenekleri hello uygulama kullanıcılar için gerek kalmadan gönderir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="f88ce-159">Resim aşağıdaki hello bu senaryo gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="f88ce-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="f88ce-160">Nasıl tooregister şablonları</span><span class="sxs-lookup"><span data-stu-id="f88ce-160">How tooregister templates</span></span>
<span data-ttu-id="f88ce-161">tooregister (tercih edilen) hello yükleme modeli kullanarak şablonları veya hello kayıt modelini bkz [kayıt yönetimi](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="f88ce-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="f88ce-162">Şablon ifade dili</span><span class="sxs-lookup"><span data-stu-id="f88ce-162">Template expression language</span></span>
<span data-ttu-id="f88ce-163">Sınırlı tooXML veya JSON Belge biçimleri şablonlarıdır.</span><span class="sxs-lookup"><span data-stu-id="f88ce-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="f88ce-164">Ayrıca, belirli yerlerde ifadeleri yalnızca koyabilirsiniz; örnek, düğüm öznitelikleri veya XML değerleri için özellik değerleri için JSON dizesi.</span><span class="sxs-lookup"><span data-stu-id="f88ce-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="f88ce-165">Merhaba aşağıdaki tabloda şablonlarında izin hello dil gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="f88ce-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="f88ce-166">ifade</span><span class="sxs-lookup"><span data-stu-id="f88ce-166">Expression</span></span> | <span data-ttu-id="f88ce-167">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f88ce-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f88ce-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="f88ce-168">$(prop)</span></span> |<span data-ttu-id="f88ce-169">Başvuru tooan olay özelliği hello verilen ada sahip.</span><span class="sxs-lookup"><span data-stu-id="f88ce-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="f88ce-170">Özellik adları büyük küçük harfe duyarlı değildir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="f88ce-171">Merhaba özellik mevcut değilse bu ifade hello özelliğin metin değeri veya boş bir dize çözümler.</span><span class="sxs-lookup"><span data-stu-id="f88ce-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="f88ce-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="f88ce-172">$(prop, n)</span></span> |<span data-ttu-id="f88ce-173">Yukarıdaki, ancak hello metin açıkça olduğu gibi n karakter kırpılmış, örneğin $(başlık, 20) hello title özelliğini Merhaba içeriğine 20 karakter kırpar.</span><span class="sxs-lookup"><span data-stu-id="f88ce-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="f88ce-174">. (prop, n)</span><span class="sxs-lookup"><span data-stu-id="f88ce-174">.(prop, n)</span></span> |<span data-ttu-id="f88ce-175">Kırpılmış olsun gibi metin yukarıdaki, ancak hello olarak üç nokta ile sonekine.</span><span class="sxs-lookup"><span data-stu-id="f88ce-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="f88ce-176">dize hello Hello toplam boyutu kırpılmış ve hello soneki n karakteri aşmayan.</span><span class="sxs-lookup"><span data-stu-id="f88ce-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="f88ce-177">. (başlık, 20) bir giriş özelliğiyle "Merhaba başlık satırı olduğu" sonuçlarında **hello başlık budur...**</span><span class="sxs-lookup"><span data-stu-id="f88ce-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="f88ce-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="f88ce-178">%(prop)</span></span> |<span data-ttu-id="f88ce-179">Bu hello çıkışı dışında benzer too$(name) URI kodlanır.</span><span class="sxs-lookup"><span data-stu-id="f88ce-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="f88ce-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="f88ce-180">#(prop)</span></span> |<span data-ttu-id="f88ce-181">JSON şablonları (örneğin, iOS ve Android şablonları için) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f88ce-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="f88ce-182">Bu işlev works tam olarak hello aynı daha önce JSON şablonları (örneğin, Apple Şablonları) kullanılması dışında belirtilen $(prop) olarak.</span><span class="sxs-lookup"><span data-stu-id="f88ce-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="f88ce-183">Bu işlev tarafından çevrelenen değil, bu durumda, "{','}" (örneğin, 'myJsonProperty': '#(ad)'), ve Javascript biçimindeki, örneğin, regexp tooa sayı değerlendirir: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, JSON bir sayıdır hello çıktı sonra.</span><span class="sxs-lookup"><span data-stu-id="f88ce-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="f88ce-184">Örneğin, ' rozet: '#(ad)' hale 'göstergeye': 40 (ve değil '40').</span><span class="sxs-lookup"><span data-stu-id="f88ce-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="f88ce-185">'text' veya "metin"</span><span class="sxs-lookup"><span data-stu-id="f88ce-185">‘text’ or “text”</span></span> |<span data-ttu-id="f88ce-186">Bir hazır değer.</span><span class="sxs-lookup"><span data-stu-id="f88ce-186">A literal.</span></span> <span data-ttu-id="f88ce-187">Değişmez değerler tek veya çift tırnak içine alınmış rastgele metin içerir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="f88ce-188">Expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="f88ce-188">expr1 + expr2</span></span> |<span data-ttu-id="f88ce-189">tek bir dize iki ifadelere birleştirme hello birleştirme işleci.</span><span class="sxs-lookup"><span data-stu-id="f88ce-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="f88ce-190">Merhaba ifadeleri herhangi forms önceki hello olabilir.</span><span class="sxs-lookup"><span data-stu-id="f88ce-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="f88ce-191">Birleştirme kullanırken hello tüm ifade alınmalıdır {} ile.</span><span class="sxs-lookup"><span data-stu-id="f88ce-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="f88ce-192">Örneğin, {$(prop) + '-' + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="f88ce-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="f88ce-193">Örneğin, hello aşağıdaki geçerli bir XML şablon değil:</span><span class="sxs-lookup"><span data-stu-id="f88ce-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="f88ce-194">Olarak yukarıda anlatıldığı, birleştirme, kullanırken ifadeleri süslü parantez içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f88ce-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="f88ce-195">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f88ce-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

