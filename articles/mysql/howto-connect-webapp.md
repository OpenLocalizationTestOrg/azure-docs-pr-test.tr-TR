---
title: "aaaConnect mevcut Azure App Service tooAzure veritabanı için MySQL | Microsoft Docs"
description: "Nasıl tooproperly bağlanacağını var olan bir Azure uygulama hizmeti tooAzure veritabanı için MySQL için yönergeler"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="edff7-103">MySQL sunucusu için var olan bir Azure uygulama hizmeti tooAzure veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="edff7-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="edff7-104">Bu belge açıklar tooconnect var olan bir Azure uygulama hizmeti tooyour Azure veritabanı nasıl MySQL sunucusu için.</span><span class="sxs-lookup"><span data-stu-id="edff7-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="edff7-105">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="edff7-105">Before you begin</span></span>
<span data-ttu-id="edff7-106">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="edff7-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="edff7-107">MySQL sunucusu için bir Azure veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="edff7-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="edff7-108">Ayrıntılar için çok başvurun[toocreate Azure veritabanı nasıl portalından MySQL sunucusu için](quickstart-create-mysql-server-database-using-azure-portal.md) veya [toocreate Azure veritabanı nasıl CLI kullanarak MySQL sunucusu için](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="edff7-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="edff7-109">Şu anda iki çözümleri tooenable erişimden Azure App Service tooan Azure veritabanı için MySQL vardır.</span><span class="sxs-lookup"><span data-stu-id="edff7-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="edff7-110">Her iki çözüm de sunucu düzeyinde güvenlik duvarı kurallarını ayarlama içerir.</span><span class="sxs-lookup"><span data-stu-id="edff7-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="edff7-111">Çözüm 1 - tüm IP'ler bir güvenlik duvarı kuralı tooallow oluşturma</span><span class="sxs-lookup"><span data-stu-id="edff7-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="edff7-112">Azure veritabanı MySQL için bir güvenlik duvarı tooprotect verilerinizi kullanarak erişim güvenliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="edff7-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="edff7-113">MySQL sunucusu için Azure App Service tooAzure veritabanı bağlantı tuttuğunuzda göz önünde bu hello giden uygulama hizmeti IP'leri doğası gereği dinamik.</span><span class="sxs-lookup"><span data-stu-id="edff7-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="edff7-114">Azure uygulama hizmetiniz hello kullanılabilirliğini tooensure, bu çözüm tooallow tüm IP'ler kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="edff7-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="edff7-115">Microsoft Azure Hizmetleri tooconnect tooAzure veritabanı için tüm IP'ler için MySQL izin vererek uzun vadeli bir çözüm tooavoid için çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="edff7-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="edff7-116">Ayarlar altında hello MySQL server dikey başlığını tıklatın **bağlantı güvenliği** tooopen hello bağlantı güvenliği dikey hello Azure veritabanı için MySQL için.</span><span class="sxs-lookup"><span data-stu-id="edff7-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure portal - bağlantı güvenliği](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="edff7-118">Girin **kural adı**, **başlangıç IP**, ve **bitiş IP**.</span><span class="sxs-lookup"><span data-stu-id="edff7-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="edff7-119">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="edff7-119">Then click **Save**.</span></span>
   - <span data-ttu-id="edff7-120">Kural adı: izin ver-tüm-IP'leri</span><span class="sxs-lookup"><span data-stu-id="edff7-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="edff7-121">Başlangıç IP: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="edff7-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="edff7-122">Bitiş IP: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="edff7-122">End IP: 255.255.255.255</span></span>

   ![Azure portal - tüm IP'leri Ekle](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="edff7-124">Çözüm 2 - oluşturmak bir güvenlik duvarı kuralı tooexplicitly giden IP'leri izin ver</span><span class="sxs-lookup"><span data-stu-id="edff7-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="edff7-125">Tüm Azure uygulama hizmetiniz, giden IP'leri hello açıkça ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edff7-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="edff7-126">Merhaba App Service özellikleri dikey penceresinde, görüntülemek, **giden IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="edff7-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure portal - görünüm giden IP'leri](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="edff7-128">Merhaba MySQL bağlantı güvenlik dikey penceresinde, giden IP'leri tek tek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="edff7-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure portal - açık IP'leri Ekle](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="edff7-130">Çok unutmayın**kaydetmek** , güvenlik duvarı kuralları.</span><span class="sxs-lookup"><span data-stu-id="edff7-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="edff7-131">Hello Azure uygulama hizmeti tookeep IP adresleri sabiti zaman içinde çalışır ancak burada hello IP adresleri değişebilir durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="edff7-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="edff7-132">Örneğin, uygulama dönüştürür zaman hello bir ölçeklendirme işlemi oluşur veya tooincrease hello kapasite merkezleri yeni makineler Azure bölgesel verilerinde zaman eklenir.</span><span class="sxs-lookup"><span data-stu-id="edff7-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="edff7-133">Değişiklik Hello IP adresleri kullanılırken hello uygulama kapalı kalma süresi, artık bağlanabilir hello olay karşılaşması toohello MySQL sunucu.</span><span class="sxs-lookup"><span data-stu-id="edff7-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="edff7-134">Bu olası çözümleri önceki hello birini seçerken göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="edff7-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="edff7-135">SSL yapılandırması</span><span class="sxs-lookup"><span data-stu-id="edff7-135">SSL configuration</span></span>
<span data-ttu-id="edff7-136">Azure veritabanı MySQL için varsayılan olarak SSL etkin sahiptir.</span><span class="sxs-lookup"><span data-stu-id="edff7-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="edff7-137">Uygulamanızı SSL tooconnect toohello veritabanı kullanmıyorsa, MySQL sunucusundaki SSL toodisable gerekir.</span><span class="sxs-lookup"><span data-stu-id="edff7-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="edff7-138">Ayrıntılar için tooconfigure SSL, bkz: [SSL kullanarak Azure veritabanı için MySQL ile](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="edff7-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="edff7-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="edff7-139">Next steps</span></span>
<span data-ttu-id="edff7-140">Bağlantı dizeleri hakkında daha fazla bilgi için çok başvuran[bağlantı dizeleri](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="edff7-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
