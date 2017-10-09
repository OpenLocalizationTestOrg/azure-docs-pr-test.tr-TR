---
title: "aaaAzure bulut Kabuğu (Önizleme) genel bakış | Microsoft Docs"
description: "Hello Azure bulut Kabuk genel bakış."
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
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a><span data-ttu-id="fd484-103">Azure bulut Kabuğu (Önizleme) genel bakış</span><span class="sxs-lookup"><span data-stu-id="fd484-103">Overview of Azure Cloud Shell (Preview)</span></span>
<span data-ttu-id="fd484-104">Azure bulut Kabuk Azure kaynaklarını yönetmek için etkileşimli, tarayıcı erişilebilir bir kabuk ' dir.</span><span class="sxs-lookup"><span data-stu-id="fd484-104">Azure Cloud Shell is an interactive, browser-accessible shell for managing Azure resources.</span></span>

![](media/overview-pic.png)

## <a name="features"></a><span data-ttu-id="fd484-105">Özellikler</span><span class="sxs-lookup"><span data-stu-id="fd484-105">Features</span></span>
### <a name="browser-based-shell-experience"></a><span data-ttu-id="fd484-106">Kabuk tarayıcı tabanlı deneyimi</span><span class="sxs-lookup"><span data-stu-id="fd484-106">Browser-based shell experience</span></span>
<span data-ttu-id="fd484-107">Azure yönetim görevlerinizi aklınızda ile oluşturulan Kabuk etkinleştirir erişim tooa tarayıcı tabanlı komut satırı deneyimi bulut.</span><span class="sxs-lookup"><span data-stu-id="fd484-107">Cloud Shell enables access tooa browser-based command-line experience built with Azure management tasks in mind.</span></span> <span data-ttu-id="fd484-108">Yerel makinede yalnızca hello bulut sağlayabilir şekilde untethered bulut Kabuk toowork yararlanın.</span><span class="sxs-lookup"><span data-stu-id="fd484-108">Leverage Cloud Shell toowork untethered from a local machine in a way only hello cloud can provide.</span></span>

### <a name="pre-configured-azure-workstation"></a><span data-ttu-id="fd484-109">Önceden yapılandırılmış Azure iş istasyonu</span><span class="sxs-lookup"><span data-stu-id="fd484-109">Pre-configured Azure workstation</span></span>
<span data-ttu-id="fd484-110">Bulut Kabuk popüler komut satırı araçları ile önceden yüklü olarak gelen ve daha hızlı çalışabilmeniz için dil desteği.</span><span class="sxs-lookup"><span data-stu-id="fd484-110">Cloud Shell comes pre-installed with popular command-line tools and language support so you can work faster.</span></span>

