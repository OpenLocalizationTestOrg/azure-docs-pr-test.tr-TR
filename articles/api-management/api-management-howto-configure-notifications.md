---
title: "aaaConfigure bildirimleri ve e-posta şablonları Azure API Management | Microsoft Docs"
description: "Bilgi nasıl tooconfigure bildirimleri ve e-posta şablonları Azure API Management'te."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="153ca-103">Nasıl tooconfigure bildirimleri ve e-posta Azure API Management şablonları</span><span class="sxs-lookup"><span data-stu-id="153ca-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="153ca-104">API Management tooconfigure bildirimleri belirli olayları ve hello Yöneticiler ve geliştiriciler API Management örneği ile kullanılan toocommunicate tooconfigure hello e-posta şablonları için hello yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="153ca-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="153ca-105">Bu konu, tooconfigure bildirimleri için kullanılabilir olayları nasıl hello gösterir ve bu olaylar için kullanılan hello e-posta şablonlarını yapılandırma genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="153ca-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="153ca-106"><a name="publisher-notifications"></a>Yayımcı bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="153ca-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="153ca-107">tooconfigure bildirimleri tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="153ca-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="153ca-108">Bu toohello API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="153ca-108">This takes you toohello API Management publisher portal.</span></span>

![Yayımcı portalı][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="153ca-110">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="153ca-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="153ca-111">Tıklatın **bildirimleri** hello gelen **API Management** hello menüsünde sol tooview hello kullanılabilir bildirim.</span><span class="sxs-lookup"><span data-stu-id="153ca-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Yayımcı bildirimleri][api-management-publisher-notifications]

<span data-ttu-id="153ca-113">Merhaba aşağıdaki olaylar listesi bildirimleri için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="153ca-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="153ca-114">**(Onay gerektiren) abonelik istekler** - belirtilen e-posta alıcılarını hello ve kullanıcıların onay gerektiren API ürünleri için abonelik isteklerini hakkında e-posta bildirimleri alır.</span><span class="sxs-lookup"><span data-stu-id="153ca-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="153ca-115">**Yeni abonelikler** - belirtilen e-posta alıcılarını hello ve kullanıcıların yeni API ürün abonelikleri hakkında e-posta bildirimleri alır.</span><span class="sxs-lookup"><span data-stu-id="153ca-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="153ca-116">**Uygulama Galerisi isteklerini** - belirtilen e-posta alıcılarını hello ve yeni uygulamalar gönderilen toohello uygulama Galerisi olduğunda kullanıcıların e-posta bildirimleri alır.</span><span class="sxs-lookup"><span data-stu-id="153ca-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="153ca-117">**Gizli** - belirtilen e-posta alıcılarını hello ve kullanıcıların e-posta gizli kopya tüm gönderilen e-postaların toodevelopers olarak alır.</span><span class="sxs-lookup"><span data-stu-id="153ca-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="153ca-118">**Yeni bir sorun veya yorum** - belirtilen e-posta alıcılarını hello ve kullanıcıların, yeni bir sorun olduğunda e-posta bildirimlerini alacak veya yorum hello Geliştirici portalında gönderildi.</span><span class="sxs-lookup"><span data-stu-id="153ca-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="153ca-119">**Hesabı Kapat iletisi** - belirtilen e-posta alıcılarını hello ve kullanıcıların bir hesap kapalı olduğunda e-posta bildirimleri alır.</span><span class="sxs-lookup"><span data-stu-id="153ca-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="153ca-120">**Yaklaşan abonelik kota sınırına** - e-posta alıcılarını aşağıdaki hello ve abonelik kullanım Kapat toousage kota aldığında kullanıcıların e-posta bildirimleri alır.</span><span class="sxs-lookup"><span data-stu-id="153ca-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="153ca-121">Her olay için hello e-posta adresi metin kutusunu kullanarak e-posta alıcılarını belirtebilirsiniz veya kullanıcıların bir listeden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="153ca-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="153ca-122">bildirim, toospecify hello e-posta adresleri toobe girin bunları hello e-posta adresi metin kutusuna.</span><span class="sxs-lookup"><span data-stu-id="153ca-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="153ca-123">Birden çok e-posta adresi varsa, bunları ayrı virgülle ayırın.</span><span class="sxs-lookup"><span data-stu-id="153ca-123">If you have multiple email addresses, separate them using commas.</span></span>

![Bildirim alıcılarını][api-management-email-addresses]

