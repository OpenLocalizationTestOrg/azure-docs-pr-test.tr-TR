---
title: "Azure bulut Kabuğu (Önizleme) genel bakış | Microsoft Docs"
description: "Azure bulut Kabuk genel bakış."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 7165633cd354eeea2e3619f839338e6af1524e56
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="6cdc7-103">Azure bulut Kabuğu (Önizleme) genel bakış</span><span class="sxs-lookup"><span data-stu-id="6cdc7-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="6cdc7-104">Azure bulut Kabuk Azure kaynaklarını yönetmek için etkileşimli, tarayıcı erişilebilir bir kabuk ' dir.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="6cdc7-105">Özellikler</span><span class="sxs-lookup"><span data-stu-id="6cdc7-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="6cdc7-106">Kabuk tarayıcı tabanlı deneyimi</span><span class="sxs-lookup"><span data-stu-id="6cdc7-106">Browser-based shell experience</span></span>
<span data-ttu-id="6cdc7-107">Bulut Kabuk aklınızda Azure yönetim görevleri ile yerleşik bir tarayıcı tabanlı komut satırı deneyimi erişmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-107">Cloud Shell enables access to a browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="6cdc7-108">Bir yalnızca bulut yolla yerel makineden untethered çalışması için Dengeleme bulut Kabuk sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-108">Leverage Cloud Shell to work untethered from a local machine in a way only the cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="6cdc7-109">Önceden yapılandırılmış Azure iş istasyonu</span><span class="sxs-lookup"><span data-stu-id="6cdc7-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="6cdc7-110">Bulut Kabuk popüler komut satırı araçları ile önceden yüklü olarak gelen ve daha hızlı çalışabilmeniz için dil desteği.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="6cdc7-111">Tam araç listesi için Azure bulut Kabuk burada görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-111">View the full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="6cdc7-112">Otomatik kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="6cdc7-112">Automatic authentication</span></span>
<span data-ttu-id="6cdc7-113">Bulut Kabuğu güvenli bir şekilde otomatik olarak her oturum için anlık kaynaklarınıza erişmek için Azure CLI 2.0 aracılığıyla üzerinde kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-113">Cloud Shell securely authenticates automatically on each session for instant access to your resources through the Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="6cdc7-114">Azure dosya depolama birimini bağlayın</span><span class="sxs-lookup"><span data-stu-id="6cdc7-114">Connect your Azure File storage</span></span>
<span data-ttu-id="6cdc7-115">Bulut Kabuk makine geçicidir ve sonuç olarak Azure dosya paylaşımının olarak bağlanmasını gerektiren `clouddrive` $Home dizininize kalıcı hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-115">Cloud Shell machines are temporary and as a result require an Azure file share to be mounted as `clouddrive` to persist your $Home directory.</span></span>
<span data-ttu-id="6cdc7-116">Bir kaynak oluşturmak için bulut Kabuk ister üzerinde ilk kez başlatıldığında, sizin adınıza grup, depolama hesabı ve dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-116">On first launch Cloud Shell prompts to create a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="6cdc7-117">Bu tek seferlik bir adımdır ve tüm oturumları için otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="6cdc7-118">Yeni depolama alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6cdc7-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="6cdc7-119">Yerel olarak yedekli depolama (LRS) hesabı sizin adınıza bir varsayılan 5 GB disk görüntüsü içeren bir Azure dosya paylaşımı ile oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="6cdc7-120">Dosya Paylaşımı bağladığı olarak `clouddrive` eşitleme ve $Home dizininize kalıcı hale getirmek için kullanılan disk görüntüsü ile etkileşim için dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-120">The file share mounts as `clouddrive` for file share interaction with the disk image being used to sync and persist your $Home directory.</span></span> <span data-ttu-id="6cdc7-121">Normal depolama ücretleri.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-121">Regular storage costs apply.</span></span>

