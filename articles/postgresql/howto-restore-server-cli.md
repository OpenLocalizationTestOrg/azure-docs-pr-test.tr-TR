---
title: "Nasıl tooback ayarlama ve Azure veritabanındaki bir sunucu için PostgreSQL geri | Microsoft Docs"
description: "Azure CLI tooback yukarı ve kullanarak Azure veritabanındaki bir sunucu için geri PostgreSQL nasıl hello öğrenin."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="3b102-103">Azure CLI tooback yukarı ve kullanarak Azure veritabanındaki bir sunucu için geri PostgreSQL nasıl hello</span><span class="sxs-lookup"><span data-stu-id="3b102-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="3b102-104">Azure veritabanı sunucusu veritabanı tooan PostgreSQL toorestore için 7 too35 günden yayılan önceki tarih kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b102-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b102-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3b102-105">Prerequisites</span></span>
<span data-ttu-id="3b102-106">toocomplete bu nasıl-tooguide, gerekir:</span><span class="sxs-lookup"><span data-stu-id="3b102-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="3b102-107">Bir [PostgreSQL sunucu ve veritabanı için Azure veritabanı](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3b102-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="3b102-108">Yükleme ve yerel olarak hello Azure CLI kullanıyorsanız, bu nasıl tooguide Azure CLI Sürüm 2.0 veya üstü kullanmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3b102-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="3b102-109">hello Azure CLI komut isteminde tooconfirm hello sürümü girin `az --version`.</span><span class="sxs-lookup"><span data-stu-id="3b102-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="3b102-110">bkz: tooinstall veya yükseltme, [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3b102-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="3b102-111">Yedekleme otomatik olarak gerçekleşir</span><span class="sxs-lookup"><span data-stu-id="3b102-111">Back up happens automatically</span></span>
<span data-ttu-id="3b102-112">Azure veritabanı için PostgreSQL kullandığınızda, hello veritabanı hizmeti hello hizmet yedeğini her 5 dakikada bir otomatik olarak yapar.</span><span class="sxs-lookup"><span data-stu-id="3b102-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="3b102-113">Temel katman için hello yedeklemeler 7 gün için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3b102-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="3b102-114">Standart katmanı için hello yedeklemeleri 35 gün için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3b102-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="3b102-115">Daha fazla bilgi için bkz: [Azure veritabanı fiyatlandırma katmanlarına PostgreSQL için](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="3b102-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="3b102-116">Bu otomatik yedekleme özelliği ile Merhaba sunucusu ve onun veritabanları tooan önceki tarih geri yükleyin veya zaman.</span><span class="sxs-lookup"><span data-stu-id="3b102-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="3b102-117">Bir veritabanı tooa önceki süre hello Azure CLI kullanarak geri yükleme noktası</span><span class="sxs-lookup"><span data-stu-id="3b102-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="3b102-118">PostgreSQL toorestore hello sunucu tooa önceki bir noktaya için Azure Database kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b102-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="3b102-119">geri hello veri kopyalanan tooa yeni sunucu ve hello var olan sunucu olduğu gibi bırakılır.</span><span class="sxs-lookup"><span data-stu-id="3b102-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="3b102-120">Örneğin, bir tablo bugün öğlen yanlışlıkla kesilirse toohello zaman öğlen hemen önce geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b102-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="3b102-121">Ardından, tablo ve hello server geri hello kopyasını verilerinden eksik hello alabilir.</span><span class="sxs-lookup"><span data-stu-id="3b102-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="3b102-122">toorestore hello sunucu, kullanım hello Azure CLI [az postgres server geri](/cli/azure/postgres/server#restore) komutu.</span><span class="sxs-lookup"><span data-stu-id="3b102-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="3b102-123">Merhaba geri yükleme komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3b102-123">Run hello restore command</span></span>

<span data-ttu-id="3b102-124">hello Azure CLI komut isteminde toorestore hello sunucusu hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="3b102-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="3b102-125">Merhaba `az postgres server restore` komutu şu parametreler hello gerektirir:</span><span class="sxs-lookup"><span data-stu-id="3b102-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="3b102-126">Ayar</span><span class="sxs-lookup"><span data-stu-id="3b102-126">Setting</span></span> | <span data-ttu-id="3b102-127">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="3b102-127">Suggested value</span></span> | <span data-ttu-id="3b102-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3b102-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="3b102-129">kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="3b102-129">resource-group</span></span> |  <span data-ttu-id="3b102-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b102-130">myResourceGroup</span></span> |  <span data-ttu-id="3b102-131">Merhaba kaynak sunucunun bulunduğu kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="3b102-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="3b102-132">ad</span><span class="sxs-lookup"><span data-stu-id="3b102-132">name</span></span> | <span data-ttu-id="3b102-133">mypgserver geri</span><span class="sxs-lookup"><span data-stu-id="3b102-133">mypgserver-restored</span></span> | <span data-ttu-id="3b102-134">Merhaba geri yükleme komutu tarafından oluşturulan yeni bir sunucu hello Hello adı.</span><span class="sxs-lookup"><span data-stu-id="3b102-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="3b102-135">zaman içinde geri yükleme noktası</span><span class="sxs-lookup"><span data-stu-id="3b102-135">restore-point-in-time</span></span> | <span data-ttu-id="3b102-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="3b102-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="3b102-137">Zaman toorestore bir nokta seçin.</span><span class="sxs-lookup"><span data-stu-id="3b102-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="3b102-138">Bu tarih ve saat hello kaynak sunucunun yedekleme saklama dönemi içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3b102-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="3b102-139">Merhaba ISO8601 tarih ve saat biçimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b102-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="3b102-140">Örneğin, kendi yerel saat dilimi gibi kullanabilir `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="3b102-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="3b102-141">Örneğin, UTC Zulu dili biçiminde hello de kullanabilirsiniz `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="3b102-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="3b102-142">Kaynak sunucusu</span><span class="sxs-lookup"><span data-stu-id="3b102-142">source-server</span></span> | <span data-ttu-id="3b102-143">mypgserver 20170401</span><span class="sxs-lookup"><span data-stu-id="3b102-143">mypgserver-20170401</span></span> | <span data-ttu-id="3b102-144">Merhaba adı veya hello kaynak sunucu toorestore kimliği.</span><span class="sxs-lookup"><span data-stu-id="3b102-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="3b102-145">Bir sunucu tooan geri önceki bir noktaya, yeni bir sunucu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3b102-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="3b102-146">Merhaba özgün sunucusu ve onun hello veritabanlarından zaman içinde nokta kopyalanan toohello yeni sunucu belirtilir.</span><span class="sxs-lookup"><span data-stu-id="3b102-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="3b102-147">geri hello sunucu kalması için hello konum ve fiyatlandırma katmanı değerlerini aynı hello özgün sunucusu olarak hello.</span><span class="sxs-lookup"><span data-stu-id="3b102-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="3b102-148">Merhaba `az postgres server restore` komut zaman uyumlu olur.</span><span class="sxs-lookup"><span data-stu-id="3b102-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="3b102-149">Merhaba server geri yüklendikten sonra onu yeniden toorepeat hello işlemi için farklı bir noktaya zamanında kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b102-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="3b102-150">Merhaba sonra geri yükleme işlemi tamamlandığında, hello yeni sunucu bulun ve hello veri beklendiği gibi geri yüklendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3b102-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b102-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3b102-151">Next steps</span></span>
[<span data-ttu-id="3b102-152">Azure veritabanı PostgreSQL için için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="3b102-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
