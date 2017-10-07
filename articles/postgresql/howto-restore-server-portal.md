---
title: "Nasıl tooRestore PostgreSQL için Azure veritabanında bir sunucu | Microsoft Docs"
description: "Bu makalede nasıl toorestore PostgreSQL kullanmak için bir sunucu Azure veritabanındaki hello Azure portalı."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="10a63-103">Azure portal tooBackup ve geri yükleme PostgreSQL kullanmak için bir sunucu Azure veritabanında nasıl hello</span><span class="sxs-lookup"><span data-stu-id="10a63-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="10a63-104">Yedekleme otomatik olarak gerçekleşir</span><span class="sxs-lookup"><span data-stu-id="10a63-104">Backup happens Automatically</span></span>
<span data-ttu-id="10a63-105">Azure veritabanı için PostgreSQL kullanırken, hello veritabanı hizmeti hello hizmet yedeğini her 5 dakikada bir otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="10a63-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="10a63-106">Temel katman ve 35 gün kullanırken Hello yedeklemeler 7 gün boyunca kullanılabilir standart katmanı kullanırken.</span><span class="sxs-lookup"><span data-stu-id="10a63-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="10a63-107">Daha fazla bilgi için bkz: [PostgreSQL hizmet katmanları için Azure veritabanı](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="10a63-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="10a63-108">Bu otomatik yedekleme özelliğini kullanarak, hello server ve tüm veritabanlarının bir yeni sunucu tooan önceki zaman içinde nokta geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10a63-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="10a63-109">Hello Azure portalına geri yükleme</span><span class="sxs-lookup"><span data-stu-id="10a63-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="10a63-110">Azure veritabanı PostgreSQL için saat ve yeni bir kopyasını tooa hello sunucusunun toorestore hello sunucusu geri tooa noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="10a63-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="10a63-111">Bu yeni sunucu toorecover verilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10a63-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="10a63-112">Örneğin, bir tablo yanlışlıkla olduysa bugün öğlen bırakılan, toohello zaman öğlen hemen önce geri ve tablo ve bu kopyasını hello sunucu verilerinden eksik hello alın.</span><span class="sxs-lookup"><span data-stu-id="10a63-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="10a63-113">Merhaba aşağıdaki adımları hello örnek sunucu tooa sürede geri yükleme noktası:</span><span class="sxs-lookup"><span data-stu-id="10a63-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="10a63-114">Merhaba içine oturum [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="10a63-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="10a63-115">Azure veritabanınız PostgreSQL sunucu için bulun.</span><span class="sxs-lookup"><span data-stu-id="10a63-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="10a63-116">Hello Azure portal'ı tıklatın **tüm kaynakları** hello sol menüsünden ve hello adı yazın gibi **mypgserver 20170401**, varolan sunucunuz için toosearch.</span><span class="sxs-lookup"><span data-stu-id="10a63-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="10a63-117">Merhaba arama sonucunda listelenen hello sunucu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="10a63-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="10a63-118">Merhaba **genel bakış** sayfası sunucunuz açar ve ek yapılandırma seçeneklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="10a63-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Azure portal - sunucunuz toolocate arama](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="10a63-120">Hello sunucu genel bakış dikey penceresinde Hello üstte tıklatın **geri** hello araç.</span><span class="sxs-lookup"><span data-stu-id="10a63-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="10a63-121">Merhaba geri yükleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="10a63-121">hello Restore blade opens.</span></span>

   ![Azure veritabanı için PostgreSQL - genel bakış - Geri Yükle düğmesi](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="10a63-123">Merhaba geri yükleme formu hello gerekli bilgilerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="10a63-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="10a63-124">Azure veritabanı PostgreSQL - geri yüklemesi bilgi için</span><span class="sxs-lookup"><span data-stu-id="10a63-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="10a63-125">**Geri yükleme noktası**: bir noktası hello sunucu değiştirilmeden önce oluşan zaman seçin</span><span class="sxs-lookup"><span data-stu-id="10a63-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="10a63-126">**Hedef sunucu**: toorestore için istediğiniz yeni bir sunucu adı sağlayın</span><span class="sxs-lookup"><span data-stu-id="10a63-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="10a63-127">**Konum**: hello bölge seçemezsiniz, varsayılan olarak hello kaynak sunucu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="10a63-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="10a63-128">**Fiyatlandırma katmanı**: bir sunucu geri yüklerken bu değer değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="10a63-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="10a63-129">Merhaba kaynak sunucu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="10a63-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="10a63-130">Tıklatın **Tamam** toorestore hello sunucu toorestore tooa bir noktaya.</span><span class="sxs-lookup"><span data-stu-id="10a63-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="10a63-131">Merhaba geri yükleme tamamlandıktan sonra verilerin beklenen şekilde geri tooverify hello oluşturulan yeni bir sunucu hello bulun.</span><span class="sxs-lookup"><span data-stu-id="10a63-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10a63-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="10a63-132">Next steps</span></span>
- [<span data-ttu-id="10a63-133">Azure veritabanı PostgreSQL için için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="10a63-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
