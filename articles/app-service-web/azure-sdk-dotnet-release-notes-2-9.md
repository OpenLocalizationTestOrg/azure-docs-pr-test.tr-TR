---
title: ".NET 2.9 için Azure SDK sürüm notları"
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
ms.openlocfilehash: 199f0906f73d693d7cd4b73c928f23ae83b99596
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="354fd-103">.NET 2.9 için Azure SDK sürüm notları</span><span class="sxs-lookup"><span data-stu-id="354fd-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="354fd-104">Bu konu için .NET 2.9 ve Azure SDK'sının 2.9.6 sürümleri için sürüm notları içerir.</span><span class="sxs-lookup"><span data-stu-id="354fd-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="354fd-105">.NET 2.9.6 için Azure SDK sürüm özeti</span><span class="sxs-lookup"><span data-stu-id="354fd-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="354fd-106">Yayın Tarihi: 11/16/2016</span><span class="sxs-lookup"><span data-stu-id="354fd-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="354fd-107">Bu sürümde hiçbir önemli değişiklikler için Azure SDK 2.9 tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="354fd-107">No breaking changes to the Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="354fd-108">Bu SDK mevcut bulut hizmeti projeleri ile yararlanmak için gereken yükseltme hiçbir işlem yok.</span><span class="sxs-lookup"><span data-stu-id="354fd-108">There is also no upgrade process needed to leverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="354fd-109">Visual Studio 2017 Sürüm Adayı</span><span class="sxs-lookup"><span data-stu-id="354fd-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="354fd-110">Visual Studio 2017 RC'de bu Azure SDK'sı sürüm .NET için Azure yükündeki yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="354fd-110">In Visual Studio 2017 RC, this release of the Azure SDK for .NET is built in in the Azure Workload.</span></span> <span data-ttu-id="354fd-111">Azure geliştirme yapmak için ihtiyacınız olan araçları, Visual Studio 2017 RC ileriye dönük bir parçası olur.</span><span class="sxs-lookup"><span data-stu-id="354fd-111">All the tools you need to do Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="354fd-112">Visual Studio 2015 ve Visual Studio 2013 için SDK Webpı kullanılabilir olmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="354fd-112">For Visual Studio 2015 and Visual Studio 2013, the SDK will still be available through WebPI.</span></span> <span data-ttu-id="354fd-113">Visual Studio 2017 son bir ürün olarak bıraktığında biz Azure SDK'sı .NET sürümleri için Visual Studio 2013 için sona erdirme.</span><span class="sxs-lookup"><span data-stu-id="354fd-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="354fd-114">Visual Studio 2017 RC indirmek için bu bağlantıyı izleyin: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="354fd-114">Follow this link to download Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="354fd-115">Azure Tanılama</span><span class="sxs-lookup"><span data-stu-id="354fd-115">Azure Diagnostics</span></span>

