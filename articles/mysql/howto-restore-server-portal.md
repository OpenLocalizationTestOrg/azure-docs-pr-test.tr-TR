---
title: "aaaHow tooRestore Azure veritabanı için MySQL Server'da | Microsoft Docs"
description: "Bu makalede nasıl toorestore MySQL kullanmak için bir sunucu Azure veritabanındaki hello Azure portalı."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="cbf6e-103">Azure portal tooBackup ve geri yükleme MySQL kullanmak için bir sunucu Azure veritabanında nasıl hello</span><span class="sxs-lookup"><span data-stu-id="cbf6e-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="cbf6e-104">Yedekleme otomatik olarak gerçekleşir</span><span class="sxs-lookup"><span data-stu-id="cbf6e-104">Backup happens Automatically</span></span>
<span data-ttu-id="cbf6e-105">Azure veritabanı için MySQL kullanırken, hello veritabanı hizmeti hello hizmet yedeğini her 5 dakikada bir otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="cbf6e-106">Temel katman ve 35 gün kullanırken Hello yedeklemeler 7 gün boyunca kullanılabilir standart katmanı kullanırken.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="cbf6e-107">Daha fazla bilgi için bkz: [Azure veritabanı için MySQL hizmet katmanları](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="cbf6e-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="cbf6e-108">Bu otomatik yedekleme özelliğini kullanarak, hello server ve tüm veritabanlarının bir yeni sunucu tooan önceki zaman içinde nokta geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="cbf6e-109">Hello Azure portalına geri yükleme</span><span class="sxs-lookup"><span data-stu-id="cbf6e-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="cbf6e-110">Azure veritabanı MySQL için saat ve yeni bir kopyasını tooa hello sunucusunun toorestore hello sunucusu geri tooa noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="cbf6e-111">Bu yeni sunucu toorecover verilerinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="cbf6e-112">Örneğin, bir tablo yanlışlıkla olduysa bugün öğlen bırakılan, toohello zaman öğlen hemen önce geri ve tablo ve bu kopyasını hello sunucu verilerinden eksik hello alın.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="cbf6e-113">Merhaba aşağıdaki adımları hello örnek sunucu tooa sürede geri yükleme noktası:</span><span class="sxs-lookup"><span data-stu-id="cbf6e-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="cbf6e-114">Merhaba içine oturum [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="cbf6e-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="cbf6e-115">MySQL sunucusu için Azure veritabanınızı bulun.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="cbf6e-116">Merhaba sol bölmesinde seçin **tüm kaynakları**, ardından hello listesinden sunucunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="cbf6e-117">Hello sunucu genel bakış dikey penceresinde Hello üstte tıklatın **geri** hello araç.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="cbf6e-118">Merhaba geri yükleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-118">hello Restore blade opens.</span></span>
<span data-ttu-id="cbf6e-119">![Geri düğmesini tıklatın](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="cbf6e-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="cbf6e-120">Merhaba geri yükleme formu hello gerekli bilgilerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="cbf6e-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="cbf6e-121">**Geri yükleme noktası (UTC)**: hello Tarih Seçici ve Saat Seçici kullanarak, bir zaman içinde nokta toorestore seçin.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="cbf6e-122">Belirtilen başlangıç saati UTC biçiminde kitabıdır tooconvert hello yerel saati UTC gerekmesi muhtemeldir.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="cbf6e-123">**Toonew sunucuyu geri**: yeni bir sunucu adı toorestore hello varolan Server'a sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="cbf6e-124">**Konum**: hello bölge seçim otomatik olarak hello kaynak sunucu bölge ile doldurur ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="cbf6e-125">**Fiyatlandırma katmanı**: katmanı seçimi otomatik olarak fiyatlandırma hello aynı fiyatlandırma katmanı hello kaynak sunucu ve burada değiştirilemez hello ile doldurur.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="cbf6e-126">![PITR geri yükleme](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="cbf6e-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="cbf6e-127">Tıklatın **Tamam** toorestore hello sunucu toorestore tooa bir noktaya.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="cbf6e-128">Merhaba geri yükleme tamamlandıktan sonra veritabanları beklendiği gibi yüklendi tooverify hello oluşturulmuş yeni bir sunucu hello bulun.</span><span class="sxs-lookup"><span data-stu-id="cbf6e-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbf6e-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cbf6e-129">Next steps</span></span>
- [<span data-ttu-id="cbf6e-130">MySQL için Azure veritabanı için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="cbf6e-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)