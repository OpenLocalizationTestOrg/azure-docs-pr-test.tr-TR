---
title: "Bildirimleri yapılandırmak ve e-posta şablonları Azure API Management | Microsoft Docs"
description: "Bildirimleri yapılandırma ve Azure API Management şablonlarında e-posta öğrenin."
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
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="a7662-103">Azure API Management’te bildirimleri ve e-posta şablonlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a7662-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="a7662-104">API Management belirli olaylar için bildirimleri yapılandırmak ve yöneticiler ve geliştiriciler API Management örneği ile iletişim kurmak için kullanılan e-posta şablonlarını yapılandırma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7662-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="a7662-105">Bu konuda kullanılabilir olayları için bildirimleri yapılandırmak nasıl gösterir ve bu olaylar için kullanılan e-posta şablonlarını yapılandırma genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7662-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="a7662-106"><a name="publisher-notifications"></a>Yayımcı bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a7662-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="a7662-107">Bildirimleri yapılandırmak için tıklatın **yayımcı portalına** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="a7662-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="a7662-108">Bu sizi API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="a7662-108">This takes you to the API Management publisher portal.</span></span>

![Yayımcı portalı][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="a7662-110">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="a7662-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="a7662-111">Tıklatın **bildirimleri** gelen **API Management** kullanılabilir bildirim görüntülemek için sola menüsünde.</span><span class="sxs-lookup"><span data-stu-id="a7662-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Yayımcı bildirimleri][api-management-publisher-notifications]

<span data-ttu-id="a7662-113">Aşağıdaki listede olayların bildirimleri için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7662-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="a7662-114">**(Onay gerektiren) abonelik istekler** -belirtilen e-posta alıcıları ve kullanıcıların onay gerektiren API ürünleri için abonelik isteklerini hakkında e-posta bildirimlerini alacak.</span><span class="sxs-lookup"><span data-stu-id="a7662-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="a7662-115">**Yeni abonelikler** -belirtilen e-posta alıcıları ve kullanıcıların yeni API ürün abonelikleri hakkında e-posta bildirimlerini alacak.</span><span class="sxs-lookup"><span data-stu-id="a7662-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="a7662-116">**Uygulama Galerisi isteklerini** -yeni uygulamalar için uygulama Galerisi gönderildiğinde belirtilen e-posta alıcıları ve kullanıcıların e-posta bildirimlerini alacak.</span><span class="sxs-lookup"><span data-stu-id="a7662-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="a7662-117">**Gizli** -belirtilen e-posta alıcıları ve kullanıcıların e-posta gizli kopya geliştiricilerine gönderilen tüm e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="a7662-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="a7662-118">**Yeni bir sorun veya yorum** - belirtilen e-posta alıcıları ve kullanıcıların yeni bir sorun olduğunda e-posta bildirimlerini alacak veya yorum Geliştirici portalında gönderildi.</span><span class="sxs-lookup"><span data-stu-id="a7662-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="a7662-119">**Hesabı Kapat iletisi** -bir hesap kapatıldığında belirtilen e-posta alıcıları ve kullanıcıların e-posta bildirimlerini alacak.</span><span class="sxs-lookup"><span data-stu-id="a7662-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="a7662-120">**Yaklaşan abonelik kota sınırına** -abonelik kullanım kullanım kotanız dolmak aldığında aşağıdaki e-posta alıcıları ve kullanıcıların e-posta bildirimlerini alacak.</span><span class="sxs-lookup"><span data-stu-id="a7662-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="a7662-121">Her olay için e-posta adresi metin kutusunu kullanarak e-posta alıcılarını belirtebilirsiniz veya kullanıcıların bir listeden seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7662-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="a7662-122">Bildirim almak için e-posta adresleri belirtmek için e-posta adresi metin kutusuna girin.</span><span class="sxs-lookup"><span data-stu-id="a7662-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="a7662-123">Birden çok e-posta adresi varsa, bunları ayrı virgülle ayırın.</span><span class="sxs-lookup"><span data-stu-id="a7662-123">If you have multiple email addresses, separate them using commas.</span></span>

![Bildirim alıcılarını][api-management-email-addresses]

