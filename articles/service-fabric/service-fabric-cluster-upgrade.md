---
title: "Azure Service Fabric kümesi aaaUpgrade | Microsoft Docs"
description: "Merhaba Service Fabric kod ve/veya küme güncelleştirme modunda, sertifikaları, uygulama bağlantı noktaları, işletim sistemi yamalarını yapılması ekleme yükseltme ayarı dahil olmak üzere bir Service Fabric kümesi çalıştıran yapılandırma yükseltin ve benzeri. Merhaba yükseltme gerçekleştirildiğinde beklentilerinizin ne?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a><span data-ttu-id="3760b-104">Azure Service Fabric kümesi yükseltme</span><span class="sxs-lookup"><span data-stu-id="3760b-104">Upgrade an Azure Service Fabric cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3760b-105">Azure küme</span><span class="sxs-lookup"><span data-stu-id="3760b-105">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="3760b-106">Tek başına küme</span><span class="sxs-lookup"><span data-stu-id="3760b-106">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

<span data-ttu-id="3760b-107">Tüm modern, upgradability tasarlama anahtar tooachieving uzun vadeli başarı ürününüzün sistemidir.</span><span class="sxs-lookup"><span data-stu-id="3760b-107">For any modern system, designing for upgradability is key tooachieving long-term success of your product.</span></span> <span data-ttu-id="3760b-108">Azure Service Fabric kümesi sahip, ancak kısmen Microsoft tarafından yönetilen bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="3760b-108">An Azure Service Fabric cluster is a resource that you own, but is partly managed by Microsoft.</span></span> <span data-ttu-id="3760b-109">Bu makalede, otomatik olarak yönetilir ve ne kendiniz yapılandırabileceğiniz anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3760b-109">This article describes what is managed automatically and what you can configure yourself.</span></span>

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="3760b-110">Kümenizde çalışan hello yapı sürümünü denetleme</span><span class="sxs-lookup"><span data-stu-id="3760b-110">Controlling hello fabric version that runs on your Cluster</span></span>
<span data-ttu-id="3760b-111">Microsoft tarafından yayımlanan veya küme toobe istediğiniz desteklenen fabric sürümü seçebileceğiniz gibi yükseltmeler küme tooreceive otomatik dokunuz ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-111">You can set your cluster tooreceive automatic fabric upgrades as they are released by Microsoft or you can select a supported fabric version you want your cluster toobe on.</span></span>

<span data-ttu-id="3760b-112">Ayar hello "upgrademode öğesinin" Küme yapılandırmasına hello portal ya da canlı bir küme oluşturma hello zaman Resource Manager veya sonraki bir sürümü kullanılarak tarafından bunu</span><span class="sxs-lookup"><span data-stu-id="3760b-112">You do this by setting hello "upgradeMode" cluster configuration on hello portal or using Resource Manager at hello time of creation or later on a live cluster</span></span> 

