---
title: "Azure CLI 1.0 İzleyici hızlı başlangıç örnekleri. | Microsoft Belgeleri"
description: "Azure İzleyicisi özelliklerine ilişkin örnek CLI 1.0 komutlar. Azure İzleyicisi uyarı bildirimleri gönderebilir, yapılandırılmış telemetri verilerini ve otomatik ölçeklendirme bulut Hizmetleri, sanal makinelerin ve Web uygulamaları değerlerine göre web URL'leri çağrı olanak sağlayan bir Microsoft Azure hizmetidir."
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
ms.openlocfilehash: ec4512500dc3c77a40d2ebd1e6b460d5bb005811
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="ae7b7-105">Azure İzleyici platformlar arası CLI 1.0 hızlı başlangıç örnekleri</span><span class="sxs-lookup"><span data-stu-id="ae7b7-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="ae7b7-106">Bu makalede, örnek Azure İzleyicisi özelliklerine erişmenize yardımcı olması için komut satırı arabirimi (CLI) komutları gösterir.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-106">This article shows you sample command-line interface (CLI) commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="ae7b7-107">Azure İzleyici otomatik ölçeklendirme bulut Hizmetleri, sanal makineleri ve Web uygulamaları ve uyarı bildirimleri gönderebilir veya web URL'leri yapılandırılmış telemetri verilerini değerlerine göre arama için sağlar.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-107">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="ae7b7-108">Azure İzleyicisi "Azure Öngörüler" olarak adlandırılmıştı için yeni 25 Eylül 2016'ya kadar adıdır.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-108">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="ae7b7-109">Bununla birlikte, ad alanları ve bu nedenle aşağıdaki komutları yine "ınsights" içerir.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-109">However, the namespaces and thus the commands below still contain the "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ae7b7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ae7b7-110">Prerequisites</span></span>
<span data-ttu-id="ae7b7-111">Azure CLI henüz yüklemediyseniz bkz [Azure CLI yükleme](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ae7b7-111">If you haven't already installed the Azure CLI, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="ae7b7-112">Azure CLI ile emin değilseniz, daha fazla bilgiyi adresinden hakkında [Mac, Linux ve Windows Azure Resource Manager ile Azure CLI kullanılmaya](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ae7b7-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="ae7b7-113">Windows, gelen npm yükleme [Node.js Web sitesi](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="ae7b7-113">In Windows, install npm from the [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="ae7b7-114">Yönetici olarak çalıştır ayrıcalıklarıyla CMD.exe kullanarak yüklemeyi tamamladıktan sonra aşağıdaki npm yüklendiği klasöründen yürütün:</span><span class="sxs-lookup"><span data-stu-id="ae7b7-114">After you complete the installation, using CMD.exe with Run As Administrator privileges, execute the following from the folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="ae7b7-115">Ardından, tüm klasör/istediğiniz ve komut satırına şunu yazın konuma gidin:</span><span class="sxs-lookup"><span data-stu-id="ae7b7-115">Next, navigate to any folder/location you want and type at the command-line:</span></span>

```console
azure help
```

## <a name="log-in-to-azure"></a><span data-ttu-id="ae7b7-116">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="ae7b7-116">Log in to Azure</span></span>
<span data-ttu-id="ae7b7-117">İlk adım, Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-117">The first step is to login to your Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="ae7b7-118">Bu komutu çalıştırdıktan sonra ekrandaki yönergeleri aracılığıyla oturum açmaya sahip.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-118">After running this command, you have to sign in via the instructions on the screen.</span></span> <span data-ttu-id="ae7b7-119">Daha sonra hesap, Tenantıd ve varsayılan abonelik kimliği bakın Tüm komutlar, varsayılan abonelik bağlamında çalışır.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in the context of your default subscription.</span></span>

<span data-ttu-id="ae7b7-120">Geçerli aboneliğiniz ayrıntılarını listelemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-120">To list the details of your current subscription, use the following command.</span></span>

```console
azure account show
```

<span data-ttu-id="ae7b7-121">Farklı bir aboneliğe çalışma bağlamını değiştirmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-121">To change working context to a different subscription, use the following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="ae7b7-122">Azure Resource Manager ve Azure İzleyici komutlarını kullanmak için Azure Kaynak Yöneticisi modunda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-122">To use Azure Resource Manager and Azure Monitor commands, you need to be in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="ae7b7-123">Tüm desteklenen Azure İzleyici komutlarının listesini görüntülemek için aşağıdakileri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-123">To view a list of all supported Azure Monitor commands, perform the following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="ae7b7-124">Bir abonelik için etkinlik günlüğü görüntüle</span><span class="sxs-lookup"><span data-stu-id="ae7b7-124">View activity log for a subscription</span></span>
<span data-ttu-id="ae7b7-125">Etkinlik günlüğü olaylarını listesini görüntülemek için aşağıdakileri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-125">To view a list of activity log events, perform the following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="ae7b7-126">Tüm kullanılabilir seçenekleri görüntülemek için aşağıdakileri deneyin.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-126">Try the following to view all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="ae7b7-127">Bir kaynak grubu tarafından listesi günlüklerine örneği</span><span class="sxs-lookup"><span data-stu-id="ae7b7-127">Here is an example to list logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="ae7b7-128">Liste günlükleri çağıran tarafından örneği</span><span class="sxs-lookup"><span data-stu-id="ae7b7-128">Example to list logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="ae7b7-129">İçinde bir başlangıç ve bitiş tarihi listesine örnek kaynak türünde çağıran tarafından günlüğe kaydeder</span><span class="sxs-lookup"><span data-stu-id="ae7b7-129">Example to list logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="ae7b7-130">Uyarılarla çalışma</span><span class="sxs-lookup"><span data-stu-id="ae7b7-130">Work with alerts</span></span>
<span data-ttu-id="ae7b7-131">Uyarılarla çalışma için bölümündeki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-131">You can use the information in the section to work with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="ae7b7-132">Uyarı kuralları bir kaynak grubunda Al</span><span class="sxs-lookup"><span data-stu-id="ae7b7-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="ae7b7-133">Ölçüm bir uyarı kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="ae7b7-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="ae7b7-134">Web testini uyarı kuralı oluştur</span><span class="sxs-lookup"><span data-stu-id="ae7b7-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="ae7b7-135">Bir uyarı kuralını Sil</span><span class="sxs-lookup"><span data-stu-id="ae7b7-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="ae7b7-136">Günlük profilleri</span><span class="sxs-lookup"><span data-stu-id="ae7b7-136">Log profiles</span></span>
<span data-ttu-id="ae7b7-137">Günlük profilleri ile çalışmak için bu bölümdeki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-137">Use the information in this section to work with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="ae7b7-138">Günlük profilini Al</span><span class="sxs-lookup"><span data-stu-id="ae7b7-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="ae7b7-139">Bekletme olmayan günlük profili Ekle</span><span class="sxs-lookup"><span data-stu-id="ae7b7-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="ae7b7-140">Günlük profilini Kaldır</span><span class="sxs-lookup"><span data-stu-id="ae7b7-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="ae7b7-141">Bekletme günlüğü profiliyle ekleme</span><span class="sxs-lookup"><span data-stu-id="ae7b7-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="ae7b7-142">Bekletme ve EventHub günlük profiliyle ekleme</span><span class="sxs-lookup"><span data-stu-id="ae7b7-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="ae7b7-143">Tanılama</span><span class="sxs-lookup"><span data-stu-id="ae7b7-143">Diagnostics</span></span>
<span data-ttu-id="ae7b7-144">Tanılama ayarları ile çalışmak için bu bölümdeki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-144">Use the information in this section to work with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="ae7b7-145">Tanılama bir ayar edinme</span><span class="sxs-lookup"><span data-stu-id="ae7b7-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="ae7b7-146">Tanılama ayarını devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="ae7b7-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="ae7b7-147">Bekletme olmadan tanılama ayarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="ae7b7-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="ae7b7-148">Otomatik Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="ae7b7-148">Autoscale</span></span>
<span data-ttu-id="ae7b7-149">Otomatik ölçeklendirme ayarları ile çalışmak için bu bölümdeki bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-149">Use the information in this section to work with autoscale settings.</span></span> <span data-ttu-id="ae7b7-150">Bu örnekler değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae7b7-150">You need to modify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="ae7b7-151">Bir kaynak grubu için otomatik ölçeklendirme ayarlarını al</span><span class="sxs-lookup"><span data-stu-id="ae7b7-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="ae7b7-152">Otomatik ölçeklendirme ayarlarını adıyla bir kaynak grubunda Al</span><span class="sxs-lookup"><span data-stu-id="ae7b7-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="ae7b7-153">Auotoscale ayarlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="ae7b7-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
