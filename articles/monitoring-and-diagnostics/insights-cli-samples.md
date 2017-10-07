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
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="a2ac5-105">Azure İzleyici platformlar arası CLI 1.0 hızlı başlangıç örnekleri</span><span class="sxs-lookup"><span data-stu-id="a2ac5-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="a2ac5-106">Bu makale Azure İzleyicisi özelliklerine erişim komut satırı arabirimi (CLI) komutları toohelp örnek gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="a2ac5-107">Azure İzleyici tooAutoScale bulut Hizmetleri, sanal makineler ve Web uygulamaları ve toosend Uyarı bildirimlerinin veya yapılandırılmış telemetri verilerini değerlerine göre çağrısı web URL'leri sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="a2ac5-108">Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için hello yeni 25 Eylül 2016'ya kadar adıdır.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="a2ac5-109">Ancak, başlangıç ad alanları ve bu nedenle aşağıdaki hello komutları hala hello "ınsights" içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a2ac5-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a2ac5-110">Prerequisites</span></span>
<span data-ttu-id="a2ac5-111">Hello Azure CLI henüz yüklemediyseniz bkz [yükleme hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a2ac5-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="a2ac5-112">Azure CLI ile emin değilseniz, daha fazla bilgiyi adresinden hakkında [kullanım hello Mac, Linux ve Windows Azure Resource Manager ile Azure CLI](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a2ac5-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="a2ac5-113">Windows hello npm yükleme [Node.js Web sitesi](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="a2ac5-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="a2ac5-114">Hello yüklemeyi tamamladıktan sonra yönetici olarak çalıştır ayrıcalıklarıyla CMD.exe kullanarak npm yüklendiği hello klasöründen hello aşağıdakileri yürütün:</span><span class="sxs-lookup"><span data-stu-id="a2ac5-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="a2ac5-115">Ardından, tooany klasörü/konum istediğiniz ve hello komut satırı yazın gidin:</span><span class="sxs-lookup"><span data-stu-id="a2ac5-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="a2ac5-116">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="a2ac5-116">Log in tooAzure</span></span>
<span data-ttu-id="a2ac5-117">Merhaba ilk adımı toologin tooyour Azure hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="a2ac5-118">Bu komutu çalıştırdıktan sonra toosign hello yönergeleri Merhaba ekranında aracılığıyla sizde.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="a2ac5-119">Daha sonra hesap, Tenantıd ve varsayılan abonelik kimliği bakın Tüm komutlar hello varsayılan aboneliğinizin bağlamında çalışır.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="a2ac5-120">Geçerli aboneliğiniz toolist hello ayrıntılarını komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="a2ac5-121">toochange çalışma bağlam tooa farklı abonelik, komutu aşağıdaki kullanım hello.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="a2ac5-122">toouse Azure Resource Manager ve Azure İzleyicisi komutları, Azure Kaynak Yöneticisi modunda toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="a2ac5-123">desteklenen tüm Azure İzleyici komutların listesini tooview hello aşağıdakileri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="a2ac5-124">Bir abonelik için etkinlik günlüğü görüntüle</span><span class="sxs-lookup"><span data-stu-id="a2ac5-124">View activity log for a subscription</span></span>
<span data-ttu-id="a2ac5-125">tooview etkinlik günlük olaylarının bir listesi hello aşağıdakileri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="a2ac5-126">Tooview aşağıdaki hello tüm kullanılabilir seçenekleri deneyin.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="a2ac5-127">İşte bir örnek toolist günlükleri resourceGroup tarafından</span><span class="sxs-lookup"><span data-stu-id="a2ac5-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="a2ac5-128">Çağıran tarafından örnek toolist günlükleri</span><span class="sxs-lookup"><span data-stu-id="a2ac5-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="a2ac5-129">Örnek toolist günlükleri çağıran bir kaynağına göre içinde bir başlangıç ve bitiş tarihi yazın</span><span class="sxs-lookup"><span data-stu-id="a2ac5-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="a2ac5-130">Uyarılarla çalışma</span><span class="sxs-lookup"><span data-stu-id="a2ac5-130">Work with alerts</span></span>
<span data-ttu-id="a2ac5-131">Merhaba bölüm toowork uyarılarla hello bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="a2ac5-132">Uyarı kuralları bir kaynak grubunda Al</span><span class="sxs-lookup"><span data-stu-id="a2ac5-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="a2ac5-133">Ölçüm bir uyarı kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="a2ac5-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="a2ac5-134">Web testini uyarı kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="a2ac5-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="a2ac5-135">Bir uyarı kuralını Sil</span><span class="sxs-lookup"><span data-stu-id="a2ac5-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="a2ac5-136">Günlük profilleri</span><span class="sxs-lookup"><span data-stu-id="a2ac5-136">Log profiles</span></span>
<span data-ttu-id="a2ac5-137">Bu bölümde toowork günlük profilleriyle Hello bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="a2ac5-138">Günlük profilini Al</span><span class="sxs-lookup"><span data-stu-id="a2ac5-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="a2ac5-139">Bekletme olmayan günlük profili Ekle</span><span class="sxs-lookup"><span data-stu-id="a2ac5-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="a2ac5-140">Günlük profilini Kaldır</span><span class="sxs-lookup"><span data-stu-id="a2ac5-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="a2ac5-141">Bekletme günlüğü profiliyle ekleme</span><span class="sxs-lookup"><span data-stu-id="a2ac5-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="a2ac5-142">Bekletme ve EventHub günlük profiliyle ekleme</span><span class="sxs-lookup"><span data-stu-id="a2ac5-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="a2ac5-143">Tanılama</span><span class="sxs-lookup"><span data-stu-id="a2ac5-143">Diagnostics</span></span>
<span data-ttu-id="a2ac5-144">Bu bölümde toowork tanılama ayarlarla Hello bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="a2ac5-145">Tanılama bir ayar edinme</span><span class="sxs-lookup"><span data-stu-id="a2ac5-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="a2ac5-146">Tanılama ayarını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="a2ac5-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="a2ac5-147">Bekletme olmadan tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="a2ac5-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="a2ac5-148">Otomatik Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="a2ac5-148">Autoscale</span></span>
<span data-ttu-id="a2ac5-149">Bu bölümde toowork otomatik ölçeklendirme ayarlarla Hello bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="a2ac5-150">Bu örnekler toomodify gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2ac5-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="a2ac5-151">Bir kaynak grubu için otomatik ölçeklendirme ayarlarını al</span><span class="sxs-lookup"><span data-stu-id="a2ac5-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="a2ac5-152">Otomatik ölçeklendirme ayarlarını adıyla bir kaynak grubunda Al</span><span class="sxs-lookup"><span data-stu-id="a2ac5-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="a2ac5-153">Auotoscale ayarlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="a2ac5-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
