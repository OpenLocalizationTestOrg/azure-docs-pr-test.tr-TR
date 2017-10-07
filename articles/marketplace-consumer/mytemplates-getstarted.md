---
title: "aaaGet özel şablonlarla çalışmaya | Microsoft Docs"
description: "Ekleme, yönetme ve hello Azure portal, hello Azure CLI veya PowerShell kullanarak özel şablonlarınızı paylaşma."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="a7ac0-103">Hello Azure Portal'da özel şablonları kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a7ac0-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="a7ac0-104">Bir [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) şablonudur bildirim temelli bir şablondur dağıtımınızı toodefine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="a7ac0-105">Merhaba kaynakları toodeploy bir çözüm için tanımlayın ve parametreleri ve farklı ortamlar için tooinput değerleri etkinleştir değişkenleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="a7ac0-106">Merhaba şablon JSON ve kullanabileceğiniz ifadeler oluşur dağıtımınız için tooconstruct değerleri.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="a7ac0-107">Merhaba yeni kullanabilirsiniz **şablonları** hello özelliği [Azure Portal](https://portal.azure.com) hello birlikte **Microsoft.Gallery** bir uzantısı olarak hello kaynak sağlayıcısı [ Azure Market](https://azure.microsoft.com/marketplace/) tooenable kullanıcılar toocreate, yönetmek ve kişisel bir kitaplıktan özel şablonları dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="a7ac0-108">Bu belge, ekleme, yönetme ve özel paylaşım yoluyla anlatan **şablonu** hello Azure Portal kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="a7ac0-109">Rehber</span><span class="sxs-lookup"><span data-stu-id="a7ac0-109">Guidance</span></span>
<span data-ttu-id="a7ac0-110">Merhaba aşağıdaki önerileri tam anlamıyla yararlanabilmek yardımcı olacak **şablonları** çözümleriniz üzerinde çalışırken:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="a7ac0-111">Bir **Şablon**, Resource Manager şablonu ve ek meta verileri içeren kapsayıcı bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="a7ac0-112">Merhaba Market tooan öğesinde çok benzer şekilde davranır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="a7ac0-113">Hello önemli fark, özel bir öğe genel Market öğelerinin karşılıklı toohello olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="a7ac0-114">Merhaba **şablonları** kitaplığı, dağıtımlarını iyi toocustomize isteyen kullanıcılar için çalışır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="a7ac0-115">**Şablonlar**, Azure içinde basit bir depoya ihtiyaç duyan kullanıcılar için iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="a7ac0-116">Var olan bir Resource Manager şablonu ile başlayın.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="a7ac0-117">[GitHub](https://github.com/Azure/azure-quickstart-templates)'da şablon bulun veya var olan bir kaynak grubundan [Şablonu dışarı aktarın](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="a7ac0-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="a7ac0-118">**Şablonları** , kendilerini yayımlayan bağlı toohello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="a7ac0-119">okuma erişimi tooit sahip görünür tooeveryone Hello yayımcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="a7ac0-120">**Şablonlar**, Resource Manager kaynaklarıdır ve yayımlandıktan sonra yeniden adlandırılamaz.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="a7ac0-121">Şablon kaynağı ekleme</span><span class="sxs-lookup"><span data-stu-id="a7ac0-121">Add a Template resource</span></span>
<span data-ttu-id="a7ac0-122">İki yolu toocreate vardır bir **şablonu** hello Azure portal kaynak.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="a7ac0-123">1. Yöntem: Çalışan bir kaynak grubundan yeni bir Şablon kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7ac0-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="a7ac0-124">Hello Azure Portal tooan mevcut kaynak grubuna gidin.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="a7ac0-125">**Ayarlar**'da **Şablonu dışarı aktarma** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="a7ac0-126">Merhaba Resource Manager şablonunu dışarı aktarıldıktan sonra hello kullan **Şablonu Kaydet** düğmesini toosave, toohello **şablonları** deposu.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="a7ac0-127">Şablonu dışarı aktarmayla ilgili tüm ayrıntıları [burada](../azure-resource-manager/resource-manager-export-template.md) bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="a7ac0-128">
   ![Kaynak grubunu dışarı aktarma](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="a7ac0-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="a7ac0-129">Select hello **tooTemplate kaydetmek** komut düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="a7ac0-130">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="a7ac0-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="a7ac0-131">Adı – hello şablon nesnesinin adı (Not: Bu Azure Resource Manager temelli adıdır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="a7ac0-132">Tüm adlandırma kısıtlamaları geçerlidir ve oluşturulduktan sonra değiştirilemez).</span><span class="sxs-lookup"><span data-stu-id="a7ac0-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="a7ac0-133">Açıklama – hello şablonla ilgili kısa bir Özet.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-133">Description – Quick summary about hello template.</span></span>
     
     ![Şablonu kaydetme](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="a7ac0-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a7ac0-136">Merhaba dışarı aktarma şablonu dikey bildirimleri hello dışarı aktarılan Resource Manager şablonu hata var, ancak mümkün toosave olmaya devam eder Bu Resource Manager şablonu toohello şablonları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="a7ac0-137">Denetleyin ve yeniden dağıtırken hello Resource Manager şablonunu dışarı önce tüm Resource Manager şablonu sorunlarını düzeltmek emin olun.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="a7ac0-138">2. Yöntem: Gözat bölümünden yeni bir Şablon kaynağı ekleme</span><span class="sxs-lookup"><span data-stu-id="a7ac0-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="a7ac0-139">Ayrıca, yeni bir ekleyebilirsiniz **şablonu** hello + Ekle komut düğmesini kullanarak sıfırdan **Gözat > şablonlar**.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="a7ac0-140">Bir ad, açıklama ve Resource Manager şablonu JSON hello tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![Şablon ekleme](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="a7ac0-142">Microsoft.Gallery, Kiracı bazlı bir Azure kaynak sağlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="a7ac0-143">Merhaba şablon kaynağı oluşturulduğu bağlı toohello kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="a7ac0-144">Bu bağlı tooany belirli aboneliği değil.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="a7ac0-145">Bir abonelik yalnızca bir şablon dağıtılırken seçilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="a7ac0-146">Şablon kaynaklarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a7ac0-146">View Template resources</span></span>
<span data-ttu-id="a7ac0-147">Tüm **şablonları** kullanılabilir tooyou adresindeki görülme **Gözat > şablonlar**.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="a7ac0-148">Buna, oluşturduğunuz **Şablonlar**'ın yanı sıra, farklı izin düzeyleriyle sizinle paylaşılanlar da dahildir.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="a7ac0-149">Merhaba, daha fazla ayrıntı [erişim denetimi](#access-control-for-a-tenant-resource-provider) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Şablonu görüntüleme](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="a7ac0-151">Merhaba ayrıntılarını görüntüleyebilirsiniz bir **şablonu** hello listedeki bir öğeye tıklayarak.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![Şablonu görüntüleme](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="a7ac0-153">Şablon kaynağını düzenleme</span><span class="sxs-lookup"><span data-stu-id="a7ac0-153">Edit a Template resource</span></span>
<span data-ttu-id="a7ac0-154">Hello için düzenleme akışını başlatabilirsiniz bir **şablonu** hello öğede sağ tıklayarak hello Gözat listesi veya hello Düzenle komutu düğmesini seçerek.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![Şablon düzenleme](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="a7ac0-156">Merhaba açıklamayı veya Resource Manager şablonu metnini düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="a7ac0-157">Bir Resource Manager kaynak adı olduğundan hello adını düzenleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="a7ac0-158">Merhaba Resource Manager şablonu JSON düzenlediğinizde biz tooensure geçerli JSON olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="a7ac0-159">Seçin **Tamam** ve ardından **kaydetmek** toosave güncelleştirilmiş şablonunuzu.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![Şablon düzenleme](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="a7ac0-161">Bir kez hello **şablonu** kaydedilen bir onay bildirimi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![Şablon düzenleme](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="a7ac0-163">Bir Şablon kaynağını dağıtma</span><span class="sxs-lookup"><span data-stu-id="a7ac0-163">Deploy a Template resource</span></span>
<span data-ttu-id="a7ac0-164">**Okuma** izniniz olan herhangi bir **Şablon**'u dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="a7ac0-165">Merhaba dağıtım akışı hello standart Azure şablon dağıtımı dikey penceresini başlatır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="a7ac0-166">Merhaba Resource Manager şablonu parametreleri tooproceed hello dağıtımı ile Merhaba değerlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![Şablon dağıtma](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="a7ac0-168">Şablon kaynağı paylaşma</span><span class="sxs-lookup"><span data-stu-id="a7ac0-168">Share a Template resource</span></span>
<span data-ttu-id="a7ac0-169">Bir **Şablon** kaynağı iş arkadaşlarınızla paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="a7ac0-170">Paylaşımı davranır benzer şekilde çok[Azure ile ilgili herhangi bir kaynak için rol ataması](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a7ac0-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="a7ac0-171">Merhaba **şablonu** sahip bir şablon kaynağıyla etkileşim kurabilen tooother kullanıcılara izinler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="a7ac0-172">Merhaba kişi veya grup hello paylaştığınız kişilerin **şablonu** mümkün toosee hello Resource Manager şablonunu ve bunun galeri özelliklerini ile sonuna olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="a7ac0-173">Merhaba Microsoft.Gallery kaynakları için erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="a7ac0-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="a7ac0-174">Rol</span><span class="sxs-lookup"><span data-stu-id="a7ac0-174">Role</span></span> | <span data-ttu-id="a7ac0-175">İzinler</span><span class="sxs-lookup"><span data-stu-id="a7ac0-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="a7ac0-176">Sahip</span><span class="sxs-lookup"><span data-stu-id="a7ac0-176">Owner</span></span> |<span data-ttu-id="a7ac0-177">Merhaba şablon kaynağı paylaşma dahil olmak üzere üzerinde tam denetim verir</span><span class="sxs-lookup"><span data-stu-id="a7ac0-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="a7ac0-178">Okuyucu</span><span class="sxs-lookup"><span data-stu-id="a7ac0-178">Reader</span></span> |<span data-ttu-id="a7ac0-179">Şablon kaynağı hello üzerinde okuma ve Execute(Deploy) verir</span><span class="sxs-lookup"><span data-stu-id="a7ac0-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="a7ac0-180">Katılımcı</span><span class="sxs-lookup"><span data-stu-id="a7ac0-180">Contributor</span></span> |<span data-ttu-id="a7ac0-181">Şablon kaynağı hello üzerinde düzenleme ve silme izni verir.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="a7ac0-182">Kullanıcı hello şablon başkalarıyla paylaşamaz</span><span class="sxs-lookup"><span data-stu-id="a7ac0-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="a7ac0-183">Seçin **paylaşımı** hello Gözat öğesine sağ tıklayarak veya belirli bir öğenin hello görünümü dikey.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="a7ac0-184">Bu, bir Paylaşma deneyimini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-184">This launches a Share experience.</span></span>

![Şablonu paylaşma](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="a7ac0-186">Bir rolü ve bir kullanıcı veya grup tooprovide erişim tooa belirli artık seçebilirsiniz **şablon**.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="a7ac0-187">Merhaba kullanılabilir roller sahip, okuyucu ve katkıda bulunan ' dir.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="a7ac0-188">Merhaba, daha fazla ayrıntı [erişim denetimi](#access-control-for-a-tenant-resource-provider) yukarıdaki bölümde.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Şablonu paylaşma](media/share-template-portal2b.png)  <br />

![Şablonu paylaşma](media/share-template-portal3b.png)  <br />

<span data-ttu-id="a7ac0-191">**Seç**'e ve **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="a7ac0-192">Şimdi hello kullanıcıları veya grupları görebilirsiniz toohello kaynak eklendi.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-192">You can now see hello users or groups you added toohello resource.</span></span>

![Şablonu paylaşma](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="a7ac0-194">Bir şablonu yalnızca kullanıcılar ve gruplar ile hello paylaşılabilir aynı Azure Active Directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="a7ac0-195">Kiracınızda olmayan e-posta adresi olan bir şablonu paylaşıyorsanız, hello kullanıcı toojoin hello Kiracı konuk olarak soran bir davet gönderilir.</span><span class="sxs-lookup"><span data-stu-id="a7ac0-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a7ac0-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7ac0-196">Next steps</span></span>
* <span data-ttu-id="a7ac0-197">Resource Manager şablonları oluşturma hakkında daha fazla toolearn bakın [şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="a7ac0-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="a7ac0-198">bir Resource Manager şablonunda kullanabileceğiniz toounderstand hello işlevleri bkz [şablon işlevleri](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="a7ac0-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="a7ac0-199">Şablonlarınızı tasarlama konusunda rehberlik için bkz. [Azure Resource Manager şablonları oluşturmaya yönelik en iyi uygulamalar](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="a7ac0-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

