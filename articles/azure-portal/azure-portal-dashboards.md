---
title: "Oluşturma ve Azure portalı panoları paylaşma | Microsoft Docs"
description: "Bu makalede, oluşturma ve Azure portalında panolar düzenleme açıklanmaktadır."
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
ms.openlocfilehash: 5429e68723448ff5db6ef0ed8da1b927e97e6dd9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-share-dashboards-in-the-azure-portal"></a><span data-ttu-id="73fa6-103">Oluşturma ve Azure portalındaki pano paylaşma</span><span class="sxs-lookup"><span data-stu-id="73fa6-103">Create and share dashboards in the Azure portal</span></span>
<span data-ttu-id="73fa6-104">Birden çok panolar oluşturun ve bunları Azure aboneliklerinize erişimi başkalarıyla paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-104">You can create multiple dashboards and share them with others who have access to your Azure subscriptions.</span></span>  <span data-ttu-id="73fa6-105">Bu makalede oluşturma, düzenleme, yayımlama ve panolar erişimi yönetme temellerini geçer.</span><span class="sxs-lookup"><span data-stu-id="73fa6-105">This article goes through the basics of creating, editing, publishing, and managing access to dashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="73fa6-106">Bir pano oluşturun</span><span class="sxs-lookup"><span data-stu-id="73fa6-106">Create a dashboard</span></span>
<span data-ttu-id="73fa6-107">Bir Pano oluşturmak için seçin **yeni Pano** geçerli Panodaki adının yanındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73fa6-107">To create a dashboard, select the **New dashboard** button next to the current dashboard's name.</span></span>  