<span data-ttu-id="153ca-125">bildirim, toospecify hello kullanıcılar toobe tıklatın **alıcı ekleyin**hello bildirim hello kullanıcılar toobe yanındaki kutuyu ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="153ca-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="153ca-126">Yalnızca Yöneticiler hello listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="153ca-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="153ca-127">Merhaba bildirim alıcılarını yapılandırdıktan sonra tıklatın **kaydetmek** tooapply hello bildirim alıcılarını güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="153ca-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="153ca-128">Merhaba çıktığınızda giderseniz **yayımcı bildirimleri** sekmesini hello yayımcı portalı, kaydedilmemiş değişiklikler var. olursa uyarıları.</span><span class="sxs-lookup"><span data-stu-id="153ca-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="153ca-129"><a name="email-templates"></a>E-posta şablonlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="153ca-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="153ca-130">API Management e-posta şablonlarını yönetme ve hello hizmetini kullanarak hello indirmelere içinde gönderilen e-posta iletilerini Merhaba sağlar.</span><span class="sxs-lookup"><span data-stu-id="153ca-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="153ca-131">e-posta şablonlarını aşağıdaki hello sağlanır.</span><span class="sxs-lookup"><span data-stu-id="153ca-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="153ca-132">Onaylanan uygulama Galerisi gönderme</span><span class="sxs-lookup"><span data-stu-id="153ca-132">Application gallery submission approved</span></span>
* <span data-ttu-id="153ca-133">Geliştirici diğer harf</span><span class="sxs-lookup"><span data-stu-id="153ca-133">Developer farewell letter</span></span>
* <span data-ttu-id="153ca-134">Bildirim yaklaşan Geliştirici kota sınırı</span><span class="sxs-lookup"><span data-stu-id="153ca-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="153ca-135">Kullanıcı Davet Et</span><span class="sxs-lookup"><span data-stu-id="153ca-135">Invite user</span></span>
* <span data-ttu-id="153ca-136">Yeni Yorum tooan sorunu eklendi</span><span class="sxs-lookup"><span data-stu-id="153ca-136">New comment added tooan issue</span></span>
* <span data-ttu-id="153ca-137">Alınan yeni sorun</span><span class="sxs-lookup"><span data-stu-id="153ca-137">New issue received</span></span>
* <span data-ttu-id="153ca-138">Yeni Abonelik etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="153ca-138">New subscription activated</span></span>
* <span data-ttu-id="153ca-139">Yenilenen abonelik onayı</span><span class="sxs-lookup"><span data-stu-id="153ca-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="153ca-140">Abonelik isteği reddettiğinde</span><span class="sxs-lookup"><span data-stu-id="153ca-140">Subscription request declines</span></span>
* <span data-ttu-id="153ca-141">Abonelik isteği alındı</span><span class="sxs-lookup"><span data-stu-id="153ca-141">Subscription request received</span></span>

<span data-ttu-id="153ca-142">Bu şablonlar değiştirilebilir istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="153ca-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="153ca-143">tooview ve hello e-posta şablonlarını API Management Örneğiniz için yapılandırmak için tıklayın **bildirimleri** hello gelen **API Management** sol hello ve select hello menüsünde **e-posta şablonları**  sekmesi.</span><span class="sxs-lookup"><span data-stu-id="153ca-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![E-posta şablonları][api-management-email-templates]

<span data-ttu-id="153ca-145">tooview veya belirli bir şablon Değiştir, hello seçin **şablonları** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="153ca-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![E-posta şablonları listesi][api-management-email-templates-list]

<span data-ttu-id="153ca-147">Düz metin biçiminde bir konu ve gövde tanımı'nda HTML biçiminde her e-posta şablonu yok.</span><span class="sxs-lookup"><span data-stu-id="153ca-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="153ca-148">Her öğe özelleştirilebilir istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="153ca-148">Each item can be customized as desired.</span></span>

![E-posta şablonu Düzenleyicisi][api-management-email-template]

<span data-ttu-id="153ca-150">Merhaba **parametreleri** listesini içeren bir liste parametrelerden biri, hangi olduğunda hello konusu ya da gövdesi eklenen, hello e-posta gönderildiğinde değiştirilen hello atanan değer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="153ca-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="153ca-151">bir parametre tooinsert burada hello parametresi toogo istiyor ve hello parametre adının hello ok toohello sol tıklayın hello imleç yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="153ca-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="153ca-152">Tıklatın **Önizleme** veya **bir sınama Gönder** toosee nasıl hello e-posta arayın veya bir test e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="153ca-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="153ca-153">Merhaba parametreleri önizleme ya da bir test gönderme gerçek değerlerle değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="153ca-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="153ca-154">toosave hello değişiklikleri toohello e-posta şablonu, tıklatın **kaydetmek**, veya toocancel hello değişiklikleri **iptal**.</span><span class="sxs-lookup"><span data-stu-id="153ca-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