<span data-ttu-id="6cdc7-122">Üç kaynakları sizin adınıza oluşturulacak:</span><span class="sxs-lookup"><span data-stu-id="6cdc7-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="6cdc7-123">Kaynak grubu adı:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="6cdc7-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="6cdc7-124">Adlı depolama hesabı:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="6cdc7-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="6cdc7-125">Adlı dosya paylaşımı:`cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="6cdc7-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="6cdc7-126">SSH anahtarları gibi $Home dizininizdeki tüm dosyalara, bağlı dosya paylaşımında depolanan kullanıcı disk görüntünüzdeki kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="6cdc7-127">Dosyaları, $Home dizin ve bağlı dosya paylaşımı kaydedilirken en iyi yöntemleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="6cdc7-128">Var olan kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="6cdc7-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="6cdc7-129">Gelişmiş bir seçenek de bulut Kabuğu mevcut kaynaklarla ilişkilendirmek olanak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-129">An advanced option is also provided allowing you to associate existing resources to Cloud Shell.</span></span> <span data-ttu-id="6cdc7-130">Depolama Kurulum istemiyle sunulduğunda "Göster ayarları" Gelişmiş ek seçenekleri seçin.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-130">When presented with the storage setup prompt, click "Show advanced settings" to select additional options.</span></span> <span data-ttu-id="6cdc7-131">Bırakmalar atanmış olan bulut Kabuk bölge ve yerel olarak/genel-yedekli depolama hesapları için filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="6cdc7-132">[Öğrenin bulut Kabuk depolama hakkında dosya paylaşımları güncelleştirme ve karşıya yükleme ve indirme dosyaları.] (kalıcı-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="6cdc7-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="6cdc7-133">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="6cdc7-133">Concepts</span></span>
* <span data-ttu-id="6cdc7-134">Bulut Kabuk bir oturuma özgü üzerinde kullanıcı başına sağlanan geçici bir makinede çalıştırır</span><span class="sxs-lookup"><span data-stu-id="6cdc7-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="6cdc7-135">Bulut Kabuk etkileşimli etkinliği olmadan 20 dakika sonra zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="6cdc7-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="6cdc7-136">Bulut Kabuk yalnızca bağlı bir dosya paylaşımı ile erişilebilir</span><span class="sxs-lookup"><span data-stu-id="6cdc7-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="6cdc7-137">Bulut Kabuk atanmış bir makine her kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="6cdc7-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="6cdc7-138">İzinler normal bir Linux kullanıcı ayarlanır</span><span class="sxs-lookup"><span data-stu-id="6cdc7-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="6cdc7-139">Tüm bulut Kabuk özellikleri hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="6cdc7-140">Örnekler</span><span class="sxs-lookup"><span data-stu-id="6cdc7-140">Examples</span></span>
* <span data-ttu-id="6cdc7-141">Oluşturma veya Azure Yönetimi otomatikleştirmek için komut dosyaları düzenleme</span><span class="sxs-lookup"><span data-stu-id="6cdc7-141">Create or edit scripts to automate Azure management</span></span>
* <span data-ttu-id="6cdc7-142">Aynı anda Azure portalı ve Azure CLI 2.0 aracılığıyla kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="6cdc7-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="6cdc7-143">Azure CLI 2.0 dediğini</span><span class="sxs-lookup"><span data-stu-id="6cdc7-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="6cdc7-144">Bulut Kabuk hızlı başlangıç, tüm bu örneklerde deneyin.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-144">Try out all these examples at the Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="6cdc7-145">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="6cdc7-145">Pricing</span></span>
<span data-ttu-id="6cdc7-146">Bulut Kabuk barındıran makine, bir önkoşul $Home dizininize kalıcı hale getirmek için bir bağlı Azure dosya paylaşımı ile ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-146">The machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share to persist your $Home directory.</span></span> <span data-ttu-id="6cdc7-147">Normal depolama ücretleri.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="6cdc7-148">Desteklenen tarayıcılar</span><span class="sxs-lookup"><span data-stu-id="6cdc7-148">Supported browsers</span></span>
<span data-ttu-id="6cdc7-149">Bulut Kabuk Chrome, sınır ve Safari için önerilir.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="6cdc7-150">Bulut Kabuk Chrome, Firefox, Safari, IE ve kenar desteklense de, bulut Kabuk belirli tarayıcı ayarları tabi değil.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject to specific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6cdc7-151">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="6cdc7-151">Troubleshooting</span></span>
1. <span data-ttu-id="6cdc7-152">Bir Azure Active Directory aboneliğine kullanırken, depolama hata nedeniyle oluşturulamıyor: 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-152">When using an Azure Active Directory subscription, I cannot create storage due to Error: 400 DisallowedOperation.</span></span> <span data-ttu-id="6cdc7-153">Bu sorunu çözmek için lütfen depolama kaynaklarını oluşturabileceğinden Azure aboneliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-153">To resolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="6cdc7-154">AD abonelikleri Azure kaynaklarını oluşturmak mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="6cdc7-154">AD subscriptions are not able to create Azure resources.</span></span>

<span data-ttu-id="6cdc7-155">Belirli bilinen sınırlamalar ziyaret [bulut Kabuk sınırlamaları](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="6cdc7-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
