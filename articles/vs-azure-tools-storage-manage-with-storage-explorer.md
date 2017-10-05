---
title: "Depolama Gezgini (Önizleme) ile çalışmaya başlama | Microsoft Docs"
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
ms.openlocfilehash: 1794a86a4185d587cf184a1f61a5720e2ab65e92
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="b1965-103">Depolama Gezgini (Önizleme) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b1965-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="b1965-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b1965-104">Overview</span></span>
<span data-ttu-id="b1965-105">Azure Depolama Gezgini (Önizleme) Windows, macOS ve Linux’ta Azure Depolama ile kolayca çalışmanızı sağlayan bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="b1965-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="b1965-106">Bu makalede Azure Depolama hesaplarınızı bağlama ve yönetme ile ilgili çeşitli yöntemler öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1965-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span></span>

![Microsoft Azure Depolama Gezgini (Önizleme)][15]

## <a name="prerequisites"></a><span data-ttu-id="b1965-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b1965-108">Prerequisites</span></span>
* [<span data-ttu-id="b1965-109">Depolama Gezgini (Önizleme) indirip yükleme</span><span class="sxs-lookup"><span data-stu-id="b1965-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a><span data-ttu-id="b1965-110">Bir depolama hesabı veya hizmetine bağlanmak</span><span class="sxs-lookup"><span data-stu-id="b1965-110">Connect to a storage account or service</span></span>
<span data-ttu-id="b1965-111">Depolama Gezgini (Önizleme) depolama hesaplarına bağlamak için birçok yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1965-111">Storage Explorer (Preview) provides several ways to connect to storage accounts.</span></span> <span data-ttu-id="b1965-112">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b1965-112">For example, you can:</span></span>
* <span data-ttu-id="b1965-113">Azure aboneliğinizle ilişkili depolama hesaplarına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b1965-113">Connect to storage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="b1965-114">Diğer Azure aboneliklerinden paylaşılan depolama hesaplarına ve hizmetlere bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b1965-114">Connect to storage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="b1965-115">Azure Depolama Öykünücüsü kullanarak yerel depolama alanınıza bağlanın ve yönetin.</span><span class="sxs-lookup"><span data-stu-id="b1965-115">Connect to and manage local storage by using the Azure Storage Emulator.</span></span> 

<span data-ttu-id="b1965-116">Ayrıca global ve ulusal Azure'daki depolama hesaplarıyla çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b1965-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="b1965-117">[Bir Azure aboneliğine bağlanma](#connect-to-an-azure-subscription): Azure aboneliğinize ait depolama kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="b1965-117">[Connect to an Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong to your Azure subscription.</span></span>
* <span data-ttu-id="b1965-118">[Yerel geliştirme deposu ile çalışma](#work-with-local-development-storage): Azure Depolama Öykünücüsü kullanarak yerel depolamayı yönetin.</span><span class="sxs-lookup"><span data-stu-id="b1965-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using the Azure Storage Emulator.</span></span>
* <span data-ttu-id="b1965-119">[Dış depolama birimine ekleme](#attach-or-detach-an-external-storage-account): Depolama hesabının adını, anahtarını ve uç noktalarını kullanarak başka bir Azure aboneliğine ait olan veya ulusal Azure bulutlarında bulunan depolama kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="b1965-119">[Attach to external storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="b1965-120">[SAS kullanarak depolama hesabı ekleme](#attach-storage-account-using-sas): Paylaşılan erişim imzası (SAS) kullanarak başka bir Azure aboneliğine ait olan depolama kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="b1965-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="b1965-121">[SAS kullanarak hizmet ekleme](#attach-service-using-sas): SAS kullanarak başka bir Azure aboneliğine ait belirli bir depolama hizmetini (blob kapsayıcısı, kuyruk veya tablo) yönetin.</span><span class="sxs-lookup"><span data-stu-id="b1965-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs to another Azure subscription by using an SAS.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="b1965-122">Bir Azure aboneliğine Bağlanma</span><span class="sxs-lookup"><span data-stu-id="b1965-122">Connect to an Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="b1965-123">Bir Azure hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="b1965-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="b1965-124">Storage Explorer’da (Önizleme) **Azure Hesap ayarları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Azure hesap ayarları][0]

2. <span data-ttu-id="b1965-126">Sol bölmede oturum açtığınız tüm Microsoft hesapları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b1965-126">The left pane displays all the Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="b1965-127">Başka bir hesaba bağlanmak için **Hesap ekle**’yi seçin ve en az bir etkin Azure aboneliği ile ilişkilendirilen bir Microsoft hesabı ile oturum açmak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="b1965-127">To connect to another account, select **Add an account**, and then follow the instructions to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b1965-128">Ulusal Azure (oturum açarak Azure Almanya, Azure Kamu ve Azure China gibi) bulutları ile bağlantı şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="b1965-128">Connecting to national Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="b1965-129">Ulusal Azure depolama hesaplarına nasıl bağlanacağınızı öğrenmek için “Harici bir depolama hesabı ekleme veya ayırma” bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b1965-129">See the "Attach or detach an external storage account" section for how to connect to national Azure storage accounts.</span></span>

3. <span data-ttu-id="b1965-130">Bir Microsoft hesabı ile başarıyla oturum açtıktan sonra sol bölme ilgili hesapla ilişkili Azure abonelikleriyle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="b1965-130">After you successfully sign in with a Microsoft account, the left pane is populated with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="b1965-131">Birlikte çalışmak istediğiniz Azure aboneliklerini seçin ve ardından **Uygula**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-131">Select the Azure subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="b1965-132">(**Tüm abonelikler**’in seçilmesi listelenen Azure aboneliklerinin tamamının seçilmesini veya hiçbirinin seçilmemesini sağlar.)</span><span class="sxs-lookup"><span data-stu-id="b1965-132">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span></span>

    ![Azure aboneliklerini seçme][3]  
    <span data-ttu-id="b1965-134">Sol bölmede seçili Azure abonelikleriyle ilişkili depolama hesapları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b1965-134">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>

    ![Seçili Azure abonelikleri][4]

## <a name="connect-to-an-azure-stack-subscription"></a><span data-ttu-id="b1965-136">Bir Azure Stack aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="b1965-136">Connect to an Azure Stack subscription</span></span>

<span data-ttu-id="b1965-137">Azure Stack aboneliğine bağlanma hakkında bilgi için bkz. [Depolama Gezgini’ni Azure Stack aboneliğine bağlama](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="b1965-137">For information about connecting to an Azure Stack subscription, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="b1965-138">Yerel geliştirme deposu ile çalışma</span><span class="sxs-lookup"><span data-stu-id="b1965-138">Work with local development storage</span></span>
<span data-ttu-id="b1965-139">Depolama Gezgini (Önizleme) ile Azure Depolama Öykünücüsü kullanarak yerel depolamaya karşı çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1965-139">With Storage Explorer (Preview), you can work against local storage by using the Azure Storage Emulator.</span></span> <span data-ttu-id="b1965-140">Bu yaklaşım, (depolama hesabı Azure Depolama Öykünücüsü tarafından öykündüğü için) depolama hesabını Azure’a dağıtmadan hesaba karşı kod yazıp test edebilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1965-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because the storage account is being emulated by the Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="b1965-141">Azure Storage Öykünücüsü şu anda yalnızca Windows için desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="b1965-141">The Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="b1965-142">Depolama Gezgini (Önizleme) sol bölmesinde **(Yerel ve Bağlı)** > **Depolama Hesapları** > **(Geliştirme)** düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="b1965-142">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Yerel geliştirme düğümü][21]

2. <span data-ttu-id="b1965-144">Azure Depolama Öykünücüsünü henüz yüklemediyseniz, bir bilgi çubuğu ile yüklemeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="b1965-144">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span></span> <span data-ttu-id="b1965-145">Bilgi çubuğu görüntülendiyse **En yeni sürümü indir**’i seçin ve öykünücüyü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b1965-145">If the infobar is displayed, select **Download the latest version**, and then install the emulator.</span></span>

    ![Azure Storage Öykünücüsünü İndirme istemi][22]

3. <span data-ttu-id="b1965-147">Öykünücü yüklendikten sonra yerel bloblar, kuyruklar ve tablolar oluşturup bunlarla çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1965-147">After the emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="b1965-148">Her depolama hesabı türü ile çalışma hakkında bilgi almak için aşağıdaki bağlantılardan birine bakın:</span><span class="sxs-lookup"><span data-stu-id="b1965-148">To learn how to work with each storage account type, see one of the following:</span></span>

    * [<span data-ttu-id="b1965-149">Azure blob depolama kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b1965-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="b1965-150">Azure dosya paylaşımı depolama kaynaklarını yönetme: *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="b1965-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="b1965-151">Azure kuyruk depolama kaynaklarını yönetme: *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="b1965-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="b1965-152">Azure Tablo Depolama kaynaklarını yönetme - *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="b1965-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="b1965-153">Harici bir depolama hesabı ekleme veya ayırma</span><span class="sxs-lookup"><span data-stu-id="b1965-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="b1965-154">Depolama Gezgini (Önizleme) ile depolama hesaplarının kolayca paylaşılabilmesi için dış depolama hesaplarına ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1965-154">With Storage Explorer (Preview), you can attach to external storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="b1965-155">Bu bölümde harici depolama hesaplarının nasıl ekleneceği (ve ayrılacağı) açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1965-155">This section explains how to attach to (and detach from) external storage accounts.</span></span>

### <a name="get-the-storage-account-credentials"></a><span data-ttu-id="b1965-156">Depolama hesabının kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="b1965-156">Get the storage account credentials</span></span>
<span data-ttu-id="b1965-157">Harici bir depolama hesabını paylaşmak için ilgili hesabın sahibi ilk olarak hesabın kimlik bilgilerini (hesap adı ve anahtarı) almalıdır, ardından bu bilgileri ilgili (harici) hesabı eklemek isteyen kişiyle paylaşmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b1965-157">To share an external storage account, the owner of that account must first get the credentials (account name and key) for the account and then share that information with the person who wants to attach to that (external) account.</span></span> <span data-ttu-id="b1965-158">Depolama hesabı kimlik bilgilerini aşağıdaki adımları izleyerek Azure portalından alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b1965-158">You can obtain the storage account credentials via the Azure portal by doing the following:</span></span>

1. <span data-ttu-id="b1965-159">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b1965-159">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="b1965-160">**Gözat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-160">Select **Browse**.</span></span>

3. <span data-ttu-id="b1965-161">**Depolama Hesapları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="b1965-162">**Depolama Hesapları** dikey penceresinde istenen depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-162">On the **Storage Accounts** blade, select the desired storage account.</span></span>

5. <span data-ttu-id="b1965-163">Seçili depolama hesabının **Ayarlar** dikey penceresinde **Erişim anahtarları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-163">On the **Settings** blade for the selected storage account, select **Access keys**.</span></span>

    ![Erişim Anahtarları seçeneği][5]

6. <span data-ttu-id="b1965-165">**Erişim anahtarları** dikey penceresinde depolama hesabını eklerken kullanılacak **Depolama hesabı adı** ve **key1** değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b1965-165">On the **Access keys** blade, copy the **Storage account name** and **key1** values for use when attaching to the storage account.</span></span>

    ![Erişim tuşları][6]

### <a name="attach-to-an-external-storage-account"></a><span data-ttu-id="b1965-167">Harici bir depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="b1965-167">Attach to an external storage account</span></span>
<span data-ttu-id="b1965-168">Bir dış depolama hesabına bağlanmak için hesabın adı ve anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b1965-168">To attach to an external storage account, you need the account's name and key.</span></span> <span data-ttu-id="b1965-169">“Depolama hesabı kimlik bilgilerini alma” bölümünde bu değerlerin Azure portalından nasıl alınacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1965-169">The "Get the storage account credentials" section explains how to obtain these values from the Azure portal.</span></span> <span data-ttu-id="b1965-170">Ancak, portalda hesap anahtarı **key1** olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="b1965-170">However, in the portal, the account key is called **key1**.</span></span> <span data-ttu-id="b1965-171">Bu nedenle, Depolama Gezgini (Önizleme) bir hesap anahtarı istediğinde **key1** değerini girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b1965-171">So where Storage Explorer (Preview) asks for an account key, you enter the **key1** value.</span></span>

1. <span data-ttu-id="b1965-172">Storage Explorer’da (Önizleme) **Azure Storage’a bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-172">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Azure Storage’a bağlanma seçeneği][23]

2. <span data-ttu-id="b1965-174">**Azure Depolama’ya Bağlan** iletişim kutusunda hesap anahtarını (Azure portalındaki **key1** değeri) belirtin ve ardından **İleri**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-174">In the **Connect to Azure Storage** dialog box, specify the account key (the **key1** value from the Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b1965-175">Depolama bağlantı dizesini, ulusal Azure bulutu üzerindeki bir depolama hesabından girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1965-175">You can enter the storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="b1965-176">Örneğin, Azure Almanya depolama hesaplarına bağlamak için aşağıdakine benzer bağlantı dizeleri girin:</span><span class="sxs-lookup"><span data-stu-id="b1965-176">For example, to connect to Azure Germany storage accounts, enter connection strings similar to the following:</span></span> 
    >
    >* <span data-ttu-id="b1965-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="b1965-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="b1965-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="b1965-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="b1965-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="b1965-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="b1965-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="b1965-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="b1965-181">Bağlantı dizesini Azure portalından "Depolama hesabı kimlik bilgilerini alma" bölümünde açıklandığı gibi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1965-181">You can get the connection string from the Azure portal in the same way as described in the "Get the storage account credentials" section.</span></span>

    ![Azure depolamaya bağlan iletişim kutusu][24]

3. <span data-ttu-id="b1965-183">**Dış Depolama Ekle** iletişim kutusundaki **Hesap adı** kutusuna depolama hesabının adını girin, istediğiniz diğer ayarları belirtin ve ardından **İleri**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-183">In the **Attach External Storage** dialog box, in the **Account name** box, enter the storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Dış depolama ekle iletişim kutusu][8]

4. <span data-ttu-id="b1965-185">**Bağlantı Özeti** iletişim kutusundaki bilgileri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b1965-185">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="b1965-186">Herhangi bir ayarı değiştirmek isterseniz **Geri**’yi seçin ve istenilen ayarları yeniden girin.</span><span class="sxs-lookup"><span data-stu-id="b1965-186">If you want to change anything, select **Back** and reenter the desired settings.</span></span> 

5. <span data-ttu-id="b1965-187">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-187">Select **Connect**.</span></span>

6. <span data-ttu-id="b1965-188">Başarıyla bağlandıktan sonra dış depolama hesabı, depolama hesabı adına **(External)** metni eklenmiş olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b1965-188">After it is successfully connected, the external storage account is displayed with **(External)** appended to the storage account name.</span></span>

    ![Harici depolama hesabına bağlanma sonucu][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="b1965-190">Harici bir depolama hesabı ayırma</span><span class="sxs-lookup"><span data-stu-id="b1965-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="b1965-191">Ayırmak istediğiniz dış depolama hesabına sağ tıklayın ve **Ayır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-191">Right-click the external storage account that you want to detach, and then select **Detach**.</span></span>

    ![Depolama alanından ayırma seçeneği][10]

2. <span data-ttu-id="b1965-193">Onay iletisinde, dış depolama hesabından ayırmayı onaylamak üzere **Evet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-193">In the confirmation message, select **Yes** to confirm the detachment from the external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="b1965-194">SAS kullanarak depolama hesabı ekleme</span><span class="sxs-lookup"><span data-stu-id="b1965-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="b1965-195">[SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) bir Azure aboneliği yöneticisinin Azure aboneliği kimlik bilgilerini vermek zorunda kalmadan bir depolama hesabına geçici erişim izni vermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b1965-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets the admin of an Azure subscription grant temporary access to a storage account without having to provide Azure subscription credentials.</span></span>

<span data-ttu-id="b1965-196">Bu senaryoyu göstermek üzere; KullanıcıA’nın bir Azure aboneliği yöneticisi olduğunu düşünelim ve KullanıcıA KullanıcıB’nin belirli bir süre çeşitli izinlerle bir depolama hesabına erişmesine izin vermek istediğini varsayalım:</span><span class="sxs-lookup"><span data-stu-id="b1965-196">To illustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="b1965-197">KullanıcıA belirli bir zaman dilimi ve istenilen izinlerle (depolama hesabı için bağlantı dizesinden oluşan) bir SAS oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="b1965-197">UserA generates an SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span></span>

2. <span data-ttu-id="b1965-198">KullanıcıA SAS’ı depolama hesabına erişmek isteyen kişiyle (bu örnekte KullanıcıB) paylaşıyor.</span><span class="sxs-lookup"><span data-stu-id="b1965-198">UserA shares the SAS with the person (UserB, in our example) who wants access to the storage account.</span></span>  

3. <span data-ttu-id="b1965-199">KullanıcıB, sağlanan SAS’ı kullanarak KullanıcıA’ya ait hesabı eklemek için Depolama Gezgini’ni (Önizleme) kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1965-199">UserB uses Storage Explorer (Preview) to attach to the account that belongs to UserA by using the supplied SAS.</span></span>

### <a name="get-an-sas-for-the-account-you-want-to-share"></a><span data-ttu-id="b1965-200">Paylaşmak istediğiniz hesap için bir SAS alma</span><span class="sxs-lookup"><span data-stu-id="b1965-200">Get an SAS for the account you want to share</span></span>
1. <span data-ttu-id="b1965-201">Depolama Gezgini’nde (Önizleme) bağlam menüsünden paylaşmak istediğiniz depolama hesabına sağ tıklayın ve **Paylaşılan Erişim İmzası Al**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-201">In Storage Explorer (Preview), right-click the storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![SAS alma içerik menüsü seçeneği][13]

2. <span data-ttu-id="b1965-203">**Paylaşılan Erişim İmzası** iletişim kutusunda hesap için istediğiniz zaman dilimi ve izinleri belirleyin, ardından **Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-203">In the **Shared Access Signature** dialog box, specify the time frame and permissions that you want for the account, and then select **Create**.</span></span>

    <span data-ttu-id="b1965-204">![SAS alma iletişim kutusu][14]</span><span class="sxs-lookup"><span data-stu-id="b1965-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="b1965-205">**Paylaşılan Erişim İmzası** iletişim kutusu açılır ve SAS gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b1965-205">The **Shared Access Signature** dialog box opens and displays the SAS.</span></span>

3. <span data-ttu-id="b1965-206">**Bağlantı Dizesi**’nin yanındaki **Kopyala**’yı seçerek panoya kopyalayın ve **Kapat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-206">Next to the **Connection String**, select **Copy** to copy it to the clipboard, and then select **Close**.</span></span>

### <a name="attach-to-the-shared-account-by-using-the-sas"></a><span data-ttu-id="b1965-207">SAS kullanarak paylaşılan hesaba ekleme</span><span class="sxs-lookup"><span data-stu-id="b1965-207">Attach to the shared account by using the SAS</span></span>
1. <span data-ttu-id="b1965-208">Storage Explorer’da (Önizleme) **Azure Storage’a bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-208">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Azure Storage’a bağlanma seçeneği][23]

2. <span data-ttu-id="b1965-210">**Azure Depolamaya Bağlan** iletişim kutusunda bağlantı dizesini belirtin ve ardından **İleri**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-210">In the **Connect to Azure Storage** dialog box, specify the connection string, and then select **Next**.</span></span>

    ![Azure depolamaya bağlan iletişim kutusu][24]

3. <span data-ttu-id="b1965-212">**Bağlantı Özeti** iletişim kutusundaki bilgileri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b1965-212">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="b1965-213">Değişiklik yapmak için **Geri**’yi seçin ve istediğiniz ayarları girin.</span><span class="sxs-lookup"><span data-stu-id="b1965-213">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="b1965-214">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-214">Select **Connect**.</span></span>

5. <span data-ttu-id="b1965-215">Eklendikten sonra, depolama hesabı sağladığınız hesap adının sonuna **(SAS)** metni eklenmiş olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b1965-215">After it is attached, the storage account is displayed with **(SAS)** appended to the account name that you supplied.</span></span>

    ![SAS kullanarak hesaba ekleme sonucu][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="b1965-217">SAS kullanarak hizmet ekleme</span><span class="sxs-lookup"><span data-stu-id="b1965-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="b1965-218">“SAS kullanarak depolama hesabı ekleme” bölümünde Azure abonelik yöneticisinin depolama hesabı için bir SAS oluşturup paylaşarak nasıl geçici erişim izni verebileceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1965-218">The "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access to a storage account by generating and sharing an SAS for the storage account.</span></span> <span data-ttu-id="b1965-219">Benzer şekilde bir depolama hesabının içinde belirli bir hizmet için (blob kapsayıcısı, kuyruk veya tablo) bir SAS oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="b1965-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-the-service-that-you-want-to-share"></a><span data-ttu-id="b1965-220">Paylaşmak istediğiniz hizmet için SAS oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1965-220">Generate an SAS for the service that you want to share</span></span>
<span data-ttu-id="b1965-221">Bu bağlamda bir hizmet, bir blob kapsayıcısı, sıra veya tablo olabilir.</span><span class="sxs-lookup"><span data-stu-id="b1965-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="b1965-222">Listelenen bir hizmet için SAS oluşturmak istiyorsanız bkz.:</span><span class="sxs-lookup"><span data-stu-id="b1965-222">To generate the SAS for a listed service, see:</span></span>

* [<span data-ttu-id="b1965-223">Blob kapsayıcısı için SAS alma</span><span class="sxs-lookup"><span data-stu-id="b1965-223">Get the SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="b1965-224">Dosya paylaşımı için SAS alma: *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="b1965-224">Get the SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="b1965-225">Bir kuyruk için SAS alma: *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="b1965-225">Get the SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="b1965-226">Bir tablo için SAS alma: *Çok yakında*</span><span class="sxs-lookup"><span data-stu-id="b1965-226">Get the SAS for a table: *Coming soon*</span></span>

### <a name="attach-to-the-shared-account-service-by-using-the-sas"></a><span data-ttu-id="b1965-227">SAS kullanarak paylaşılan hesap hizmetine ekleme</span><span class="sxs-lookup"><span data-stu-id="b1965-227">Attach to the shared account service by using the SAS</span></span>
1. <span data-ttu-id="b1965-228">Storage Explorer’da (Önizleme) **Azure Storage’a bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-228">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Azure Storage’a bağlanma seçeneği][23]

2. <span data-ttu-id="b1965-230">**Azure Storage’a Bağlan** iletişim kutusunda SAS URI’sini belirtin ve ardından **İleri**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-230">In the **Connect to Azure Storage** dialog box, specify the SAS URI, and then select **Next**.</span></span>

    ![Azure depolamaya bağlan iletişim kutusu][24]

3. <span data-ttu-id="b1965-232">**Bağlantı Özeti** iletişim kutusundaki bilgileri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b1965-232">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="b1965-233">Değişiklik yapmak için **Geri**’yi seçin ve istediğiniz ayarları girin.</span><span class="sxs-lookup"><span data-stu-id="b1965-233">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="b1965-234">**Bağlan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b1965-234">Select **Connect**.</span></span>

5. <span data-ttu-id="b1965-235">Eklendikten sonra yeni eklenen hizmet **(Hizmet SAS’ı)** düğümü altında görüntülenecektir.</span><span class="sxs-lookup"><span data-stu-id="b1965-235">After it is attached, the newly attached service is displayed under the **(Service SAS)** node.</span></span>

    ![SAS kullanarak paylaşılan hizmete ekleme sonucu][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="b1965-237">Depolama hesapları arama</span><span class="sxs-lookup"><span data-stu-id="b1965-237">Search for storage accounts</span></span>
<span data-ttu-id="b1965-238">Depolama hesaplarından oluşan uzun bir listeniz varsa, sol bölmenin üzerindeki arama kutusunu kullanmak belirli bir depolama hesabını bulmak için hızlı bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="b1965-238">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span></span>

<span data-ttu-id="b1965-239">Arama kutusuna yazarken sol bölmede o noktaya kadar girdiğiniz arama değeriyle eşleşen depolama hesapları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b1965-239">As you type in the search box, the left pane displays the storage accounts that match the search value you've entered up to that point.</span></span> <span data-ttu-id="b1965-240">Örneğin, adında **tarcher** bulunan tüm depolama hesapları için yapılan bir arama aşağıdaki ekran görüntüsünde gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b1965-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in the following screenshot:</span></span>

![Depolama hesabı araması][11]

## <a name="next-steps"></a><span data-ttu-id="b1965-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1965-242">Next steps</span></span>
* [<span data-ttu-id="b1965-243">Depolama Gezgini (Önizleme) ile Azure Blob Depolama kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b1965-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

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
