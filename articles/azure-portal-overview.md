---
title: "Azure portalına genel bakış | Microsoft Docs"
description: "Microsoft Azure portalını kullanmayı öğrenin."
services: 
documentationcenter: 
author: davidwrede
manager: erikre
editor: jimbe
ms.assetid: 53cb9df1-c96a-4f4e-b022-18336cd3d697
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/16/2015
ms.author: dwrede
ms.openlocfilehash: 71820306716c6297085a29f3ceab89b55396bfe6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-azure-portal-overview"></a><span data-ttu-id="085b8-103">Microsoft Azure portalına genel bakış</span><span class="sxs-lookup"><span data-stu-id="085b8-103">Microsoft Azure portal overview</span></span>
<span data-ttu-id="085b8-104">Microsoft Azure portalı, Azure kaynaklarınızı sağlayabileceğiniz ve yönetebileceğiniz merkezi bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="085b8-104">The Microsoft Azure portal is a central place where you can provision and manage your Azure resources.</span></span>  <span data-ttu-id="085b8-105">Bu öğretici, portal hakkında bilgi edinmenizi sağlar ve şu temel özellikleri nasıl kullanacağınızı gösterir:</span><span class="sxs-lookup"><span data-stu-id="085b8-105">This tutorial will familiarize you with the portal and show you how to use some of these key capabilities:</span></span>

* <span data-ttu-id="085b8-106">**Kapsamlı bir market**, Microsoft ve diğer sağlayıcılar tarafından sunulan satın alabileceğiniz ve/veya sağlayabileceğiniz binlerce öğeye göz atmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="085b8-106">A **comprehensive marketplace** that lets you browse through thousands of items from Microsoft and other vendors that can be purchased and/or provisioned.</span></span>
* <span data-ttu-id="085b8-107">**Birleştirilmiş ve ölçeklenebilir gezinme deneyimi** önem verdiğiniz kaynakları bulmanızı ve çeşitli yönetim işlemlerini gerçekleştirmenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="085b8-107">A **unified and scalable browse experience** that makes it easy to find the resources you care about and perform various management operations.</span></span>
* <span data-ttu-id="085b8-108">**Tutarlı yönetim sayfaları** (veya dikey pencereler) ayarları, eylemleri, fatura bilgilerini, durum izleme ve kullanım verilerini ve çok daha fazlasını tutarlı bir yolla kullanıma sunarak Azure'un çok çeşitli hizmetlerini yönetmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="085b8-108">**Consistent management pages** (or blades) that let you manage Azure’s wide variety of services through a consistent way of exposing settings, actions, billing information, health monitoring and usage data, and much more.</span></span>
* <span data-ttu-id="085b8-109">**Kişisel bir deneyim** oturum açtığınızda görmek istediğiniz bilgileri gösteren özelleştirilmiş bir başlangıç ekranı oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="085b8-109">A **personal experience** that lets you create a customized start screen that shows the information that you want to see whenever you log in.</span></span>  <span data-ttu-id="085b8-110">Kutucuk içeren tüm yönetim dikey pencerelerini özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="085b8-110">You can also customize any of the management blades that contain tiles.</span></span>
  
  ![Azure Portal UI Yönlendirme][UIOrientation]