> [!NOTE]
> <span data-ttu-id="3760b-113">Desteklenen fabric sürümü her zaman çalışması kümenizi emin tookeep olun.</span><span class="sxs-lookup"><span data-stu-id="3760b-113">Make sure tookeep your cluster running a supported fabric version always.</span></span> <span data-ttu-id="3760b-114">Gibi ve biz hello service fabric yeni bir sürümü sunmaktan zaman hello önceki sürümü en az 60 gün o tarihten sonra destek sona ermesi için işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="3760b-114">As and when we announce hello release of a new version of service fabric, hello previous version is marked for end of support after a minimum of 60 days from that date.</span></span> <span data-ttu-id="3760b-115">Merhaba hello yeni sürümler duyurulur [hello service fabric ekip blogunda](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="3760b-115">hello  hello new releases are announced [on hello service fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="3760b-116">Merhaba yeni sürüm kullanılabilir toochoose ise.</span><span class="sxs-lookup"><span data-stu-id="3760b-116">hello new release is available toochoose then.</span></span> 
> 
> 

<span data-ttu-id="3760b-117">14 gün önceki toohello bitiş hello sürümü kümenizi çalışıyor, sistem durumu olayı, sistem durumu uyarısı kümenizi koyan oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3760b-117">14 days prior toohello expiry of hello release your cluster is running, a health event is generated that puts your cluster into a warning health state.</span></span> <span data-ttu-id="3760b-118">tooa desteklenen yapı sürümü'ı yükseltmeden hello küme bir uyarı durumunda kalır.</span><span class="sxs-lookup"><span data-stu-id="3760b-118">hello cluster remains in a warning state until you upgrade tooa supported fabric version.</span></span>

### <a name="setting-hello-upgrade-mode-via-portal"></a><span data-ttu-id="3760b-119">Portal aracılığıyla hello yükseltme modunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="3760b-119">Setting hello upgrade mode via portal</span></span>
<span data-ttu-id="3760b-120">Merhaba kümesi oluştururken hello küme tooautomatic veya el ile ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-120">You can set hello cluster tooautomatic or manual when you are creating hello cluster.</span></span>

![Create_Manualmode][Create_Manualmode]

<span data-ttu-id="3760b-122">Veya, canlı bir kümede el ile hello kullanarak yönetebileceğiniz deneyimi hello küme tooautomatic ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-122">You can set hello cluster tooautomatic or manual when on a live cluster, using hello manage experience.</span></span> 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a><span data-ttu-id="3760b-123">Yükseltme tooa yeni sürüm bir kümede tooManual modu Portalı aracılığıyla ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3760b-123">Upgrading tooa new version on a cluster that is set tooManual mode via portal.</span></span>
<span data-ttu-id="3760b-124">tooupgrade tooa yeni sürümü, tek toodo ihtiyacınız olan hello kullanılabilir sürüm hello aşağı açılır listeden seçin ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3760b-124">tooupgrade tooa new version, all you need toodo is select hello available version from hello dropdown and save.</span></span> <span data-ttu-id="3760b-125">Merhaba Fabric yükseltmesi otomatik olarak koparılan.</span><span class="sxs-lookup"><span data-stu-id="3760b-125">hello Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="3760b-126">Merhaba küme sistem durumu ilkeleri (düğüm durumu ve tüm hello hello kümede çalışan uygulamaları hello durumu birleşimi) bağlı tooduring hello yükseltme.</span><span class="sxs-lookup"><span data-stu-id="3760b-126">hello cluster health policies (a combination of node health and hello health all hello applications running in hello cluster) are adhered tooduring hello upgrade.</span></span>

<span data-ttu-id="3760b-127">Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır.</span><span class="sxs-lookup"><span data-stu-id="3760b-127">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="3760b-128">Bu belge tooread konusunda daha fazla aşağı tooset bu özel sistem durumu ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="3760b-128">Scroll down this document tooread more on how tooset those custom health policies.</span></span> 

<span data-ttu-id="3760b-129">Merhaba geri alma sonuçlandı hello sorunları çözümledik. sonra tooinitiate hello yükseltme yeniden öncekiyle aynı adımları aşağıdaki hello tarafından gerekir.</span><span class="sxs-lookup"><span data-stu-id="3760b-129">Once you have fixed hello issues that resulted in hello rollback, you need tooinitiate hello upgrade again, by following hello same steps as before.</span></span>

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a><span data-ttu-id="3760b-131">Resource Manager şablonu aracılığıyla hello yükseltme modunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="3760b-131">Setting hello upgrade mode via a Resource Manager template</span></span>
<span data-ttu-id="3760b-132">"Upgrademode öğesinin" yapılandırma toohello Microsoft.ServiceFabric/clusters kaynak tanımı hello ve kümesi hello "clusterCodeVersion" tooone Merhaba, aşağıda gösterildiği gibi desteklenen doku sürümleri ve hello şablonu dağıtmak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3760b-132">Add hello "upgradeMode" configuration toohello Microsoft.ServiceFabric/clusters resource definition and set hello "clusterCodeVersion" tooone of hello supported fabric versions as shown below and then deploy hello template.</span></span> <span data-ttu-id="3760b-133">"Elle" veya "Otomatik" Hello "upgrademode öğesinin" için geçerli değerler şunlardır</span><span class="sxs-lookup"><span data-stu-id="3760b-133">hello valid values for "upgradeMode" are "Manual" or "Automatic"</span></span>

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a><span data-ttu-id="3760b-135">Resource Manager şablonu aracılığıyla tooManual modunu ayarlama bir kümede tooa yeni sürümüne yükseltme.</span><span class="sxs-lookup"><span data-stu-id="3760b-135">Upgrading tooa new version on a cluster that is set tooManual mode via a Resource Manager template.</span></span>
<span data-ttu-id="3760b-136">Merhaba küme el ile modunda tooupgrade tooa yeni sürümü, olduğunda hello "clusterCodeVersion" tooa desteklenen sürüm değiştirin ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3760b-136">When hello cluster is in Manual mode, tooupgrade tooa new version, change hello "clusterCodeVersion" tooa supported version and deploy it.</span></span> <span data-ttu-id="3760b-137">Merhaba dağıtım hello şablonunun hello Fabric yükseltmesi kicks başlayacağı zamana otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="3760b-137">hello deployment of hello template, kicks of hello Fabric upgrade gets kicked off automatically.</span></span> <span data-ttu-id="3760b-138">Merhaba küme sistem durumu ilkeleri (düğüm durumu ve tüm hello hello kümede çalışan uygulamaları hello durumu birleşimi) bağlı tooduring hello yükseltme.</span><span class="sxs-lookup"><span data-stu-id="3760b-138">hello cluster health policies (a combination of node health and hello health all hello applications running in hello cluster) are adhered tooduring hello upgrade.</span></span>

<span data-ttu-id="3760b-139">Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır.</span><span class="sxs-lookup"><span data-stu-id="3760b-139">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="3760b-140">Bu belge tooread konusunda daha fazla aşağı tooset bu özel sistem durumu ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="3760b-140">Scroll down this document tooread more on how tooset those custom health policies.</span></span> 

<span data-ttu-id="3760b-141">Merhaba geri alma sonuçlandı hello sorunları çözümledik. sonra tooinitiate hello yükseltme yeniden öncekiyle aynı adımları aşağıdaki hello tarafından gerekir.</span><span class="sxs-lookup"><span data-stu-id="3760b-141">Once you have fixed hello issues that resulted in hello rollback, you need tooinitiate hello upgrade again, by following hello same steps as before.</span></span>

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a><span data-ttu-id="3760b-142">Belirli bir aboneliğe için tüm ortamlar için tüm kullanılabilir sürüm listesini al</span><span class="sxs-lookup"><span data-stu-id="3760b-142">Get list of all available version for all environments for a given subscription</span></span>
<span data-ttu-id="3760b-143">Çalıştır komutunu aşağıdaki hello ve çıktı benzer toothis almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3760b-143">Run hello following command, and you should get an output similar toothis.</span></span>

<span data-ttu-id="3760b-144">"supportExpiryUtc" söyler, zaman belirli bir yayın doluyor veya süresi dolmuş.</span><span class="sxs-lookup"><span data-stu-id="3760b-144">"supportExpiryUtc" tells your when a given release is expiring or has expired.</span></span> <span data-ttu-id="3760b-145">Merhaba en son sürüm geçerli bir tarih yok - değerine sahip "9999-12-31T23:59:59.9999999", yalnızca başka bir deyişle, hello sona erme tarihi henüz ayarlanmadı.</span><span class="sxs-lookup"><span data-stu-id="3760b-145">hello latest release does not have a valid date - it has a value of "9999-12-31T23:59:59.9999999", which just means that hello expiry date is not yet set.</span></span>

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a><span data-ttu-id="3760b-146">Merhaba Küme yükseltme modu otomatik olduğunda doku yükseltme davranışı</span><span class="sxs-lookup"><span data-stu-id="3760b-146">Fabric upgrade behavior when hello cluster Upgrade Mode is Automatic</span></span>
<span data-ttu-id="3760b-147">Microsoft hello fabric kod ve Azure bir kümede çalışan yapılandırma bulundurur.</span><span class="sxs-lookup"><span data-stu-id="3760b-147">Microsoft maintains hello fabric code and configuration that runs in an Azure cluster.</span></span> <span data-ttu-id="3760b-148">Biz gerektiği ölçüde temeline göre otomatik izlenen yükseltme toohello yazılım gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3760b-148">We perform automatic monitored upgrades toohello software on an as-needed basis.</span></span> <span data-ttu-id="3760b-149">Bu yükseltme, kod, yapılandırma veya her ikisi de olabilir.</span><span class="sxs-lookup"><span data-stu-id="3760b-149">These upgrades could be code, configuration, or both.</span></span> <span data-ttu-id="3760b-150">Uygulamanız herhangi bir etkisi veya düşük etkili toothese yükseltmeler son yükselmesine emin toomake, biz aşamaları aşağıdaki hello hello yükseltmeleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3760b-150">toomake sure that your application suffers no impact or minimal impact due toothese upgrades, we perform hello upgrades in hello following phases:</span></span>

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a><span data-ttu-id="3760b-151">1. Aşama: Tüm küme sistem durumu ilkeleri kullanarak yükseltme gerçekleştirilir</span><span class="sxs-lookup"><span data-stu-id="3760b-151">Phase 1: An upgrade is performed by using all cluster health policies</span></span>
<span data-ttu-id="3760b-152">Bu aşamasında, aynı anda tek bir yükseltme etki alanı hello yükseltme devam ve hello kümede çalışan hello uygulamalar toorun herhangi kesinti olmadan devam eder.</span><span class="sxs-lookup"><span data-stu-id="3760b-152">During this phase, hello upgrades proceed one upgrade domain at a time, and hello applications that were running in hello cluster continue toorun without any downtime.</span></span> <span data-ttu-id="3760b-153">Merhaba küme sistem durumu ilkeleri (düğüm durumu ve tüm hello hello kümede çalışan uygulamaları hello durumu birleşimi) bağlı tooduring hello yükseltme.</span><span class="sxs-lookup"><span data-stu-id="3760b-153">hello cluster health policies (a combination of node health and hello health all hello applications running in hello cluster) are adhered tooduring hello upgrade.</span></span>

<span data-ttu-id="3760b-154">Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır.</span><span class="sxs-lookup"><span data-stu-id="3760b-154">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="3760b-155">Daha sonra bir e-posta hello aboneliğin toohello sahibi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3760b-155">Then an email is sent toohello owner of hello subscription.</span></span> <span data-ttu-id="3760b-156">Merhaba e-posta bilgisinden hello içerir:</span><span class="sxs-lookup"><span data-stu-id="3760b-156">hello email contains hello following information:</span></span>

* <span data-ttu-id="3760b-157">Bildirim biz tooroll geri Küme yükseltme vardı.</span><span class="sxs-lookup"><span data-stu-id="3760b-157">Notification that we had tooroll back a cluster upgrade.</span></span>
* <span data-ttu-id="3760b-158">Varsa önerilen düzeltici eylemler.</span><span class="sxs-lookup"><span data-stu-id="3760b-158">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="3760b-159">Merhaba gün sayısı (biz Aşama 2 yürütme kadar n)</span><span class="sxs-lookup"><span data-stu-id="3760b-159">hello number of days (n) until we execute Phase 2.</span></span>

<span data-ttu-id="3760b-160">Biz tooexecute hello herhangi bir yükseltmesinin altyapı nedenlerden dolayı başarısız olduysa aynı yükseltme birkaç kez daha deneyin.</span><span class="sxs-lookup"><span data-stu-id="3760b-160">We try tooexecute hello same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="3760b-161">Merhaba sonra n gün başlangıç tarihi hello e-posta gönderildi, tooPhase 2 ilerlemeden.</span><span class="sxs-lookup"><span data-stu-id="3760b-161">After hello n days from hello date hello email was sent, we proceed tooPhase 2.</span></span>

<span data-ttu-id="3760b-162">Merhaba küme sistem durumu ilkeleri karşılanıyorsa hello yükseltme başarılı olarak kabul ve tam olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="3760b-162">If hello cluster health policies are met, hello upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="3760b-163">Bu aşamada bu hello ilk yükseltme veya hello yükseltme tekrar bölümlerini hiçbirini sırasında meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="3760b-163">This can happen during hello initial upgrade or any of hello upgrade reruns in this phase.</span></span> <span data-ttu-id="3760b-164">Hiçbir e-posta onayı başarılı bir çalışma yoktur.</span><span class="sxs-lookup"><span data-stu-id="3760b-164">There is no email confirmation of a successful run.</span></span> <span data-ttu-id="3760b-165">Bu, çok fazla e-postaların bir e-postayı--bir özel durum toonormal görülmelidir gönderme tooavoid olur.</span><span class="sxs-lookup"><span data-stu-id="3760b-165">This is tooavoid sending you too many emails--receiving an email should be seen as an exception toonormal.</span></span> <span data-ttu-id="3760b-166">Uygulama kullanılabilirliği etkilemeden hello Küme yükseltme toosucceed çoğunu bekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="3760b-166">We expect most of hello cluster upgrades toosucceed without impacting your application availability.</span></span>

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a><span data-ttu-id="3760b-167">2. Aşama: Yalnızca varsayılan sistem durumu ilkeleri kullanarak yükseltme gerçekleştirilir</span><span class="sxs-lookup"><span data-stu-id="3760b-167">Phase 2: An upgrade is performed by using default health policies only</span></span>
<span data-ttu-id="3760b-168">Merhaba sistem durumu ilkeleri bu aşamasında, hello hello yükseltme başında sağlıklı uygulama hello sayısı için aynı hello yükseltme işleminin süresi hello hello kalmasını bir şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3760b-168">hello health policies in this phase are set in such a way that hello number of applications that were healthy at hello beginning of hello upgrade remains hello same for hello duration of hello upgrade process.</span></span> <span data-ttu-id="3760b-169">1. aşaması, olduğu gibi aynı anda tek bir yükseltme etki alanı hello Aşama 2 Yükseltme devam ve hello kümede çalışan hello uygulamalar toorun herhangi kesinti olmadan devam eder.</span><span class="sxs-lookup"><span data-stu-id="3760b-169">As in Phase 1, hello Phase 2 upgrades proceed one upgrade domain at a time, and hello applications that were running in hello cluster continue toorun without any downtime.</span></span> <span data-ttu-id="3760b-170">Merhaba küme durumu (düğüm durumu ve tüm hello kümede çalışan uygulamaları hello hello durumu birleşimi) bağlı toofor hello hello yükseltme süresince ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="3760b-170">hello cluster health policies (a combination of node health and hello health all hello applications running in hello cluster) are adhered toofor hello duration of hello upgrade.</span></span>

<span data-ttu-id="3760b-171">Merhaba küme sistem durumu ilkeleri yürürlükte karşılanmazsa hello yükseltme geri alınır.</span><span class="sxs-lookup"><span data-stu-id="3760b-171">If hello cluster health policies in effect are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="3760b-172">Daha sonra bir e-posta hello aboneliğin toohello sahibi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3760b-172">Then an email is sent toohello owner of hello subscription.</span></span> <span data-ttu-id="3760b-173">Merhaba e-posta bilgisinden hello içerir:</span><span class="sxs-lookup"><span data-stu-id="3760b-173">hello email contains hello following information:</span></span>

* <span data-ttu-id="3760b-174">Bildirim biz tooroll geri Küme yükseltme vardı.</span><span class="sxs-lookup"><span data-stu-id="3760b-174">Notification that we had tooroll back a cluster upgrade.</span></span>
* <span data-ttu-id="3760b-175">Varsa önerilen düzeltici eylemler.</span><span class="sxs-lookup"><span data-stu-id="3760b-175">Suggested remedial actions, if any.</span></span>
* <span data-ttu-id="3760b-176">Merhaba gün sayısı (biz aşama 3 yürütme kadar n)</span><span class="sxs-lookup"><span data-stu-id="3760b-176">hello number of days (n) until we execute Phase 3.</span></span>

<span data-ttu-id="3760b-177">Biz tooexecute hello herhangi bir yükseltmesinin altyapı nedenlerden dolayı başarısız olduysa aynı yükseltme birkaç kez daha deneyin.</span><span class="sxs-lookup"><span data-stu-id="3760b-177">We try tooexecute hello same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="3760b-178">Birkaç gün n gün hazır olduğunuzda önce anımsatıcı e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3760b-178">A reminder email is sent a couple of days before n days are up.</span></span> <span data-ttu-id="3760b-179">Merhaba sonra n gün başlangıç tarihi hello e-posta gönderildi, tooPhase 3 ilerlemeden.</span><span class="sxs-lookup"><span data-stu-id="3760b-179">After hello n days from hello date hello email was sent, we proceed tooPhase 3.</span></span> <span data-ttu-id="3760b-180">size Aşama 2'de göndereceğiz hello e-postaları ciddi alınması ve düzeltici eylemler alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3760b-180">hello emails we send you in Phase 2 must be taken seriously and remedial actions must be taken.</span></span>

<span data-ttu-id="3760b-181">Merhaba küme sistem durumu ilkeleri karşılanıyorsa hello yükseltme başarılı olarak kabul ve tam olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="3760b-181">If hello cluster health policies are met, hello upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="3760b-182">Bu aşamada bu hello ilk yükseltme veya hello yükseltme tekrar bölümlerini hiçbirini sırasında meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="3760b-182">This can happen during hello initial upgrade or any of hello upgrade reruns in this phase.</span></span> <span data-ttu-id="3760b-183">Hiçbir e-posta onayı başarılı bir çalışma yoktur.</span><span class="sxs-lookup"><span data-stu-id="3760b-183">There is no email confirmation of a successful run.</span></span>

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a><span data-ttu-id="3760b-184">3. Aşama: Agresif sistem durumu ilkeleri kullanarak yükseltme gerçekleştirilir</span><span class="sxs-lookup"><span data-stu-id="3760b-184">Phase 3: An upgrade is performed by using aggressive health policies</span></span>
<span data-ttu-id="3760b-185">Bu sistem durumu ilkeleri bu aşamasında, hello uygulamaları hello durumunu yerine hello yükseltme tamamlanmasından sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="3760b-185">These health policies in this phase are geared towards completion of hello upgrade rather than hello health of hello applications.</span></span> <span data-ttu-id="3760b-186">Bu aşamada çok az sayıda Küme yükseltme sonlanır.</span><span class="sxs-lookup"><span data-stu-id="3760b-186">Very few cluster upgrades end up in this phase.</span></span> <span data-ttu-id="3760b-187">Kümenizi toothis aşaması alırsa, uygulamanızın bozulur ve/veya kullanılabilirlik kaybına olduğunu şansı yoktur.</span><span class="sxs-lookup"><span data-stu-id="3760b-187">If your cluster gets toothis phase, there is a good chance that your application becomes unhealthy and/or lose availability.</span></span>

<span data-ttu-id="3760b-188">Benzer toohello diğer iki aşama, aşama 3 yükseltmeler, aynı anda tek bir yükseltme etki alanı geçin.</span><span class="sxs-lookup"><span data-stu-id="3760b-188">Similar toohello other two phases, Phase 3 upgrades proceed one upgrade domain at a time.</span></span>

<span data-ttu-id="3760b-189">Merhaba küme sistem durumu ilkeleri karşılanmazsa hello yükseltme geri alınır.</span><span class="sxs-lookup"><span data-stu-id="3760b-189">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="3760b-190">Biz tooexecute hello herhangi bir yükseltmesinin altyapı nedenlerden dolayı başarısız olduysa aynı yükseltme birkaç kez daha deneyin.</span><span class="sxs-lookup"><span data-stu-id="3760b-190">We try tooexecute hello same upgrade a few more times in case any upgrades failed for infrastructure reasons.</span></span> <span data-ttu-id="3760b-191">Böylece, destek ve/veya yükseltmeler almayacaksınız bundan sonra hello küme, sabitlenir.</span><span class="sxs-lookup"><span data-stu-id="3760b-191">After that, hello cluster is pinned, so that it will no longer receive support and/or upgrades.</span></span>

<span data-ttu-id="3760b-192">Bu bilgileri içeren bir e-posta toohello abonelik sahibi, hello eylemlerden gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3760b-192">An email with this information is sent toohello subscription owner, along with hello remedial actions.</span></span> <span data-ttu-id="3760b-193">Tüm küme tooget aşama 3 başarısız olduğu bir duruma bekliyoruz değil.</span><span class="sxs-lookup"><span data-stu-id="3760b-193">We do not expect any clusters tooget into a state where Phase 3 has failed.</span></span>

<span data-ttu-id="3760b-194">Merhaba küme sistem durumu ilkeleri karşılanıyorsa hello yükseltme başarılı olarak kabul ve tam olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="3760b-194">If hello cluster health policies are met, hello upgrade is considered successful and marked complete.</span></span> <span data-ttu-id="3760b-195">Bu aşamada bu hello ilk yükseltme veya hello yükseltme tekrar bölümlerini hiçbirini sırasında meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="3760b-195">This can happen during hello initial upgrade or any of hello upgrade reruns in this phase.</span></span> <span data-ttu-id="3760b-196">Hiçbir e-posta onayı başarılı bir çalışma yoktur.</span><span class="sxs-lookup"><span data-stu-id="3760b-196">There is no email confirmation of a successful run.</span></span>

## <a name="cluster-configurations-that-you-control"></a><span data-ttu-id="3760b-197">Denetim küme yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="3760b-197">Cluster configurations that you control</span></span>
<span data-ttu-id="3760b-198">Ayrıca toohello özelliği tooset hello Küme yükseltme modu, canlı bir küme üzerinde değiştirebileceğiniz hello yapılandırmalar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="3760b-198">In addition toohello ability tooset hello cluster upgrade mode, Here are hello configurations that you can change on a live cluster.</span></span>

### <a name="certificates"></a><span data-ttu-id="3760b-199">Sertifikalar</span><span class="sxs-lookup"><span data-stu-id="3760b-199">Certificates</span></span>
<span data-ttu-id="3760b-200">Yeni ekleyebilir veya sertifikaları hello küme ve istemci hello Portalı aracılığıyla kolayca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-200">You can add new or delete certificates for hello cluster and client via hello portal easily.</span></span> <span data-ttu-id="3760b-201">Çok başvuran[ayrıntılı yönergeler için bu belgenin](service-fabric-cluster-security-update-certs-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3760b-201">Refer too[this document for detailed instructions](service-fabric-cluster-security-update-certs-azure.md)</span></span>

![Sertifika parmak izlerini hello Azure portal gösteren ekran görüntüsü.][CertificateUpgrade]

### <a name="application-ports"></a><span data-ttu-id="3760b-203">Uygulama bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="3760b-203">Application ports</span></span>
<span data-ttu-id="3760b-204">Uygulama bağlantı noktalarını hello düğüm türü ile ilişkili hello yük dengeleyici kaynak özelliklerini değiştirerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-204">You can change application ports by changing hello Load Balancer resource properties that are associated with hello node type.</span></span> <span data-ttu-id="3760b-205">Resource Manager PowerShell doğrudan kullanabilirsiniz veya hello portalı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-205">You can use hello portal, or you can use Resource Manager PowerShell directly.</span></span>

<span data-ttu-id="3760b-206">bir düğüm türü içindeki tüm sanal makineleri üzerinde yeni bir bağlantı noktası tooopen hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="3760b-206">tooopen a new port on all VMs in a node type, do hello following:</span></span>

1. <span data-ttu-id="3760b-207">Yeni bir araştırma toohello uygun yük dengeleyici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3760b-207">Add a new probe toohello appropriate load balancer.</span></span>
   
    <span data-ttu-id="3760b-208">Merhaba portalını kullanarak kümenizi dağıttıysanız hello yük dengeleyici "LB-adının hello kaynak grubu nodetypename-adlı" adlı her düğüm türü için bir tane.</span><span class="sxs-lookup"><span data-stu-id="3760b-208">If you deployed your cluster by using hello portal, hello load balancers are named "LB-name of hello Resource group-NodeTypename", one for each node type.</span></span> <span data-ttu-id="3760b-209">Merhaba yük dengeleyici adları yalnızca bir kaynak grubunda benzersiz olduğundan, bunlar için belirli bir kaynak grubu altında arama en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="3760b-209">Since hello load balancer names are unique only within a resource group, it is best if you search for them under a specific resource group.</span></span>
   
    ![Bir araştırma tooa ekleme gösteren ekran görüntüsü yük dengeleyici hello Portalı'nda.][AddingProbes]
2. <span data-ttu-id="3760b-211">Yeni bir kural toohello yük dengeleyiciye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3760b-211">Add a new rule toohello load balancer.</span></span>
   
    <span data-ttu-id="3760b-212">Aynı hello önceki adımda oluşturduğunuz hello araştırma kullanarak yük dengeleyici yeni bir kural toohello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3760b-212">Add a new rule toohello same load balancer by using hello probe that you created in hello previous step.</span></span>
   
    ![Yeni bir kural tooa yük dengeleyici hello Portalı'nda ekleniyor.][AddingLBRules]

### <a name="placement-properties"></a><span data-ttu-id="3760b-214">Yerleşim özellikleri</span><span class="sxs-lookup"><span data-stu-id="3760b-214">Placement properties</span></span>
<span data-ttu-id="3760b-215">Her hello düğüm türleri için uygulamalarınızda toouse istediğiniz özel yerleşim özellikleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-215">For each of hello node types, you can add custom placement properties that you want toouse in your applications.</span></span> <span data-ttu-id="3760b-216">NodeType açıkça eklemeden kullanabileceğiniz varsayılan bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="3760b-216">NodeType is a default property that you can use without adding it explicitly.</span></span>

> [!NOTE]
> <span data-ttu-id="3760b-217">Düğüm özellikleri kısıtlamalarından hello kullanımı ile ilgili ayrıntılar için ve nasıl toodefine bunları başvuruda hello Service Fabric kümesi Resource Manager belge "Yerleştirme kısıtlamaları ve düğüm özellikleri" bölümünde toohello üzerinde [açıklayan bilgisayarınızı küme ](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="3760b-217">For details on hello use of placement constraints, node properties, and how toodefine them, refer toohello section "Placement Constraints and Node Properties" in hello Service Fabric Cluster Resource Manager Document on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>
> 
> 

### <a name="capacity-metrics"></a><span data-ttu-id="3760b-218">Kapasite ölçümleri</span><span class="sxs-lookup"><span data-stu-id="3760b-218">Capacity metrics</span></span>
<span data-ttu-id="3760b-219">Her hello düğüm türleri için uygulamaları tooreport yükleme toouse istediğiniz özel kapasite ölçümleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-219">For each of hello node types, you can add custom capacity metrics that you want toouse in your applications tooreport load.</span></span> <span data-ttu-id="3760b-220">Kapasite ölçümleri tooreport yükü hello kullanımı hakkında daha fazla bilgi için üzerinde toohello Service Fabric kümesi Resource Manager belgeleri başvuran [açıklayan bilgisayarınızı küme](service-fabric-cluster-resource-manager-cluster-description.md) ve [ölçümleri ve yük](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3760b-220">For details on hello use of capacity metrics tooreport load, refer toohello Service Fabric Cluster Resource Manager Documents on [Describing Your Cluster](service-fabric-cluster-resource-manager-cluster-description.md) and [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md).</span></span>

### <a name="fabric-upgrade-settings---health-polices"></a><span data-ttu-id="3760b-221">Fabric yükseltme ayarları - sistem durumu ilkeleri</span><span class="sxs-lookup"><span data-stu-id="3760b-221">Fabric upgrade settings - Health polices</span></span>
<span data-ttu-id="3760b-222">Fabric yükseltmesi için özel sistem durumu ilkeleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-222">You can specify custom health polices for fabric upgrade.</span></span> <span data-ttu-id="3760b-223">Fabric yükseltmelerinin küme tooAutomatic ayarladıysanız, bu ilkeler uygulanan toohello Aşama 1 hello otomatik fabric yükseltmelerinin alın.</span><span class="sxs-lookup"><span data-stu-id="3760b-223">If you have set your cluster tooAutomatic fabric upgrades, then these policies get applied toohello Phase-1 of hello automatic fabric upgrades.</span></span>
<span data-ttu-id="3760b-224">Yükseltmeler, kümeniz için el ile doku ayarladıysanız bu ilkelerin her zaman uygulanacağını sonra hello sistem tookick hello fabric yükseltmesi kümenizdeki kapalı tetikleme yeni bir sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="3760b-224">If you have set your cluster for Manual fabric upgrades, then these policies get applied each time you select a new version triggering hello system tookick off hello fabric upgrade in your cluster.</span></span> <span data-ttu-id="3760b-225">Merhaba ilkelerini geçersiz kılmaz hello Varsayılanları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3760b-225">If you do not override hello policies, hello defaults are used.</span></span>

<span data-ttu-id="3760b-226">Merhaba özel sistem durumu ilkeleri belirtin veya Gelişmiş yükseltme ayarlarını hello seçerek hello "fabric yükseltmesi" dikey penceresinde hello geçerli ayarlarında gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3760b-226">You can specify hello custom health policies or review hello current settings under hello "fabric upgrade" blade, by selecting hello advanced upgrade settings.</span></span> <span data-ttu-id="3760b-227">Resim nasıl üzerinde aşağıdaki hello gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3760b-227">Review hello following picture on how to.</span></span> 

![Özel sistem durumu ilkeleri yönetme][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a><span data-ttu-id="3760b-229">Yapı ayarları kümeniz için özelleştirme</span><span class="sxs-lookup"><span data-stu-id="3760b-229">Customize Fabric settings for your cluster</span></span>
<span data-ttu-id="3760b-230">Çok başvuran[hizmet doku küme yapı ayarları](service-fabric-cluster-fabric-settings.md) ne ve bunları nasıl özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3760b-230">Refer too[service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md) on what and how you can customize them.</span></span>

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a><span data-ttu-id="3760b-231">İşletim sistemi düzeltme eklerinin hello hello küme olun VM'ler</span><span class="sxs-lookup"><span data-stu-id="3760b-231">OS patches on hello VMs that make up hello cluster</span></span>
<span data-ttu-id="3760b-232">Çok başvuran[düzeltme eki Orchestration uygulama](service-fabric-patch-orchestration-application.md) dağıtılabilecek, küme tooinstall düzeltme eklerini Windows Update'ten üzerinde hello Hizmetleri kullanılabilir tüm hello zaman tutma orchestrated bir biçimde.</span><span class="sxs-lookup"><span data-stu-id="3760b-232">Refer too[Patch Orchestration Application](service-fabric-patch-orchestration-application.md) which can be deployed on your cluster tooinstall patches from Windows Update in an orchestrated manner, keeping hello services available all hello time.</span></span> 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a><span data-ttu-id="3760b-233">İşletim sistemi yükseltmeleri hello hello küme olun VM'ler hakkında</span><span class="sxs-lookup"><span data-stu-id="3760b-233">OS upgrades on hello VMs that make up hello cluster</span></span>
<span data-ttu-id="3760b-234">Merhaba işletim sistemi görüntüsü hello kümesinin hello sanal makinelerde yükseltmeniz gerekir, aynı anda bir VM yapmalısınız.</span><span class="sxs-lookup"><span data-stu-id="3760b-234">If you must upgrade hello OS image on hello virtual machines of hello cluster, you must do it one VM at a time.</span></span> <span data-ttu-id="3760b-235">Sorumlu olduğunuz bu yükseltmeyi--var. şu anda bu Otomasyon.</span><span class="sxs-lookup"><span data-stu-id="3760b-235">You are responsible for this upgrade--there is currently no automation for this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3760b-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3760b-236">Next steps</span></span>
* <span data-ttu-id="3760b-237">Bilgi nasıl toocustomize hello bazıları [hizmet doku küme yapı ayarları](service-fabric-cluster-fabric-settings.md)</span><span class="sxs-lookup"><span data-stu-id="3760b-237">Learn how toocustomize some of hello [service fabric cluster fabric settings](service-fabric-cluster-fabric-settings.md)</span></span>
* <span data-ttu-id="3760b-238">Nasıl çok öğrenin[kümenizi ölçeğini](service-fabric-cluster-scale-up-down.md)</span><span class="sxs-lookup"><span data-stu-id="3760b-238">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md)</span></span>
* <span data-ttu-id="3760b-239">Hakkında bilgi edinin [uygulama yükseltme](service-fabric-application-upgrade.md)</span><span class="sxs-lookup"><span data-stu-id="3760b-239">Learn about [application upgrades](service-fabric-application-upgrade.md)</span></span>

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
