---
title: "aaaAzure SDK .NET 2.9 sürüm notları"
description: ".NET 2.9 için Azure SDK sürüm notları"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="bce2e-103">.NET 2.9 için Azure SDK sürüm notları</span><span class="sxs-lookup"><span data-stu-id="bce2e-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="bce2e-104">Bu konu için .NET 2.9 ve Azure SDK'sının 2.9.6 sürümleri için sürüm notları içerir.</span><span class="sxs-lookup"><span data-stu-id="bce2e-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="bce2e-105">.NET 2.9.6 için Azure SDK sürüm özeti</span><span class="sxs-lookup"><span data-stu-id="bce2e-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="bce2e-106">Yayın Tarihi: 11/16/2016</span><span class="sxs-lookup"><span data-stu-id="bce2e-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="bce2e-107">Hiçbir en son değişiklikleri toohello Azure SDK 2.9 sunulan bu sürümde.</span><span class="sxs-lookup"><span data-stu-id="bce2e-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="bce2e-108">Bu SDK mevcut bulut hizmeti projeleri ile de hiçbir gereken yükseltme işlemi tooleverage yoktur.</span><span class="sxs-lookup"><span data-stu-id="bce2e-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="bce2e-109">Visual Studio 2017 Sürüm Adayı</span><span class="sxs-lookup"><span data-stu-id="bce2e-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="bce2e-110">Visual Studio 2017 RC'de bu hello Azure SDK'sı sürüm .NET için Azure iş yükü hello yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="bce2e-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="bce2e-111">Toodo Azure geliştirme gereken tüm hello araçları Visual Studio 2017 RC ileriye dönük bir parçası olur.</span><span class="sxs-lookup"><span data-stu-id="bce2e-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="bce2e-112">Visual Studio 2015 ve Visual Studio 2013 için hello SDK Webpı kullanılabilir olmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="bce2e-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="bce2e-113">Visual Studio 2017 son bir ürün olarak bıraktığında biz Azure SDK'sı .NET sürümleri için Visual Studio 2013 için sona erdirme.</span><span class="sxs-lookup"><span data-stu-id="bce2e-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="bce2e-114">Bu bağlantıyı toodownload Visual Studio 2017 RC izleyin: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="bce2e-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="bce2e-115">Azure Tanılama</span><span class="sxs-lookup"><span data-stu-id="bce2e-115">Azure Diagnostics</span></span>

- <span data-ttu-id="bce2e-116">Değiştirilen hello davranışı tooonly bulut Hizmetleri tanılama depolama bağlantı dizesi için bir belirteç değiştirilmiştir hello anahtarla bir kısmi bağlantı dizesi depolar.</span><span class="sxs-lookup"><span data-stu-id="bce2e-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="bce2e-117">kendi erişim denetlenebilir şekilde hello gerçek depolama anahtarı artık hello kullanıcı profili klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="bce2e-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="bce2e-118">Visual Studio yerel hata ayıklama ve yayımlama işlemi için kullanıcı profili klasöründen hello depolama anahtarı okur.</span><span class="sxs-lookup"><span data-stu-id="bce2e-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="bce2e-119">Yanıt toohello değişiklik yukarıda açıklanan Visual Studio Online ekip Gelişmiş hello Azure Cloud Services Dağıtımı görev şablonu kullanıcılar tooAzure içinde sürekli tümleştirme yayımlarken tanılama uzantısını ayarlamak için hello depolama anahtarı belirtebilirsiniz şekilde ve dağıtım.</span><span class="sxs-lookup"><span data-stu-id="bce2e-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="bce2e-120">Bu olası toostore güvenli bağlantı dizesi ve simgeleştirme için Azure tanılama (WAD), environements arasında yapılandırma sorunlarını çözmek toohelp yaptık.</span><span class="sxs-lookup"><span data-stu-id="bce2e-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="bce2e-121">Windows Server 2016 sanal makineler</span><span class="sxs-lookup"><span data-stu-id="bce2e-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="bce2e-122">Visual Studio şimdi dağıtma bulut Hizmetleri tooOS ailesi 5 (Windows Server 2016) sanal makineleri destekler.</span><span class="sxs-lookup"><span data-stu-id="bce2e-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="bce2e-123">Mevcut bulut hizmetlerini ayarları tootarget değiştirebilirsiniz yeni işletim sistemi ailesi hello.</span><span class="sxs-lookup"><span data-stu-id="bce2e-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="bce2e-124">.Net 4.6 ya da daha yüksek kullanarak toocreate hello hizmet seçerseniz yeni bulut Hizmetleri, oluştururken, varsayılan olarak hello hizmet toouse işletim sistemi ailesi 5 alır.</span><span class="sxs-lookup"><span data-stu-id="bce2e-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="bce2e-125">Daha fazla bilgi için hello gözden geçirebilirsiniz [konuk işletim sistemi ailesi destek tablo](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="bce2e-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="bce2e-126">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="bce2e-126">Known issues</span></span>

