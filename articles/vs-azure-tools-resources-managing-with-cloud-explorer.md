---
title: aaaManaging Azure Cloud Explorer kaynaklarla | Microsoft Docs
description: "Bilgi nasıl toouse Cloud Explorer toobrowse ve Visual Studio içinde Azure kaynaklarını yönetin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="91e4e-103">Visual Studio Cloud Explorer'da, Azure hesaplarıyla ilişkili hello kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="91e4e-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="91e4e-104">Cloud Explorer, tooview Azure kaynaklarınızı etkinleştirir ve kaynak grupları, bunların özelliklerini inceleyebilir ve Visual Studio içinde anahtar Geliştirici tanılama eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="91e4e-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="91e4e-105">Hello gibi [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer hello Azure Kaynak Yöneticisi yığınında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="91e4e-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="91e4e-106">Bu nedenle, Cloud Explorer anlar Azure kaynak gruplarını gibi kaynakları ve Logic apps ve API uygulamaları gibi Azure Hizmetleri ve destekliyorsa [rol tabanlı erişim denetimi](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="91e4e-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="91e4e-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="91e4e-107">Prerequisites</span></span>
- <span data-ttu-id="91e4e-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) hello ile **Azure iş yükü** seçili veya önceki bir sürümünü Visual Studio ile Merhaba [.NET 2.9 için Microsoft Azure SDK'sı](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="91e4e-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="91e4e-109">Microsoft Azure hesabı - bir hesabınız yoksa, şunları yapabilirsiniz [ücretsiz deneme için kaydolun](http://go.microsoft.com/fwlink/?LinkId=623901) veya [Visual Studio abone Avantajlarınızı etkinleştirebilir](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="91e4e-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="91e4e-110">tooview Cloud Explorer seçin **Görünüm** > **Cloud Explorer** hello menü çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="91e4e-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="91e4e-111">Bir Azure hesabı tooCloud Explorer ekleme</span><span class="sxs-lookup"><span data-stu-id="91e4e-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="91e4e-112">bir Azure hesabı ile ilişkili tooview hello kaynakları hello hesap tooCloud Explorer ilk eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="91e4e-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="91e4e-113">İçinde **Cloud Explorer**seçin **Azure hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="91e4e-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="91e4e-115">Seçin **yeni hesap eklemek**.</span><span class="sxs-lookup"><span data-stu-id="91e4e-115">Select **Add new account**.</span></span> 

    ![Cloud Explorer hesabı Ekle bağlantı](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="91e4e-117">Toohello kaynakları istediğiniz Azure hesabı oturum toobrowse.</span><span class="sxs-lookup"><span data-stu-id="91e4e-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="91e4e-118">Tooan Azure hesabı oturum sonra bu hesapla ilişkili hello abonelikleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="91e4e-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="91e4e-119">Merhaba toobrowse istediğiniz ve ardından hello hesap aboneliklerinin onay kutularını seçin **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="91e4e-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: Azure abonelikleri toodisplay seçin](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="91e4e-121">Kaynakları istediğiniz hello abonelikleri seçtikten sonra toobrowse, bu abonelikleri ve kaynakları hello Cloud Explorer görüntüler.</span><span class="sxs-lookup"><span data-stu-id="91e4e-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Cloud Explorer kaynak bir Azure hesabı için listeleme](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="91e4e-123">Bir Azure hesabı bulut gezgininden Kaldır</span><span class="sxs-lookup"><span data-stu-id="91e4e-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="91e4e-124">İçinde **Cloud Explorer**seçin **Azure hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="91e4e-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="91e4e-126">Sonraki toohello hesabı tooremove, istediğiniz **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="91e4e-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="91e4e-128">Kaynak türleri veya kaynak gruplarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="91e4e-128">View resource types or resource groups</span></span>
<span data-ttu-id="91e4e-129">tooview ya da seçin, Azure kaynaklarınıza **kaynak türleri** veya **kaynak grupları** görünümü.</span><span class="sxs-lookup"><span data-stu-id="91e4e-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="91e4e-130">İçinde **Cloud Explorer**, select hello kaynak görünümü açılır.</span><span class="sxs-lookup"><span data-stu-id="91e4e-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Cloud Explorer açılır liste tooselect istenen hello kaynakları görünümü](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="91e4e-132">Merhaba bağlam menüsünden istenen hello görünümü seçin:</span><span class="sxs-lookup"><span data-stu-id="91e4e-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="91e4e-133">**Kaynak türleri** görünümü - hello üzerinde kullanılan hello ortak [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), web uygulamaları, depolama hesapları ve sanal makineler gibi kendi türüne göre kategorize Azure kaynaklarınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="91e4e-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="91e4e-134">**Kaynak grupları** view - kategorilere ayıran Azure kaynakları ile bunların ilişkili hello Azure kaynak grubu tarafından.</span><span class="sxs-lookup"><span data-stu-id="91e4e-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="91e4e-135">Bir kaynak grubu genellikle belirli bir uygulama tarafından kullanılan Azure kaynaklarını paketidir.</span><span class="sxs-lookup"><span data-stu-id="91e4e-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="91e4e-136">Azure kaynak grupları hakkında daha fazla toolearn bkz [Azure Resource Manager'a genel bakış](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91e4e-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="91e4e-137">Merhaba aşağıdaki resimde hello karşılaştırması iki kaynak görünümleri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="91e4e-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Cloud Explorer kaynak görünümleri karşılaştırma](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="91e4e-139">Görüntülemek ve bulut Explorer'da kaynaklara gidin</span><span class="sxs-lookup"><span data-stu-id="91e4e-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="91e4e-140">Azure kaynak toonavigate tooan ve Cloud Explorer'da bilgilerini görüntülemek, hello öğenin türü veya ilişkili kaynak grubunu genişletin ve ardından hello kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="91e4e-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="91e4e-141">Bir kaynak seçtiğinizde, bilgi hello iki sekmeleri - görünür **Eylemler** ve **özellikleri** - Cloud Explorer hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="91e4e-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="91e4e-142">**Eylemler** sekmesi - listeleri hello eylemler için seçili hello kaynak Cloud Explorer'da alabilir.</span><span class="sxs-lookup"><span data-stu-id="91e4e-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="91e4e-143">Ayrıca bu seçenekler hello kaynak tooview sağ tıklayarak bağlam menüsünü görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91e4e-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="91e4e-144">**Özellikler** sekmesi - olduğu ilişkili türü, yerel ayar ve kaynak grubu gibi hello kaynak hello özelliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="91e4e-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="91e4e-145">Merhaba aşağıdaki resimde, her bir sekmede bir uygulama hizmeti için gördüğünüz bir örnek karşılaştırması gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="91e4e-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="91e4e-146">Her kaynak hello eyleminin **portalında açık**.</span><span class="sxs-lookup"><span data-stu-id="91e4e-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="91e4e-147">Bu eylem seçtiğinizde, bulut Explorer seçili hello kaynak hello görüntüler. [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="91e4e-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="91e4e-148">Merhaba **portalında açık** özelliktir iç içe geçmiş toodeeply kaynakları gezinmek için kullanışlı.</span><span class="sxs-lookup"><span data-stu-id="91e4e-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="91e4e-149">Ek eylemleri ve özellik değerlerini de hello Azure kaynak üzerinde tabanlı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="91e4e-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="91e4e-150">Örneğin, web uygulamaları ve logic apps hello eylemleri de **tarayıcıda aç** ve **hata ayıklayıcısını** ayrıca çok**portalında açık**.</span><span class="sxs-lookup"><span data-stu-id="91e4e-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="91e4e-151">Depolama hesabı blob, kuyruk veya tablo seçtiğinizde Eylemler tooopen düzenleyicileri görünür.</span><span class="sxs-lookup"><span data-stu-id="91e4e-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="91e4e-152">Azure uygulamaları **URL** ve **durum** depolama kaynaklarını anahtar ve bağlantı dizesi özellikleri varken özellikleri.</span><span class="sxs-lookup"><span data-stu-id="91e4e-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="91e4e-153">Cloud Explorer'da kaynakları bulun</span><span class="sxs-lookup"><span data-stu-id="91e4e-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="91e4e-154">Azure hesabı aboneliklerinizi belirli bir adla toolocate kaynaklarla hello hello adı girin **arama** Cloud Explorer'da kutusu.</span><span class="sxs-lookup"><span data-stu-id="91e4e-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Cloud Explorer'da kaynakları bulma](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="91e4e-156">Hello karakter girerken **arama** kutusu, bu karakterler karşılayan kaynakları hello kaynak ağacında görünür.</span><span class="sxs-lookup"><span data-stu-id="91e4e-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
