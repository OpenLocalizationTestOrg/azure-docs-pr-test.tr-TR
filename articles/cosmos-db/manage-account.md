---
title: "aaaManage hello Azure Portalı aracılığıyla Azure Cosmos DB hesap | Microsoft Docs"
description: "Nasıl toomanage Azure Cosmos DB hesap hello Azure Portal öğrenin. Hello Azure Portal tooview, kopyalama, silme ve erişimi hesaplarını kullanma hakkında bir kılavuz bulabilirsiniz."
keywords: Azure Portal, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="c02ac-105">Nasıl toomanage Azure Cosmos DB hesabı</span><span class="sxs-lookup"><span data-stu-id="c02ac-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="c02ac-106">Bilgi nasıl tooset genel tutarlılık, iş anahtarlarla ve hello Azure portalında Azure Cosmos DB hesabında silin.</span><span class="sxs-lookup"><span data-stu-id="c02ac-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="c02ac-107"><a id="consistency"></a>Azure Cosmos DB tutarlılık ayarlarını yönet</span><span class="sxs-lookup"><span data-stu-id="c02ac-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="c02ac-108">Merhaba sağ tutarlılık düzeyi seçerek uygulamanızı hello semantiği bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c02ac-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="c02ac-109">Azure Cosmos veritabanı hello kullanılabilir tutarlılık düzeylerini okuyarak öğrenmeniz [toomaximize kullanılabilirlik ve Azure Cosmos veritabanı performans düzeyleri tutarlılık kullanarak][consistency].</span><span class="sxs-lookup"><span data-stu-id="c02ac-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="c02ac-110">Azure Cosmos DB tutarlılık, kullanılabilirlik ve veritabanı hesabınız için kullanılabilir her tutarlılık düzeyinde performans garantileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c02ac-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="c02ac-111">Güçlü tutarlılık düzeyi olan veritabanı hesabınızı yapılandırma verilerinizi yalıtılmış tooa tek Azure bölgesi olmasını gerektirir ve genel olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c02ac-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="c02ac-112">Üzerinde diğer yandan Merhaba, gevşek tutarlılık düzeylerini - sınırlanmış eskime durumu, session veya son etkinleştir Merhaba, tooassociate veritabanı hesabınızı bilgileriyle Azure bölgelerinin herhangi bir sayı.</span><span class="sxs-lookup"><span data-stu-id="c02ac-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="c02ac-113">şu basit adımları hello nasıl tooselect hello veritabanı hesabınız için varsayılan tutarlılık düzeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="c02ac-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="c02ac-114">bir Azure Cosmos DB hesap toospecify hello varsayılan tutarlılık</span><span class="sxs-lookup"><span data-stu-id="c02ac-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="c02ac-115">Merhaba, [Azure portal](https://portal.azure.com/), Azure Cosmos DB hesabınıza erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="c02ac-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="c02ac-116">Merhaba hesabı dikey penceresinde tıklayın **varsayılan tutarlılık**.</span><span class="sxs-lookup"><span data-stu-id="c02ac-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="c02ac-117">Merhaba, **varsayılan tutarlılık** dikey penceresinde, select hello yeni tutarlılık düzeyi ve tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c02ac-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="c02ac-118">![Varsayılan tutarlılık oturumu][5]</span><span class="sxs-lookup"><span data-stu-id="c02ac-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="c02ac-119"><a id="keys"></a>Görüntülemek, kopyalamak ve erişim anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="c02ac-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="c02ac-120">Bir Azure Cosmos DB hesabı oluşturduğunuzda, hello hizmeti hello Azure Cosmos DB hesap erişildiğinde, kimlik doğrulaması için kullanılan iki ana erişim tuşu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c02ac-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="c02ac-121">İki erişim tuşu sağlayarak Azure Cosmos DB tooregenerate hello herhangi kesinti tooyour Azure Cosmos DB hesap anahtarlarla sağlar.</span><span class="sxs-lookup"><span data-stu-id="c02ac-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="c02ac-122">Merhaba, [Azure portal](https://portal.azure.com/), erişim hello **anahtarları** dikey penceresinde hello hello kaynak menüsünden **Azure Cosmos DB hesap** dikey tooview, kopyalama ve yeniden oluşturma hello erişim tuşları kullanılan tooaccess Azure Cosmos DB hesabınız var.</span><span class="sxs-lookup"><span data-stu-id="c02ac-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Azure Portal ekran, anahtarlar dikey penceresinde](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="c02ac-124">Merhaba **anahtarları** dikey penceresinde de içeren birincil ve kullanılan tooconnect tooyour olabilir ikincil bağlantı dizeleri hesap hello [veri geçiş aracı](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="c02ac-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="c02ac-125">Salt okunur anahtarları de bu dikey pencerede kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c02ac-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="c02ac-126">Okuma ve salt okunur işlemler while, siler, oluşturur ve değiştirir değil sorgular.</span><span class="sxs-lookup"><span data-stu-id="c02ac-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="c02ac-127">Hello Azure portalına erişim tuşu kopyalama</span><span class="sxs-lookup"><span data-stu-id="c02ac-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="c02ac-128">Hello üzerinde **anahtarları** dikey penceresinde hello tıklatın **kopyalama** düğmesini toohello hello anahtar sağında toocopy istiyor.</span><span class="sxs-lookup"><span data-stu-id="c02ac-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![Görüntüleme ve hello Azure Portal, anahtarlar dikey penceresinde bir erişim tuşu kopyalama](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="c02ac-130">Erişim anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="c02ac-130">Regenerate access keys</span></span>
<span data-ttu-id="c02ac-131">Merhaba erişim anahtarları tooyour Azure Cosmos DB hesabı değiştirmelisiniz düzenli aralıklarla toohelp tutmak bağlantılarınızı daha güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="c02ac-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="c02ac-132">İki erişim tuşu tooenable atanır, toomaintain bağlantıları toohello bir erişim anahtarı kullanırken, yeniden Azure Cosmos DB hesap hello diğer erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="c02ac-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="c02ac-133">Erişim anahtarlarını yeniden hello geçerli anahtarı bağımlı olan tüm uygulamaları etkiler.</span><span class="sxs-lookup"><span data-stu-id="c02ac-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="c02ac-134">Merhaba erişim anahtar tooaccess hello Azure Cosmos DB hesabı kullanan tüm istemciler güncelleştirilmiş toouse hello yeni anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c02ac-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="c02ac-135">Uygulama veya hello Azure Cosmos DB hesabı kullanarak bulut Hizmetleri varsa, anahtarları, yeniden yüklerseniz anahtarları toplamazsanız hello bağlantıları kaybedeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c02ac-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="c02ac-136">Merhaba aşağıdaki adımları hello süreci anahtarlarınızı çalışırken söz konusu ana hatlarıyla anlatılır.</span><span class="sxs-lookup"><span data-stu-id="c02ac-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="c02ac-137">Merhaba, uygulama kodu tooreference hello ikincil erişim tuşunu hello Azure Cosmos DB hesap erişim tuşu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c02ac-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="c02ac-138">Hello Azure Cosmos DB hesabınız için birincil erişim tuşunu yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c02ac-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="c02ac-139">Merhaba, [Azure Portal](https://portal.azure.com/), Azure Cosmos DB hesabınıza erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="c02ac-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="c02ac-140">Merhaba, **Azure Cosmos DB hesabı** dikey penceresinde tıklatın **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="c02ac-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="c02ac-141">Merhaba üzerinde **anahtarları** dikey penceresinde hello üretme düğmesine tıklayın ve ardından **Tamam** tooconfirm toogenerate yeni bir anahtar istiyor.</span><span class="sxs-lookup"><span data-stu-id="c02ac-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="c02ac-142">![Erişim anahtarlarını yeniden oluştur](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="c02ac-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="c02ac-143">Merhaba yeni anahtara kullanılabilir durumda doğruladıktan sonra (yaklaşık 5 dakika sonra yeniden üretme), uygulama kodu tooreference hello yeni birincil erişim anahtarınızı hello erişim tuşu güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c02ac-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="c02ac-144">Merhaba ikincil erişim tuşunu yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c02ac-144">Regenerate hello secondary access key.</span></span>
   
    ![Erişim anahtarlarını yeniden oluştur](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="c02ac-146">Azure Cosmos DB hesabınızı, yeni oluşturulan anahtarı kullanılan tooaccess çalıştırılmadan önce birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c02ac-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="c02ac-147">Merhaba bağlantı dizesi Al</span><span class="sxs-lookup"><span data-stu-id="c02ac-147">Get hello  connection string</span></span>
<span data-ttu-id="c02ac-148">tooretrieve, bağlantı dizesi, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="c02ac-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="c02ac-149">Merhaba, [Azure portal](https://portal.azure.com), Azure Cosmos DB hesabınıza erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="c02ac-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="c02ac-150">Merhaba kaynak menüye tıklayın **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="c02ac-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="c02ac-151">Merhaba tıklatın **kopyalama** düğmesine bir sonraki toohello **birincil bağlantı dizesi** veya **ikincil bağlantı dizesi** kutusu.</span><span class="sxs-lookup"><span data-stu-id="c02ac-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="c02ac-152">Hello hello bağlantı dizesi kullanıyorsanız [Azure Cosmos DB veritabanı geçiş aracı](import-data.md), hello veritabanı adı toohello hello bağlantı dizesi sonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c02ac-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="c02ac-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="c02ac-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="c02ac-154"><a id="delete"></a>Bir Azure Cosmos DB hesabını silme</span><span class="sxs-lookup"><span data-stu-id="c02ac-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="c02ac-155">bir Azure Cosmos DB tooremove hesap hello Azure artık kullanıyorsanız, portalı hello hesap adını sağ tıklatın, ve tıklatın **hesabı Sil**.</span><span class="sxs-lookup"><span data-stu-id="c02ac-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![Azure portalı bir Azure Cosmos DB toodelete hesabına nasıl hello](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="c02ac-157">Merhaba, [Azure portal](https://portal.azure.com/), erişim hello Azure Cosmos DB hesabı toodelete istiyor.</span><span class="sxs-lookup"><span data-stu-id="c02ac-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="c02ac-158">Merhaba üzerinde **Azure Cosmos DB hesabı** dikey penceresinde hello hesabını sağ tıklatın ve ardından **hesabı Sil**.</span><span class="sxs-lookup"><span data-stu-id="c02ac-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="c02ac-159">Hello elde edilen onay dikey penceresinde hello Azure Cosmos DB hesap adı tooconfirm toodelete hello hesap istediğinizi yazın.</span><span class="sxs-lookup"><span data-stu-id="c02ac-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="c02ac-160">Merhaba tıklatın **silmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c02ac-160">Click hello **Delete** button.</span></span>

![Azure portalı bir Azure Cosmos DB toodelete hesabına nasıl hello](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="c02ac-162"><a id="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c02ac-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="c02ac-163">Nasıl çok öğrenin[Azure Cosmos DB hesabınız ile çalışmaya başlama](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="c02ac-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