- <span data-ttu-id="bce2e-127">Azure .NET SDK 2.9.6 sunulan desteklenmeyen .NET çerçeveleri (örneğin, .NET 4.6) tooany işletim sistemi ailesi kullanarak projeleri dağıtılmasını engelleyen bir kısıtlama < 5.</span><span class="sxs-lookup"><span data-stu-id="bce2e-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="bce2e-128">Geçici bir çözüm sağlanmaktadır [burada](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="bce2e-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="bce2e-129">Azure rol içi önbellek</span><span class="sxs-lookup"><span data-stu-id="bce2e-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="bce2e-130">Azure rol içi önbelleği uçları 30 Kasım 2016 desteği.</span><span class="sxs-lookup"><span data-stu-id="bce2e-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="bce2e-131">Daha fazla ayrıntı için tıklatın [burada](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="bce2e-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="bce2e-132">Azure yığını için Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="bce2e-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="bce2e-133">Azure Resource Manager şablonlarınızı dağıtım hedefi olarak biz Azure yığın ekledik.</span><span class="sxs-lookup"><span data-stu-id="bce2e-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="bce2e-134">.NET 2.9 özeti için Azure SDK'sı</span><span class="sxs-lookup"><span data-stu-id="bce2e-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="bce2e-135">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bce2e-135">Overview</span></span>
<span data-ttu-id="bce2e-136">Bu belge .NET 2.9 yayımı için Azure SDK'sı hello hello sürüm notları içeriyor.</span><span class="sxs-lookup"><span data-stu-id="bce2e-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="bce2e-137">Merhaba bu sürümde güncelleştirmeler hakkında ayrıntılı bilgi için bkz [Azure SDK 2.9 duyuru post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="bce2e-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="bce2e-138">Visual Studio 2015 güncelleştirme 2 ve Visual Studio "15" için Azure SDK 2.9 Önizleme</span><span class="sxs-lookup"><span data-stu-id="bce2e-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="bce2e-139">Bu güncelleştirme, aşağıdaki hata düzeltmeleri hello içerir:</span><span class="sxs-lookup"><span data-stu-id="bce2e-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="bce2e-140">İlgili tooREST API İstemci oluşturma sorunu içinde hangi hello dizesinde "Bilinmeyen tür" Merhaba hello kod gen klasörün adını ve/veya oluşturulan hello koda bırakılan hello ad hello adı olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="bce2e-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="bce2e-141">İlgili tooScheduled WebJobs hangi hello toohello Zamanlayıcı sağlama işlemini geçirilen toobe başarısız kimlik doğrulama bilgilerini verin.</span><span class="sxs-lookup"><span data-stu-id="bce2e-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="bce2e-142">Bu güncelleştirme, yeni bir özellik aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="bce2e-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="bce2e-143">Uygulama hizmeti sağlama iletişim hello hello "Hizmetler" sekmesinde ikincil uygulama hizmetleri için destek.</span><span class="sxs-lookup"><span data-stu-id="bce2e-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="bce2e-144">Visual Studio 2015 güncelleştirme 2 için Azure Data Lake araçları</span><span class="sxs-lookup"><span data-stu-id="bce2e-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="bce2e-145">Bu güncelleştirmeleri hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="bce2e-145">This updates includes hello following:</span></span>

* <span data-ttu-id="bce2e-146">**Azure Data Lake Araçları** için Visual Studio şimdi .NET sürüm için Azure SDK'sı hello içine birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bce2e-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="bce2e-147">Azure SDK'yı yüklediğinizde hello aracı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="bce2e-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="bce2e-148">Merhaba aracı sık güncelleştirilen, Git [burada](http://aka.ms/datalaketool) tooget hello güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="bce2e-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="bce2e-149">**Sunucu Gezgini** şimdi tooview tüm sağlar ve bazı U-SQL meta verileri varlıklar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bce2e-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="bce2e-150">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blogu.</span><span class="sxs-lookup"><span data-stu-id="bce2e-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="bce2e-151">Hdınsight araçları</span><span class="sxs-lookup"><span data-stu-id="bce2e-151">HDInsight Tools</span></span>
<span data-ttu-id="bce2e-152">**Hdınsight Araçları** destekler Hdınsight sürüm 3.3 Tez grafiklerinde ve başka bir dilde gösteren dahil olmak üzere, düzeltmeleri şimdi Visual Studio için.</span><span class="sxs-lookup"><span data-stu-id="bce2e-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="bce2e-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bce2e-153">Azure Resource Manager</span></span>
<span data-ttu-id="bce2e-154">Bu sürüm ekler [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) için Resource Manager şablonları destekler.</span><span class="sxs-lookup"><span data-stu-id="bce2e-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="bce2e-155">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bce2e-155">See also</span></span>
[<span data-ttu-id="bce2e-156">Azure SDK 2.9 duyuru post</span><span class="sxs-lookup"><span data-stu-id="bce2e-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

