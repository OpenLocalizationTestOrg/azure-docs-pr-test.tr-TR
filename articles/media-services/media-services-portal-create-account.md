---
title: "aaaCreate hello Azure portal ile bir Azure Media Services hesabı | Microsoft Docs"
description: "Bu öğretici, hello Azure portal ile Azure Media Services hesabı oluşturma hello adım adım anlatılmaktadır."
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
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="868f0-103">Hello Azure portal kullanarak bir Azure Media Services hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="868f0-103">Create an Azure Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="868f0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="868f0-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="868f0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="868f0-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="868f0-106">REST</span><span class="sxs-lookup"><span data-stu-id="868f0-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="868f0-107">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="868f0-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="868f0-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="868f0-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="868f0-109">Hello Azure portal tooquickly bir Azure Media Services (AMS) hesap oluşturma bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="868f0-109">hello Azure portal provides a way tooquickly create an Azure Media Services (AMS) account.</span></span> <span data-ttu-id="868f0-110">Hesap tooaccess, toostore etkinleştirmek, şifrelemek, kodlama, yönetmek ve azure'da medya içeriği akış medya Hizmetleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f0-110">You can use your account tooaccess Media Services that enable you toostore, encrypt, encode, manage, and stream media content in Azure.</span></span> <span data-ttu-id="868f0-111">Merhaba zaman, Media Services hesabı oluşturma, ayrıca ilişkili bir depolama hesabı oluşturun (veya mevcut bir kullanabilirsiniz) hello içinde aynı coğrafi bölgede hello Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="868f0-111">At hello time you create a Media Services account, you also create an associated storage account (or use an existing one) in hello same geographic region as hello Media Services account.</span></span>

<span data-ttu-id="868f0-112">Bu makalede, bazı ortak kavramları açıklar ve nasıl toocreate Media Services hesap hello Azure portal ile gösterir.</span><span class="sxs-lookup"><span data-stu-id="868f0-112">This article explains some common concepts and shows how toocreate a Media Services account with hello Azure portal.</span></span>

## <a name="concepts"></a><span data-ttu-id="868f0-113">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="868f0-113">Concepts</span></span>
<span data-ttu-id="868f0-114">Media Services’e erişim iki ilişkili hesap gerektirir:</span><span class="sxs-lookup"><span data-stu-id="868f0-114">Accessing Media Services requires two associated accounts:</span></span>

* <span data-ttu-id="868f0-115">Bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="868f0-115">A Media Services account.</span></span> <span data-ttu-id="868f0-116">Mevcut olan bulut tabanlı Media Services tooa kümesi erişim, hesap sağlar.</span><span class="sxs-lookup"><span data-stu-id="868f0-116">Your account gives you access tooa set of cloud-based Media Services that are available in Azure.</span></span> <span data-ttu-id="868f0-117">Bir Media Services hesabı gerçek medya verilerini depolamaz.</span><span class="sxs-lookup"><span data-stu-id="868f0-117">A Media Services account does not store actual media content.</span></span> <span data-ttu-id="868f0-118">Bunun yerine, hesabınızdaki hello medya içeriği ve medya işleme işleri hakkındaki meta verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="868f0-118">Instead it stores metadata about hello media content and media processing jobs in your account.</span></span> <span data-ttu-id="868f0-119">Merhaba hesabı oluşturma hello aynı anda kullanılabilir bir Media Services bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="868f0-119">At hello time you create hello account, you select an available Media Services region.</span></span> <span data-ttu-id="868f0-120">Seçtiğiniz hello hello hesabınız için meta veri kayıtlarını saklayan bir veri merkezi bölgedir.</span><span class="sxs-lookup"><span data-stu-id="868f0-120">hello region you select is a data center that stores hello metadata records for your account.</span></span>
  
* <span data-ttu-id="868f0-121">Bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="868f0-121">An Azure storage account.</span></span> <span data-ttu-id="868f0-122">Hello depolama hesapları bulunan aynı coğrafi bölgede hello Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="868f0-122">Storage accounts must be located in hello same geographic region as hello Media Services account.</span></span> <span data-ttu-id="868f0-123">Bir Media Services hesabı oluşturduğunuzda ya da mevcut bir depolama hesabını seçebileceğiniz hello hello içinde yeni bir depolama hesabı aynı bölgede veya oluşturabilirsiniz aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="868f0-123">When you create a Media Services account, you can either choose an existing storage account in hello same region, or you can create a new storage account in hello same region.</span></span> <span data-ttu-id="868f0-124">Bir Media Services hesabını silerseniz ilişkili depolama hesabınızdaki hello BLOB'lar silinmez.</span><span class="sxs-lookup"><span data-stu-id="868f0-124">If you delete a Media Services account, hello blobs in your related storage account are not deleted.</span></span>

