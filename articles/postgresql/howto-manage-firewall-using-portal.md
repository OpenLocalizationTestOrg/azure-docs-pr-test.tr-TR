---
title: "aaaCreate ve PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak Azure veritabanını yönetme | Microsoft Docs"
description: "Oluşturma ve Azure veritabanı için PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="d8163-103">Oluşturma ve Azure veritabanı için PostgreSQL güvenlik duvarı kuralları hello Azure portal kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="d8163-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="d8163-104">Sunucu düzeyinde güvenlik duvarı kuralları Yöneticiler tooaccess Azure veritabanı PostgreSQL sunucu için belirtilen bir IP adresi veya IP adresleri aralığını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d8163-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d8163-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d8163-105">Prerequisites</span></span>
<span data-ttu-id="d8163-106">toostep bu nasıl tooguide aracılığıyla, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="d8163-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="d8163-107">Bir sunucu [PostgreSQL için bir Azure veritabanı oluşturma](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d8163-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="d8163-108">Hello Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8163-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="d8163-109">Ayarlar altında hello PostgreSQL sunucu dikey başlığını tıklatın **bağlantı güvenliği** tooopen hello bağlantı güvenliği dikey penceresinde hello Azure veritabanı PostgreSQL için.</span><span class="sxs-lookup"><span data-stu-id="d8163-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="d8163-111">Tıklatın **eklemek IP** hello araç.</span><span class="sxs-lookup"><span data-stu-id="d8163-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="d8163-112">Bu kural otomatik olarak hello Azure sistem tarafından algılanan olarak bilgisayarınızın hello IP adresiyle oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d8163-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Azure portal - My IP Ekle'yi tıklatın](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="d8163-114">Merhaba yapılandırmayı kaydetmeden önce IP adresinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d8163-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="d8163-115">Bazı durumlarda, Azure portal tarafından gözlenen hello IP adresi başlangıç IP adresinden kullanılan farklı olduğunda erişme hello Internet ve Azure sunucuları.</span><span class="sxs-lookup"><span data-stu-id="d8163-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="d8163-116">Bu nedenle, beklendiği gibi toochange hello IP başlangıç ve bitiş IP toomake hello kural işlevi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d8163-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="d8163-117">Bir arama motoru veya diğer çevrimiçi aracı toocheck kendi IP adresi ("Benim IP nedir" Örneğin, Bing arama) kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8163-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Bing arama my IP nedir](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="d8163-119">Ek adres aralıklarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d8163-119">Add additional address ranges.</span></span> <span data-ttu-id="d8163-120">Hello Azure veritabanı PostgreSQL Güvenlik Duvarı'nda Hello kurallarında, tek bir IP adresi veya adres aralığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8163-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="d8163-121">Toolimit hello kural tooone tek bir IP adresi, aynı hello alanında IP başlangıç ve bitiş IP adresi türü hello istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d8163-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="d8163-122">Merhaba Güvenlik Duvarı'nı açma hello geçerli kimlik bilgilerine sahip oldukları PostgreSQL sunucu toowhich Yöneticiler ve kullanıcılar toologin tooany veritabanında sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8163-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="d8163-123">Azure portal - güvenlik duvarı kuralları</span><span class="sxs-lookup"><span data-stu-id="d8163-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="d8163-124">Tıklatın **kaydetmek** üzerinde bu sunucu düzeyinde güvenlik duvarı kuralı araç toosave hello.</span><span class="sxs-lookup"><span data-stu-id="d8163-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="d8163-125">Merhaba güncelleştirme toohello güvenlik duvarı kuralları başarılı oldu hello onaylanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d8163-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Azure portal - Kaydet](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="d8163-127">Var olan sunucu düzeyinde güvenlik duvarı kuralları hello Azure portal aracılığıyla yönetin</span><span class="sxs-lookup"><span data-stu-id="d8163-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="d8163-128">Merhaba adımları toomanage hello güvenlik duvarı kuralları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d8163-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="d8163-129">tooadd hello geçerli bilgisayar düğmesini hello çok + **eklemek IP**.</span><span class="sxs-lookup"><span data-stu-id="d8163-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="d8163-130">Tıklatın **kaydetmek** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="d8163-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="d8163-131">Kural adı, IP adresi başlangıç ve bitiş IP adresi hello tooadd ek IP adreslerini yazın.</span><span class="sxs-lookup"><span data-stu-id="d8163-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="d8163-132">Tıklatın **kaydetmek** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="d8163-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="d8163-133">Mevcut bir kuralı toomodify hello kural hello alanlarında birini tıklatın ve değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d8163-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="d8163-134">Tıklatın **kaydetmek** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="d8163-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="d8163-135">Mevcut bir kuralı toodelete hello üç nokta [...] ve silme Kaldır hello kuralı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8163-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="d8163-136">Tıklatın **kaydetmek** toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="d8163-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8163-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8163-137">Next steps</span></span>
- <span data-ttu-id="d8163-138">Benzer şekilde, çok komut dosyası oluşturabileceğiniz[oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d8163-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="d8163-139">Tooan Azure veritabanı PostgreSQL sunucusu bağlanma konusunda yardım için bkz [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="d8163-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