[<span data-ttu-id="fd484-111">Görünüm hello tam araç listesini Azure bulut Kabuğu burada.</span><span class="sxs-lookup"><span data-stu-id="fd484-111">View hello full tooling list for Azure Cloud Shell here.</span></span>](features.md#tools)

### <a name="automatic-authentication"></a><span data-ttu-id="fd484-112">Otomatik kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="fd484-112">Automatic authentication</span></span>
<span data-ttu-id="fd484-113">Bulut Kabuğu güvenli bir şekilde otomatik olarak her oturum için anında erişim tooyour kaynaklara hello Azure CLI 2.0 aracılığıyla üzerinde kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="fd484-113">Cloud Shell securely authenticates automatically on each session for instant access tooyour resources through hello Azure CLI 2.0.</span></span>

### <a name="connect-your-azure-file-storage"></a><span data-ttu-id="fd484-114">Azure dosya depolama birimini bağlayın</span><span class="sxs-lookup"><span data-stu-id="fd484-114">Connect your Azure File storage</span></span>
<span data-ttu-id="fd484-115">Bulut Kabuk makineler geçicidir ve sonuç olarak olarak oluşturulmuş bir Azure dosya paylaşımı toobe gerektiren `clouddrive` toopersist $Home dizin.</span><span class="sxs-lookup"><span data-stu-id="fd484-115">Cloud Shell machines are temporary and as a result require an Azure file share toobe mounted as `clouddrive` toopersist your $Home directory.</span></span>
<span data-ttu-id="fd484-116">Üzerinde ilk kez başlatıldığında, sizin adınıza bir kaynak grubu, depolama hesabı ve dosya paylaşımı toocreate bulut Kabuk ister.</span><span class="sxs-lookup"><span data-stu-id="fd484-116">On first launch Cloud Shell prompts toocreate a resource group, storage account, and file share on your behalf.</span></span> <span data-ttu-id="fd484-117">Bu tek seferlik bir adımdır ve tüm oturumları için otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="fd484-117">This is a one-time step and will be automatically attached for all sessions.</span></span> 

#### <a name="create-new-storage"></a><span data-ttu-id="fd484-118">Yeni depolama alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd484-118">Create new storage</span></span>
![](media/basic-storage.png)

<span data-ttu-id="fd484-119">Yerel olarak yedekli depolama (LRS) hesabı sizin adınıza bir varsayılan 5 GB disk görüntüsü içeren bir Azure dosya paylaşımı ile oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="fd484-119">A locally-redundant storage (LRS) account can be created on your behalf with an Azure file share containing a default 5-GB disk image.</span></span> <span data-ttu-id="fd484-120">Merhaba dosya paylaşımı bağladığı olarak `clouddrive` hello disk görüntüsü ile etkileşim için dosya paylaşımı kullanılan toosync olması ve $Home dizininize kalır.</span><span class="sxs-lookup"><span data-stu-id="fd484-120">hello file share mounts as `clouddrive` for file share interaction with hello disk image being used toosync and persist your $Home directory.</span></span> <span data-ttu-id="fd484-121">Normal depolama ücretleri.</span><span class="sxs-lookup"><span data-stu-id="fd484-121">Regular storage costs apply.</span></span>

<span data-ttu-id="fd484-122">Üç kaynakları sizin adınıza oluşturulacak:</span><span class="sxs-lookup"><span data-stu-id="fd484-122">Three resources will be created on your behalf:</span></span>
1. <span data-ttu-id="fd484-123">Kaynak grubu adı:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="fd484-123">Resource Group named: `cloud-shell-storage-<region>`</span></span>
2. <span data-ttu-id="fd484-124">Adlı depolama hesabı:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="fd484-124">Storage Account named: `cs<uniqueGuid>`</span></span>
3. <span data-ttu-id="fd484-125">Adlı dosya paylaşımı:`cs-<user>-<domain>-com-uniqueGuid`</span><span class="sxs-lookup"><span data-stu-id="fd484-125">File Share named: `cs-<user>-<domain>-com-uniqueGuid`</span></span>

> [!Note]
> <span data-ttu-id="fd484-126">SSH anahtarları gibi $Home dizininizdeki tüm dosyalara, bağlı dosya paylaşımında depolanan kullanıcı disk görüntünüzdeki kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="fd484-126">All files in your $Home directory such as SSH keys are persisted in your user disk image stored in your mounted file share.</span></span> <span data-ttu-id="fd484-127">Dosyaları, $Home dizin ve bağlı dosya paylaşımı kaydedilirken en iyi yöntemleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="fd484-127">Apply best practices when saving files in your $Home directory and mounted file share.</span></span>

#### <a name="use-existing-resources"></a><span data-ttu-id="fd484-128">Var olan kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="fd484-128">Use existing resources</span></span>
![](media/advanced-storage.png)

<span data-ttu-id="fd484-129">Gelişmiş bir seçenek de izin verme, tooassociate mevcut kaynakları tooCloud Kabuk sağlanır.</span><span class="sxs-lookup"><span data-stu-id="fd484-129">An advanced option is also provided allowing you tooassociate existing resources tooCloud Shell.</span></span> <span data-ttu-id="fd484-130">Merhaba depolama Kurulum istemiyle sunulduğunda "Gelişmiş Göster ayarları" tooselect Ek Seçenekler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="fd484-130">When presented with hello storage setup prompt, click "Show advanced settings" tooselect additional options.</span></span> <span data-ttu-id="fd484-131">Bırakmalar atanmış olan bulut Kabuk bölge ve yerel olarak/genel-yedekli depolama hesapları için filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="fd484-131">Dropdowns are filtered for your assigned Cloud Shell region and locally/globally-redundant storage accounts.</span></span>

<span data-ttu-id="fd484-132">[Öğrenin bulut Kabuk depolama hakkında dosya paylaşımları güncelleştirme ve karşıya yükleme ve indirme dosyaları.] (kalıcı-shell-storage.md)</span><span class="sxs-lookup"><span data-stu-id="fd484-132">[Learn about Cloud Shell storage, updating file shares, and uploading/downloading files.] (persisting-shell-storage.md)</span></span>

## <a name="concepts"></a><span data-ttu-id="fd484-133">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="fd484-133">Concepts</span></span>
* <span data-ttu-id="fd484-134">Bulut Kabuk bir oturuma özgü üzerinde kullanıcı başına sağlanan geçici bir makinede çalıştırır</span><span class="sxs-lookup"><span data-stu-id="fd484-134">Cloud Shell runs on a temporary machine provided on a per-session, per-user basis</span></span>
* <span data-ttu-id="fd484-135">Bulut Kabuk etkileşimli etkinliği olmadan 20 dakika sonra zaman aşımına uğradı</span><span class="sxs-lookup"><span data-stu-id="fd484-135">Cloud Shell times out after 20 minutes without interactive activity</span></span>
* <span data-ttu-id="fd484-136">Bulut Kabuk yalnızca bağlı bir dosya paylaşımı ile erişilebilir</span><span class="sxs-lookup"><span data-stu-id="fd484-136">Cloud Shell can only be accessed with a file share attached</span></span>
* <span data-ttu-id="fd484-137">Bulut Kabuk atanmış bir makine her kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="fd484-137">Cloud Shell is assigned one machine per user account</span></span>
* <span data-ttu-id="fd484-138">İzinler normal bir Linux kullanıcı ayarlanır</span><span class="sxs-lookup"><span data-stu-id="fd484-138">Permissions are set as a regular Linux user</span></span>

[<span data-ttu-id="fd484-139">Tüm bulut Kabuk özellikleri hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="fd484-139">Learn more about all Cloud Shell features.</span></span>](features.md)

## <a name="examples"></a><span data-ttu-id="fd484-140">Örnekler</span><span class="sxs-lookup"><span data-stu-id="fd484-140">Examples</span></span>
* <span data-ttu-id="fd484-141">Oluşturma veya komut dosyaları tooautomate Azure Yönetimi düzenleme</span><span class="sxs-lookup"><span data-stu-id="fd484-141">Create or edit scripts tooautomate Azure management</span></span>
* <span data-ttu-id="fd484-142">Aynı anda Azure portalı ve Azure CLI 2.0 aracılığıyla kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="fd484-142">Simultaneously manage resources via Azure portal and Azure CLI 2.0</span></span>
* <span data-ttu-id="fd484-143">Azure CLI 2.0 dediğini</span><span class="sxs-lookup"><span data-stu-id="fd484-143">Test-drive Azure CLI 2.0</span></span>

[<span data-ttu-id="fd484-144">Bu örnekler hello bulut Kabuk hızlı başlangıç adresindeki deneyin.</span><span class="sxs-lookup"><span data-stu-id="fd484-144">Try out all these examples at hello Cloud Shell quickstart.</span></span>](quickstart.md)

## <a name="pricing"></a><span data-ttu-id="fd484-145">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="fd484-145">Pricing</span></span>
<span data-ttu-id="fd484-146">Merhaba makine bulut Kabuk barındırma ücretsizdir, önkoşul bağlı Azure dosyasının ile toopersist $Home dizininize paylaşma.</span><span class="sxs-lookup"><span data-stu-id="fd484-146">hello machine hosting Cloud Shell is free, with a pre-requisite of a mounted Azure file share toopersist your $Home directory.</span></span> <span data-ttu-id="fd484-147">Normal depolama ücretleri.</span><span class="sxs-lookup"><span data-stu-id="fd484-147">Regular storage costs apply.</span></span>

## <a name="supported-browsers"></a><span data-ttu-id="fd484-148">Desteklenen tarayıcılar</span><span class="sxs-lookup"><span data-stu-id="fd484-148">Supported browsers</span></span>
<span data-ttu-id="fd484-149">Bulut Kabuk Chrome, sınır ve Safari için önerilir.</span><span class="sxs-lookup"><span data-stu-id="fd484-149">Cloud Shell is recommended for Chrome, Edge, and Safari.</span></span> <span data-ttu-id="fd484-150">Bulut Kabuk Chrome, Firefox, Safari, IE ve kenar desteklense de, bulut Kabuk konu toospecific tarayıcı ayarları'dır.</span><span class="sxs-lookup"><span data-stu-id="fd484-150">While Cloud Shell is supported for Chrome, Firefox, Safari, IE, and Edge, Cloud Shell is subject toospecific browser settings.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fd484-151">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fd484-151">Troubleshooting</span></span>
1. <span data-ttu-id="fd484-152">Bir Azure Active Directory aboneliğine kullanırken, depolama oluşturulamıyor son tooError: 400 DisallowedOperation.</span><span class="sxs-lookup"><span data-stu-id="fd484-152">When using an Azure Active Directory subscription, I cannot create storage due tooError: 400 DisallowedOperation.</span></span> <span data-ttu-id="fd484-153">tooresolve Bu, lütfen depolama kaynaklarını oluşturabileceğinden Azure aboneliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="fd484-153">tooresolve this, please use an Azure subscription capable of creating storage resources.</span></span> <span data-ttu-id="fd484-154">AD aboneliklerini erişilemiyor toocreate Azure kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="fd484-154">AD subscriptions are not able toocreate Azure resources.</span></span>

<span data-ttu-id="fd484-155">Belirli bilinen sınırlamalar ziyaret [bulut Kabuk sınırlamaları](limitations.md).</span><span class="sxs-lookup"><span data-stu-id="fd484-155">For specific known limitations, visit [limitations of Cloud Shell](limitations.md).</span></span>