> [!NOTE]
> <span data-ttu-id="868f0-125">Azure Media Services özelliklerinin farklı bölgelerde kullanılabilirliği hakkında bilgi için bkz. [Veri merkezleri arasında AMS özelliklerinin kullanılabilirliği](scenarios-and-availability.md#availability).</span><span class="sxs-lookup"><span data-stu-id="868f0-125">For information about availability of Azure Media Services features in different regions, see [availability of AMS features across datacenters](scenarios-and-availability.md#availability).</span></span>

## <a name="create-an-ams-account"></a><span data-ttu-id="868f0-126">AMS hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="868f0-126">Create an AMS account</span></span>
<span data-ttu-id="868f0-127">Merhaba adımları bu bölümünde Göster nasıl toocreate bir AMS hesabının.</span><span class="sxs-lookup"><span data-stu-id="868f0-127">hello steps in this section show how toocreate an AMS account.</span></span>

1. <span data-ttu-id="868f0-128">Merhaba oturum açma [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="868f0-128">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="868f0-129">**+Yeni** > **Web + Mobil** > **Media Services**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="868f0-129">Click **+New** > **Web + Mobile** > **Media Services**.</span></span>
   
    ![Media Services Oluşturma](./media/media-services-create-account/media-services-new1.png)
3. <span data-ttu-id="868f0-131">**MEDYA HİZMETLERİ HESABI OLUŞTUR**’a gerekli değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="868f0-131">In **CREATE MEDIA SERVICES ACCOUNT** enter required values.</span></span>
   
    ![Media Services Oluşturma](./media/media-services-create-account/media-services-new3.png)
   
   1. <span data-ttu-id="868f0-133">İçinde **hesap adı**, hello hello yeni AMS hesabının adını girin.</span><span class="sxs-lookup"><span data-stu-id="868f0-133">In **Account Name**, enter hello name of hello new AMS account.</span></span> <span data-ttu-id="868f0-134">Bir Media Services hesabı adı tüm küçük harf ya da boşluk numaralarıyla ve 3 too24 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="868f0-134">A Media Services account name is all lowercase letters or numbers with no spaces, and is 3 too24 characters in length.</span></span>
   2. <span data-ttu-id="868f0-135">Abonelikte erişiminiz hello farklı Azure abonelikleri arasından seçim.</span><span class="sxs-lookup"><span data-stu-id="868f0-135">In Subscription, select among hello different Azure subscriptions that you have access to.</span></span>
   3. <span data-ttu-id="868f0-136">İçinde **kaynak grubu**, hello yeni veya mevcut bir kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="868f0-136">In **Resource Group**, select hello new or existing resource.</span></span>  <span data-ttu-id="868f0-137">Kaynak grubu; yaşam döngüsünü, izinleri ve ilkeleri paylaşan kaynakların bir koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="868f0-137">A resource group is a collection of resources that share lifecycle, permissions, and policies.</span></span> <span data-ttu-id="868f0-138">[Burada](../azure-resource-manager/resource-group-overview.md#resource-groups) daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="868f0-138">Learn more [here](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   4. <span data-ttu-id="868f0-139">İçinde **konumu**, hello Media Services hesabınız için kullanılan toostore hello medya ve meta veri kayıtlarını olacaktır coğrafi bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="868f0-139">In **Location**,  select hello geographic region that will be used toostore hello media and metadata records for your Media Services account.</span></span> <span data-ttu-id="868f0-140">Bu bölge medyanızı akışını sağlamak ve kullanılan tooprocess olması.</span><span class="sxs-lookup"><span data-stu-id="868f0-140">This  region will be used tooprocess and stream your media.</span></span> <span data-ttu-id="868f0-141">Yalnızca hello Media Services kullanılabilen bölgeler hello aşağı açılan liste kutusunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="868f0-141">Only hello available Media Services regions appear in hello drop-down list box.</span></span> 
   5. <span data-ttu-id="868f0-142">İçinde **depolama hesabı**, Media Services hesabınızdan bir depolama hesabı tooprovide blob depolama hello medya içeriği seçin.</span><span class="sxs-lookup"><span data-stu-id="868f0-142">In **Storage Account**, select a storage account tooprovide blob storage of hello media content from your Media Services account.</span></span> <span data-ttu-id="868f0-143">Mevcut bir depolama hesabını hello seçebilirsiniz Media Services hesabınızla veya aynı coğrafi bölgede bir depolama hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f0-143">You can select an existing storage account in hello same geographic region as your Media Services account, or you can create a storage account.</span></span> <span data-ttu-id="868f0-144">Yeni bir depolama hesabı aynı hello oluşturulan bölge.</span><span class="sxs-lookup"><span data-stu-id="868f0-144">A new storage account is created in hello same region.</span></span> <span data-ttu-id="868f0-145">Depolama hesabı için adları hello kurallar aynı Media Services hesapları için olduğu gibi hello.</span><span class="sxs-lookup"><span data-stu-id="868f0-145">hello rules for storage account names are hello same as for Media Services accounts.</span></span>
      
       <span data-ttu-id="868f0-146">Depolama hakkında daha fazla bilgi [burada](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="868f0-146">Learn more about storage [here](../storage/common/storage-introduction.md).</span></span>
   6. <span data-ttu-id="868f0-147">Seçin **PIN toodashboard** toosee hello hello hesap dağıtımının ilerlemesini.</span><span class="sxs-lookup"><span data-stu-id="868f0-147">Select **Pin toodashboard** toosee hello progress of hello account deployment.</span></span>
4. <span data-ttu-id="868f0-148">Tıklatın **oluşturma** hello form hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="868f0-148">Click **Create** at hello bottom of hello form.</span></span>
   
    <span data-ttu-id="868f0-149">Merhaba hesap başarıyla oluşturulduktan sonra genel bakış sayfasına yükler.</span><span class="sxs-lookup"><span data-stu-id="868f0-149">Once hello account is successfully created, overview page loads.</span></span> <span data-ttu-id="868f0-150">Hello uç nokta tablo hello hesabı Akış akış uç noktası hello içinde varsayılan olacaktır **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="868f0-150">In hello streaming endpoint table hello account will have a default streaming endpoint in hello **Stopped** state.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="868f0-151">AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu.</span><span class="sxs-lookup"><span data-stu-id="868f0-151">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="868f0-152">İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu.</span><span class="sxs-lookup"><span data-stu-id="868f0-152">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
   
## <a name="toomanage-your-ams-account"></a><span data-ttu-id="868f0-153">toomanage AMS hesabınızı</span><span class="sxs-lookup"><span data-stu-id="868f0-153">toomanage your AMS account</span></span>

<span data-ttu-id="868f0-154">toomanage AMS hesabınızı (örneğin, toohello AMS API program aracılığıyla bağlanmak, videoları karşıya yüklemek, varlıkları kodlamak, içerik koruma yapılandırma, işin ilerleme durumunu izlemek) seçin **ayarları** yan hello portalının sol hello üzerinde.</span><span class="sxs-lookup"><span data-stu-id="868f0-154">toomanage your AMS account (for example, connect toohello AMS API programmatically, upload videos, encode assets, configure content protection, monitor job progress) select **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="868f0-155">Merhaba gelen **ayarları**, hello kullanılabilir Kanatlar tooone gidin (örneğin: **API erişimini**, **varlıklar**, **işleri**, **İçerik koruma**).</span><span class="sxs-lookup"><span data-stu-id="868f0-155">From hello **Settings**, navigate tooone of hello available blades (for example: **API access**, **Assets**, **Jobs**, **Content protection**).</span></span>


## <a name="next-steps"></a><span data-ttu-id="868f0-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="868f0-156">Next steps</span></span>

<span data-ttu-id="868f0-157">Bundan böyle dosyaları AMS hesabınıza yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="868f0-157">You can now upload files into your AMS account.</span></span> <span data-ttu-id="868f0-158">Daha fazla bilgi için bkz. [Dosya yükleme](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="868f0-158">For more information, see [Upload files](media-services-portal-upload-files.md).</span></span>

<span data-ttu-id="868f0-159">Tooaccess AMS API program aracılığıyla planlıyorsanız bkz [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="868f0-159">If you plan tooaccess AMS API programmatically, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="868f0-160">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="868f0-160">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="868f0-161">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="868f0-161">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

