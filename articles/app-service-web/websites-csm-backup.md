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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>REST tooback kullanır ve App Service uygulamalarının geri yükleme
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [REST API](websites-csm-backup.md)
> 
> 

[App Service uygulamalarının](https://azure.microsoft.com/services/app-service/web/) bloblar olarak Azure storage'da yedeklenebilir. Merhaba yedekleme hello uygulamanın veritabanları de içerebilir. Merhaba uygulama herhangi bir zamanda yanlışlıkla silinirse veya hello uygulama gereksinimlerini toobe tooa önceki sürüme geri döndürüldü, önceki bir yedeklemeden geri yüklenebilir. İsteğe bağlı herhangi bir zamanda yedeklemeler yapılabilir veya yedeklemeleri uygun aralıklarla zamanlanabilir.

Bu makalede uygulamayı RESTful API'si ile nasıl toobackup ve geri yükleme istekleri açıklanmaktadır. İster toocreate ve uygulama yedeklemeleri grafik hello Azure portal aracılığıyla yönetmeniz, bkz: [Azure App Service'in web uygulamasında yedekleyin](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Başlarken
toosend REST istekleri, uygulamanızın tooknow gerek **adı**, **kaynak grubu**, ve **abonelik kimliği**. Bu bilgiler uygulamanıza hello tıklayarak bulunabilir **uygulama hizmeti** hello dikey [Azure portal](https://portal.azure.com). Bu makalede Hello örnekler için biz hello Web sitesi yapılandırmakta olduğunuz **backuprestoreapiexamples.azurewebsites.net**. Merhaba varsayılan Web WestUS kaynak grubunda depolanır ve hello kimliği 00001111-2222-3333-4444-555566667777 abonelikle çalışıyor.

![Örnek Web sitesi bilgileri][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>Yedekleme ve geri yükleme REST API'si
Biz şimdi nasıl toouse REST API toobackup hello ve bir uygulamayı geri çeşitli örnekler ele alınacaktır. Her örneğin bir URL ve HTTP istek gövdesi içerir. Merhaba örnek URL'si {subscrıptıon-ID} gibi süslü ayraçlar sarmalanmış yer tutucular içerir. Uygulamanız için hello karşılık gelen bilgilerle Hello yer tutucuları değiştirin. Başvuru için burada hello örnek URL'lerinde görüntülenen her bir yer tutucu bir açıklaması verilmiştir.

* Abonelik kimliği – hello Azure aboneliğini içeren hello uygulamasının kimliği
* kaynak-grubu-adı – hello kaynak grubu içeren hello uygulaması adı
* adı – hello uygulamasının adı
* Yedekleme-id – hello uygulama yedekleme kimliği

Merhaba kapsamlı belgeler hello API için hello bkz hello HTTP isteğine dahil birkaç isteğe bağlı parametreleri de dahil olmak üzere [Azure kaynak Gezgini](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>İsteğe bağlı bir uygulama yedekleme
bir uygulama yukarı tooback hemen gönder bir **POST** çok istek**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Yedekleme /**.

Bizim örnek Web sitesini kullanarak gibi hello URL göründüğünü aşağıda verilmiştir. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backup/**

Hangi depolama hesabı toouse toostore hello yedekleme, istek toospecify hello gövdesinde bir JSON nesnesi sağlayın. Merhaba JSON nesnesi adlı bir özellik olması gerekir **storageAccountUrl**, hangi ayrı tutma bir [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello yedekleme blob tutan yazma erişimi toohello Azure depolama kapsayıcısının verme. Veritabanlarınızı tooback istiyorsanız hello adlar, türler ve yedeklenen hello veritabanları toobe bağlantı dizeleri içeren bir liste sağlamanız gerekir.

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

Hemen hello isteği alındığında hello uygulama yedeğini başlar. Merhaba Yedekleme işleminin uzun süre toocomplete alabilir. Hello HTTP yanıtı başka bir istek toosee hello durumunu hello yedekleme kullanabileceğiniz bir kimlik içeriyor. Merhaba hello HTTP yanıt tooour yedekleme istek gövdesi bir örneği burada verilmiştir.

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
> Hata iletileri hello günlük özelliği hello HTTP yanıtı içinde bulunabilir.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Otomatik yedeklemeler zamanlama
İsteğe bağlı bir uygulama yukarı toplama toobacking içinde de Yedekleme toohappen otomatik olarak zamanlayabilirsiniz.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Yeni bir otomatik yedekleme zamanlama ayarlamak
bir yedekleme zamanlaması yukarı tooset Gönder bir **PUT** çok istek**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config / Yedekleme**.

İşte ne hello URL bizim örnek Web sitesi için benzer. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/config/Backup**

Merhaba istek gövdesi hello yedekleme yapılandırmasını belirten bir JSON nesnesi olmalıdır. Burada, tüm gerekli hello parametrelere sahip bir örnek verilmiştir.

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

Bu örnek yedi günde bir otomatik olarak yedeklenir hello uygulama toobe yapılandırır. Merhaba parametreleri **frequencyInterval** ve **frequencyUnit** birlikte ne sıklıkta hello yedeklemeleri durum belirler. İçin geçerli değerler **frequencyUnit** olan **saat** ve **gün**. Örneğin, bir uygulama her 12 saatte yukarı tooback frequencyInterval too12 ve frequencyUnit toohour ayarlayın.

Eski yedeklemeleri hello depolama hesabından otomatik olarak kaldırılır. Yedekleme ayarı hello tarafından olabilir ne kadar eski hello denetleyebilirsiniz **retentionPeriodInDays** parametresi. Tooalways sahip kaydedildi, ne kadar eski ayarlanır bağımsız olarak en az bir yedekleme istiyorsanız **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Merhaba otomatik yedekleme zamanlamasını almak
tooget bir uygulamaya ait yedekleme yapılandırması, Gönder bir **POST** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ siteleri / {ad} / yedekleme/config/listesi**.

Bizim örnek site Hello URL'si **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Bir yedekleme Hello durumunu Al
Ne kadar büyük hello uygulamaya bağlı olarak olduğundan, bir yedek alabilir toocomplete. Yedeklemeler de başarısız, zaman aşımı veya kısmen başarılı olabilir. bir uygulamanın tüm yedeklemeler, toosee hello durumunu Gönder bir **almak** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscrıptıon-ID} /resourceGroups/ {kaynak grubu adı} /providers/ Microsoft.Web/sites/{name}/backups**.

belirli bir yedekleme toosee hello durumu bir GET isteği toohello URL Gönder **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ { Yedekleme-id}**.

İşte ne hello URL bizim örnek Web sitesi için benzer. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**

Merhaba yanıt gövdesi bir JSON nesnesi benzer toothis örneği içerir.

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

bir yedekleme Hello durumunu numaralandırılmış bir türüdür. Aşağıda, her olası durum verilmiştir.

* 0 – devam ediyor: hello yedekleme başlatıldı ancak henüz tamamlanmadı.
* 1 – başarısız oldu: hello yedekleme başarısız oldu.
* 2 – başarılı oldu: Yedekleme başarıyla tamamlandı hello.
* 3 – süresi sona erdi: hello yedekleme sürede tamamlanmadı ve iptal edildi.
* 4 – oluşturulan: hello yedekleme isteği sıraya alındı, ancak başlatılmadı.
* 5 – atlandı: hello yedekleme tooa zamanlama çok fazla yedekleme tetikleme devam.
* 6-kısmen başarılı: hello yedekleme başarılı oldu ancak bunlar okunamıyor çünkü bazı dosyaları yedeklenmedi. Bu, genellikle özel bir kilit hello dosyalarda yerleştirilen çünkü gerçekleşir.
* 7-DeleteInProgress: hello yedekleme silinmiş istenen toobe olmuştur, ancak henüz silinmediğini.
* 8 – DeleteFailed: hello yedekleme silinemedi. Merhaba kullanılan toocreate hello yedekleme SAS URL süresi dolduğundan bu durum oluşabilir.
* 9 – silindi: hello Yedekleme başarıyla silindi.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Bir uygulama bir yedekten geri yükleyin
Uygulamanızı sildiyseniz ya da uygulamanın tooa önceki sürüm toorevert istiyorsanız hello uygulama bir yedekten geri yükleyebilirsiniz. bir geri yükleme tooinvoke Gönder bir **POST** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ Yedekleme / {yedekleme-id} / geri yükle**.

İşte ne hello URL bizim örnek Web sitesi için benzer. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/Restore**

Merhaba istek gövdesinde hello geri yükleme işlemi hello özelliklerini içeren bir JSON nesnesi gönderin. Aşağıda, tüm gerekli özellikleri içeren bir örnek verilmiştir:

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

### <a name="restore-tooa-new-app"></a>Yeni uygulama tooa geri yükleme
Bazı durumlarda zaten mevcut bir uygulamayı üzerine yerine, bir yedekleme geri yüklediğinizde toocreate yeni bir uygulama isteyebilirsiniz. toodo toocreate istediğiniz ve hello değiştirin Bu, değişiklik hello istek URL'si toopoint toohello yeni uygulama **üzerine** özelliğinde hello JSON çok**false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Bir uygulama yedek Sil
Toodelete yedekleme isterseniz Gönder bir **silmek** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ siteleri / {{kimliği yedekleme} /backups/ adı}**.

İşte ne hello URL bizim örnek Web sitesi için benzer. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Bir yedeğin SAS URL yönetme
Azure uygulama hizmeti Azure Storage hello hello yedekleme oluşturulduğunda, sağlanan SAS URL kullanarak yedekleme toodelete dener. Bu SAS URL artık geçerli değilse hello yedekleme hello REST API silinemiyor. Ancak, SAS URL'si göndererek yedekleme ile ilişkili hello güncelleştirebilirsiniz bir **POST** isteği toohello URL'si **https://management.azure.com/subscriptions/ {subscrıptıon-ID} /resourceGroups/ {kaynak grubu adı} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

İşte ne hello URL bizim örnek Web sitesi için benzer. **https://Management.Azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/Sites/backuprestoreapiexamples/Backups/1/List**

Merhaba istek gövdesinde hello yeni SAS URL'si içeren bir JSON nesnesi gönderin. Bir örnek verilmiştir.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Güvenlik nedenleriyle, belirli bir yedekleme için bir GET isteği gönderirken, SAS URL'si yedekleme ile ilişkili hello döndürülmez. SAS URL bir yedekleme ile ilişkili tooview hello isterseniz, bir POST isteği toohello gönderin yukarıdaki aynı URL. Boş bir JSON nesnesi hello istek gövdesinde içerir. Merhaba sunucusundan Hello yanıt SAS URL'SİNİN dahil olmak üzere bu yedeğin bilgilerin tümünü içerir.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
