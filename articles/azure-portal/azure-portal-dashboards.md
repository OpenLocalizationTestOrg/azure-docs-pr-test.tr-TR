---
title: "aaaCreate ve Azure portalı panoları paylaşmak | Microsoft Docs"
description: "Bu makalede, Azure portalını nasıl toocreate ve düzenleme panolarında hello açıklanmaktadır."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a><span data-ttu-id="6bdb9-103">Oluşturma ve hello Azure portal panolarında paylaşma</span><span class="sxs-lookup"><span data-stu-id="6bdb9-103">Create and share dashboards in hello Azure portal</span></span>
<span data-ttu-id="6bdb9-104">Birden çok panolar oluşturun ve erişim tooyour Azure sahip başkalarıyla paylaşmadan abonelikleri.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-104">You can create multiple dashboards and share them with others who have access tooyour Azure subscriptions.</span></span>  <span data-ttu-id="6bdb9-105">Bu makalede oluşturma, düzenleme, yayımlama ve yönetme erişimi toodashboards hello temelleri gider.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-105">This article goes through hello basics of creating, editing, publishing, and managing access toodashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="6bdb9-106">Bir pano oluşturun</span><span class="sxs-lookup"><span data-stu-id="6bdb9-106">Create a dashboard</span></span>
<span data-ttu-id="6bdb9-107">toocreate bir Pano seçin hello **yeni Pano** sonraki toohello geçerli Pano kişinin adı düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-107">toocreate a dashboard, select hello **New dashboard** button next toohello current dashboard's name.</span></span>  

