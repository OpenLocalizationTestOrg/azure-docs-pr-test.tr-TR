---
title: "Azure portalı ile Azure Media Services hesabı oluşturma | Microsoft Belgeleri"
description: "Bu öğretici, Azure portalıyla bir Azure Media Services hesabı oluşturma adımlarında size kılavuzluk eder."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: 919a0b2f390bab353d24423d7f216e7031581aba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-media-services-account-using-the-azure-portal"></a><span data-ttu-id="a2e91-103">Azure portal ile Azure Media Services hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e91-103">Create an Azure Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2e91-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a2e91-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="a2e91-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2e91-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="a2e91-106">REST</span><span class="sxs-lookup"><span data-stu-id="a2e91-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="a2e91-107">Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2e91-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="a2e91-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2e91-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="a2e91-109">Azure portalı bir Azure Media Services (AMS) hesabını hızlıca oluşturmanın yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2e91-109">The Azure portal provides a way to quickly create an Azure Media Services (AMS) account.</span></span> <span data-ttu-id="a2e91-110">Azure’da medya içeriği depolamanıza, şifrelemenize, kodlamanıza, yönetmenize ve akış yapmanıza imkan tanıyan Media Services’e erişmek için hesabınızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e91-110">You can use your account to access Media Services that enable you to store, encrypt, encode, manage, and stream media content in Azure.</span></span> <span data-ttu-id="a2e91-111">Bir Media Services hesabı oluşturduğunuzda Media Services hesabı ile aynı coğrafi bölgede ilişkili bir depolama hesabı da oluşturursunuz (ya da var olanı kullanırsınız).</span><span class="sxs-lookup"><span data-stu-id="a2e91-111">At the time you create a Media Services account, you also create an associated storage account (or use an existing one) in the same geographic region as the Media Services account.</span></span>

<span data-ttu-id="a2e91-112">Bu makalede bazı genel kavramlar ve Azure portalı ile Media Services hesabı oluşturma işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a2e91-112">This article explains some common concepts and shows how to create a Media Services account with the Azure portal.</span></span>

## <a name="concepts"></a><span data-ttu-id="a2e91-113">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="a2e91-113">Concepts</span></span>
<span data-ttu-id="a2e91-114">Media Services’e erişim iki ilişkili hesap gerektirir:</span><span class="sxs-lookup"><span data-stu-id="a2e91-114">Accessing Media Services requires two associated accounts:</span></span>

* <span data-ttu-id="a2e91-115">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="a2e91-115">A Media Services account.</span></span> <span data-ttu-id="a2e91-116">Hesabınız Azure’da mevcut olan bir dizi bulut tabanlı Media Services hizmetine erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2e91-116">Your account gives you access to a set of cloud-based Media Services that are available in Azure.</span></span> <span data-ttu-id="a2e91-117">Bir Media Services hesabı gerçek medya verilerini depolamaz.</span><span class="sxs-lookup"><span data-stu-id="a2e91-117">A Media Services account does not store actual media content.</span></span> <span data-ttu-id="a2e91-118">Bunun yerine, hesabınızdaki medya içeriği ve medya işleme işleri hakkındaki meta verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="a2e91-118">Instead it stores metadata about the media content and media processing jobs in your account.</span></span> <span data-ttu-id="a2e91-119">Hesabı oluşturduğunuz sırada mevcut Media Services bölgelerinden birini seçin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-119">At the time you create the account, you select an available Media Services region.</span></span> <span data-ttu-id="a2e91-120">Seçtiğiniz bölge hesabınız için meta veri kayıtlarını saklayan veri merkezidir.</span><span class="sxs-lookup"><span data-stu-id="a2e91-120">The region you select is a data center that stores the metadata records for your account.</span></span>
  
