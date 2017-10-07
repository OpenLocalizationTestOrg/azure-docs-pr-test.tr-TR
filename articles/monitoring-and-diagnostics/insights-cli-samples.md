---
title: "aaaAzure İzleyici CLI 1.0 hızlı başlangıç örnekleri. | Microsoft Belgeleri"
description: "Azure İzleyicisi özelliklerine ilişkin örnek CLI 1.0 komutlar. Azure İzleyici toosend Uyarı bildirimlerini sağlayan bir Microsoft Azure hizmet, arama web URL'leri yapılandırılmış telemetri verilerini ve otomatik ölçeklendirme bulut Hizmetleri, sanal makinelerin ve Web uygulamaları değerlerine göre."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Azure İzleyici platformlar arası CLI 1.0 hızlı başlangıç örnekleri
Bu makale Azure İzleyicisi özelliklerine erişim komut satırı arabirimi (CLI) komutları toohelp örnek gösterir. Azure İzleyici tooAutoScale bulut Hizmetleri, sanal makineler ve Web uygulamaları ve toosend Uyarı bildirimlerinin veya yapılandırılmış telemetri verilerini değerlerine göre çağrısı web URL'leri sağlar.

> [!NOTE]
> Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için hello yeni 25 Eylül 2016'ya kadar adıdır. Ancak, başlangıç ad alanları ve bu nedenle aşağıdaki hello komutları hala hello "ınsights" içeriyor.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Hello Azure CLI henüz yüklemediyseniz bkz [yükleme hello Azure CLI](../cli-install-nodejs.md). Azure CLI ile emin değilseniz, daha fazla bilgiyi adresinden hakkında [kullanım hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](../xplat-cli-azure-resource-manager.md).

Windows hello npm yükleme [Node.js Web sitesi](https://nodejs.org/). Hello yüklemeyi tamamladıktan sonra yönetici olarak çalıştır ayrıcalıklarıyla CMD.exe kullanarak npm yüklendiği hello klasöründen hello aşağıdakileri yürütün:

```console
npm install azure-cli --global
```

Ardından, tooany klasörü/konum istediğiniz ve hello komut satırı yazın gidin:

```console
azure help
```

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum
Merhaba ilk adımı toologin tooyour Azure hesabı oluşturur.

```console
azure login
```

Bu komutu çalıştırdıktan sonra toosign hello yönergeleri Merhaba ekranında aracılığıyla sizde. Daha sonra hesap, Tenantıd ve varsayılan abonelik kimliği bakın Tüm komutlar hello varsayılan aboneliğinizin bağlamında çalışır.

Geçerli aboneliğiniz toolist hello ayrıntılarını komutu aşağıdaki hello kullanın.

```console
azure account show
```

toochange çalışma bağlam tooa farklı abonelik, komutu aşağıdaki kullanım hello.

```console
azure account set "subscription ID or subscription name"
```

toouse Azure Resource Manager ve Azure İzleyicisi komutları, Azure Kaynak Yöneticisi modunda toobe gerekir.

```console
azure config mode arm
```

desteklenen tüm Azure İzleyici komutların listesini tooview hello aşağıdakileri gerçekleştirin.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Bir abonelik için etkinlik günlüğü görüntüle
tooview etkinlik günlük olaylarının bir listesi hello aşağıdakileri gerçekleştirin.

```console
azure insights logs list [options]
```

Tooview aşağıdaki hello tüm kullanılabilir seçenekleri deneyin.

```console
azure insights logs list -help
```

İşte bir örnek toolist günlükleri resourceGroup tarafından

```console
azure insights logs list --resourceGroup "myrg1"
```

Çağıran tarafından örnek toolist günlükleri

```console
azure insights logs list --caller "myname@company.com"
```

Örnek toolist günlükleri çağıran bir kaynağına göre içinde bir başlangıç ve bitiş tarihi yazın

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Uyarılarla çalışma
Merhaba bölüm toowork uyarılarla hello bilgileri kullanabilirsiniz.

### <a name="get-alert-rules-in-a-resource-group"></a>Uyarı kuralları bir kaynak grubunda Al
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Ölçüm bir uyarı kuralı oluştur
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Web testini uyarı kuralı oluştur
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Bir uyarı kuralını Sil
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Günlük profilleri
Bu bölümde toowork günlük profilleriyle Hello bilgileri kullanın.

### <a name="get-a-log-profile"></a>Günlük profilini Al
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Bekletme olmayan günlük profili Ekle
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Günlük profilini Kaldır
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Bekletme günlüğü profiliyle ekleme
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Bekletme ve EventHub günlük profiliyle ekleme
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Tanılama
Bu bölümde toowork tanılama ayarlarla Hello bilgileri kullanın.

### <a name="get-a-diagnostic-setting"></a>Tanılama bir ayar edinme
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Tanılama ayarını devre dışı bırak
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Bekletme olmadan tanılama ayarını etkinleştirin
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Otomatik Ölçeklendirme
Bu bölümde toowork otomatik ölçeklendirme ayarlarla Hello bilgileri kullanın. Bu örnekler toomodify gerekir.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Bir kaynak grubu için otomatik ölçeklendirme ayarlarını al
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Otomatik ölçeklendirme ayarlarını adıyla bir kaynak grubunda Al
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Auotoscale ayarlarını belirleme
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
