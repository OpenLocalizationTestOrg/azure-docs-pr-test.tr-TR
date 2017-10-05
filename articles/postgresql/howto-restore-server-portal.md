---
title: "Azure veritabanı Server'da PostgreSQL için geri yükleme | Microsoft Docs"
description: "Bu makalede, Azure veritabanındaki bir sunucu için Azure portalını kullanarak PostgreSQL geri açıklar."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: 3fbdb7741481bd3620466c3489d3609f9ea6961f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="e2c38-103">Yedekleme ve Azure veritabanındaki bir sunucu için Azure portalını kullanarak PostgreSQL geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e2c38-103">How To Backup and Restore a server in Azure Database for PostgreSQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="e2c38-104">Yedekleme otomatik olarak gerçekleşir</span><span class="sxs-lookup"><span data-stu-id="e2c38-104">Backup happens Automatically</span></span>
<span data-ttu-id="e2c38-105">Azure veritabanı için PostgreSQL kullanırken, veritabanı hizmeti yedekleme hizmetinin her 5 dakikada bir otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="e2c38-105">When using Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="e2c38-106">Temel katman ve 35 gün kullanırken yedeklemeler 7 gün için kullanılabilir olan standart katmanı kullanırken.</span><span class="sxs-lookup"><span data-stu-id="e2c38-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="e2c38-107">Daha fazla bilgi için bkz: [PostgreSQL hizmet katmanları için Azure veritabanı](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="e2c38-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="e2c38-108">Bu otomatik yedekleme özelliğini kullanarak, sunucu ve tüm veritabanlarını içine bir önceki noktası zaman içinde yeni bir sunucuya geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2c38-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="e2c38-109">Azure portalında geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e2c38-109">Restore in the Azure portal</span></span>
<span data-ttu-id="e2c38-110">Azure veritabanı PostgreSQL için sağlar, sunucu saati ve içine bir noktaya geri geri yüklemek sunucu yeni bir kopyasını için.</span><span class="sxs-lookup"><span data-stu-id="e2c38-110">Azure Database for PostgreSQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="e2c38-111">Bu yeni sunucu verilerinizi kurtarmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e2c38-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="e2c38-112">Örneğin, bir tablo yanlışlıkla varsa bugün öğlen bırakılan, zaman öğlen hemen önce geri yükleme ve bu sunucunun yeni kopyadan eksik tablo ve veri almak.</span><span class="sxs-lookup"><span data-stu-id="e2c38-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="e2c38-113">Aşağıdaki adımları örnek sunucunun saat içinde bir noktaya geri:</span><span class="sxs-lookup"><span data-stu-id="e2c38-113">The following steps restore the sample server to a point in time:</span></span>
1. <span data-ttu-id="e2c38-114">Oturum [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="e2c38-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="e2c38-115">Azure veritabanınız PostgreSQL sunucu için bulun.</span><span class="sxs-lookup"><span data-stu-id="e2c38-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="e2c38-116">Azure portalında tıklatın **tüm kaynakları** adı yazın ve sol taraftaki menüden gibi **mypgserver 20170401**, varolan sunucunuz için aranacak.</span><span class="sxs-lookup"><span data-stu-id="e2c38-116">In the Azure portal, click **All Resources** from the left-hand menu and type in the name, such as **mypgserver-20170401**, to search for your existing server.</span></span> <span data-ttu-id="e2c38-117">Arama sonucunda listelenen sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e2c38-117">Click the server name listed in the search result.</span></span> <span data-ttu-id="e2c38-118">Sunucunuzun **Genel bakış** sayfası açılır ve daha fazla yapılandırma seçenekleri sunulur.</span><span class="sxs-lookup"><span data-stu-id="e2c38-118">The **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Azure portal - sunucunuz bulmak için arama](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="e2c38-120">Sunucu genel bakış dikey üst kısmında tıklayın **geri** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="e2c38-120">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="e2c38-121">Geri yükleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="e2c38-121">The Restore blade opens.</span></span>

   ![Azure veritabanı için PostgreSQL - genel bakış - Geri Yükle düğmesi](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="e2c38-123">Gerekli bilgileri geri yükleme formu doldurun:</span><span class="sxs-lookup"><span data-stu-id="e2c38-123">Fill out the Restore form with the required information:</span></span>

   ![<span data-ttu-id="e2c38-124">Azure veritabanı PostgreSQL - geri yüklemesi bilgi için</span><span class="sxs-lookup"><span data-stu-id="e2c38-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="e2c38-125">**Geri yükleme noktası**: bir nokta sunucu değiştirilmeden önce oluşan zaman seçin</span><span class="sxs-lookup"><span data-stu-id="e2c38-125">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="e2c38-126">**Hedef sunucu**: geri yüklemek istediğiniz yeni bir sunucu adı sağlayın</span><span class="sxs-lookup"><span data-stu-id="e2c38-126">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="e2c38-127">**Konum**: bölge seçemezsiniz, varsayılan olarak kaynak sunucuyla aynı.</span><span class="sxs-lookup"><span data-stu-id="e2c38-127">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="e2c38-128">**Fiyatlandırma katmanı**: bir sunucu geri yüklerken bu değer değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="e2c38-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="e2c38-129">Kaynak sunucu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="e2c38-129">It is same as the source server.</span></span> 

5. <span data-ttu-id="e2c38-130">Tıklatın **Tamam** zaman içinde bir noktaya geri yüklemenizi sunucuyu geri yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="e2c38-130">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="e2c38-131">Geri yükleme tamamlandıktan sonra verilerin beklenen şekilde geri doğrulamak için oluşturulan yeni sunucu bulun.</span><span class="sxs-lookup"><span data-stu-id="e2c38-131">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2c38-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e2c38-132">Next steps</span></span>
- [<span data-ttu-id="e2c38-133">Azure veritabanı PostgreSQL için için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="e2c38-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
