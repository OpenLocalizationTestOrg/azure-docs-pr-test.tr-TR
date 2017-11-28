---
title: "Azure depolama hesabı listesi"
description: "Eclipse için Azure Araç Seti kullanarak depolama hesap ayarlarınızı yönetme"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="89bce-103">Azure depolama hesabı listesi</span><span class="sxs-lookup"><span data-stu-id="89bce-103">Azure Storage Account List</span></span>
<span data-ttu-id="89bce-104">Azure depolama hesapları JDK, uygulama sunucusu ve isteğe bağlı bileşenler için yanı sıra durumu önbelleğe alma kullanırken depolamak için kullanılacak yükleme konumları sağlar.</span><span class="sxs-lookup"><span data-stu-id="89bce-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="89bce-105">Eclipse projelerinizi Eclipse çalışma alanında kullanılabilir bilinen depolama hesaplarının listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="89bce-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="89bce-106">Açmak için **depolama hesapları** Eclipse içinde bu listesini yönetmek için kullanılan iletişim tıklatın **penceresi**, tıklatın **Tercihler**, genişletin **Azure**ve ardından **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="89bce-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="89bce-107">Aşağıdaki gösterildiği **depolama hesapları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89bce-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="89bce-108">Bu iletişim kutusunu da açılabilir bir **hesapları** aşağıdaki gibi depolama hesaplarını kullanmak iletişim kutularında bağlantı:</span><span class="sxs-lookup"><span data-stu-id="89bce-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="89bce-109">**JDK** sekmesinde **sunucu yapılandırması** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89bce-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="89bce-110">**Server** sekmesinde **sunucu yapılandırması** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89bce-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="89bce-111">**Bileşen Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89bce-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="89bce-112">**Önbelleğe alma** Özellikleri iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="89bce-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="89bce-113">Yayımlama ayarları dosyası kullanarak depolama hesaplarınızı içeri aktarmak için</span><span class="sxs-lookup"><span data-stu-id="89bce-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="89bce-114">İçinde **depolama hesapları** iletişim kutusunda, tıklatın **yayımlama ayarları dosyasını içeri aktar**.</span><span class="sxs-lookup"><span data-stu-id="89bce-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="89bce-115">(Yerel makinenize yayımlama ayarları dosyası kaydettiyseniz bu adımı atlayın.) İçinde **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **yayımlama ayarları dosyası karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="89bce-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="89bce-116">Azure hesabınızda henüz tutulmaz, oturum açmak için istenir.</span><span class="sxs-lookup"><span data-stu-id="89bce-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="89bce-117">Ardından Azure yayımlama ayarları dosyası istenir.</span><span class="sxs-lookup"><span data-stu-id="89bce-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="89bce-118">(Oturum açma sayfalarında - gösterilen elde edilen yönergeleri yoksayabilirsiniz bunlar Azure portalı tarafından sağlanan ve Visual Studio kullanıcılar için tasarlanmıştır.) Yerel makinenize kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89bce-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="89bce-119">Hala **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **Gözat** düğmesi, yerel olarak daha önce kaydettiğiniz yayımlama ayarları dosyasını seçin ve ardından **açmak**.</span><span class="sxs-lookup"><span data-stu-id="89bce-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="89bce-120">Tıklatın **Tamam** kapatmak için **alma abonelik bilgilerini** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89bce-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="89bce-121">Yeni bir depolama hesabı oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="89bce-121">To create a new storage account</span></span>
1. <span data-ttu-id="89bce-122">İçinde **depolama hesapları** iletişim kutusunda, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89bce-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="89bce-123">İçinde **depolama hesabı Ekle** iletişim kutusunda, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="89bce-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="89bce-124">İçinde **yeni depolama hesabı** iletişim kutusunda, aşağıdaki değerleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="89bce-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="89bce-125">Depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="89bce-125">Storage account name.</span></span>

   * <span data-ttu-id="89bce-126">Depolama hesabı konumu.</span><span class="sxs-lookup"><span data-stu-id="89bce-126">Location of the storage account.</span></span>

   * <span data-ttu-id="89bce-127">Depolama hesabı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="89bce-127">Description of the storage account.</span></span>

   * <span data-ttu-id="89bce-128">Depolama hesabına ait olduğu abonelik.</span><span class="sxs-lookup"><span data-stu-id="89bce-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="89bce-129">Tıklatın **Tamam** kapatmak için **yeni depolama hesabı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89bce-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="89bce-130">Oluşturulacak depolama hesabınız için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="89bce-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="89bce-131">Oluşturulduktan sonra tıklatın **Tamam** kapatmak için **depolama hesabı Ekle** iletişim ve yeni depolama hesabınız, kullanılabilir depolama alanı hesaplar listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="89bce-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="89bce-132">Mevcut bir depolama hesabını listeye eklemek için</span><span class="sxs-lookup"><span data-stu-id="89bce-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="89bce-133">Bir Azure depolama hesabı zaten yoksa, listelenen adımları izleyerek oluşturun **yeni bir depolama hesabı bölüm oluşturmak için** üstünde.</span><span class="sxs-lookup"><span data-stu-id="89bce-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="89bce-134">(Alternatif olarak, yeni bir depolama hesabı oluşturabilirsiniz [Azure Yönetim Portalı][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="89bce-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="89bce-135">İçinde **depolama hesapları** iletişim kutusunda, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="89bce-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="89bce-136">İçinde **depolama hesabı Ekle** iletişim için değerleri girin **adı** ve **erişim tuşu**.</span><span class="sxs-lookup"><span data-stu-id="89bce-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="89bce-137">Hesap adı ve erişim anahtarı mevcut bir Azure depolama hesabı için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89bce-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="89bce-138">Kullanım **depolama** bölümünü [Azure Yönetim Portalı] [ Azure Management Portal] depolama hesabı adları ve anahtarlarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="89bce-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="89bce-139">**Depolama hesabı Ekle** iletişim aşağıdakine benzer görünür.</span><span class="sxs-lookup"><span data-stu-id="89bce-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="89bce-140">Tıklatın **Tamam** kapatmak için **depolama hesabı Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89bce-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="89bce-141">Yeni bir erişim anahtarı kullanmak üzere bir depolama hesabı değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="89bce-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="89bce-142">İçinde **depolama hesapları** iletişim, depolama hesabına o düzenlemek istiyorsanız tıklatın ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="89bce-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="89bce-143">İçinde **Düzenle depolama hesabının erişim anahtarı** iletişim kutusunda, değiştirmek **erişim tuşu** değeri.</span><span class="sxs-lookup"><span data-stu-id="89bce-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="89bce-144">Tıklatın **Tamam** kapatmak için **Düzenle depolama hesabının erişim anahtarı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="89bce-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="89bce-145">Eclipse'te tutulan listesinden bir depolama hesabını kaldırmak için</span><span class="sxs-lookup"><span data-stu-id="89bce-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="89bce-146">İçinde **depolama hesapları** iletişim, depolama hesabına o düzenlemek istiyorsanız tıklatın ve ardından **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="89bce-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="89bce-147">Tıklatın **Tamam** depolama hesabını kaldırmak isteyip istemediğiniz sorulduğunda.</span><span class="sxs-lookup"><span data-stu-id="89bce-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="89bce-148">Üzerinden depolama hesabı kaldırma **depolama hesapları** iletişim yalnızca onu kaldırır listesinden depolama hesaplarının Eclipse içinde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="89bce-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="89bce-149">Depolama hesabı Azure aboneliğinizden kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="89bce-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="89bce-150">Ayrıca, Eclipse aboneliğinizi ayrıntılarını yeniden yükler sonra depolama hesabını yeniden listenizde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="89bce-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="89bce-151">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="89bce-151">See Also</span></span>
<span data-ttu-id="89bce-152">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89bce-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="89bce-153">[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89bce-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="89bce-154">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="89bce-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="89bce-155">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="89bce-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
