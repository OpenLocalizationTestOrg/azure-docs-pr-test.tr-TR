---
title: "Oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure Portalı'nı kullanarak yönetme | Microsoft Docs"
description: "Oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure Portalı'nı kullanarak yönetme"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="d86e1-103">Oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure Portalı'nı kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="d86e1-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="d86e1-104">Belirtilen IP adresi veya IP adresi aralığı PostgreSQL sunucusu için bir Azure veritabanına erişmek yöneticiler sunucu düzeyinde güvenlik duvarı kuralları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d86e1-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d86e1-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d86e1-105">Prerequisites</span></span>
<span data-ttu-id="d86e1-106">Nasıl yapılır bu kılavuzu adım için gerekir:</span><span class="sxs-lookup"><span data-stu-id="d86e1-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="d86e1-107">Bir sunucu [PostgreSQL için bir Azure veritabanı oluşturma](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d86e1-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="d86e1-108">Azure portalında sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d86e1-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="d86e1-109">PostgreSQL server dikey penceresinde, ayarlar altında başlığını tıklatın **bağlantı güvenliği** PostgreSQL için Azure veritabanı için bağlantı güvenliği dikey penceresini açmak için.</span><span class="sxs-lookup"><span data-stu-id="d86e1-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="d86e1-111">Tıklatın **eklemek IP** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="d86e1-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="d86e1-112">Bu kural otomatik olarak, bilgisayarınızın IP adresi ile Azure sistem tarafından algılanan olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d86e1-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Azure portal - My IP Ekle'yi tıklatın](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="d86e1-114">Yapılandırmayı kaydetmeden önce IP adresinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="d86e1-115">Bazı durumlarda, Azure portal tarafından gözlenen IP adresi internet ve Azure sunucuları erişirken kullanılan IP adresinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d86e1-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="d86e1-116">Bu nedenle, başlangıç IP ve bitiş IP beklendiği gibi kural işlevi yapmak için değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d86e1-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="d86e1-117">Kendi IP adresini ("Benim IP nedir" Örneğin, Bing arama) denetlemek için bir arama motoru veya diğer çevrimiçi aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Bing arama my IP nedir](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="d86e1-119">Ek adres aralıklarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d86e1-119">Add additional address ranges.</span></span> <span data-ttu-id="d86e1-120">Azure veritabanı PostgreSQL güvenlik duvarı kuralları'nda tek bir IP adresi veya adres aralığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d86e1-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="d86e1-121">Kural tek bir IP adresi için sınırlamak istiyorsanız, IP başlangıç ve bitiş IP için aynı adres alanına yazın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="d86e1-122">Güvenlik Duvarı'nı açarak, Yöneticiler ve kullanıcılar oturum açmak için PostgreSQL sunucu üzerindeki herhangi bir veritabanı için geçerli kimlik bilgilerine sahip oldukları için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="d86e1-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="d86e1-123">Azure portal - güvenlik duvarı kuralları</span><span class="sxs-lookup"><span data-stu-id="d86e1-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="d86e1-124">Tıklatın **kaydetmek** bu sunucu düzeyinde güvenlik duvarı kuralını kaydetmek için araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="d86e1-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="d86e1-125">Güvenlik duvarı kurallarının Güncelleştirme başarılı onaylanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d86e1-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Azure portal - Kaydet](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="d86e1-127">Azure portalı aracılığıyla mevcut sunucu düzeyinde güvenlik duvarı kurallarını yönetme</span><span class="sxs-lookup"><span data-stu-id="d86e1-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="d86e1-128">Güvenlik duvarı kurallarını yönetmek için gereken adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="d86e1-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="d86e1-129">Geçerli bilgisayar eklemek için düğmeyi tıklatın + **eklemek IP**.</span><span class="sxs-lookup"><span data-stu-id="d86e1-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="d86e1-130">Değişiklikleri kaydetmek için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="d86e1-131">Daha fazla IP adresi eklemek için Kural Adı, Başlangıç IP Adresi ve Bitiş IP Adresi’ni yazın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="d86e1-132">Değişiklikleri kaydetmek için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="d86e1-133">Mevcut bir kuralı değiştirmek için kuraldaki alanlardan dilediğinize tıklayıp değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d86e1-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="d86e1-134">Değişiklikleri kaydetmek için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="d86e1-135">Mevcut bir kuralı silmek için üç nokta işaretine [...] ve kural silme Kaldır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="d86e1-136">Değişiklikleri kaydetmek için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d86e1-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d86e1-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d86e1-137">Next steps</span></span>
- <span data-ttu-id="d86e1-138">Benzer şekilde, yazabilirsiniz [oluşturma ve Azure veritabanı PostgreSQL güvenlik duvarı kuralları için Azure CLI kullanarak yönetme](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d86e1-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="d86e1-139">PostgreSQL sunucu için bir Azure veritabanına bağlanma konusunda yardım için bkz: [PostgreSQL için Azure veritabanı için bağlantı kitaplıkları](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="d86e1-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