<span data-ttu-id="a7662-125">Bilgi verilecek kullanıcıları belirtmek için tıklatın **alıcı ekleyin**, kullanıcıların bildirilmesini ve tıklatın yanındaki kutuyu **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a7662-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="a7662-126">Yalnızca Yöneticiler listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a7662-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="a7662-127">Bildirim alıcılarını yapılandırdıktan sonra tıklatın **kaydetmek** güncelleştirilmiş bildirim alıcılarını uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="a7662-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="a7662-128">Merkezden giderseniz **yayımcı bildirimleri** yayımcı portalına Uyarılar sekmesi, kaydedilmemiş değişiklikler var. durumunda.</span><span class="sxs-lookup"><span data-stu-id="a7662-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="a7662-129"><a name="email-templates"></a>E-posta şablonlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a7662-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="a7662-130">API Management yönetme ve hizmet kullanarak esnasında gönderilen e-posta iletileri için e-posta şablonları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7662-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="a7662-131">Aşağıdaki e-posta şablonlarını sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a7662-131">The following email templates are provided.</span></span>

* <span data-ttu-id="a7662-132">Onaylanan uygulama Galerisi gönderme</span><span class="sxs-lookup"><span data-stu-id="a7662-132">Application gallery submission approved</span></span>
* <span data-ttu-id="a7662-133">Geliştirici diğer harf</span><span class="sxs-lookup"><span data-stu-id="a7662-133">Developer farewell letter</span></span>
* <span data-ttu-id="a7662-134">Bildirim yaklaşan Geliştirici kota sınırı</span><span class="sxs-lookup"><span data-stu-id="a7662-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="a7662-135">Kullanıcı Davet Et</span><span class="sxs-lookup"><span data-stu-id="a7662-135">Invite user</span></span>
* <span data-ttu-id="a7662-136">Yeni açıklama soruna eklendi</span><span class="sxs-lookup"><span data-stu-id="a7662-136">New comment added to an issue</span></span>
* <span data-ttu-id="a7662-137">Alınan yeni sorun</span><span class="sxs-lookup"><span data-stu-id="a7662-137">New issue received</span></span>
* <span data-ttu-id="a7662-138">Yeni Abonelik etkinleştirildi</span><span class="sxs-lookup"><span data-stu-id="a7662-138">New subscription activated</span></span>
* <span data-ttu-id="a7662-139">Yenilenen abonelik onayı</span><span class="sxs-lookup"><span data-stu-id="a7662-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="a7662-140">Abonelik isteği reddettiğinde</span><span class="sxs-lookup"><span data-stu-id="a7662-140">Subscription request declines</span></span>
* <span data-ttu-id="a7662-141">Abonelik isteği alındı</span><span class="sxs-lookup"><span data-stu-id="a7662-141">Subscription request received</span></span>

<span data-ttu-id="a7662-142">Bu şablonlar değiştirilebilir istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="a7662-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="a7662-143">API Management Örneğiniz için e-posta şablonlarını yapılandırma ve görüntülemek için tıklatın **bildirimleri** gelen **API Management** sol ve select menüsünde **e-posta şablonlarını**sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a7662-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![E-posta şablonları][api-management-email-templates]

<span data-ttu-id="a7662-145">Görüntülemek veya belirli bir şablon değiştirmek için dosyayı seçin **şablonları** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="a7662-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![E-posta şablonları listesi][api-management-email-templates-list]

<span data-ttu-id="a7662-147">Düz metin biçiminde bir konu ve gövde tanımı'nda HTML biçiminde her e-posta şablonu yok.</span><span class="sxs-lookup"><span data-stu-id="a7662-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="a7662-148">Her öğe özelleştirilebilir istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="a7662-148">Each item can be customized as desired.</span></span>

![E-posta şablonu Düzenleyicisi][api-management-email-template]

<span data-ttu-id="a7662-150">**Parametreleri** listesi parametrelerinin listesini içeren hangi olduğunda konusu ya da gövdesi eklenen olacaktır e-posta gönderildiğinde, belirtilen değeri değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="a7662-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="a7662-151">Bir parametre eklemek için imleci gitmek için parametre istediğiniz yere yerleştirin ve parametre adının solundaki oka tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a7662-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="a7662-152">Tıklatın **Önizleme** veya **bir sınama Gönder** nasıl e-posta arayın veya bir test e-posta Gönder görmek için.</span><span class="sxs-lookup"><span data-stu-id="a7662-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="a7662-153">Parametreleri önizleme ya da bir test gönderme asıl değerlerle değiştirilmedi.</span><span class="sxs-lookup"><span data-stu-id="a7662-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="a7662-154">E-posta şablonuna yapılan değişiklikleri kaydetmek için tıklatın **kaydetmek**, veya değişiklikleri tıklatın iptal etmek için **iptal**.</span><span class="sxs-lookup"><span data-stu-id="a7662-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