![bir pano oluşturun](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="73fa6-109">Bu eylem, yeni, boş, özel bir Pano oluşturur ve burada panonuzu adlandırın ve ekleyebilir veya kutucukları yeniden özelleştirme moduna geçirir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="73fa6-110">Bu modda olduğunda, sol gezinti menüsü daraltılabilir döşeme galeri alır.</span><span class="sxs-lookup"><span data-stu-id="73fa6-110">When in this mode, the collapsible tile gallery takes over the left navigation menu.</span></span>  <span data-ttu-id="73fa6-111">Döşeme galeri Azure kaynaklarınızın çeşitli şekillerde döşeme bulmanıza olanak sağlar: tarafından göz atabilirsiniz [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups), göre kaynak türü, göre [etiketi](../azure-resource-manager/resource-group-using-tags.md), ya da kaynak ada göre arayarak.</span><span class="sxs-lookup"><span data-stu-id="73fa6-111">The tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![Pano özelleştirme](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="73fa6-113">Döşeme sürükleyip istediğiniz yere Pano yüzeyine bırakarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="73fa6-113">Add tiles by dragging and dropping them onto the dashboard surface wherever you want.</span></span>

<span data-ttu-id="73fa6-114">Yeni bir kategori yok **genel** belirli bir kaynakla ilişkili olmayan kutucuklar için.</span><span class="sxs-lookup"><span data-stu-id="73fa6-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="73fa6-115">Bu örnekte, Markdown kutucuğu sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="73fa6-115">In this example, we pin the Markdown tile.</span></span>  <span data-ttu-id="73fa6-116">Özel içerik panonuza eklemek için bu kutucuğu kullanın.</span><span class="sxs-lookup"><span data-stu-id="73fa6-116">You use this tile to add custom content to your dashboard.</span></span>  <span data-ttu-id="73fa6-117">Düz metin kutucuğu destekleyen [Markdown söz dizimi](https://daringfireball.net/projects/markdown/syntax)ve HTML sınırlı sayıda.</span><span class="sxs-lookup"><span data-stu-id="73fa6-117">The tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="73fa6-118">(Güvenlik için ekleme gibi işlemler yapamayacağı `<script>` etiketler veya belirli portalıyla engelleyebilmesi CSS stil öğesi kullanın.)</span><span class="sxs-lookup"><span data-stu-id="73fa6-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with the portal.)</span></span> 

![markdown Ekle](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="73fa6-120">Bir Pano Düzenle</span><span class="sxs-lookup"><span data-stu-id="73fa6-120">Edit a dashboard</span></span>
<span data-ttu-id="73fa6-121">Panonuz oluşturduktan sonra kutucukları döşeme galeri veya dikey pencereleri döşe gösterimini sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73fa6-121">After creating your dashboard, you can pin tiles from the tile gallery or the tile representation of blades.</span></span> <span data-ttu-id="73fa6-122">Şimdi, kaynak grubu gösterimini sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="73fa6-122">Let's pin the representation of our resource group.</span></span> <span data-ttu-id="73fa6-123">Öğe göz atarken veya kaynak grubu dikey ya da PIN olabilir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-123">You can either pin when browsing the item, or from the resource group blade.</span></span> <span data-ttu-id="73fa6-124">Her iki yaklaşım, kaynak grubu döşeme gösterimini sabitleme neden.</span><span class="sxs-lookup"><span data-stu-id="73fa6-124">Both approaches result in pinning the tile representation of the resource group.</span></span>

![Panoya Sabitle](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="73fa6-126">Öğeyi sabitleme sonra Panonuzda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-126">After pinning the item, it appears on your dashboard.</span></span>

![Görünüm Panosu](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="73fa6-128">Bir Markdown döşeme sahibiz ve bir kaynak grubu panosuna sabitlediğiniz göre biz yeniden boyutlandırma ve uygun bir düzen kutucukları yeniden.</span><span class="sxs-lookup"><span data-stu-id="73fa6-128">Now that we have a Markdown tile and a resource group pinned to the dashboard, we can resize and rearrange the tiles into a suitable layout.</span></span>

<span data-ttu-id="73fa6-129">Vurgulama ve seçerek "..." veya bir kutucuğa sağ tıklayarak bu kutucuğu tüm bağlamsal komutlarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73fa6-129">By hovering and selecting "…" or right-clicking on a tile you can see all the contextual commands for that tile.</span></span> <span data-ttu-id="73fa6-130">Varsayılan olarak, iki öğe vardır:</span><span class="sxs-lookup"><span data-stu-id="73fa6-130">By default, there are two items:</span></span>

1. <span data-ttu-id="73fa6-131">**Panodan sabitleme** – kutucuğu panodan kaldırır</span><span class="sxs-lookup"><span data-stu-id="73fa6-131">**Unpin from dashboard** – removes the tile from the dashboard</span></span>
2. <span data-ttu-id="73fa6-132">**Özelleştirme** – girer modu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="73fa6-132">**Customize** – enters customize mode</span></span>

![Döşeme özelleştirme](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="73fa6-134">Seçerek özelleştirme, yeniden boyutlandırma ve kutucukları yeniden Sırala.</span><span class="sxs-lookup"><span data-stu-id="73fa6-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="73fa6-135">Bir kutucuk yeniden boyutlandırmak için aşağıdaki görüntüde gösterildiği gibi bağlamsal menüsünden Yeni boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="73fa6-135">To resize a tile, select the new size from the contextual menu, as shown in the following image.</span></span>

![Döşeme yeniden boyutlandırma](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="73fa6-137">Ya da döşeme herhangi bir boyutta destekliyorsa, istenen boyuta alt sağ köşesinde sürükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73fa6-137">Or, if the tile supports any size, you can drag the bottom right-hand corner to the desired size.</span></span>

![Döşeme yeniden boyutlandırma](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="73fa6-139">Kutucukları yeniden boyutlandırma sonra Pano görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="73fa6-139">After resizing tiles, view the dashboard.</span></span>

![Görünümü kutucuğu](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="73fa6-141">Bir Pano özelleştirme bittiğinde seçmeniz yeterlidir **özelleştirme Bitti** çıkmak için özelleştirme moduna veya sağ tıklatın ve seçin **özelleştirme Bitti** ve bağlam menüsünden.</span><span class="sxs-lookup"><span data-stu-id="73fa6-141">Once you are finished customizing a dashboard, simply select the **Done customizing** to exit customize mode or right-click and select **Done customizing** from the context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="73fa6-142">Bir Pano yayımlayın ve erişim denetimi yönetin</span><span class="sxs-lookup"><span data-stu-id="73fa6-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="73fa6-143">Bir Pano oluşturduğunuzda, görebileceğiniz tek kişi olduğunuz anlamına gelir varsayılan olarak özeldir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-143">When you create a dashboard, it is private by default, which means you are the only person who can see it.</span></span>  <span data-ttu-id="73fa6-144">Başkaları için görünür yapmak için kullanın **paylaşımı** yanı sıra diğer Pano komutları görünür düğmesi.</span><span class="sxs-lookup"><span data-stu-id="73fa6-144">To make it visible to others, use the **Share** button that appears alongside the other dashboard commands.</span></span>

![Pano paylaşımı](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="73fa6-146">Abonelik ve kaynak grubu için yayımlanması panonuz için seçim istenir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-146">You are asked to choose a subscription and resource group for your dashboard to be published to.</span></span> <span data-ttu-id="73fa6-147">(Size bir e-posta adresi yazarak paylaşamaz şekilde) sorunsuz bir şekilde panolar ekosistemi tümleştirmek için paylaşılan panoları Azure kaynaklarını uyguladık.</span><span class="sxs-lookup"><span data-stu-id="73fa6-147">To seamlessly integrate dashboards into the ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="73fa6-148">Portal döşemeleri çoğu tarafından görüntülenen bilgilere erişim tarafından yönetilir [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="73fa6-148">Access to the information displayed by most of the tiles in the portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="73fa6-149">Bir erişim denetimi açısından bakıldığında, paylaşılan Pano sanal makine ya da bir depolama hesabı hiç farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="73fa6-150">Bir Azure aboneliğiniz varsa ve ekibinizin üyeleri rolleri atanmış düşünelim **sahibi**, **katkıda bulunan**, veya **okuyucu** abonelik.</span><span class="sxs-lookup"><span data-stu-id="73fa6-150">Let's say you have an Azure subscription and members of your team have been assigned the roles of **owner**, **contributor**, or **reader** of the subscription.</span></span>  <span data-ttu-id="73fa6-151">Sahipler veya katkıda bulunanlar kullanıcılar listesinde, görüntülemek, oluşturmak, değiştirmek veya bu abonelik içindeki panolar silmek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73fa6-151">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="73fa6-152">Okuyucular kullanıcılar listesi ve görünümü panolarına kullanabilirsiniz ancak değiştirin veya silin.</span><span class="sxs-lookup"><span data-stu-id="73fa6-152">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="73fa6-153">Okuyucu erişimi olan kullanıcılar bir paylaşılan Pano yerel düzenlemeler yapabilir, ancak bu değişiklikleri geri sunucuya yayımlayın mümkün değildir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-153">Users with reader access are able to make local edits to a shared dashboard, but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="73fa6-154">Ancak, bunlar Pano kendi kullanmak için özel bir kopyasını yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73fa6-154">However, they can make a private copy of the dashboard for their own use.</span></span>  <span data-ttu-id="73fa6-155">Her zaman olduğu gibi tek tek döşeme Panoda için karşılık gelen kaynaklara göre kendi erişim denetim kurallarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="73fa6-155">As always, individual tiles on the dashboard enforce their own access control rules based on the resources they correspond to.</span></span>  

<span data-ttu-id="73fa6-156">Kolaylık olması için portal, bir kaynak grubunda panolar nereye bir desen doğru olarak adlandırılan deneyimi kılavuzları yayımlama kullanıcının **panolar**.</span><span class="sxs-lookup"><span data-stu-id="73fa6-156">For convenience, the portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![Pano yayımlama](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="73fa6-158">Belirli bir kaynak grubunu için bir Pano yayımlamayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73fa6-158">You can also choose to publish a dashboard to a particular resource group.</span></span>  <span data-ttu-id="73fa6-159">Bu Pano için erişim denetimi, kaynak grubu için erişim denetimi ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-159">The access control for that dashboard matches the access control for the resource group.</span></span>  <span data-ttu-id="73fa6-160">Bu kaynak grubundaki kaynakları yönetebilir kullanıcılar da panoları erişiminiz.</span><span class="sxs-lookup"><span data-stu-id="73fa6-160">Users that can manage the resources in that resource group also have access to the dashboards.</span></span>

![kaynak grubu için Pano yayımlama](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="73fa6-162">Panonuz yayımlandıktan sonra **paylaşım + erişim** denetim bölmesinde yenileyin ve Pano kullanıcı erişimini yönetmek için bir bağlantı da dahil olmak üzere yayımlanan Pano hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="73fa6-162">After your dashboard is published, the **Sharing + access** control pane will refresh and show you information about the published dashboard, including a link to manage user access to the dashboard.</span></span>  <span data-ttu-id="73fa6-163">Bu bağlantı, herhangi bir Azure kaynak erişimi yönetmek için kullanılan standart rol tabanlı erişim denetimi dikey penceresini başlatır.</span><span class="sxs-lookup"><span data-stu-id="73fa6-163">This link launches the standard Role Based Access Control blade used to manage access for any Azure resource.</span></span>  <span data-ttu-id="73fa6-164">Her zaman geri bu görünüme seçerek alabilirsiniz **paylaşımı**.</span><span class="sxs-lookup"><span data-stu-id="73fa6-164">You can always get back to this view by selecting **Share**.</span></span>

![erişim denetimi yönetme](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="73fa6-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73fa6-166">Next steps</span></span>
* <span data-ttu-id="73fa6-167">Kaynakları yönetmek için bkz: [yönetmek Azure kaynakları portal üzerinden](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="73fa6-167">To manage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="73fa6-168">Kaynakları dağıtmak için bkz: [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="73fa6-168">To deploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

