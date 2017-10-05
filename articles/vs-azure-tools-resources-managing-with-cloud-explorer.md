---
title: "Bulut Gezgini ile Azure kaynaklarını yönetme | Microsoft Docs"
description: "Cloud Explorer göz atın ve Visual Studio içinde Azure kaynaklarınızı yönetmek için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 6e6d8d559f0251b71bfa6d529ead82a246cb3235
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="5aac0-103">Visual Studio Cloud Explorer'da, Azure hesaplarıyla ilişkili kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="5aac0-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="5aac0-104">Cloud Explorer Azure kaynakları ve kaynak gruplarını görüntülemek özelliklerini inceleyin ve Visual Studio içinde anahtar Geliştirici tanılama eylemleri gerçekleştirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="5aac0-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="5aac0-105">Gibi [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer Azure Kaynak Yöneticisi yığınında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5aac0-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span></span> <span data-ttu-id="5aac0-106">Bu nedenle, Cloud Explorer anlar Azure kaynak gruplarını gibi kaynakları ve Logic apps ve API uygulamaları gibi Azure Hizmetleri ve destekliyorsa [rol tabanlı erişim denetimi](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="5aac0-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5aac0-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5aac0-107">Prerequisites</span></span>
- <span data-ttu-id="5aac0-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) ile **Azure iş yükü** seçili, ya da Visual Studio ile önceki bir sürümünü [.NET 2.9 için Microsoft Azure SDK'sı](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="5aac0-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="5aac0-109">Microsoft Azure hesabı - bir hesabınız yoksa, şunları yapabilirsiniz [ücretsiz deneme için kaydolun](http://go.microsoft.com/fwlink/?LinkId=623901) veya [Visual Studio abone Avantajlarınızı etkinleştirebilir](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="5aac0-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="5aac0-110">Cloud Explorer görüntülemek için seçin **Görünüm** > **Cloud Explorer** menü çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="5aac0-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-to-cloud-explorer"></a><span data-ttu-id="5aac0-111">Bir Azure eklemek hesabı bulut Gezgini</span><span class="sxs-lookup"><span data-stu-id="5aac0-111">Add an Azure account to Cloud Explorer</span></span>
<span data-ttu-id="5aac0-112">Bir Azure hesabı ile ilişkili kaynakları görüntülemek için hesabı bulut Gezgini'ne eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5aac0-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span></span> 

1. <span data-ttu-id="5aac0-113">İçinde **Cloud Explorer**seçin **Azure hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="5aac0-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="5aac0-115">Seçin **yeni hesap eklemek**.</span><span class="sxs-lookup"><span data-stu-id="5aac0-115">Select **Add new account**.</span></span> 

    ![Cloud Explorer hesabı Ekle bağlantı](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="5aac0-117">Gözatmak istediğiniz kaynakları Azure hesabı için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5aac0-117">Log in to the Azure account whose resources you want to browse.</span></span> 

1. <span data-ttu-id="5aac0-118">Bir Azure hesabına oturum sonra bu hesapla ilişkili abonelikleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5aac0-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span></span> <span data-ttu-id="5aac0-119">Göz atın ve ardından istediğiniz hesap aboneliklerinin onay kutularını işaretleyin **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="5aac0-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer: görüntülemek için Azure aboneliklerini seçin](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="5aac0-121">Kaynakları gözatmak istediğiniz abonelikleri seçtikten sonra bu abonelikleri ve kaynakları bulut Gezgini'nde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5aac0-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span></span>

    ![Cloud Explorer kaynak bir Azure hesabı için listeleme](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="5aac0-123">Bir Azure hesabı bulut gezgininden Kaldır</span><span class="sxs-lookup"><span data-stu-id="5aac0-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="5aac0-124">İçinde **Cloud Explorer**seçin **Azure hesap ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="5aac0-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="5aac0-126">Kaldırmak istediğiniz hesabı yanındaki seçin **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="5aac0-126">Next to the account you want to remove, select **Remove**.</span></span>

    ![Cloud Explorer Azure hesabı ayarları simgesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="5aac0-128">Kaynak türleri veya kaynak gruplarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="5aac0-128">View resource types or resource groups</span></span>
<span data-ttu-id="5aac0-129">Azure kaynaklarınızı görüntülemeyi ya da seçebilir **kaynak türleri** veya **kaynak grupları** görünümü.</span><span class="sxs-lookup"><span data-stu-id="5aac0-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="5aac0-130">İçinde **Cloud Explorer**, kaynak görünümü açılır seçin.</span><span class="sxs-lookup"><span data-stu-id="5aac0-130">In **Cloud Explorer**, select the resource view dropdown.</span></span>

    ![İstenen kaynakları görünüm seçmek için bulut Explorer açılır listesi](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="5aac0-132">Bağlam menüsünden istediğiniz görünümü seçin:</span><span class="sxs-lookup"><span data-stu-id="5aac0-132">From the context menu, select the desired view:</span></span> 

    - <span data-ttu-id="5aac0-133">**Kaynak türleri** view - üzerinde kullanılan genel görünüm [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), web uygulamaları, depolama hesapları ve sanal makineler gibi kendi türüne göre kategorize Azure kaynaklarınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5aac0-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="5aac0-134">**Kaynak grupları** view - kategorilere ayıran Azure kaynakları ile bunların ilişkili Azure kaynak grubu tarafından.</span><span class="sxs-lookup"><span data-stu-id="5aac0-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span></span> <span data-ttu-id="5aac0-135">Bir kaynak grubu genellikle belirli bir uygulama tarafından kullanılan Azure kaynaklarını paketidir.</span><span class="sxs-lookup"><span data-stu-id="5aac0-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="5aac0-136">Azure kaynak grupları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5aac0-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="5aac0-137">Aşağıdaki görüntü iki kaynak görünümleri karşılaştırması göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="5aac0-137">The following image shows a comparison of the two resource views:</span></span>

    ![Cloud Explorer kaynak görünümleri karşılaştırma](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="5aac0-139">Görüntülemek ve bulut Explorer'da kaynaklara gidin</span><span class="sxs-lookup"><span data-stu-id="5aac0-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="5aac0-140">Bir Azure kaynağı gidin ve Cloud Explorer'da bilgilerini görüntülemek için öğenin türü veya ilişkili kaynak grubunu genişletin ve ardından kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="5aac0-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span></span> <span data-ttu-id="5aac0-141">Bir kaynak seçtiğinizde, bilgiler iki sekmeleri - görünür **Eylemler** ve **özellikleri** - Cloud Explorer'ın altındaki.</span><span class="sxs-lookup"><span data-stu-id="5aac0-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="5aac0-142">**Eylemler** sekmesi - Cloud Explorer'da seçilen kaynak için gerçekleştirebileceğiniz eylemleri listeler.</span><span class="sxs-lookup"><span data-stu-id="5aac0-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span></span> <span data-ttu-id="5aac0-143">Bu seçenekler, bağlam menüsü görüntülemek için kaynak sağ tıklayarak da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aac0-143">You can also view these options by right-clicking the resource to view its context menu.</span></span>

- <span data-ttu-id="5aac0-144">**Özellikler** sekmesi - olduğu ilişkili türü, yerel ayar ve kaynak grubu gibi kaynak özelliklerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5aac0-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="5aac0-145">Aşağıdaki resimde, her bir sekmede bir uygulama hizmeti için gördüğünüz bir örnek karşılaştırması gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="5aac0-145">The following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="5aac0-146">Her kaynak eyleme sahip **portalında açık**.</span><span class="sxs-lookup"><span data-stu-id="5aac0-146">Every resource has the action **Open in portal**.</span></span> <span data-ttu-id="5aac0-147">Bu eylem seçtiğinizde, seçilen kaynak Cloud Explorer görüntüler [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="5aac0-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="5aac0-148">**Portalında açık** özelliktir iç içe kaynaklarına gezinmek için kullanışlı.</span><span class="sxs-lookup"><span data-stu-id="5aac0-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span></span>

<span data-ttu-id="5aac0-149">Ek eylemleri ve özellik değerlerini de Azure kaynak tabanlı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="5aac0-149">Additional actions and property values may also appear based on the Azure resource.</span></span> <span data-ttu-id="5aac0-150">Örneğin, web uygulamaları ve mantıksal uygulamalar eylemleri de **tarayıcıda aç** ve **hata ayıklayıcısını** ek olarak **portalında açık**.</span><span class="sxs-lookup"><span data-stu-id="5aac0-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span></span> <span data-ttu-id="5aac0-151">Depolama hesabı blob, kuyruk veya tablo seçtiğinizde, düzenleyiciler açmak için Eylemler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5aac0-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="5aac0-152">Azure uygulamaları **URL** ve **durum** depolama kaynaklarını anahtar ve bağlantı dizesi özellikleri varken özellikleri.</span><span class="sxs-lookup"><span data-stu-id="5aac0-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="5aac0-153">Cloud Explorer'da kaynakları bulun</span><span class="sxs-lookup"><span data-stu-id="5aac0-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="5aac0-154">Azure hesabı aboneliklerinizi belirli bir ada sahip kaynaklarını bulmak için ad girin **arama** Cloud Explorer'da kutusu.</span><span class="sxs-lookup"><span data-stu-id="5aac0-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span></span>

![Cloud Explorer'da kaynakları bulma](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="5aac0-156">Karakter girerken **arama** kutusu, bu karakterler karşılayan kaynakları kaynak ağacında görünür.</span><span class="sxs-lookup"><span data-stu-id="5aac0-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span></span>
