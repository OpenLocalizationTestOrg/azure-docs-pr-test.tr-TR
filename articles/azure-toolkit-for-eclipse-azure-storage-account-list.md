---
title: "aaaAzure depolama hesabı listesi"
description: "Eclipse için Hello Azure Araç Seti kullanarak depolama hesap ayarlarınızı yönetme"
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
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="3d50f-103">Azure depolama hesabı listesi</span><span class="sxs-lookup"><span data-stu-id="3d50f-103">Azure Storage Account List</span></span>
<span data-ttu-id="3d50f-104">Azure depolama hesaplarını etkinleştirme JDK, uygulama sunucusu ve isteğe bağlı bileşenler için yanı sıra durumu önbelleğe alma kullanırken depolamak için kullanılan konumlardan toobe indirin.</span><span class="sxs-lookup"><span data-stu-id="3d50f-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="3d50f-105">Eclipse Eclipse çalışma alanında kullanılabilir tooyour projeleri bilinen depolama hesaplarının listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="3d50f-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="3d50f-106">tooopen hello **depolama hesapları** listesinde, Eclipse içinde kullanılan toomanage olan iletişim tıklatın **penceresi**, tıklatın **Tercihler**, genişletin **Azure** ve ardından **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="3d50f-107">Merhaba aşağıdaki gösterir hello **depolama hesapları** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d50f-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="3d50f-108">Bu iletişim kutusunu da açılabilir bir **hesapları** hello aşağıdaki gibi depolama hesaplarını kullanmak iletişim kutularında bağlantı:</span><span class="sxs-lookup"><span data-stu-id="3d50f-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="3d50f-109">Merhaba **JDK** hello sekmesinde **sunucu yapılandırması** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d50f-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="3d50f-110">Merhaba **Server** hello sekmesinde **sunucu yapılandırması** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d50f-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="3d50f-111">Merhaba **Bileşen Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d50f-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="3d50f-112">Merhaba **önbelleğe alma** Özellikleri iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="3d50f-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="3d50f-113">Depolama hesaplarını kullanarak tooimport yayımlama ayarları dosyası</span><span class="sxs-lookup"><span data-stu-id="3d50f-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="3d50f-114">Merhaba içinde **depolama hesapları** iletişim kutusunda, tıklatın **yayımlama ayarları dosyasını içeri aktar**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="3d50f-115">(Bir yayımlama ayarları dosyası tooyour yerel makine zaten kaydedilmiş dosyalarınız varsa bu adımı atlayın.) Merhaba, **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **yayımlama ayarları dosyası karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="3d50f-116">Azure hesabınızda henüz tutulmaz içinde istendiğinde toolog olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3d50f-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="3d50f-117">Size sorulacaktır sonra toosave Azure yayımlama ayarları dosyası.</span><span class="sxs-lookup"><span data-stu-id="3d50f-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="3d50f-118">(Merhaba elde edilen yönergeleri hello oturum açma sayfalarında - gösterilen yoksayabilirsiniz bunlar hello Azure portalı tarafından sağlanan ve Visual Studio kullanıcılar için tasarlanmıştır.) Tooyour yerel makine kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3d50f-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="3d50f-119">Merhaba yine de **alma abonelik bilgilerini** iletişim kutusunda, hello tıklatın **Gözat** düğmesi, select hello yayımlama yerel olarak daha önce kaydettiğiniz ayarları dosyası ve ardından **açın**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="3d50f-120">Tıklatın **Tamam** tooclose hello **alma abonelik bilgilerini** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d50f-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="3d50f-121">toocreate yeni bir depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="3d50f-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="3d50f-122">Merhaba içinde **depolama hesapları** iletişim kutusunda, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="3d50f-123">Merhaba içinde **depolama hesabı Ekle** iletişim kutusunda, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="3d50f-124">Merhaba içinde **yeni depolama hesabı** iletişim kutusunda, hello aşağıdaki değerleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="3d50f-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="3d50f-125">Depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="3d50f-125">Storage account name.</span></span>

   * <span data-ttu-id="3d50f-126">Merhaba depolama hesabı konumu.</span><span class="sxs-lookup"><span data-stu-id="3d50f-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="3d50f-127">Merhaba depolama hesabı açıklaması.</span><span class="sxs-lookup"><span data-stu-id="3d50f-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="3d50f-128">Merhaba abonelik toowhich hello depolama hesabına ait.</span><span class="sxs-lookup"><span data-stu-id="3d50f-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="3d50f-129">Tıklatın **Tamam** tooclose hello **yeni depolama hesabı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d50f-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="3d50f-130">Oluşturulan, depolama hesabı toobe için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3d50f-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="3d50f-131">Oluşturulduktan sonra tıklatın **Tamam** tooclose hello **depolama hesabı Ekle** iletişim ve yeni depolama hesabınız, kullanılabilir depolama hesaplarını toohello listesine eklenecek.</span><span class="sxs-lookup"><span data-stu-id="3d50f-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="3d50f-132">Varolan bir depolama hesabı toohello listesini tooadd</span><span class="sxs-lookup"><span data-stu-id="3d50f-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="3d50f-133">Bir Azure depolama hesabı, bir oluşturma zaten yoksa hello adımları izleyerek hello listelenen **toocreate yeni bir depolama hesabı bölüm** üstünde.</span><span class="sxs-lookup"><span data-stu-id="3d50f-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="3d50f-134">(Alternatif olarak, hello yeni bir depolama hesabı oluşturabilirsiniz [Azure Yönetim Portalı][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="3d50f-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="3d50f-135">Merhaba içinde **depolama hesapları** iletişim kutusunda, tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="3d50f-136">Merhaba içinde **depolama hesabı Ekle** iletişim için değerleri girin **adı** ve **erişim tuşu**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="3d50f-137">Merhaba hesap adı ve erişim anahtarı mevcut bir Azure depolama hesabı için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3d50f-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="3d50f-138">Kullanım hello **depolama** hello bölümünü [Azure Yönetim Portalı] [ Azure Management Portal] tooview depolama hesabı adları ve anahtarları.</span><span class="sxs-lookup"><span data-stu-id="3d50f-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="3d50f-139">**Depolama hesabı Ekle** benzer toohello aşağıdaki iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="3d50f-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="3d50f-140">Tıklatın **Tamam** tooclose hello **depolama hesabı Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d50f-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="3d50f-141">toomodify bir depolama hesabı toouse yeni bir erişim anahtarı</span><span class="sxs-lookup"><span data-stu-id="3d50f-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="3d50f-142">Merhaba içinde **depolama hesapları** iletişim kutusunda, tooedit istediğiniz ve ardından hello depolama hesabını tıklatın **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="3d50f-143">Merhaba içinde **Düzenle depolama hesabının erişim anahtarı** iletişim kutusunda, hello değiştirme **erişim tuşu** değeri.</span><span class="sxs-lookup"><span data-stu-id="3d50f-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="3d50f-144">Tıklatın **Tamam** tooclose hello **Düzenle depolama hesabının erişim anahtarı** iletişim.</span><span class="sxs-lookup"><span data-stu-id="3d50f-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="3d50f-145">tooremove Eclipse'te tutulan hello listesinden bir depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="3d50f-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="3d50f-146">Merhaba içinde **depolama hesapları** iletişim kutusunda, tooedit istediğiniz ve ardından hello depolama hesabını tıklatın **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="3d50f-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="3d50f-147">Tıklatın **Tamam** zaman istendiğinde tooremove hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="3d50f-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="3d50f-148">Merhaba üzerinden Hello depolama hesabı kaldırma **depolama hesapları** iletişim yalnızca onu kaldırır hello listesinden depolama hesapları Eclipse içinde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="3d50f-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="3d50f-149">Merhaba depolama hesabı Azure aboneliğinizden kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="3d50f-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="3d50f-150">Ayrıca, Eclipse aboneliğinizi hello ayrıntılarını yeniden yükler sonra hello depolama hesabı yeniden listenizde görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="3d50f-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="3d50f-151">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="3d50f-151">See Also</span></span>
<span data-ttu-id="3d50f-152">[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3d50f-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="3d50f-153">[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3d50f-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="3d50f-154">[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3d50f-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="3d50f-155">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="3d50f-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