* <span data-ttu-id="a2e91-121">Bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a2e91-121">An Azure storage account.</span></span> <span data-ttu-id="a2e91-122">Depolama hesapları Media Services hesabıyla aynı coğrafi bölgede olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2e91-122">Storage accounts must be located in the same geographic region as the Media Services account.</span></span> <span data-ttu-id="a2e91-123">Bir Media Services hesabı oluşturduğunuzda aynı bölgede var olan bir depolama hesabını seçebilir veya aynı bölgede yeni bir depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e91-123">When you create a Media Services account, you can either choose an existing storage account in the same region, or you can create a new storage account in the same region.</span></span> <span data-ttu-id="a2e91-124">Bir Media Services hesabını silerseniz ilişkili depolama hesabınızdaki blob’lar silinmez.</span><span class="sxs-lookup"><span data-stu-id="a2e91-124">If you delete a Media Services account, the blobs in your related storage account are not deleted.</span></span>

> [!NOTE]
> <span data-ttu-id="a2e91-125">Azure Media Services özelliklerinin farklı bölgelerde kullanılabilirliği hakkında bilgi için bkz. [Veri merkezleri arasında AMS özelliklerinin kullanılabilirliği](scenarios-and-availability.md#availability).</span><span class="sxs-lookup"><span data-stu-id="a2e91-125">For information about availability of Azure Media Services features in different regions, see [availability of AMS features across datacenters](scenarios-and-availability.md#availability).</span></span>

## <a name="create-an-ams-account"></a><span data-ttu-id="a2e91-126">AMS hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2e91-126">Create an AMS account</span></span>
<span data-ttu-id="a2e91-127">Bu bölümdeki adımlar bir AMS hesabının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2e91-127">The steps in this section show how to create an AMS account.</span></span>

1. <span data-ttu-id="a2e91-128">[Azure portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a2e91-128">Log in at the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a2e91-129">**+Yeni** > **Web + Mobil** > **Media Services**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2e91-129">Click **+New** > **Web + Mobile** > **Media Services**.</span></span>
   
    ![Media Services Oluşturma](./media/media-services-create-account/media-services-new1.png)
3. <span data-ttu-id="a2e91-131">**MEDYA HİZMETLERİ HESABI OLUŞTUR**’a gerekli değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-131">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span></span>
   
    ![Media Services Oluşturma](./media/media-services-create-account/media-services-new3.png)
   
   1. <span data-ttu-id="a2e91-133">**Hesap Adı**’nda, yeni AMS hesabının adını girin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-133">In **Account Name**, enter the name of the new AMS account.</span></span> <span data-ttu-id="a2e91-134">Media Services hesabı adı, boşluk olmadan, tümü sayı ve küçük harften oluşmalı ve 3-24 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2e91-134">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 to 24 characters in length.</span></span>
   2. <span data-ttu-id="a2e91-135">Abonelik’te, erişiminiz bulunan farklı Azure abonelikleri arasından seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="a2e91-135">In Subscription, select among the different Azure subscriptions that you have access to.</span></span>
   3. <span data-ttu-id="a2e91-136">**Kaynak Grubu**’nda yeni veya mevcut bir kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-136">In **Resource Group**, select the new or existing resource.</span></span>  <span data-ttu-id="a2e91-137">Kaynak grubu; yaşam döngüsünü, izinleri ve ilkeleri paylaşan kaynakların bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="a2e91-137">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="a2e91-138">[Burada](../azure-resource-manager/resource-group-overview.md#resource-groups) daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-138">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   4. <span data-ttu-id="a2e91-139">**Konum**’da, Media Services hesabınız için medya ve meta veri kayıtlarını depolamak üzere kullanılacak coğrafi bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-139">In **Location**,  select the geographic region that will be used to store the media and metadata records for your Media Services account.</span></span> <span data-ttu-id="a2e91-140">Bu bölge medyanızı işlemek ve akışını sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a2e91-140">This  region will be used to process and stream your media.</span></span> <span data-ttu-id="a2e91-141">Yalnızca Media Services kullanılabilen bölgeler açılır listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a2e91-141">Only the available Media Services regions appear in the drop-down list box.</span></span> 
   5. <span data-ttu-id="a2e91-142">**Depolama Hesabı** alanında, Media Services hesabınızdan gelen medya içeriğine blob depolama sağlamak üzere bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-142">In **Storage Account**, select a storage account to provide blob storage of the media content from your Media Services account.</span></span> <span data-ttu-id="a2e91-143">Media Services hesabınızla aynı coğrafi bölgede bulunan mevcut bir depolama hesabını seçebilir ya da bir depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e91-143">You can select an existing storage account in the same geographic region as your Media Services account, or you can create a storage account.</span></span> <span data-ttu-id="a2e91-144">Aynı bölgede yeni bir depolama hesabı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a2e91-144">A new storage account is created in the same region.</span></span> <span data-ttu-id="a2e91-145">Depolama hesabı adları için kurallar Media Services hesapları ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="a2e91-145">The rules for storage account names are the same as for Media Services accounts.</span></span>
      
       <span data-ttu-id="a2e91-146">Depolama hakkında daha fazla bilgi [burada](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a2e91-146">Learn more about storage [here](../storage/common/storage-introduction.md).</span></span>
   6. <span data-ttu-id="a2e91-147">Hesap dağıtımını ilerleme durumunu görmek için **Panoya sabitle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-147">Select **Pin to dashboard** to see the progress of the account deployment.</span></span>
4. <span data-ttu-id="a2e91-148">Formun alt kısmındaki **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2e91-148">Click **Create** at the bottom of the form.</span></span>
   
    <span data-ttu-id="a2e91-149">Hesap başarıyla oluşturulduktan sonra genel bakış sayfası yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a2e91-149">Once the account is successfully created, overview page loads.</span></span> <span data-ttu-id="a2e91-150">Akış uç noktası tablosunda hesapta **Durdurulmuş** durumda bir varsayılan akış uç noktası yer alır.</span><span class="sxs-lookup"><span data-stu-id="a2e91-150">In the streaming endpoint table the account will have a default streaming endpoint in the **Stopped** state.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="a2e91-151">AMS hesabınız oluşturulduğunda hesabınıza **Durdurulmuş** durumda bir **varsayılan** akış uç noktası eklenir.</span><span class="sxs-lookup"><span data-stu-id="a2e91-151">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="a2e91-152">İçerik akışını başlatmak ve dinamik paketleme ile dinamik şifrelemeden yararlanmak için içerik akışı yapmak istediğiniz akış uç noktasının **Çalışıyor** durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2e91-152">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
   
## <a name="to-manage-your-ams-account"></a><span data-ttu-id="a2e91-153">AMS hesabınızı yönetmek için</span><span class="sxs-lookup"><span data-stu-id="a2e91-153">To manage your AMS account</span></span>

<span data-ttu-id="a2e91-154">AMS hesabınızı yönetmek için (örneğin, AMS API’ye programlama aracılığıyla bağlanarak karşıya video yükleme, varlıkları kodlama, içerik korumayı yapılandırma, iş ilerleme durumunu izleme) portalın sol tarafında bulunan **Ayarlar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-154">To manage your AMS account (for example, connect to the AMS API programmatically, upload videos, encode assets, configure content protection, monitor job progress) select **Settings** on the left side of the portal.</span></span> <span data-ttu-id="a2e91-155">**Ayarlar**’da, kullanılabilir dikey pencerelerden birine (örneğin **API Erişimi**, **Varlıklar**, **İşler**, **İçerik koruma**) gidin.</span><span class="sxs-lookup"><span data-stu-id="a2e91-155">From the **Settings**, navigate to one of the available blades (for example: **API access**, **Assets**, **Jobs**, **Content protection**).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a2e91-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2e91-156">Next steps</span></span>

<span data-ttu-id="a2e91-157">Bundan böyle dosyaları AMS hesabınıza yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2e91-157">You can now upload files into your AMS account.</span></span> <span data-ttu-id="a2e91-158">Daha fazla bilgi için bkz. [Dosya yükleme](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="a2e91-158">For more information, see [Upload files](media-services-portal-upload-files.md).</span></span>

<span data-ttu-id="a2e91-159">AMS API’ye programlama aracılığıyla erişmeyi planlıyorsanız bkz. [Azure AD kimlik doğrulamasıyla Azure Media Services API’ye erişim](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a2e91-159">If you plan to access AMS API programmatically, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a2e91-160">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="a2e91-160">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a2e91-161">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="a2e91-161">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

