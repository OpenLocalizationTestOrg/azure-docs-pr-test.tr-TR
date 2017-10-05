---
title: "Var olan Azure App Service için MySQL Azure veritabanına bağlanmak | Microsoft Docs"
description: "Nasıl düzgün şekilde var olan bir Azure uygulama hizmeti için MySQL Azure veritabanına bağlanmak için yönergeler"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="5e1ce-103">Var olan bir Azure uygulama hizmeti MySQL sunucusu için Azure veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="5e1ce-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="5e1ce-104">Bu belgede, mevcut bir Azure uygulama hizmeti MySQL sunucusu için Azure veritabanına bağlanmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-104">This document explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5e1ce-105">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5e1ce-105">Before you begin</span></span>
<span data-ttu-id="5e1ce-106">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5e1ce-107">MySQL sunucusu için bir Azure veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="5e1ce-108">Ayrıntılar için başvurmak [portalından MySQL sunucusu için Azure veritabanı oluşturmak nasıl](quickstart-create-mysql-server-database-using-azure-portal.md) veya [CLI kullanarak MySQL sunucusu için Azure veritabanı oluşturmak nasıl](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5e1ce-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="5e1ce-109">Şu anda bir Azure uygulama hizmeti bir erişimden Azure veritabanı için MySQL etkinleştirmek için iki çözümü vardır.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="5e1ce-110">Her iki çözüm de sunucu düzeyinde güvenlik duvarı kurallarını ayarlama içerir.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="5e1ce-111">Çözüm 1 - tüm IP'ler izin veren bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e1ce-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="5e1ce-112">Azure veritabanı için MySQL verilerinizi korumak için bir Güvenlik Duvarı'nı kullanarak erişim güvenliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="5e1ce-113">Bir Azure uygulama hizmetinden MySQL sunucusu için Azure veritabanına bağlanırken giden uygulama IP'leri hizmeti doğası gereği dinamik olduğunu aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="5e1ce-114">Azure uygulama hizmetiniz kullanılabilirliğini sağlamak için tüm IP'ler izin vermek için bu çözüm kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="5e1ce-115">Microsoft Azure Hizmetleri için tüm IP'ler için MySQL Azure veritabanına bağlanmak izin verme önlemek uzun vadeli bir çözüm için çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-115">Microsoft is working for a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="5e1ce-116">MySQL server dikey penceresinde, ayarlar altında başlığını tıklatın **bağlantı güvenliği** MySQL için Azure veritabanı için bağlantı güvenliği dikey penceresini açmak için.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-116">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="5e1ce-118">Girin **kural adı**, **başlangıç IP**, ve **bitiş IP**.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="5e1ce-119">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-119">Then click **Save**.</span></span>
   - <span data-ttu-id="5e1ce-120">Kural adı: izin ver-tüm-IP'leri</span><span class="sxs-lookup"><span data-stu-id="5e1ce-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="5e1ce-121">Başlangıç IP: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="5e1ce-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="5e1ce-122">Bitiş IP: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="5e1ce-122">End IP: 255.255.255.255</span></span>

   ![Azure portal - tüm IP'leri Ekle](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="5e1ce-124">Çözüm 2 - açıkça giden IP'leri izin veren bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e1ce-124">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="5e1ce-125">Azure uygulama hizmetiniz tüm giden IP'leri açıkça ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-125">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="5e1ce-126">Uygulama hizmeti özellikler dikey penceresini görüntülemek, **giden IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-126">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure portal - görünüm giden IP'leri](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="5e1ce-128">MySQL bağlantı güvenlik dikey penceresinde, giden IP'leri tek tek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-128">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure portal - açık IP'leri Ekle](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="5e1ce-130">Unutmayın **kaydetmek** , güvenlik duvarı kuralları.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-130">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="5e1ce-131">IP adreslerini zamanla sabit tutmak Azure uygulama hizmeti çalışır ancak burada IP adresleri değişebilir durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-131">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="5e1ce-132">Örneğin, zaman uygulama geri dönüştürüldüğünde ya da bir ölçeklendirme işlemi oluşur veya yeni makineler kapasiteyi artırmak için Azure bölgesel veri merkezleri zaman eklenir.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-132">For example, when the app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers to increase the capacity.</span></span> <span data-ttu-id="5e1ce-133">IP adresleri, artık MySQL sunucusuna bağlanabilir durumunda uygulama kapalı kalma süresi karşılaşabilir.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-133">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="5e1ce-134">Bu olası Yukarıdaki çözümlerden birini seçerken göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-134">Consider this potential when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="5e1ce-135">SSL yapılandırması</span><span class="sxs-lookup"><span data-stu-id="5e1ce-135">SSL configuration</span></span>
<span data-ttu-id="5e1ce-136">Azure veritabanı MySQL için varsayılan olarak SSL etkin sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="5e1ce-137">Uygulamanız veritabanına bağlanmak için SSL kullanmıyorsa, SSL MySQL sunucuda devre dışı bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5e1ce-137">If your application is not using SSL to connect to the database, then you need to disable SSL on MySQL server.</span></span> <span data-ttu-id="5e1ce-138">SSL, nasıl yapılandırılacağı hakkında ayrıntılı bilgi için bkz: [SSL kullanarak Azure veritabanı için MySQL ile](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="5e1ce-138">For details on how to configure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e1ce-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e1ce-139">Next steps</span></span>
<span data-ttu-id="5e1ce-140">Bağlantı dizeleri hakkında daha fazla bilgi için bkz [bağlantı dizeleri](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="5e1ce-140">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
