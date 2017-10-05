---
title: "MySQL için Azure veritabanı bir sunucuya geri yükleme | Microsoft Docs"
description: "Bu makalede, Azure portalını kullanarak MySQL için Azure veritabanındaki bir sunucuyu geri yüklemek açıklar."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="9c83b-103">Yedekleme ve MySQL için Azure portalını kullanarak Azure veritabanı bir sunucuya geri yükleme</span><span class="sxs-lookup"><span data-stu-id="9c83b-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="9c83b-104">Yedekleme otomatik olarak gerçekleşir</span><span class="sxs-lookup"><span data-stu-id="9c83b-104">Backup happens Automatically</span></span>
<span data-ttu-id="9c83b-105">Azure veritabanı için MySQL kullanırken, veritabanı hizmeti yedekleme hizmetinin her 5 dakikada bir otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="9c83b-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="9c83b-106">Temel katman ve 35 gün kullanırken yedeklemeler 7 gün için kullanılabilir olan standart katmanı kullanırken.</span><span class="sxs-lookup"><span data-stu-id="9c83b-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="9c83b-107">Daha fazla bilgi için bkz: [Azure veritabanı için MySQL hizmet katmanları](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="9c83b-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="9c83b-108">Bu otomatik yedekleme özelliğini kullanarak, sunucu ve tüm veritabanlarını içine bir önceki noktası zaman içinde yeni bir sunucuya geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c83b-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="9c83b-109">Azure portalında geri yükleme</span><span class="sxs-lookup"><span data-stu-id="9c83b-109">Restore in the Azure portal</span></span>
<span data-ttu-id="9c83b-110">Azure veritabanı için MySQL sağlar, sunucu saati ve içine bir noktaya geri geri yüklemek sunucu yeni bir kopyasını için.</span><span class="sxs-lookup"><span data-stu-id="9c83b-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="9c83b-111">Bu yeni sunucu verilerinizi kurtarmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c83b-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="9c83b-112">Örneğin, bir tablo yanlışlıkla varsa bugün öğlen bırakılan, zaman öğlen hemen önce geri yükleme ve bu sunucunun yeni kopyadan eksik tablo ve veri almak.</span><span class="sxs-lookup"><span data-stu-id="9c83b-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="9c83b-113">Aşağıdaki adımları örnek sunucunun saat içinde bir noktaya geri:</span><span class="sxs-lookup"><span data-stu-id="9c83b-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="9c83b-114">Oturum [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9c83b-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="9c83b-115">MySQL sunucusu için Azure veritabanınızı bulun.</span><span class="sxs-lookup"><span data-stu-id="9c83b-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="9c83b-116">Sol bölmede seçin **tüm kaynakları**, ardından listeden sunucunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="9c83b-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="9c83b-117">Sunucu genel bakış dikey üst kısmında tıklayın **geri** araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="9c83b-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="9c83b-118">Geri yükleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="9c83b-118">The Restore blade opens.</span></span>
<span data-ttu-id="9c83b-119">![Geri düğmesini tıklatın](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="9c83b-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="9c83b-120">Gerekli bilgileri geri yükleme formu doldurun:</span><span class="sxs-lookup"><span data-stu-id="9c83b-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="9c83b-121">**Geri yükleme noktası (UTC)**: Tarih Seçici ve Saat Seçici kullanarak bir noktası geri yüklemek için zaman içinde seçin.</span><span class="sxs-lookup"><span data-stu-id="9c83b-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="9c83b-122">Belirtilen süre UTC biçiminde kitabıdır olasılıkla yerel saati UTC dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c83b-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="9c83b-123">**Yeni bir sunucuya geri**: var olan sunucuya geri yüklemek için yeni bir sunucu adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9c83b-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="9c83b-124">**Konum**: bölge seçimi otomatik olarak kaynak sunucu bölge ile doldurur ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="9c83b-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="9c83b-125">**Fiyatlandırma katmanı**: fiyatlandırma katmanı seçimi otomatik olarak kaynak sunucuyla aynı fiyatlandırma katmanı doldurur ve burada değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="9c83b-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="9c83b-126">![PITR geri yükleme](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="9c83b-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="9c83b-127">Tıklatın **Tamam** zaman içinde bir noktaya geri yüklemenizi sunucuyu geri yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="9c83b-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="9c83b-128">Geri yükleme tamamlandıktan sonra veritabanları beklendiği gibi yüklendi doğrulamak için oluşturulan yeni sunucu bulun.</span><span class="sxs-lookup"><span data-stu-id="9c83b-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c83b-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c83b-129">Next steps</span></span>
- [<span data-ttu-id="9c83b-130">MySQL için Azure veritabanı için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="9c83b-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)