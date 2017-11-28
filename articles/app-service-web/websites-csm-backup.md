---
title: "aaaUse yukarı tooback tutun ve App Service uygulamalarının geri yükleme"
description: "Nasıl tooback toouse RESTful API'si çağıran öğrenin ve Azure App Service'te bir uygulama geri yükleme"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="beb72-103">REST tooback kullanır ve App Service uygulamalarının geri yükleme</span><span class="sxs-lookup"><span data-stu-id="beb72-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="beb72-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="beb72-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="beb72-105">REST API</span><span class="sxs-lookup"><span data-stu-id="beb72-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="beb72-106">[App Service uygulamalarının](https://azure.microsoft.com/services/app-service/web/) bloblar olarak Azure storage'da yedeklenebilir.</span><span class="sxs-lookup"><span data-stu-id="beb72-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="beb72-107">Merhaba yedekleme hello uygulamanın veritabanları de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="beb72-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="beb72-108">Merhaba uygulama herhangi bir zamanda yanlışlıkla silinirse veya hello uygulama gereksinimlerini toobe tooa önceki sürüme geri döndürüldü, önceki bir yedeklemeden geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="beb72-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="beb72-109">İsteğe bağlı herhangi bir zamanda yedeklemeler yapılabilir veya yedeklemeleri uygun aralıklarla zamanlanabilir.</span><span class="sxs-lookup"><span data-stu-id="beb72-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="beb72-110">Bu makalede uygulamayı RESTful API'si ile nasıl toobackup ve geri yükleme istekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="beb72-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="beb72-111">İster toocreate ve uygulama yedeklemeleri grafik hello Azure portal aracılığıyla yönetmeniz, bkz: [Azure App Service'in web uygulamasında yedekleyin](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="beb72-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="beb72-112">Başlarken</span><span class="sxs-lookup"><span data-stu-id="beb72-112">Getting Started</span></span>
<span data-ttu-id="beb72-113">toosend REST istekleri, uygulamanızın tooknow gerek **adı**, **kaynak grubu**, ve **abonelik kimliği**. Bu bilgiler uygulamanıza hello tıklayarak bulunabilir **uygulama hizmeti** hello dikey [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="beb72-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="beb72-114">Bu makalede Hello örnekler için biz hello Web sitesi yapılandırmakta olduğunuz **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="beb72-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="beb72-115">Merhaba varsayılan Web WestUS kaynak grubunda depolanır ve hello kimliği 00001111-2222-3333-4444-555566667777 abonelikle çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="beb72-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![Örnek Web sitesi bilgileri][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="beb72-117">Yedekleme ve geri yükleme REST API'si</span><span class="sxs-lookup"><span data-stu-id="beb72-117">Backup and restore REST API</span></span>
<span data-ttu-id="beb72-118">Biz şimdi nasıl toouse REST API toobackup hello ve bir uygulamayı geri çeşitli örnekler ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="beb72-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="beb72-119">Her örneğin bir URL ve HTTP istek gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="beb72-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="beb72-120">Merhaba örnek URL'si {subscrıptıon-ID} gibi süslü ayraçlar sarmalanmış yer tutucular içerir.</span><span class="sxs-lookup"><span data-stu-id="beb72-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="beb72-121">Uygulamanız için hello karşılık gelen bilgilerle Hello yer tutucuları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="beb72-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="beb72-122">Başvuru için burada hello örnek URL'lerinde görüntülenen her bir yer tutucu bir açıklaması verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="beb72-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="beb72-123">Abonelik kimliği – hello Azure aboneliğini içeren hello uygulamasının kimliği</span><span class="sxs-lookup"><span data-stu-id="beb72-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="beb72-124">kaynak-grubu-adı – hello kaynak grubu içeren hello uygulaması adı</span><span class="sxs-lookup"><span data-stu-id="beb72-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="beb72-125">adı – hello uygulamasının adı</span><span class="sxs-lookup"><span data-stu-id="beb72-125">name – Name of hello app</span></span>
* <span data-ttu-id="beb72-126">Yedekleme-id – hello uygulama yedekleme kimliği</span><span class="sxs-lookup"><span data-stu-id="beb72-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="beb72-127">Merhaba kapsamlı belgeler hello API için hello bkz hello HTTP isteğine dahil birkaç isteğe bağlı parametreleri de dahil olmak üzere [Azure kaynak Gezgini](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="beb72-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="beb72-128">İsteğe bağlı bir uygulama yedekleme</span><span class="sxs-lookup"><span data-stu-id="beb72-128">Backup an app on demand</span></span>
<span data-ttu-id="beb72-129">bir uygulama yukarı tooback hemen gönder bir **POST** çok istek**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Yedekleme /**.</span><span class="sxs-lookup"><span data-stu-id="beb72-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="beb72-130">Bizim örnek Web sitesini kullanarak gibi hello URL göründüğünü aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="beb72-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="beb72-131">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backup/**</span><span class="sxs-lookup"><span data-stu-id="beb72-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="beb72-132">Hangi depolama hesabı toouse toostore hello yedekleme, istek toospecify hello gövdesinde bir JSON nesnesi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="beb72-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="beb72-133">Merhaba JSON nesnesi adlı bir özellik olması gerekir **storageAccountUrl**, hangi ayrı tutma bir [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello yedekleme blob tutan yazma erişimi toohello Azure depolama kapsayıcısının verme.</span><span class="sxs-lookup"><span data-stu-id="beb72-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="beb72-134">Veritabanlarınızı tooback istiyorsanız hello adlar, türler ve yedeklenen hello veritabanları toobe bağlantı dizeleri içeren bir liste sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="beb72-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="beb72-135">Hemen hello isteği alındığında hello uygulama yedeğini başlar.</span><span class="sxs-lookup"><span data-stu-id="beb72-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="beb72-136">Merhaba Yedekleme işleminin uzun süre toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="beb72-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="beb72-137">Hello HTTP yanıtı başka bir istek toosee hello durumunu hello yedekleme kullanabileceğiniz bir kimlik içeriyor.</span><span class="sxs-lookup"><span data-stu-id="beb72-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="beb72-138">Merhaba hello HTTP yanıt tooour yedekleme istek gövdesi bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="beb72-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="beb72-139">Hata iletileri hello günlük özelliği hello HTTP yanıtı içinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="beb72-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="beb72-140">Otomatik yedeklemeler zamanlama</span><span class="sxs-lookup"><span data-stu-id="beb72-140">Schedule automatic backups</span></span>
<span data-ttu-id="beb72-141">İsteğe bağlı bir uygulama yukarı toplama toobacking içinde de Yedekleme toohappen otomatik olarak zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="beb72-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="beb72-142">Yeni bir otomatik yedekleme zamanlama ayarlamak</span><span class="sxs-lookup"><span data-stu-id="beb72-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="beb72-143">bir yedekleme zamanlaması yukarı tooset Gönder bir **PUT** çok istek**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / Yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="beb72-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="beb72-144">İşte ne hello URL bizim örnek Web sitesi için benzer.</span><span class="sxs-lookup"><span data-stu-id="beb72-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="beb72-145">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/config/Backup**</span><span class="sxs-lookup"><span data-stu-id="beb72-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="beb72-146">Merhaba istek gövdesi hello yedekleme yapılandırmasını belirten bir JSON nesnesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="beb72-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="beb72-147">Burada, tüm gerekli hello parametrelere sahip bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="beb72-147">Here is an example with all hello required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="beb72-148">Bu örnek yedi günde bir otomatik olarak yedeklenir hello uygulama toobe yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="beb72-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="beb72-149">Merhaba parametreleri **frequencyInterval** ve **frequencyUnit** birlikte ne sıklıkta hello yedeklemeleri durum belirler.</span><span class="sxs-lookup"><span data-stu-id="beb72-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="beb72-150">İçin geçerli değerler **frequencyUnit** olan **saat** ve **gün**.</span><span class="sxs-lookup"><span data-stu-id="beb72-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="beb72-151">Örneğin, bir uygulama her 12 saatte yukarı tooback frequencyInterval too12 ve frequencyUnit toohour ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="beb72-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="beb72-152">Eski yedeklemeleri hello depolama hesabından otomatik olarak kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="beb72-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="beb72-153">Yedekleme ayarı hello tarafından olabilir ne kadar eski hello denetleyebilirsiniz **retentionPeriodInDays** parametresi.</span><span class="sxs-lookup"><span data-stu-id="beb72-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="beb72-154">Tooalways sahip kaydedildi, ne kadar eski ayarlanır bağımsız olarak en az bir yedekleme istiyorsanız **keepAtLeastOneBackup** tootrue.</span><span class="sxs-lookup"><span data-stu-id="beb72-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="beb72-155">Merhaba otomatik yedekleme zamanlamasını almak</span><span class="sxs-lookup"><span data-stu-id="beb72-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="beb72-156">tooget bir uygulamaya ait yedekleme yapılandırması, Gönder bir **POST** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ siteleri / {ad} / yedekleme/config/listesi**.</span><span class="sxs-lookup"><span data-stu-id="beb72-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="beb72-157">Bizim örnek site Hello URL'si **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="beb72-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="beb72-158">Bir yedekleme Hello durumunu Al</span><span class="sxs-lookup"><span data-stu-id="beb72-158">Get hello status of a backup</span></span>
<span data-ttu-id="beb72-159">Ne kadar büyük hello uygulamaya bağlı olarak olduğundan, bir yedek alabilir toocomplete.</span><span class="sxs-lookup"><span data-stu-id="beb72-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="beb72-160">Yedeklemeler de başarısız, zaman aşımı veya kısmen başarılı olabilir.</span><span class="sxs-lookup"><span data-stu-id="beb72-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="beb72-161">bir uygulamanın tüm yedeklemeler, toosee hello durumunu Gönder bir **almak** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscrıptıon-ID} /resourceGroups/ {kaynak grubu adı} /providers/ Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="beb72-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="beb72-162">belirli bir yedekleme toosee hello durumu bir GET isteği toohello URL Gönder **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { Yedekleme-id}**.</span><span class="sxs-lookup"><span data-stu-id="beb72-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="beb72-163">İşte ne hello URL bizim örnek Web sitesi için benzer.</span><span class="sxs-lookup"><span data-stu-id="beb72-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="beb72-164">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**</span><span class="sxs-lookup"><span data-stu-id="beb72-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="beb72-165">Merhaba yanıt gövdesi bir JSON nesnesi benzer toothis örneği içerir.</span><span class="sxs-lookup"><span data-stu-id="beb72-165">hello response body contains a JSON object similar toothis example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="beb72-166">bir yedekleme Hello durumunu numaralandırılmış bir türüdür.</span><span class="sxs-lookup"><span data-stu-id="beb72-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="beb72-167">Aşağıda, her olası durum verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="beb72-167">Here is every possible state.</span></span>

* <span data-ttu-id="beb72-168">0 – devam ediyor: hello yedekleme başlatıldı ancak henüz tamamlanmadı.</span><span class="sxs-lookup"><span data-stu-id="beb72-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="beb72-169">1 – başarısız oldu: hello yedekleme başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="beb72-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="beb72-170">2 – başarılı oldu: Yedekleme başarıyla tamamlandı hello.</span><span class="sxs-lookup"><span data-stu-id="beb72-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="beb72-171">3 – süresi sona erdi: hello yedekleme sürede tamamlanmadı ve iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="beb72-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="beb72-172">4 – oluşturulan: hello yedekleme isteği sıraya alındı, ancak başlatılmadı.</span><span class="sxs-lookup"><span data-stu-id="beb72-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="beb72-173">5 – atlandı: hello yedekleme tooa zamanlama çok fazla yedekleme tetikleme devam.</span><span class="sxs-lookup"><span data-stu-id="beb72-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="beb72-174">6-kısmen başarılı: hello yedekleme başarılı oldu ancak bunlar okunamıyor çünkü bazı dosyaları yedeklenmedi.</span><span class="sxs-lookup"><span data-stu-id="beb72-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="beb72-175">Bu, genellikle özel bir kilit hello dosyalarda yerleştirilen çünkü gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="beb72-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="beb72-176">7-DeleteInProgress: hello yedekleme silinmiş istenen toobe olmuştur, ancak henüz silinmediğini.</span><span class="sxs-lookup"><span data-stu-id="beb72-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="beb72-177">8 – DeleteFailed: hello yedekleme silinemedi.</span><span class="sxs-lookup"><span data-stu-id="beb72-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="beb72-178">Merhaba kullanılan toocreate hello yedekleme SAS URL süresi dolduğundan bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="beb72-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="beb72-179">9 – silindi: hello Yedekleme başarıyla silindi.</span><span class="sxs-lookup"><span data-stu-id="beb72-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="beb72-180">Bir uygulama bir yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="beb72-180">Restore an app from a backup</span></span>
<span data-ttu-id="beb72-181">Uygulamanızı sildiyseniz ya da uygulamanın tooa önceki sürüm toorevert istiyorsanız hello uygulama bir yedekten geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="beb72-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="beb72-182">bir geri yükleme tooinvoke Gönder bir **POST** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Yedekleme / {yedekleme-id} / geri yükle**.</span><span class="sxs-lookup"><span data-stu-id="beb72-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="beb72-183">İşte ne hello URL bizim örnek Web sitesi için benzer.</span><span class="sxs-lookup"><span data-stu-id="beb72-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="beb72-184">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/Restore**</span><span class="sxs-lookup"><span data-stu-id="beb72-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="beb72-185">Merhaba istek gövdesinde hello geri yükleme işlemi hello özelliklerini içeren bir JSON nesnesi gönderin.</span><span class="sxs-lookup"><span data-stu-id="beb72-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="beb72-186">Aşağıda, tüm gerekli özellikleri içeren bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="beb72-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="beb72-187">Yeni uygulama tooa geri yükleme</span><span class="sxs-lookup"><span data-stu-id="beb72-187">Restore tooa new app</span></span>
<span data-ttu-id="beb72-188">Bazı durumlarda zaten mevcut bir uygulamayı üzerine yerine, bir yedekleme geri yüklediğinizde toocreate yeni bir uygulama isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="beb72-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="beb72-189">toodo toocreate istediğiniz ve hello değiştirin Bu, değişiklik hello istek URL'si toopoint toohello yeni uygulama **üzerine** özelliğinde hello JSON çok**false**.</span><span class="sxs-lookup"><span data-stu-id="beb72-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="beb72-190">Bir uygulama yedek Sil</span><span class="sxs-lookup"><span data-stu-id="beb72-190">Delete an app backup</span></span>
<span data-ttu-id="beb72-191">Toodelete yedekleme isterseniz Gönder bir **silmek** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ siteleri / {{kimliği yedekleme} /backups/ adı}**.</span><span class="sxs-lookup"><span data-stu-id="beb72-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="beb72-192">İşte ne hello URL bizim örnek Web sitesi için benzer.</span><span class="sxs-lookup"><span data-stu-id="beb72-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="beb72-193">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**</span><span class="sxs-lookup"><span data-stu-id="beb72-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="beb72-194">Bir yedeğin SAS URL yönetme</span><span class="sxs-lookup"><span data-stu-id="beb72-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="beb72-195">Azure uygulama hizmeti Azure Storage hello hello yedekleme oluşturulduğunda, sağlanan SAS URL kullanarak yedekleme toodelete dener.</span><span class="sxs-lookup"><span data-stu-id="beb72-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="beb72-196">Bu SAS URL artık geçerli değilse hello yedekleme hello REST API silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="beb72-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="beb72-197">Ancak, SAS URL'si göndererek yedekleme ile ilişkili hello güncelleştirebilirsiniz bir **POST** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscrıptıon-ID} /resourceGroups/ {kaynak grubu adı} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="beb72-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="beb72-198">İşte ne hello URL bizim örnek Web sitesi için benzer.</span><span class="sxs-lookup"><span data-stu-id="beb72-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="beb72-199">**https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/List**</span><span class="sxs-lookup"><span data-stu-id="beb72-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="beb72-200">Merhaba istek gövdesinde hello yeni SAS URL'si içeren bir JSON nesnesi gönderin.</span><span class="sxs-lookup"><span data-stu-id="beb72-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="beb72-201">Bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="beb72-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="beb72-202">Güvenlik nedenleriyle, belirli bir yedekleme için bir GET isteği gönderirken, SAS URL'si yedekleme ile ilişkili hello döndürülmez.</span><span class="sxs-lookup"><span data-stu-id="beb72-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="beb72-203">SAS URL bir yedekleme ile ilişkili tooview hello isterseniz, bir POST isteği toohello gönderin yukarıdaki aynı URL.</span><span class="sxs-lookup"><span data-stu-id="beb72-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="beb72-204">Boş bir JSON nesnesi hello istek gövdesinde içerir.</span><span class="sxs-lookup"><span data-stu-id="beb72-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="beb72-205">Merhaba sunucusundan Hello yanıt SAS URL'SİNİN dahil olmak üzere bu yedeğin bilgilerin tümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="beb72-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