- <span data-ttu-id="354fd-116">Yalnızca bulut Hizmetleri tanılama depolama bağlantı dizesi için bir belirteç değiştirilmiştir anahtarla bir kısmi bağlantı dizesi depolamak için kullanılacak davranışı değişti.</span><span class="sxs-lookup"><span data-stu-id="354fd-116">Changed the behavior to only store a partial connection string with the key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="354fd-117">Kendi erişim denetlenebilir için gerçek depolama anahtarı artık kullanıcı profili klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="354fd-117">The actual storage key is now stored in the user profile folder so its access can be controlled.</span></span> <span data-ttu-id="354fd-118">Visual Studio yerel hata ayıklama ve yayımlama işlemi için kullanıcı profili klasöründen depolama anahtarı okur.</span><span class="sxs-lookup"><span data-stu-id="354fd-118">Visual Studio will read the storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="354fd-119">Kullanıcıların Azure'da sürekli tümleştirme ve dağıtım için yayımlarken tanılama uzantısını ayarlamak için depolama anahtarı belirtebilirsiniz şekilde yukarıda açıklanan değişikliğe yanıt olarak, Visual Studio Online ekibi Azure Cloud Services Dağıtımı görev şablonu geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="354fd-119">In response to the change described above, Visual Studio Online team enhanced the Azure Cloud Services deployment task template so users could specify the storage key for setting diagnostics extension when publishing to Azure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="354fd-120">Bu güvenli bağlantı dizesini ve simgeleştirme için Azure tanılama (arasında environements yapılandırmasındaki sorunları gidermenize yardımcı olacak WAD), depolanmasını mümkün yaptık.</span><span class="sxs-lookup"><span data-stu-id="354fd-120">We’ve made it possible to store secure connection string and tokenization for Azure Diagnostics (WAD), to help you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="354fd-121">Windows Server 2016 sanal makineler</span><span class="sxs-lookup"><span data-stu-id="354fd-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="354fd-122">Visual Studio artık işletim sistemi ailesi 5 (Windows Server 2016) sanal makineler için bulut Hizmetleri dağıtma destekler.</span><span class="sxs-lookup"><span data-stu-id="354fd-122">Visual Studio now supports deploying Cloud Services to OS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="354fd-123">Mevcut bulut hizmetlerini yeni işletim sistemi ailesi hedeflemek için ayarlarınızı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="354fd-123">For existing cloud services, you can change your settings to target the new OS Family.</span></span> <span data-ttu-id="354fd-124">.Net 4.6 ya da daha yüksek kullanarak hizmet oluşturmayı seçerseniz yeni bulut Hizmetleri, oluştururken, varsayılan olarak işletim sistemi ailesi 5 kullanmak için hizmet alır.</span><span class="sxs-lookup"><span data-stu-id="354fd-124">When creating new cloud services, if you choose to create the service using .net 4.6 or higher, it will default the service to use OS Family 5.</span></span>  <span data-ttu-id="354fd-125">Daha fazla bilgi için gözden geçirebilirsiniz [konuk işletim sistemi ailesi destek tablo](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="354fd-125">For more information, you can review the [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="354fd-126">Bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="354fd-126">Known issues</span></span>