![bir pano oluşturun](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="6bdb9-109">Bu eylem, yeni, boş, özel bir Pano oluşturur ve burada panonuzu adlandırın ve ekleyebilir veya kutucukları yeniden özelleştirme moduna geçirir.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="6bdb9-110">Bu modda, hello daraltılabilir parçasında galeri alır hello sol gezinti menüsü.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-110">When in this mode, hello collapsible tile gallery takes over hello left navigation menu.</span></span>  <span data-ttu-id="6bdb9-111">Merhaba döşeme galeri Azure kaynaklarınızın çeşitli şekillerde döşeme bulmanıza olanak sağlar: tarafından göz atabilirsiniz [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups), göre kaynak türü, göre [etiketi](../azure-resource-manager/resource-group-using-tags.md), ya da kaynak ada göre arayarak.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-111">hello tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![Pano özelleştirme](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="6bdb9-113">Döşeme sürükleyip istediğiniz yere hello Pano yüzeyine bırakarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-113">Add tiles by dragging and dropping them onto hello dashboard surface wherever you want.</span></span>

<span data-ttu-id="6bdb9-114">Yeni bir kategori yok **genel** belirli bir kaynakla ilişkili olmayan kutucuklar için.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="6bdb9-115">Bu örnekte, hello Markdown kutucuğu sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-115">In this example, we pin hello Markdown tile.</span></span>  <span data-ttu-id="6bdb9-116">Bu kutucuğu tooadd özel içerik tooyour panoyu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-116">You use this tile tooadd custom content tooyour dashboard.</span></span>  <span data-ttu-id="6bdb9-117">Merhaba döşeme destekleyen düz metin [Markdown söz dizimi](https://daringfireball.net/projects/markdown/syntax)ve HTML sınırlı sayıda.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-117">hello tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="6bdb9-118">(Güvenlik için ekleme gibi işlemler yapamayacağı `<script>` etiketler veya belirli hello portalıyla engelleyebilmesi CSS stil öğesi kullanın.)</span><span class="sxs-lookup"><span data-stu-id="6bdb9-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with hello portal.)</span></span> 

![markdown Ekle](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="6bdb9-120">Bir Pano Düzenle</span><span class="sxs-lookup"><span data-stu-id="6bdb9-120">Edit a dashboard</span></span>
<span data-ttu-id="6bdb9-121">Panonuz oluşturduktan sonra kutucukları hello döşeme galeri veya hello döşeme Kanatlar gösterimini sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-121">After creating your dashboard, you can pin tiles from hello tile gallery or hello tile representation of blades.</span></span> <span data-ttu-id="6bdb9-122">Şimdi, kaynak grubu hello gösterimini sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-122">Let's pin hello representation of our resource group.</span></span> <span data-ttu-id="6bdb9-123">Öğe veya hello kaynak grubu dikey hello göz atarken ya da sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-123">You can either pin when browsing hello item, or from hello resource group blade.</span></span> <span data-ttu-id="6bdb9-124">Her iki yaklaşımın hello döşeme hello kaynak grubu gösterimini sabitleme neden.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-124">Both approaches result in pinning hello tile representation of hello resource group.</span></span>

![PIN toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="6bdb9-126">Merhaba öğeyi sabitleme sonra Panonuzda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-126">After pinning hello item, it appears on your dashboard.</span></span>

![Görünüm Panosu](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="6bdb9-128">Bir Markdown kutucuk ve bir kaynak grubu sabitlenmiş toohello Panosu sahibiz, biz yeniden boyutlandırma ve uygun bir düzen hello kutucukları yeniden.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-128">Now that we have a Markdown tile and a resource group pinned toohello dashboard, we can resize and rearrange hello tiles into a suitable layout.</span></span>

<span data-ttu-id="6bdb9-129">Vurgulama ve seçerek "..." veya bir kutucuğa sağ tıklayarak bu döşeme için tüm hello bağlamsal komutları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-129">By hovering and selecting "…" or right-clicking on a tile you can see all hello contextual commands for that tile.</span></span> <span data-ttu-id="6bdb9-130">Varsayılan olarak, iki öğe vardır:</span><span class="sxs-lookup"><span data-stu-id="6bdb9-130">By default, there are two items:</span></span>

1. <span data-ttu-id="6bdb9-131">**Panodan sabitleme** – hello panosundan kaldırır hello döşeme</span><span class="sxs-lookup"><span data-stu-id="6bdb9-131">**Unpin from dashboard** – removes hello tile from hello dashboard</span></span>
2. <span data-ttu-id="6bdb9-132">**Özelleştirme** – girer modu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="6bdb9-132">**Customize** – enters customize mode</span></span>

![Döşeme özelleştirme](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="6bdb9-134">Seçerek özelleştirme, yeniden boyutlandırma ve kutucukları yeniden Sırala.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="6bdb9-135">tooresize kutucuğu, select hello görüntü aşağıdaki gösterildiği gibi hello bağlam menüsünden Yeni boyutunu hello.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-135">tooresize a tile, select hello new size from hello contextual menu, as shown in hello following image.</span></span>

![Döşeme yeniden boyutlandırma](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="6bdb9-137">Veya herhangi bir boyutta hello döşeme destekliyorsa, hello alt sağ köşesinde toohello istenen boyutu sürükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-137">Or, if hello tile supports any size, you can drag hello bottom right-hand corner toohello desired size.</span></span>

![Döşeme yeniden boyutlandırma](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="6bdb9-139">Kutucukları yeniden boyutlandırma sonra hello Pano görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-139">After resizing tiles, view hello dashboard.</span></span>

![Görünümü kutucuğu](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="6bdb9-141">Bir Pano özelleştirme bittiğinde, hello seçmeniz yeterlidir **özelleştirme Bitti** tooexit özelleştirme modu veya sağ tıklatın ve seçin **özelleştirme Bitti** hello bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-141">Once you are finished customizing a dashboard, simply select hello **Done customizing** tooexit customize mode or right-click and select **Done customizing** from hello context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="6bdb9-142">Bir Pano yayımlayın ve erişim denetimi yönetin</span><span class="sxs-lookup"><span data-stu-id="6bdb9-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="6bdb9-143">Bir Pano oluşturduğunuzda, görebileceğiniz tek kişi hello olduğu anlamına gelir varsayılan olarak özeldir.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-143">When you create a dashboard, it is private by default, which means you are hello only person who can see it.</span></span>  <span data-ttu-id="6bdb9-144">toomake onu görünen tooothers hello kullanın **paylaşımı** yanında görüntülenen düğmesini hello diğer Pano komutları.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-144">toomake it visible tooothers, use hello **Share** button that appears alongside hello other dashboard commands.</span></span>

![Pano paylaşımı](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="6bdb9-146">Bir abonelik ve kaynak grubu, Pano toobe için yayımlanan toochoose istenir.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-146">You are asked toochoose a subscription and resource group for your dashboard toobe published to.</span></span> <span data-ttu-id="6bdb9-147">tooseamlessly hello ekosistemi panolar tümleştirmek, (size bir e-posta adresi yazarak paylaşamaz şekilde) paylaşılan panoları Azure kaynaklarını uyguladık.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-147">tooseamlessly integrate dashboards into hello ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="6bdb9-148">Çoğu hello döşeme hello portalında tarafından görüntülenen erişim toohello bilgileri tarafından yönetilir [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6bdb9-148">Access toohello information displayed by most of hello tiles in hello portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="6bdb9-149">Bir erişim denetimi açısından bakıldığında, paylaşılan Pano sanal makine ya da bir depolama hesabı hiç farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="6bdb9-150">Bir Azure aboneliğiniz varsa ve ekibinizin üyeleri hello rolleri atanmış düşünelim **sahibi**, **katkıda bulunan**, veya **okuyucu** hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-150">Let's say you have an Azure subscription and members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** of hello subscription.</span></span>  <span data-ttu-id="6bdb9-151">Sahipler veya katkıda bulunanlar kullanıcılar mümkün toolist, görünüm olan, oluşturmak, değiştirmek veya bu abonelik içindeki panoları silin.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-151">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="6bdb9-152">Okuyucular kullanıcılar mümkün toolist ve görünüm panolar, ancak değiştirin veya silin.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-152">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="6bdb9-153">Okuyucu erişimi olan kullanıcılar mümkün toomake yerel düzenlemeleri tooa paylaşılan Pano, ancak şu toopublish bu değişiklikleri geri toohello sunucu.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-153">Users with reader access are able toomake local edits tooa shared dashboard, but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="6bdb9-154">Ancak, bunlar hello panonun kendi kullanmak için özel bir kopyasını yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-154">However, they can make a private copy of hello dashboard for their own use.</span></span>  <span data-ttu-id="6bdb9-155">Her zaman olduğu gibi tek tek döşeme hello Panoda için karşılık gelen hello kaynaklara göre kendi erişim denetim kurallarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-155">As always, individual tiles on hello dashboard enforce their own access control rules based on hello resources they correspond to.</span></span>  

<span data-ttu-id="6bdb9-156">Kolaylık olması için bir kaynak grubunda panolar nereye bir desen doğrultusunda aradığınız deneyimi kılavuzları hello portalını yayımlama **panolar**.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-156">For convenience, hello portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![Pano yayımlama](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="6bdb9-158">Ayrıca, Pano tooa belirli bir kaynak grubunu toopublish tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-158">You can also choose toopublish a dashboard tooa particular resource group.</span></span>  <span data-ttu-id="6bdb9-159">Bu Pano için Hello erişim denetimi hello kaynak grubu için hello erişim denetimi ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-159">hello access control for that dashboard matches hello access control for hello resource group.</span></span>  <span data-ttu-id="6bdb9-160">Kaynak grubunda hello kaynakları yönetebilir kullanıcılar toohello mimarilere de.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-160">Users that can manage hello resources in that resource group also have access toohello dashboards.</span></span>

![Pano tooresource Grup yayımlama](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="6bdb9-162">Panonuz yayımlandıktan sonra hello **paylaşım + erişim** denetim bölmesinde yenileyin ve bir bağlantı toomanage kullanıcı erişimi toohello panosu da dahil olmak üzere hello yayımlanan Pano hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-162">After your dashboard is published, hello **Sharing + access** control pane will refresh and show you information about hello published dashboard, including a link toomanage user access toohello dashboard.</span></span>  <span data-ttu-id="6bdb9-163">Bu bağlantıyı hello standart rol tabanlı erişim denetimi kullanılan dikey toomanage erişim herhangi bir Azure kaynağı için başlatır.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-163">This link launches hello standard Role Based Access Control blade used toomanage access for any Azure resource.</span></span>  <span data-ttu-id="6bdb9-164">Her zaman geri toothis görünümü seçerek alabilirsiniz **paylaşımı**.</span><span class="sxs-lookup"><span data-stu-id="6bdb9-164">You can always get back toothis view by selecting **Share**.</span></span>

![erişim denetimi yönetme](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="6bdb9-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6bdb9-166">Next steps</span></span>
* <span data-ttu-id="6bdb9-167">toomanage kaynaklara bakın [yönetmek Azure kaynakları portal üzerinden](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6bdb9-167">toomanage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="6bdb9-168">toodeploy kaynaklara bakın [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6bdb9-168">toodeploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

