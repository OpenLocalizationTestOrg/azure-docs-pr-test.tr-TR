---
title: "Azure App Service (GoDaddy) bir özel etki alanı adı yapılandırma"
description: "GoDaddy etki alanı adından Azure Web uygulamaları ile kullanma hakkında bilgi edinin"
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
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="f8caf-103">Azure App Service’te özel etki alanı adı yapılandırma (GoDaddy’den doğrudan satın alınan)</span><span class="sxs-lookup"><span data-stu-id="f8caf-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="f8caf-104">Azure App Service Web Apps aracılığıyla etki alanı satın aldıktan sonra son adıma bakın [Web uygulamaları için etki alanı satın](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="f8caf-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="f8caf-105">Bu makalede doğrudan satın alınmış bir özel etki alanı adını kullanarak yönergeler sağlar. [GoDaddy](https://godaddy.com) ile [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f8caf-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="f8caf-106">DNS kayıtlarını anlama</span><span class="sxs-lookup"><span data-stu-id="f8caf-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="f8caf-107">Özel etki alanınız için DNS kaydı ekleyin</span><span class="sxs-lookup"><span data-stu-id="f8caf-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="f8caf-108">App Service'in web uygulamasında özel etki alanınızı ilişkilendirmek için yeni bir giriş DNS tabloda özel etki alanınız için GoDaddy tarafından sağlanan araçları kullanarak eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8caf-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="f8caf-109">DNS araçları için GoDaddy.com bulmak için aşağıdaki adımları kullanın</span><span class="sxs-lookup"><span data-stu-id="f8caf-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="f8caf-110">Hesabınıza GoDaddy.com ile oturum açın ve seçin **hesabım** ve ardından **my etki alanlarını yönetme**.</span><span class="sxs-lookup"><span data-stu-id="f8caf-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="f8caf-111">Azure web uygulaması ile kullanın ve seçmek istediğiniz etki alanı adı açılan menüsünü **yönetmek DNS**.</span><span class="sxs-lookup"><span data-stu-id="f8caf-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![GoDaddy için özel etki alanı sayfası](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="f8caf-113">Gelen **etki alanı ayrıntıları** sayfasında, kaydırarak **DNS bölge dosyasına** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f8caf-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="f8caf-114">Bu, ekleme ve etki alanı adınız için DNS kayıtlarını değiştirme için kullanılan bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="f8caf-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![DNS bölge dosyasına sekmesi](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="f8caf-116">Seçin **ekleme kaydı** varolan bir kayıt eklemek için.</span><span class="sxs-lookup"><span data-stu-id="f8caf-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="f8caf-117">İçin **Düzenle** varolan bir kaydı kağıt kaydın yanındaki simge & Kalem seçin.</span><span class="sxs-lookup"><span data-stu-id="f8caf-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f8caf-118">Yeni kayıtlar eklemeden önce GoDaddy popüler alt etki alanları için DNS kayıtlarını zaten oluşturmuş olduğunu unutmayın (adlı **konak** düzenleyicisinde) gibi **e-posta**, **dosyaları**, **posta**ve diğerleri.</span><span class="sxs-lookup"><span data-stu-id="f8caf-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="f8caf-119">Zaten kullanmak istediğiniz adı zaten varsa, yeni bir tane oluşturmak yerine var olan kayıt değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f8caf-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="f8caf-120">Bir kayıt eklerken, kayıt türünü seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8caf-120">When adding a record, you must first select the record type.</span></span>
   
    ![Kayıt türü seçin](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="f8caf-122">Ardından, sağlamanız gereken **konak** (özel etki alanı veya alt etki alanı) ve neyin **işaret**.</span><span class="sxs-lookup"><span data-stu-id="f8caf-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![Bölge kaydı ekleme](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="f8caf-124">Eklerken bir **(ana) kaydı** -ayarlamanız gerekir **konak** ya da alan  **@**  (Bu, kök etki alanı adı gibi temsil eden **contoso.com**,) * (birden çok alt etki alanlarını eşleştirmek için joker karakter) veya kullanmak istediğiniz alt etki alanı (örneğin, **www**.) Ayarlamalısınız **işaret** Azure web uygulamanızın IP adresi alanı.</span><span class="sxs-lookup"><span data-stu-id="f8caf-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="f8caf-125">Eklerken bir **CNAME kaydını (diğer ad)** -ayarlamalısınız **konak** kullanmak istediğiniz alt etki alanı.</span><span class="sxs-lookup"><span data-stu-id="f8caf-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="f8caf-126">Örneğin, **www**.</span><span class="sxs-lookup"><span data-stu-id="f8caf-126">For example, **www**.</span></span> <span data-ttu-id="f8caf-127">Ayarlamalısınız **işaret** alanı **. azurewebsites.net** Azure web uygulamanızın etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="f8caf-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="f8caf-128">Örneğin, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="f8caf-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="f8caf-129">Tıklatın **başka bir tane eklemek**.</span><span class="sxs-lookup"><span data-stu-id="f8caf-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="f8caf-130">Seçin **TXT** kayıt türü olarak ardından belirtin bir **konak** değerini  **@**  ve **işaret** değerini  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="f8caf-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f8caf-131">Bu TXT kaydı, bir kayıt veya ilk TXT kaydı tarafından açıklanan etki alanına sahip olduğunuz doğrulamak için Azure tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f8caf-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="f8caf-132">Etki alanı Azure Portal'da web uygulamasına eşlenen sonra bu TXT kayıt girişi kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8caf-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="f8caf-133">Ne zaman ekleme tamamlandı veya kayıtları değiştirme tıklatın **son** değişiklikler kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="f8caf-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="f8caf-134">Web uygulamanızdan etki alanı adını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="f8caf-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="f8caf-135">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="f8caf-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f8caf-136">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f8caf-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="f8caf-137">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="f8caf-137">What's changed</span></span>
* <span data-ttu-id="f8caf-138">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f8caf-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

