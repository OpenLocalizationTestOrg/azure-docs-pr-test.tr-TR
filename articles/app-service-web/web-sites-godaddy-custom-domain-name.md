---
title: "aaaConfigure (GoDaddy) Azure App Service'te özel etki alanı adı"
description: "Nasıl toouse bir etki alanı adını Azure Web uygulamalarıyla GoDaddy gelen öğrenin"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="cc20e-103">Azure App Service’te özel etki alanı adı yapılandırma (GoDaddy’den doğrudan satın alınan)</span><span class="sxs-lookup"><span data-stu-id="cc20e-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="cc20e-104">Azure App Service Web Apps aracılığıyla etki alanı satın aldıktan sonra toohello son adımı başvuran [Web uygulamaları için etki alanı satın](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="cc20e-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="cc20e-105">Bu makalede doğrudan satın alınmış bir özel etki alanı adını kullanarak yönergeler sağlar. [GoDaddy](https://godaddy.com) ile [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="cc20e-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="cc20e-106">DNS kayıtlarını anlama</span><span class="sxs-lookup"><span data-stu-id="cc20e-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="cc20e-107">Özel etki alanınız için DNS kaydı ekleyin</span><span class="sxs-lookup"><span data-stu-id="cc20e-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="cc20e-108">tooassociate App Service'te bir web uygulaması ile özel etki alanınızı, yeni bir giriş hello DNS tabloda özel etki alanınız için GoDaddy tarafından sağlanan araçları kullanarak eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc20e-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="cc20e-109">GoDaddy.com için adımları toolocate hello DNS araçları aşağıdaki hello kullanın</span><span class="sxs-lookup"><span data-stu-id="cc20e-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="cc20e-110">GoDaddy.com tooyour hesabıyla oturum ve seçin **hesabım** ve ardından **my etki alanlarını yönetme**.</span><span class="sxs-lookup"><span data-stu-id="cc20e-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="cc20e-111">Azure web uygulaması ile toouse istiyor ve seçin hello etki alanı adı için Select hello açılır menü **yönetmek DNS**.</span><span class="sxs-lookup"><span data-stu-id="cc20e-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![GoDaddy için özel etki alanı sayfası](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="cc20e-113">Merhaba gelen **etki alanı ayrıntıları** sayfasında, toohello kaydırma **DNS bölge dosyasına** sekmesi. Bu ekleme ve etki alanı adınız için DNS kayıtlarını değiştirme için kullanılan hello bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="cc20e-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![DNS bölge dosyasına sekmesi](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="cc20e-115">Seçin **ekleme kaydı** tooadd varolan bir kaydı.</span><span class="sxs-lookup"><span data-stu-id="cc20e-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="cc20e-116">çok**Düzenle** varolan kaydı, hello kaydın yanındaki select hello Kalem & kağıt simgesi.</span><span class="sxs-lookup"><span data-stu-id="cc20e-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cc20e-117">Yeni kayıtlar eklemeden önce GoDaddy popüler alt etki alanları için DNS kayıtlarını zaten oluşturmuş olduğunu unutmayın (adlı **konak** düzenleyicisinde) gibi **e-posta**, **dosyaları**, **posta**ve diğerleri.</span><span class="sxs-lookup"><span data-stu-id="cc20e-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="cc20e-118">Toouse zaten istediğiniz hello adı zaten varsa, yeni bir tane oluşturmak yerine varolan kaydına hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cc20e-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="cc20e-119">Bir kayıt eklerken hello kayıt türü seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc20e-119">When adding a record, you must first select hello record type.</span></span>
   
    ![Kayıt türü seçin](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="cc20e-121">Ardından, hello sağlamalısınız **konak** (özel veya alt etki alanı hello) ve BT'nin **işaret**.</span><span class="sxs-lookup"><span data-stu-id="cc20e-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![Bölge kaydı ekleme](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="cc20e-123">Eklerken bir **(ana) kaydı** -hello ayarlamalısınız **konak** alan tooeither  **@**  (Bu, kök etki alanı adı gibi temsil eder  **contoso.com**,) * (birden çok alt etki alanlarını eşleştirmek için joker karakter) veya toouse istediğiniz hello alt etki alanı (örneğin, **www**.) Merhaba ayarlamalısınız **işaret** alan toohello IP adresi, Azure web uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="cc20e-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="cc20e-124">Eklerken bir **CNAME kaydını (diğer ad)** -hello ayarlamalısınız **konak** toouse istediğiniz alan toohello alt etki alanı.</span><span class="sxs-lookup"><span data-stu-id="cc20e-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="cc20e-125">Örneğin, **www**.</span><span class="sxs-lookup"><span data-stu-id="cc20e-125">For example, **www**.</span></span> <span data-ttu-id="cc20e-126">Merhaba ayarlamalısınız **işaret** alan toohello **. azurewebsites.net** Azure web uygulamanızın etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="cc20e-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="cc20e-127">Örneğin, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="cc20e-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="cc20e-128">Tıklatın **başka bir tane eklemek**.</span><span class="sxs-lookup"><span data-stu-id="cc20e-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="cc20e-129">Seçin **TXT** hello kayıt türü olarak ardından belirtin bir **konak** değerini  **@**  ve **işaret** değerini  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="cc20e-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cc20e-130">Bu TXT kaydı hello etki alanı kaydı veya hello ilk TXT kaydı hello tarafından açıklanan kendi Azure toovalidate tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cc20e-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="cc20e-131">Merhaba etki alanı hello Azure Portal web uygulamasında eşlenen toohello silindikten sonra bu TXT kayıt girişi kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc20e-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="cc20e-132">Ne zaman ekleme tamamlandı veya kayıtları değiştirme tıklatın **son** toosave değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="cc20e-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="cc20e-133">Web uygulamanızdan Hello etki alanı adını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="cc20e-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="cc20e-134">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc20e-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="cc20e-135">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="cc20e-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="cc20e-136">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="cc20e-136">What's changed</span></span>
* <span data-ttu-id="cc20e-137">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="cc20e-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

