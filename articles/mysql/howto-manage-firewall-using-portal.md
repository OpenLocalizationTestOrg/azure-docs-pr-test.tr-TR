---
title: "aaaCreate ve Azure veritabanı için MySQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme | Microsoft Docs"
description: "Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="5b66c-103">Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="5b66c-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="5b66c-104">Sunucu düzeyinde güvenlik duvarı kuralları Yöneticiler tooaccess Azure veritabanı MySQL sunucusu için belirtilen bir IP adresi veya IP adresi aralığı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5b66c-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="5b66c-105">Hello Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b66c-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="5b66c-106">Ayarlar altında hello MySQL server dikey başlığını tıklatın **bağlantı güvenliği** tooopen hello bağlantı güvenliği dikey hello Azure veritabanı için MySQL için.</span><span class="sxs-lookup"><span data-stu-id="5b66c-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="5b66c-108">Tıklatın **eklemek IP** hello araç toocreate hello Azure sistem tarafından algılanan gibi bilgisayarınızın hello IP adresine sahip bir kural üzerinde.</span><span class="sxs-lookup"><span data-stu-id="5b66c-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Azure portal - My IP Ekle'yi tıklatın](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="5b66c-110">Merhaba yapılandırmayı kaydetmeden önce IP adresinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5b66c-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="5b66c-111">Bazı durumlarda, Azure portal tarafından gözlenen hello IP adresi başlangıç IP adresinden kullanılan farklı olduğunda erişme hello Internet ve Azure sunucuları.</span><span class="sxs-lookup"><span data-stu-id="5b66c-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="5b66c-112">Bu nedenle, beklendiği gibi toochange hello IP başlangıç ve bitiş IP toomake hello kural işlevi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5b66c-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="5b66c-113">Bir arama motoru veya diğer çevrimiçi aracı toocheck kendi IP adresini kullanın (örneğin, "IP adresimi nedir" için arama yapın).</span><span class="sxs-lookup"><span data-stu-id="5b66c-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![My IP nedir için Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="5b66c-115">Ek adres aralıklarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b66c-115">Add additional address ranges.</span></span> <span data-ttu-id="5b66c-116">MySQL Güvenlik Duvarı'nda hello Azure veritabanı için Hello kuralları'nda tek bir IP adresi veya adres aralığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b66c-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="5b66c-117">Toolimit hello kural tooone tek bir IP adresi, aynı hello alanında IP başlangıç ve bitiş IP adresi türü hello istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="5b66c-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="5b66c-118">Merhaba Güvenlik Duvarı'nı açma Yöneticiler ve kullanıcılar tooaccess hello MySQL server toowhich geçerli kimlik bilgilerine sahip oldukları herhangi bir veritabanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b66c-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="5b66c-119">Azure portal - güvenlik duvarı kuralları</span><span class="sxs-lookup"><span data-stu-id="5b66c-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="5b66c-120">Tıklatın **kaydetmek** üzerinde bu sunucu düzeyinde güvenlik duvarı kuralı araç toosave hello.</span><span class="sxs-lookup"><span data-stu-id="5b66c-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="5b66c-121">Merhaba güncelleştirme toohello güvenlik duvarı kuralları başarılı oldu hello onaylanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b66c-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Azure portal - Kaydet](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="5b66c-123">Var olan sunucu düzeyinde güvenlik duvarı kuralları hello Azure portal aracılığıyla yönetin</span><span class="sxs-lookup"><span data-stu-id="5b66c-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="5b66c-124">Merhaba adımları toomanage hello güvenlik duvarı kuralları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="5b66c-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="5b66c-125">tooadd hello geçerli bilgisayar, **+ IP eklemek**.</span><span class="sxs-lookup"><span data-stu-id="5b66c-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="5b66c-126">tooadd ek IP adreslerini yazın hello **kural adı**, **başlangıç IP**, ve **bitiş IP**.</span><span class="sxs-lookup"><span data-stu-id="5b66c-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="5b66c-127">Mevcut bir kuralı toomodify hello kural hello alanlarında birini tıklatın ve değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5b66c-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="5b66c-128">var olan toodelete kural hello üç nokta [...] ve'ı tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="5b66c-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="5b66c-129">Tıklatın **kaydetmek** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="5b66c-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b66c-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b66c-130">Next steps</span></span>
- <span data-ttu-id="5b66c-131">MySQL sunucusu için Azure veritabanı tooan bağlanma konusunda yardım için bkz: [Azure veritabanı için MySQL için bağlantı kitaplıkları](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="5b66c-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
