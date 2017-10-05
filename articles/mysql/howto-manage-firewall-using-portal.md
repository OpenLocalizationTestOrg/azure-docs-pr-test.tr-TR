---
title: "Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure Portalı'nı kullanarak yönetme | Microsoft Docs"
description: "Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure Portalı'nı kullanarak yönetme"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="f9df5-103">Oluşturma ve Azure veritabanı için MySQL güvenlik duvarı kuralları Azure Portalı'nı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="f9df5-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="f9df5-104">Belirtilen IP adresi veya IP adresi aralığı MySQL sunucusu için bir Azure veritabanına erişmek yöneticiler sunucu düzeyinde güvenlik duvarı kuralları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9df5-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="f9df5-105">Azure portalında sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9df5-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="f9df5-106">MySQL server dikey penceresinde, ayarlar altında başlığını tıklatın **bağlantı güvenliği** MySQL için Azure veritabanı için bağlantı güvenliği dikey penceresini açmak için.</span><span class="sxs-lookup"><span data-stu-id="f9df5-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="f9df5-108">Tıklatın **eklemek IP** Azure sistem tarafından algılanan gibi bilgisayarınızın IP adresiyle bir kural oluşturmak için araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="f9df5-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Azure portal - My IP Ekle'yi tıklatın](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="f9df5-110">Yapılandırmayı kaydetmeden önce IP adresinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f9df5-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="f9df5-111">Bazı durumlarda, Azure portal tarafından gözlenen IP adresi internet ve Azure sunucuları erişirken kullanılan IP adresinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="f9df5-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="f9df5-112">Bu nedenle, başlangıç IP ve bitiş IP beklendiği gibi kural işlevi yapmak için değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f9df5-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="f9df5-113">Kendi IP adresini denetlemek için bir arama motoru veya diğer çevrimiçi aracını kullanın (örneğin, "IP adresimi nedir" için arama yapın).</span><span class="sxs-lookup"><span data-stu-id="f9df5-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![My IP nedir için Bing](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="f9df5-115">Ek adres aralıklarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f9df5-115">Add additional address ranges.</span></span> <span data-ttu-id="f9df5-116">Azure veritabanı için MySQL güvenlik duvarı kuralları, tek bir IP adresi veya adres aralığını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9df5-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="f9df5-117">Kural tek bir IP adresi için sınırlamak istiyorsanız, IP başlangıç ve bitiş IP için aynı adres alanına yazın.</span><span class="sxs-lookup"><span data-stu-id="f9df5-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="f9df5-118">Güvenlik Duvarı'nı açarak, Yöneticiler ve kullanıcılar geçerli kimlik bilgilerine sahip oldukları MySQL server üzerinde herhangi bir veritabanına erişmek etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="f9df5-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="f9df5-119">Azure portal - güvenlik duvarı kuralları</span><span class="sxs-lookup"><span data-stu-id="f9df5-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="f9df5-120">Tıklatın **kaydetmek** bu sunucu düzeyinde güvenlik duvarı kuralını kaydetmek için araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="f9df5-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="f9df5-121">Güvenlik duvarı kurallarının Güncelleştirme başarılı onaylanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="f9df5-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Azure portal - Kaydet](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="f9df5-123">Azure portalı aracılığıyla mevcut sunucu düzeyinde güvenlik duvarı kurallarını yönetme</span><span class="sxs-lookup"><span data-stu-id="f9df5-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="f9df5-124">Güvenlik duvarı kurallarını yönetmek için gereken adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="f9df5-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="f9df5-125">Geçerli bilgisayar eklemek için tıklatın **+ IP eklemek**.</span><span class="sxs-lookup"><span data-stu-id="f9df5-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="f9df5-126">Ek IP adresleri eklemek için yazın **kural adı**, **başlangıç IP**, ve **bitiş IP**.</span><span class="sxs-lookup"><span data-stu-id="f9df5-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="f9df5-127">Mevcut bir kuralı değiştirmek için kuraldaki alanlardan dilediğinize tıklayıp değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f9df5-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="f9df5-128">Mevcut bir kuralı silmek için [...] üç nokta düğmesine tıklayın ve **silmek**.</span><span class="sxs-lookup"><span data-stu-id="f9df5-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="f9df5-129">Değişiklikleri kaydetmek için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9df5-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9df5-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9df5-130">Next steps</span></span>
- <span data-ttu-id="f9df5-131">MySQL sunucusu için bir Azure veritabanına bağlanmada daha fazla yardım için bkz: [Azure veritabanı için MySQL için bağlantı kitaplıkları](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="f9df5-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