## <a name="before-you-get-started"></a><span data-ttu-id="085b8-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="085b8-112">Before you get started</span></span>
<span data-ttu-id="085b8-113">Bu öğreticiyi incelemek için geçerli bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="085b8-113">You will need a valid Azure subscription to go through this tutorial.</span></span>  <span data-ttu-id="085b8-114">Bir aboneliğiniz yoksa, hemen şimdi [ücretsiz deneme için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="085b8-114">If you don’t have one, then [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/) today.</span></span>  <span data-ttu-id="085b8-115">Abonelik aldıktan sonra, <https://portal.azure.com> adresinden portala erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="085b8-115">Once you have a subscription, you can access the portal at <https://portal.azure.com>.</span></span>

## <a name="how-to-create-a-resource"></a><span data-ttu-id="085b8-116">Kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="085b8-116">How to create a resource</span></span>
<span data-ttu-id="085b8-117">Azure’da, tek bir yerden oluşturabileceğiniz binlerce öğe içeren bir market bulunur.</span><span class="sxs-lookup"><span data-stu-id="085b8-117">Azure has a marketplace with thousands of items that you can create from one place.</span></span>  <span data-ttu-id="085b8-118">Yeni bir Windows Server 2012 VM oluşturmak istediğinizi düşünelim.</span><span class="sxs-lookup"><span data-stu-id="085b8-118">Let’s say you want to create a new Windows Server 2012 VM.</span></span>  <span data-ttu-id="085b8-119">+YENİ hub’ı, markette öne çıkan bir dizi seçkin kategoriye giriş noktanızdır.</span><span class="sxs-lookup"><span data-stu-id="085b8-119">The +NEW hub is your entry point into a curated set of featured categories from the marketplace.</span></span>  <span data-ttu-id="085b8-120">Her kategoride bir dizi öne çıkan öğenin yanı sıra tüm kategorileri ve arama işlevini gösteren tüm markete bir bağlantı bulunur.</span><span class="sxs-lookup"><span data-stu-id="085b8-120">Each category has a small set of featured items along with a link to the full marketplace that shows all categories and search.</span></span> <span data-ttu-id="085b8-121">Yeni bir Windows Server 2012 VM oluşturmak için aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="085b8-121">To create that new Windows Server 2012 VM, perform the following actions:</span></span>  

1. <span data-ttu-id="085b8-122">Windows Server 2012 öne çıkan bir öğedir, bu nedenle İşlem kategorisinden seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="085b8-122">Windows Server 2012 is featured, so you can select it from the Compute category.</span></span>  
2. <span data-ttu-id="085b8-123">Forma bazı temel bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="085b8-123">Fill out some basic inputs on a form.</span></span>
3. <span data-ttu-id="085b8-124">‘Oluştur’a tıkladığınızda sanal makineniz anında sağlama işlemine başlar.</span><span class="sxs-lookup"><span data-stu-id="085b8-124">Click ‘Create’ and your VM will begin to provision immediately.</span></span>

<span data-ttu-id="085b8-125">Bildirim hub'ı kaynağınız oluşturulduğunda ve yönetim dikey penceresi açılacağı zaman sizi uyarır (isterseniz daha sonra kaynaklara göz atabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="085b8-125">The notifications hub will alert you when your resource has been created and a management blade will open (you can always browse to resources later).</span></span>

![Portal Kategorileri][PortalCategories]

## <a name="how-to-find-your-resources"></a><span data-ttu-id="085b8-127">Kaynaklarınızın bulma</span><span class="sxs-lookup"><span data-stu-id="085b8-127">How to find your resources</span></span>
<span data-ttu-id="085b8-128">Sık erişilen kaynaklar başlangıç panonuza sabitleyebilirsiniz, ancak sık erişmediğiniz bir kaynağı bulmak için gezinmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="085b8-128">You can always pin frequently accessed resources to your startboard, but you might need to browse to something that you don’t frequently access.</span></span>  <span data-ttu-id="085b8-129">Aşağıda gösterilen gözatma hub’ı tüm kaynaklarınızı almanın bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="085b8-129">The browse hub shown below is your way to get to all of your resources.</span></span>  <span data-ttu-id="085b8-130">Aboneliğe göre filtre uygulayabilir, sütunları seçebilir/yeniden boyutlandırabilir ve tek tek öğelere tıklayarak yönetim dikey pencerelerine gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="085b8-130">You can filter by subscription, choose/resize columns, and navigate to the management blades by clicking on individual items.</span></span>

![Gözatma Hub’ı][BrowseHub]

## <a name="how-to-manage-and-delegate-access-to-a-resource"></a><span data-ttu-id="085b8-132">Kaynağa erişimi yönetme ve erişimi devretme</span><span class="sxs-lookup"><span data-stu-id="085b8-132">How to manage and delegate access to a resource</span></span>
<span data-ttu-id="085b8-133">Bu dikey pencereden, uzak masaüstünü kullanarak sanal makineye bağlanabilir, temel performans ölçümlerini izleyebilir, rol tabanlı erişim (RBAC) kullanarak bu sanal makineye erişimi denetleyebilir, sanal makineyi yapılandırabilir veya diğer önemli yönetim görevleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="085b8-133">From this blade you can connect to the virtual machine using remote desktop, monitor key performance metrics, control access to this VM using role based access (RBAC), configure the VM, and perform other important management tasks.</span></span>  <span data-ttu-id="085b8-134">Rol tabanlı olarak erişim devretme büyük ölçekli yönetim görevleri için kritik önem taşır.</span><span class="sxs-lookup"><span data-stu-id="085b8-134">Delegating access based on role is critical to managing at scale.</span></span>  <span data-ttu-id="085b8-135">Daha fazla bilgi edinmek için [buraya](active-directory/role-based-access-control-configure.md) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="085b8-135">Click [here](active-directory/role-based-access-control-configure.md) to learn more about it.</span></span> <span data-ttu-id="085b8-136">Bir kaynağa erişim devretmek için aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="085b8-136">To delegate access to a resource, perform the following actions:</span></span>

1. <span data-ttu-id="085b8-137">Kaynağınızı bulun.</span><span class="sxs-lookup"><span data-stu-id="085b8-137">Browse to your resource.</span></span>
2. <span data-ttu-id="085b8-138">Temel Parçalar bölümünde ‘Tüm Ayarlar'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="085b8-138">Click ‘All settings’ in the Essentials section.</span></span>
3. <span data-ttu-id="085b8-139">Ayarlar listesinde ‘Kullanıcılar’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="085b8-139">Click ‘Users’ in the settings list.</span></span>
4. <span data-ttu-id="085b8-140">Komut çubuğunda ‘Ekle’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="085b8-140">Click ‘Add’ in the command bar.</span></span>
5. <span data-ttu-id="085b8-141">Bir kullanıcı ve rol seçin.</span><span class="sxs-lookup"><span data-stu-id="085b8-141">Choose a user and a role.</span></span>

![Kaynak Yönetme][ManageResource]

## <a name="how-to-get-help"></a><span data-ttu-id="085b8-143">Yardım alma</span><span class="sxs-lookup"><span data-stu-id="085b8-143">How to get help</span></span>
<span data-ttu-id="085b8-144">Bir sorununuz varsa, size yardımcı olmaya hazırız.</span><span class="sxs-lookup"><span data-stu-id="085b8-144">If you ever have a problem, we’re here for you.</span></span>  <span data-ttu-id="085b8-145">Portalda sağ tarafta görebileceğiniz üzere bir yardım ve destek sayfası vardır.</span><span class="sxs-lookup"><span data-stu-id="085b8-145">The portal has a help and support page that can point you in the right direction.</span></span>  <span data-ttu-id="085b8-146">Ayrıca, [destek planınıza](https://azure.microsoft.com/support/plans/) bağlı olarak doğrudan portal üzerinden destek bileti oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="085b8-146">Depending on your [support plan](https://azure.microsoft.com/support/plans/), you can also create support tickets directly in the portal.</span></span>  <span data-ttu-id="085b8-147">Bir destek bileti oluşturduktan sonra portal üzerinden bu biletin yaşam döngüsünü yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="085b8-147">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span> <span data-ttu-id="085b8-148">Gözat -> Yardım + destek bölümüne giderek yardım ve destek sayfasına ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="085b8-148">You can get to the help and support page by navigating to Browse -> Help + support.</span></span>  

![Yardım ve destek][HelpSupport]

## <a name="summary"></a><span data-ttu-id="085b8-150">Özet</span><span class="sxs-lookup"><span data-stu-id="085b8-150">Summary</span></span>
<span data-ttu-id="085b8-151">Şimdi bu öğreticide öğrendiklerinizi gözden geçirelim:</span><span class="sxs-lookup"><span data-stu-id="085b8-151">Let’s review what you learned in this tutorial:</span></span>

* <span data-ttu-id="085b8-152">Kaydolmayı, abonelik almayı ve portalda gezinmeyi öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="085b8-152">You learned how to sign up, get a subscription, and browse to the portal</span></span>
* <span data-ttu-id="085b8-153">UI portalı hakkında bilgi edindiniz ve kaynak oluşturmayı ve kaynaklara göz atmayı öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="085b8-153">You got oriented with the portal UI and learned how to create and browse resources</span></span>
* <span data-ttu-id="085b8-154">Kaynak oluşturmayı ve kaynaklara göz atmayı öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="085b8-154">You learned how to create a resource and browse resources</span></span>
* <span data-ttu-id="085b8-155">Dikey pencerelerin yapısı veya yönetimi ve farklı türdeki kaynakların tutarlı şekilde yönetilmesi hakkında bilgi edindiniz</span><span class="sxs-lookup"><span data-stu-id="085b8-155">You learned about the structure or management blades and how you can consistently manage different types of resources</span></span>
* <span data-ttu-id="085b8-156">Sizin için önemli bilgileri ön plana çıkarmak üzere portalı nasıl özelleştireceğinizi öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="085b8-156">You learned how to customize the portal to bring the information you care about to the front and center</span></span>
* <span data-ttu-id="085b8-157">Rol tabanlı erişim (RBAC) kullanarak kaynaklarına erişimi denetlemeyi öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="085b8-157">You learned how to control access to resources using role based access (RBAC)</span></span>
* <span data-ttu-id="085b8-158">Yardım ve destek alma yollarını öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="085b8-158">You learned how to get help and support</span></span>

<span data-ttu-id="085b8-159">Microsoft Azure portalını uygulamalarınızı bulutta oluşturma ve yönetme sürecini önemli ölçüde basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="085b8-159">The Microsoft Azure portal radically simplifies building and managing your applications in the cloud.</span></span>  <span data-ttu-id="085b8-160">[Geri bildirimlerinizi önemsiyor](https://feedback.azure.com/forums/223579-azure-preview-portal/) ve buna uygun geliştirmeler yapıyoruz. En son gelişmelerden haberdar olmak için [yönetim bloguna](https://azure.microsoft.com/blog/topics/management/) göz atın. </span><span class="sxs-lookup"><span data-stu-id="085b8-160">Take a look at the [management blog](https://azure.microsoft.com/blog/topics/management/) to keep up to date as we’re constantly [listening to feedback](https://feedback.azure.com/forums/223579-azure-preview-portal/) and making improvements.</span></span>  <span data-ttu-id="085b8-161">Tüm Azure güncelleştirmelerini görebileceğiniz için bir diğer önemli yer ise [ScottGu’nun blogudur](http://weblogs.asp.net/scottgu).</span><span class="sxs-lookup"><span data-stu-id="085b8-161">[ScottGu’s blog](http://weblogs.asp.net/scottgu) is another great place to look for all Azure updates.</span></span>

[UIOrientation]: ./media/azure-portal-how-to-use/azure_portal_1.png
[PortalCategories]: ./media/azure-portal-how-to-use/azure_portal_2.png
[BrowseHub]: ./media/azure-portal-how-to-use/azure_portal_3.png
[ManageResource]: ./media/azure-portal-how-to-use/azure_portal_4.png
[CustomizeBlades]: ./media/azure-portal-how-to-use/azure_portal_5.png
[HelpSupport]: ./media/azure-portal-how-to-use/azure_portal_6.png
