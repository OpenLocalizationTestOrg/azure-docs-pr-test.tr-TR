---
title: "aaaLog Analytics günlük arama REST API | Microsoft Docs"
description: "Bu kılavuz hello nasıl kullanabileceğinizi tanımlayan temel bir öğretici günlük analizi REST API hello Operations Management Suite (OMS) arama yapın ve bunu nasıl yapacağınızı örnekler verilmektedir sağlar toouse hello komutları."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>Günlük analizi günlük arama REST API'si
Bu kılavuz, hello günlük analizi Search REST API'sini nasıl kullanabileceğinize dair örnekler dahil olmak üzere temel bir öğretici sağlar. Günlük analizi hello Operations Management Suite (OMS) bir parçasıdır.

> [!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra da bu makalede açıklanan toouse hello eski sorgu dili hello günlük arama API ile devam etmelidir.  Yükseltilen çalışma alanları için yeni bir API yayımlanır ve o anda hello belgeleri güncelleştirilir. 

> [!NOTE]
> Günlük analizi önceden hello kaynak sağlayıcısındaki kullanılan hello adı olmasının olan Operational Insights çağrıldı.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Merhaba günlük Search REST API'sini genel bakış
Hello günlük analizi Search REST API'sini RESTful olan ve hello Azure Kaynak Yöneticisi API'si erişilebilir. Bu makalede hello API aracılığıyla erişme örnekler [ARMClient](https://github.com/projectkudu/ARMClient), çağırma basitleştiren bir açık kaynak komut satırı aracı hello Azure Kaynak Yöneticisi API'si. ARMClient Hello kullanımını birçok seçenekleri tooaccess hello günlük analizi arama API biridir. Arama erişmek için cmdlet'leri içerir OperationalInsights için toouse hello Azure PowerShell modülü başka bir seçenektir. Bu araçları ile hello Azure Kaynak Yöneticisi API'si toomake çağrıları tooOMS çalışma alanları kullanma ve bunların içindeki arama komutları gerçekleştirin. Arama sonuçları toouse hello arama sonuçları birçok farklı yolla program aracılığıyla sağlayarak JSON biçiminde Hello API çıkarır.

Hello Azure Resource Manager aracılığıyla kullanılabilir bir [.NET kitaplığı](https://msdn.microsoft.com/library/azure/dn910477.aspx) ve hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn daha hello bağlantılı web sayfalarını gözden geçirin.

> [!NOTE]
> Gibi bir toplama komutunu kullanırsanız `|measure count()` veya `distinct`, her çağrı toosearch fazla 500.000 kayıt geri dönebilirsiniz. Bir toplama komutu dahil etmeyin aramaları fazla 5.000 kayıtları döndürür.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Temel günlük analizi Search REST API'sini Öğreticisi
### <a name="toouse-armclient"></a>toouse ARMClient
1. Yükleme [Chocolatey](https://chocolatey.org/), Windows için bir açık kaynak Paket Yöneticisi olduğu. Yönetici olarak bir komut istemi penceresi açın ve ardından hello aşağıdaki komutu çalıştırın:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. ARMClient hello aşağıdaki komutu çalıştırarak yükleyin:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>bir arama ARMClient kullanarak tooperform
1. Microsoft hesabınızı veya iş veya Okul hesabınızı kullanarak oturum açın:

    ```
    armclient login
    ```

    Başarılı oturum açma hesabı verilen tüm abonelikleri bağlı toohello listeler:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Merhaba Operations Management Suite çalışma alanları alın:

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Başarılı bir Get çağrısı tüm çalışma alanları toohello abonelik bağlı çıkış:

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Arama değişkeni oluşturun:

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Yeni arama değişkenini kullanarak ara:

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Günlük analizi arama REST API başvuru örnekleri
Örnek hello hello arama API nasıl kullanabileceğinizi gösterir.

### <a name="search---actionread"></a>Arama - eylem/okuma
**Örnek URL'si:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**İsteği:**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Aşağıdaki tablonun hello kullanılabilir hello özellikleri açıklar.

| **Özellik** | **Açıklama** |
| --- | --- |
| Sayfanın Üstü |Merhaba en fazla sonuçları tooreturn sayısı. |
| Vurgula |Eşleşen alanları vurgulamak için genellikle kullanılan öncesi ve sonrası parametreleri içerir |
| öncesi |Eşleşen tooyour alanlarına verilen hello ekler. |
| Yayınla |Eşleşen tooyour alanlarına verilen hello ekler. |
| sorgu |Merhaba arama sorgusu toocollect kullanılan ve sonuçları döndürür. |
| start |Merhaba gelen bulunan sonuçları toobe istediğiniz hello zaman penceresi başlangıcı. |
| Bitiş |Merhaba hello zaman penceresi istediğiniz sonuna gelen bulunan toobe sonuçlanır. |

**Yanıtı:**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Arama / {kimliği} - eylem/okuma
**Kayıtlı arama Merhaba içeriğine isteyin:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Merhaba arama 'Bekleyen' durumuyla döndürürse, yoklama hello güncelleştirilmiş sonuçları bu API aracılığıyla yapılabilir. 6 min sonra hello arama hello sonucu hello önbellekten bırakılacak ve HTTP gitti döndürülür. Merhaba ilk arama isteği 'Başarılı' durumunu hemen döndürürse, bu API tooreturn HTTP gitti sorgularsa neden toohello önbellek hello sonuçları eklenmedi. bir HTTP 200 sonuç Merhaba içeriğine aynı hello ilk arama isteği yalnızca güncelleştirilmiş değerlerle olarak biçimi hello arasındadır.
>
>

### <a name="saved-searches"></a>Kaydedilen aramalar
**Kaydedilmiş aramaları listesini isteyin:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Algoritmalardan: GET, PUT Sil

Koleksiyon yöntemleri desteklenir: Al

Aşağıdaki tablonun hello kullanılabilir hello özellikleri açıklar.

| Özellik | Açıklama |
| --- | --- |
| Kimlik |Merhaba benzersiz tanımlayıcısı. |
| ETag |**Düzeltme eki için gerekli**. Sunucu tarafından her yazma güncelleştirildi. Değer eşit toohello geçerli depolanan değer olmalıdır veya ' *' tooupdate. 409 eski/geçersiz değerler için döndürdü. |
| Properties.Query |**Gerekli**. Merhaba arama sorgusu. |
| properties.displayName |**Gerekli**. Merhaba sorgu Hello kullanıcı tanımlı görünen adı. |
| Properties.Category |**Gerekli**. Merhaba kullanıcı tanımlı kategori hello sorgu. |

> [!NOTE]
> Merhaba günlük analizi arama API şu anda kayıtlı bir çalışma alanında Kaydedilmiş aramaları için sorgulanan zaman aramalar kullanıcı tarafından oluşturulan döndürür. Merhaba API çözümler tarafından sağlanan Kaydedilmiş aramaları döndürmez.
>
>

### <a name="create-saved-searches"></a>Kaydedilen Aramalar oluşturun
**İsteği:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> Tüm kayıtlı aramaları, zamanlamaları ve günlük analizi API hello ile oluşturulan eylemler için Hello adı küçük olması gerekir.

### <a name="delete-saved-searches"></a>Kaydedilmiş aramaları silin
**İsteği:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Kaydedilmiş aramaları güncelleştirme
 **İsteği:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Meta veriler - yalnızca JSON
Burada, bir şekilde toosee hello alanları çalışma alanınızda toplanan hello verileri için tüm günlük türleri verilmiştir. Örneğin, olay türü hello bilgisayar adında bir alan olup olmadığını bilmek istiyorsanız, bu sorgu tek yönlü toocheck olur.

**İsteği alanları için:**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Yanıtı:**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Aşağıdaki tablonun hello kullanılabilir hello özellikleri açıklar.

| **Özellik** | **Açıklama** |
| --- | --- |
| ad |Alan adı. |
| Görünen adı |Merhaba hello alanın adını görüntüler. |
| type |Merhaba hello alan değerin türü. |
| modellenebilir |'Dizine', geçerli birleşimi ' depolanan ' ve 'model' özellikleri. |
| Görüntüleme |Geçerli 'display' özelliği. Alan aramada görünür ise true. |
| ownerType |Azaltılmış tooonly türleri tooonboarded IP'ın ait. |

## <a name="optional-parameters"></a>İsteğe bağlı parametreler
Merhaba bilgisinden isteğe bağlı parametreler kullanılabilir açıklar.

### <a name="highlighting"></a>Vurgulama
Merhaba "Highlight" parametresi toorequest hello arama alt kullanabilir isteğe bağlı bir parametre yanıt olarak bir dizi işaretçileri dahil edilir.

Bu işaretçileri hello başlangıç belirtmek ve sağlanan arama sorgunuzu hello koşulları eşleşen vurgulanan metin bitmelidir.
Merhaba başlangıç belirtin ve arama toowrap vurgulanmış hello terimi tarafından kullanılan işaretçileri bitiş.

**Örnek arama sorgusu**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Örnek sonuçları:**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

Önceki sonuç hello bildirimi öneki ve eklenmiş olan bir hata iletisi içerir.

## <a name="computer-groups"></a>Bilgisayar grupları
Bilgisayar, bir bilgisayar kümesi döndüren özel Kaydedilmiş aramaları gruplarıdır.  Bir bilgisayar grubu hello grubundaki diğer sorgular toolimit hello sonuçları toohello bilgisayarlar kullanabilirsiniz.  Bir bilgisayar grubu, bilgisayar değerini içeren bir Grup etiketi bir kayıtlı arama olarak uygulanır.

Bir bilgisayar grubu için bir örnek yanıt aşağıdadır.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>Bilgisayar grupları alınıyor
tooretrieve kullanım hello hello grubuyla Get yöntemi bir bilgisayar grubu kimliği

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Oluştururken veya güncelleştirirken bir bilgisayar grubu
toocreate bir bilgisayar grubu benzersiz kayıtlı arama kimliği ile Merhaba Put yöntemini kullanın Var olan bir bilgisayar grubu kimliği kullanırsanız, bir değiştirilir. Merhaba günlük analizi portalında bir bilgisayar grubu oluşturduğunuzda hello kimliği hello grubu ve ad oluşturulur.

Merhaba grubu tanımı için kullanılan hello sorgu hello Grup toofunction için bir bilgisayarlar kümesi düzgün döndürmesi gerekir.  Sorgunuz ile sona önerilir `| Distinct Computer` tooensure hello doğru veriler döndürülür.

Kaydedilmiş aramayı hello Hello tanımını grup bilgisayar değeri olan bir bilgisayar grubu olarak sınıflandırılmış hello arama toobe adlı bir etiket içermelidir.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Bilgisayar gruplarını silme
toodelete kullanım hello hello Grup Delete yöntemiyle bir bilgisayar grubu kimliği

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) özel alanlar için ölçüt kullanarak toobuild sorgular.
