---
title: "aaaGet başlatılan Depolama Gezgini (Önizleme) | Microsoft Docs"
description: "Depolama Gezgini (Önizleme) ile Azure Storage kaynaklarını yönetme"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="95082-103">Depolama Gezgini (Önizleme) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="95082-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="95082-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="95082-104">Overview</span></span>
<span data-ttu-id="95082-105">Azure Depolama Gezgini (Önizleme), Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan tek başına bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="95082-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="95082-106">Bu makalede, hello Azure storage hesaplarınızı yönetmeye tooand bağlanma çeşitli yollarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="95082-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Microsoft Azure Depolama Gezgini (Önizleme)][15]

## <a name="prerequisites"></a><span data-ttu-id="95082-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="95082-108">Prerequisites</span></span>
* [<span data-ttu-id="95082-109">Depolama Gezgini (Önizleme) indirip yükleme</span><span class="sxs-lookup"><span data-stu-id="95082-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="95082-110">Tooa depolama hesabı veya hizmetine bağlanmak</span><span class="sxs-lookup"><span data-stu-id="95082-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="95082-111">Depolama Gezgini (Önizleme) tooconnect toostorage hesapları çeşitli yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="95082-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="95082-112">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95082-112">For example, you can:</span></span>
* <span data-ttu-id="95082-113">Azure aboneliği ile ilişkili toostorage hesaplarını bağlayın.</span><span class="sxs-lookup"><span data-stu-id="95082-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="95082-114">Toostorage hesapları ve paylaşılan hizmetler diğer Azure aboneliklerinden bağlayın.</span><span class="sxs-lookup"><span data-stu-id="95082-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="95082-115">Connect tooand hello Azure Storage öykünücüsü kullanarak yerel depolama yönetin.</span><span class="sxs-lookup"><span data-stu-id="95082-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="95082-116">Ayrıca global ve ulusal Azure'daki depolama hesaplarıyla çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95082-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="95082-117">[Tooan Azure aboneliğine bağlanma](#connect-to-an-azure-subscription): tooyour Azure aboneliğine ait depolama kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="95082-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="95082-118">[İş yerel geliştirme depolama ile](#work-with-local-development-storage): hello Azure Storage öykünücüsü kullanarak yerel depolama yönetin.</span><span class="sxs-lookup"><span data-stu-id="95082-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="95082-119">[Tooexternal depolama ekleme](#attach-or-detach-an-external-storage-account): tooanother Azure aboneliğine ait depolama kaynaklarını yönetmek veya hello depolama hesabının adını, anahtar ve uç noktaları kullanarak Azure Ulusal Bulutlar altında olan.</span><span class="sxs-lookup"><span data-stu-id="95082-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="95082-120">[Bir SAS kullanarak bir depolama hesabı ekleme](#attach-storage-account-using-sas): paylaşılan erişim imzası (SAS) kullanılarak tooanother Azure aboneliğine ait depolama kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="95082-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="95082-121">[Bir SAS kullanarak hizmet ekleme](#attach-service-using-sas): bir SAS kullanarak tooanother Azure aboneliğine ait belirli bir depolama hizmetini (blob kapsayıcısı, kuyruk veya tablo) yönetme.</span><span class="sxs-lookup"><span data-stu-id="95082-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="95082-122">Tooan Azure aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="95082-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="95082-123">Bir Azure hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="95082-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="95082-124">Storage Explorer’da (Önizleme) **Azure Hesap ayarları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="95082-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Azure hesap ayarları][0]

2. <span data-ttu-id="95082-126">Merhaba sol bölmede oturum açtığınız tüm hello Microsoft hesapları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="95082-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="95082-127">tooconnect tooanother hesabı, select **Hesap Ekle**, en az bir etkin Azure aboneliği ile ilişkili bir Microsoft hesabıyla hello yönergeleri toosign izleyin.</span><span class="sxs-lookup"><span data-stu-id="95082-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="95082-128">Toonational Azure (örneğin, Azure Almanya, Azure kamu ve oturum açma aracılığıyla Azure Çin) bağlanması şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="95082-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="95082-129">Merhaba bkz "ekleme veya harici bir depolama hesabı ayırma" bölümü için nasıl tooconnect toonational Azure depolama hesapları.</span><span class="sxs-lookup"><span data-stu-id="95082-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="95082-130">Sonra başarıyla ile hello bölmesini doldurulmuş bir Microsoft hesabı, sol hello bu hesapla ilişkili Azure abonelikleri oturum açın.</span><span class="sxs-lookup"><span data-stu-id="95082-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="95082-131">Select hello toowork ile istediğiniz ve ardından Azure abonelikleri **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="95082-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="95082-132">(Seçme **tüm abonelikleri** değiştirir veya hello hiçbirinin seçerek listelenen Azure aboneliklerinin.)</span><span class="sxs-lookup"><span data-stu-id="95082-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![Azure aboneliklerini seçme][3]  
    <span data-ttu-id="95082-134">Hello sol bölmede seçili hello Azure abonelikleriyle ilişkilendirilen hello depolama hesapları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="95082-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![Seçili Azure abonelikleri][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="95082-136">Tooan Azure yığın abonelik'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="95082-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="95082-137">Bağlantı tooan Azure yığın aboneliği hakkında daha fazla bilgi için bkz: [bağlanmak Depolama Gezgini tooan Azure yığın abonelik](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="95082-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="95082-138">Yerel geliştirme deposu ile çalışma</span><span class="sxs-lookup"><span data-stu-id="95082-138">Work with local development storage</span></span>
<span data-ttu-id="95082-139">Depolama Gezgini (Önizleme) ile hello Azure Storage öykünücüsü kullanarak yerel depolama karşı çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95082-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="95082-140">Bu yaklaşım hello depolama hesabı hello Azure Storage öykünücüsü tarafından öykündüğü için mutlaka Azure üzerinde dağıtılan bir depolama hesabı gerek kalmadan karşı kodu ve test depolama yazmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="95082-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="95082-141">Hello Azure Storage öykünücüsü şu anda yalnızca Windows için desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="95082-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="95082-142">Merhaba sol depolama Gezgini'nin (Önizleme) hello bölmesinde **(yerel ve iliştirildiği)** > **depolama hesapları** > **(Geliştirme)** düğümü.</span><span class="sxs-lookup"><span data-stu-id="95082-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Yerel geliştirme düğümü][21]

2. <span data-ttu-id="95082-144">Hello Azure Storage öykünücüsünü henüz yüklü değilse, istendiğinde toodo olan bir bilgi çubuğu aracılığıyla bunu.</span><span class="sxs-lookup"><span data-stu-id="95082-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="95082-145">Merhaba bilgi çubuğu görüntülendiyse seçin **indirme hello en son sürümünü**ve ardından hello öykünücüsü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="95082-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![Azure Storage Öykünücüsünü İndirme istemi][22]

3. <span data-ttu-id="95082-147">Merhaba öykünücü yüklendikten sonra oluşturun ve yerel bloblar, kuyruklar ve tablolar ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="95082-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="95082-148">Her bir depolama hesabıyla toowork nasıl türü, toolearn hello aşağıdakilerden birini bakın:</span><span class="sxs-lookup"><span data-stu-id="95082-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="95082-149">Azure blob depolama kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="95082-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="95082-150">Azure dosya paylaşımı depolama kaynaklarını yönetme: *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="95082-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="95082-151">Azure kuyruk depolama kaynaklarını yönetme: *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="95082-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="95082-152">Azure Tablo Depolama kaynaklarını yönetme - *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="95082-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="95082-153">Harici bir depolama hesabı ekleme veya ayırma</span><span class="sxs-lookup"><span data-stu-id="95082-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="95082-154">Depolama Gezgini (Önizleme) ile depolama hesapları kolaylıkla paylaşılabilir böylece tooexternal depolama hesapları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95082-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="95082-155">Bu bölümde nasıl tooattach too(and detach from) harici depolama hesapları.</span><span class="sxs-lookup"><span data-stu-id="95082-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="95082-156">Merhaba depolama hesabı bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="95082-156">Get hello storage account credentials</span></span>
<span data-ttu-id="95082-157">tooshare harici bir depolama hesabı, hello hesabının sahibi söz konusu ilk hello hesabı için (hesap adı ve anahtar) hello kimlik bilgileri alın ve sonra bu bilgileri tooattach toothat (harici) hesabı isteyen hello kişiyle paylaşabilirsiniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="95082-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="95082-158">Merhaba aşağıdakileri yaparak hello depolama hesabının kimlik bilgilerini hello Azure portal aracılığıyla elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95082-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="95082-159">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="95082-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="95082-160">**Gözat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="95082-160">Select **Browse**.</span></span>

3. <span data-ttu-id="95082-161">**Depolama Hesapları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="95082-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="95082-162">Merhaba üzerinde **depolama hesapları** dikey penceresinde, select hello istenen depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="95082-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="95082-163">Merhaba üzerinde **ayarları** hello dikey penceresinde seçili depolama hesabı, seçin **erişim anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="95082-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![Erişim Anahtarları seçeneği][5]

6. <span data-ttu-id="95082-165">Merhaba üzerinde **erişim anahtarları** dikey penceresinde, kopyalama hello **depolama hesabı adı** ve **key1** toohello depolama hesabı eklenirken kullanılacak değerler.</span><span class="sxs-lookup"><span data-stu-id="95082-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![Erişim tuşları][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="95082-167">Tooan harici depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="95082-167">Attach tooan external storage account</span></span>
<span data-ttu-id="95082-168">tooattach tooan harici depolama hesabı, hello hesabın adı ve anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="95082-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="95082-169">Bu değerleri tooobtain hello Azure portalına nasıl Hello "Get hello depolama hesabı kimlik" bölümde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="95082-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="95082-170">Ancak, hello Portalı'nda hello hesap anahtarı olarak adlandırılır **key1**.</span><span class="sxs-lookup"><span data-stu-id="95082-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="95082-171">Hesap anahtarı için Depolama Gezgini (Önizleme) ister burada şekilde hello girin **key1** değeri.</span><span class="sxs-lookup"><span data-stu-id="95082-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="95082-172">Depolama Gezgini (Önizleme), seçin **tooAzure depolama birimini bağlayın**.</span><span class="sxs-lookup"><span data-stu-id="95082-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![TooAzure depolama seçeneği Bağlan][23]

2. <span data-ttu-id="95082-174">Merhaba, **tooAzure depolama bağlanmak** iletişim kutusunda, hello hesap anahtarı belirtin (Merhaba **key1** hello Azure portal değerinden) ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="95082-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95082-175">Ulusal Azure üzerinde bir depolama hesabından hello depolama bağlantı dizesi girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95082-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="95082-176">Örneğin, tooconnect tooAzure Almanya depolama hesapları, bağlantı dizeleri benzer toohello aşağıdakileri girin:</span><span class="sxs-lookup"><span data-stu-id="95082-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="95082-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="95082-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="95082-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="95082-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="95082-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="95082-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="95082-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="95082-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="95082-181">Merhaba bağlantı dizesi hello Azure ' alabileceğiniz hello portal aynı şekilde açıklandığı gibi bölüm "Merhaba depolama hesabı bilgilerini al" Merhaba.</span><span class="sxs-lookup"><span data-stu-id="95082-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![Bağlan tooAzure depolama iletişim kutusu][24]

3. <span data-ttu-id="95082-183">Merhaba, **harici depolama ekleme** iletişim kutusunda hello **hesap adı** kutusuna hello depolama hesabı adı girin, istediğiniz diğer ayarları belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="95082-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Dış depolama ekle iletişim kutusu][8]

4. <span data-ttu-id="95082-185">Merhaba, **bağlantı Özet** iletişim kutusunda, hello bilgilerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="95082-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="95082-186">Toochange herhangi bir şey istiyorsanız seçin **geri** ve istenen hello ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="95082-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="95082-187">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="95082-187">Select **Connect**.</span></span>

6. <span data-ttu-id="95082-188">Başarıyla bağlandıktan sonra hello harici depolama hesabı ile görüntülenir **(harici)** toohello depolama hesabı adı eklenir.</span><span class="sxs-lookup"><span data-stu-id="95082-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![Sonuç tooan harici depolama hesabına bağlanma][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="95082-190">Harici bir depolama hesabı ayırma</span><span class="sxs-lookup"><span data-stu-id="95082-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="95082-191">Toodetach istediğiniz ve ardından hello harici depolama hesabına sağ **ayırma**.</span><span class="sxs-lookup"><span data-stu-id="95082-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![Depolama alanından ayırma seçeneği][10]

2. <span data-ttu-id="95082-193">Merhaba onay iletisinde seçin **Evet** tooconfirm hello ayrılmayı hello harici depolama hesabından.</span><span class="sxs-lookup"><span data-stu-id="95082-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="95082-194">SAS kullanarak depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="95082-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="95082-195">Bir [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide Azure aboneliği kimlik gerek kalmadan geçici erişim tooa depolama hesabına vermek hello Yöneticisi bir Azure aboneliğinin olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="95082-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="95082-196">tooillustrate bu senaryo, şimdi bu Kullanıcıa bir Azure aboneliği Yöneticisi deyin olduğu ve Kullanıcıa istediği tooallow UserB tooaccess sınırlı bir süre çeşitli izinlerle bir depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="95082-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="95082-197">Kullanıcıa (Merhaba bağlantı dizesi hello depolama hesabı için oluşan) bir SAS dönemi ve istenen hello izinlerle belirli bir süre oluşturur.</span><span class="sxs-lookup"><span data-stu-id="95082-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="95082-198">Kullanıcıa paylaşımları SAS erişim toohello depolama hesabı isteyen hello kişiyle (örneğimizde, UserB) hello.</span><span class="sxs-lookup"><span data-stu-id="95082-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="95082-199">Kullanıcıb kullanarak tooUserA ait Depolama Gezgini (Önizleme) tooattach toohello hesabı kullanan hello sağlanan SAS.</span><span class="sxs-lookup"><span data-stu-id="95082-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="95082-200">Tooshare istediğiniz hello hesabı için bir SAS alma</span><span class="sxs-lookup"><span data-stu-id="95082-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="95082-201">Depolama Gezgini (Önizleme), paylaşımı ve ardından istediğiniz hello depolama hesabını sağ tıklatın **paylaşılan erişim imzası Al**.</span><span class="sxs-lookup"><span data-stu-id="95082-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![SAS alma içerik menüsü seçeneği][13]

2. <span data-ttu-id="95082-203">Merhaba, **paylaşılan erişim imzası** iletişim kutusunda, hello zaman dilimi ve hello hesap için istediğiniz ve ardından izinleri belirtin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="95082-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="95082-204">![SAS alma iletişim kutusu][14]</span><span class="sxs-lookup"><span data-stu-id="95082-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="95082-205">Merhaba **paylaşılan erişim imzası** iletişim kutusu açılır ve hello SAS görüntüler.</span><span class="sxs-lookup"><span data-stu-id="95082-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="95082-206">Sonraki toohello **bağlantı dizesi**seçin **kopya** toocopy, toohello Pano ve ardından **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="95082-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="95082-207">Merhaba SAS kullanarak paylaşılan toohello hesap ekleme</span><span class="sxs-lookup"><span data-stu-id="95082-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="95082-208">Depolama Gezgini (Önizleme), seçin **tooAzure depolama birimini bağlayın**.</span><span class="sxs-lookup"><span data-stu-id="95082-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![TooAzure depolama seçeneği Bağlan][23]

2. <span data-ttu-id="95082-210">Merhaba, **tooAzure depolama bağlanmak** iletişim kutusu, hello bağlantı dizesini belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="95082-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![Bağlan tooAzure depolama iletişim kutusu][24]

3. <span data-ttu-id="95082-212">Merhaba, **bağlantı Özet** iletişim kutusunda, hello bilgilerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="95082-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="95082-213">toomake değişiklikleri seçin **geri**ve ardından istediğiniz hello ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="95082-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="95082-214">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="95082-214">Select **Connect**.</span></span>

5. <span data-ttu-id="95082-215">Bunu bağlandıktan sonra hello depolama hesabı ile görüntülenir **(SAS)** sağladığınız toohello hesap adı eklenir.</span><span class="sxs-lookup"><span data-stu-id="95082-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![SAS kullanarak hesap ekli tooan sonucu][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="95082-217">SAS kullanarak hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="95082-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="95082-218">Merhaba "bir SAS kullanarak bir depolama hesabı ekleme" bölümde, nasıl Azure abonelik yöneticisinin geçici erişim tooa depolama hesabı oluşturma ve hello depolama hesabı için bir SAS paylaşarak erişim izni verebilir açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="95082-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="95082-219">Benzer şekilde bir depolama hesabının içinde belirli bir hizmet için (blob kapsayıcısı, kuyruk veya tablo) bir SAS oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="95082-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="95082-220">Tooshare istediğiniz hello hizmeti için bir SAS oluşturmak</span><span class="sxs-lookup"><span data-stu-id="95082-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="95082-221">Bu bağlamda bir hizmet, bir blob kapsayıcısı, sıra veya tablo olabilir.</span><span class="sxs-lookup"><span data-stu-id="95082-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="95082-222">toogenerate hello SAS listelenen hizmet için bkz:</span><span class="sxs-lookup"><span data-stu-id="95082-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="95082-223">Blob kapsayıcısı için Hello SAS alma</span><span class="sxs-lookup"><span data-stu-id="95082-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="95082-224">Bir dosya paylaşımı için Hello SAS alma: *çok yakında*</span><span class="sxs-lookup"><span data-stu-id="95082-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="95082-225">Bir kuyruk için SAS Hello alın: *çok yakında*</span><span class="sxs-lookup"><span data-stu-id="95082-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="95082-226">Bir tablo için SAS Hello alın: *çok yakında*</span><span class="sxs-lookup"><span data-stu-id="95082-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="95082-227">SAS kullanarak hizmet hello paylaşılan toohello hesap ekleme</span><span class="sxs-lookup"><span data-stu-id="95082-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="95082-228">Depolama Gezgini (Önizleme), seçin **tooAzure depolama birimini bağlayın**.</span><span class="sxs-lookup"><span data-stu-id="95082-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![TooAzure depolama seçeneği Bağlan][23]

2. <span data-ttu-id="95082-230">Merhaba, **tooAzure depolama bağlanmak** iletişim kutusu, hello SAS URI'sini belirtin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="95082-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![Bağlan tooAzure depolama iletişim kutusu][24]

3. <span data-ttu-id="95082-232">Merhaba, **bağlantı Özet** iletişim kutusunda, hello bilgilerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="95082-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="95082-233">toomake değişiklikleri seçin **geri**ve ardından istediğiniz hello ayarlarını girin.</span><span class="sxs-lookup"><span data-stu-id="95082-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="95082-234">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="95082-234">Select **Connect**.</span></span>

5. <span data-ttu-id="95082-235">Bunu bağlandıktan sonra hello yeni eklenen hizmet hello altında görüntülenen **(hizmet SAS)** düğümü.</span><span class="sxs-lookup"><span data-stu-id="95082-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![Sonuç bir SAS kullanarak paylaşılan tooa hizmet ekleme][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="95082-237">Depolama hesapları arama</span><span class="sxs-lookup"><span data-stu-id="95082-237">Search for storage accounts</span></span>
<span data-ttu-id="95082-238">Depolama hesaplarının uzun bir listeniz varsa, hızlı şekilde toolocate belirli bir depolama hesabını toouse hello arama hello sol bölmenin hello üstünde kutusudur.</span><span class="sxs-lookup"><span data-stu-id="95082-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="95082-239">Hello arama kutusuna yazarken hello bölmesini toothat noktası girmiş olduğunuz hello arama değeriyle eşleşen görüntüler hello depolama hesapları kalmadı.</span><span class="sxs-lookup"><span data-stu-id="95082-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="95082-240">Örneğin, bir arama adı tüm depolama hesapları için içeren **tarcher** hello aşağıdaki ekran gösterilir:</span><span class="sxs-lookup"><span data-stu-id="95082-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![Depolama hesabı araması][11]

## <a name="next-steps"></a><span data-ttu-id="95082-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95082-242">Next steps</span></span>
* [<span data-ttu-id="95082-243">Depolama Gezgini (Önizleme) ile Azure Blob Depolama kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="95082-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