- <span data-ttu-id="354fd-127">Azure .NET SDK 2.9.6 sunulan tüm işletim sistemi ailesi desteklenmeyen .NET Framework (örneğin, .NET 4.6) kullanarak projeleri dağıtılmasını engelleyen bir kısıtlama < 5.</span><span class="sxs-lookup"><span data-stu-id="354fd-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) to any OS Family < 5.</span></span> <span data-ttu-id="354fd-128">Geçici bir çözüm sağlanmaktadır [burada](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="354fd-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="354fd-129">Azure rol içi önbellek</span><span class="sxs-lookup"><span data-stu-id="354fd-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="354fd-130">Azure rol içi önbelleği uçları 30 Kasım 2016 desteği.</span><span class="sxs-lookup"><span data-stu-id="354fd-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="354fd-131">Daha fazla ayrıntı için tıklatın [burada](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="354fd-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="354fd-132">Azure yığını için Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="354fd-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="354fd-133">Azure Resource Manager şablonlarınızı dağıtım hedefi olarak biz Azure yığın ekledik.</span><span class="sxs-lookup"><span data-stu-id="354fd-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="354fd-134">.NET 2.9 özeti için Azure SDK'sı</span><span class="sxs-lookup"><span data-stu-id="354fd-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="354fd-135">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="354fd-135">Overview</span></span>
<span data-ttu-id="354fd-136">Bu belge, .NET 2.9 yayın için Azure SDK'sı için sürüm notlarını içermektedir.</span><span class="sxs-lookup"><span data-stu-id="354fd-136">This document contains the release notes for the Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="354fd-137">Bu sürümde güncelleştirmeler hakkında ayrıntılı bilgi için bkz: [Azure SDK 2.9 duyuru post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="354fd-137">For detailed information about updates in this release, see the [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="354fd-138">Visual Studio 2015 güncelleştirme 2 ve Visual Studio "15" için Azure SDK 2.9 Önizleme</span><span class="sxs-lookup"><span data-stu-id="354fd-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="354fd-139">Bu güncelleştirme aşağıdaki hata düzeltmeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="354fd-139">This update includes the following bug fixes:</span></span>

* <span data-ttu-id="354fd-140">REST API İstemci oluşturma ile ilgili sorun "Bilinmeyen türü" dize kod gen klasörün adını ve/veya ad alanı görüneceği oluşturulan koda bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="354fd-140">Issue related to REST API Client Generation in in which the string "Unknown Type” would appear as the name of the code-gen folder and/or the name of the namespace dropped into the generated code.</span></span>
* <span data-ttu-id="354fd-141">Hangi kimlik doğrulama bilgilerini sağlama işlemi Zamanlayıcı geçirilmesi başarısız Web işleri zamanlanmış ilgili bir sorun.</span><span class="sxs-lookup"><span data-stu-id="354fd-141">Issue related to Scheduled WebJobs in which the authentication information was failing to be passed to the Scheduler provisioning process.</span></span>

<span data-ttu-id="354fd-142">Bu güncelleştirme aşağıdaki yeni özellik içerir:</span><span class="sxs-lookup"><span data-stu-id="354fd-142">This update includes the following new feature:</span></span>

* <span data-ttu-id="354fd-143">Uygulama hizmeti sağlama iletişim "Hizmetler" sekmesinde ikincil uygulama hizmetleri için destek.</span><span class="sxs-lookup"><span data-stu-id="354fd-143">Support for secondary App Services in the "Services" tab of the App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="354fd-144">Visual Studio 2015 güncelleştirme 2 için Azure Data Lake araçları</span><span class="sxs-lookup"><span data-stu-id="354fd-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="354fd-145">Bu güncelleştirmeler şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="354fd-145">This updates includes the following:</span></span>

* <span data-ttu-id="354fd-146">**Azure Data Lake Araçları** için Visual Studio şimdi .NET sürüm için Azure SDK'sı içine birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="354fd-146">**Azure Data Lake Tools** for Visual Studio is now merged into the Azure SDK for .NET release.</span></span> <span data-ttu-id="354fd-147">Azure SDK'yı yüklediğinizde aracı otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="354fd-147">The tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="354fd-148">Aracı sık sık güncelleştirilen, Git [burada](http://aka.ms/datalaketool) güncelleştirmeleri almak için.</span><span class="sxs-lookup"><span data-stu-id="354fd-148">The tool is updated frequently, go [here](http://aka.ms/datalaketool) to get the updates.</span></span>
* <span data-ttu-id="354fd-149">**Sunucu Gezgini** şimdi tüm görüntülemek ve bazı U-SQL meta veri varlıklarını oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="354fd-149">**Server Explorer** now enables you to view all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="354fd-150">Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blogu.</span><span class="sxs-lookup"><span data-stu-id="354fd-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="354fd-151">Hdınsight araçları</span><span class="sxs-lookup"><span data-stu-id="354fd-151">HDInsight Tools</span></span>
<span data-ttu-id="354fd-152">**Hdınsight Araçları** destekler Hdınsight sürüm 3.3 Tez grafiklerinde ve başka bir dilde gösteren dahil olmak üzere, düzeltmeleri şimdi Visual Studio için.</span><span class="sxs-lookup"><span data-stu-id="354fd-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="354fd-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="354fd-153">Azure Resource Manager</span></span>
<span data-ttu-id="354fd-154">Bu sürüm ekler [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) için Resource Manager şablonları destekler.</span><span class="sxs-lookup"><span data-stu-id="354fd-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="354fd-155">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="354fd-155">See also</span></span>
[<span data-ttu-id="354fd-156">Azure SDK 2.9 duyuru post</span><span class="sxs-lookup"><span data-stu-id="354fd-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

