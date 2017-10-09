---
title: "Depolama Gezgini (Önizleme) Azure File storage ile aaaUsing | Microsoft Docs"
description: "Bilgi nasıl toouse Depolama Gezgini (Önizleme) toowork dosya paylaşımları ve dosyaları nasıl öğrenin."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="4938b-103">Depolama Gezgini’ni (Önizleme) Azure Dosya Depolama ile kullanma</span><span class="sxs-lookup"><span data-stu-id="4938b-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="4938b-104">Depolama dosya sunan bir hizmet hello kullanılarak bulut paylaşır azure dosyası hello standart sunucu ileti bloğu (SMB) protokolü.</span><span class="sxs-lookup"><span data-stu-id="4938b-104">Azure File storage is a service that offers file shares in hello cloud using hello standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="4938b-105">SMB 2.1 ve SMB 3.0 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4938b-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="4938b-106">Azure File storage, dosya paylaşımları tooAzure üzerinde maliyetli yeniden yazdırmaya gerek duymadan ve hızla kullanan eski uygulamalar geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4938b-106">With Azure File storage, you can migrate legacy applications that rely on file shares tooAzure quickly and without costly rewrites.</span></span> <span data-ttu-id="4938b-107">Dosya depolama tooexpose verileri kullanabileceğiniz genel olarak toohello world veya toostore uygulama verilerini özel olarak.</span><span class="sxs-lookup"><span data-stu-id="4938b-107">You can use File storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="4938b-108">Bu makalede, nasıl toouse Depolama Gezgini (Önizleme) toowork dosya paylaşımları ve dosyaları öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="4938b-108">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4938b-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4938b-109">Prerequisites</span></span>

<span data-ttu-id="4938b-110">Bu makaledeki toocomplete hello adımları, hello aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="4938b-110">toocomplete hello steps in this article, you'll need hello following:</span></span>

- [<span data-ttu-id="4938b-111">Depolama Gezgini (önizleme) indirip yükleme</span><span class="sxs-lookup"><span data-stu-id="4938b-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="4938b-112">Tooa Azure depolama hesabı veya hizmetine bağlanmak</span><span class="sxs-lookup"><span data-stu-id="4938b-112">Connect tooa Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="4938b-113">Dosya Paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4938b-113">Create a File Share</span></span>

<span data-ttu-id="4938b-114">Tüm dosyalar, basitçe dosyaların mantıksal bir gruplandırması olan dosya paylaşımında bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4938b-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="4938b-115">Bir hesapta sınırsız sayıda dosya paylaşımı olabilir ve her paylaşım sınırsız sayıda dosya depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="4938b-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="4938b-116">Aşağıdaki adımları hello nasıl toocreate bir dosya paylaşımı Depolama Gezgini (Önizleme) içinde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4938b-116">hello following steps illustrate how toocreate a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="4938b-117">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="4938b-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="4938b-118">Merhaba sol bölmede toocreate hello dosya paylaşımı içinde istediğiniz hello depolama hesabı genişletin</span><span class="sxs-lookup"><span data-stu-id="4938b-118">In hello left pane, expand hello storage account within which you wish toocreate hello File Share</span></span>

3. <span data-ttu-id="4938b-119">Sağ **dosya paylaşımları**ve - hello bağlam menüsünden - seçin **dosya paylaşımı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="4938b-119">Right-click **File Shares**, and - from hello context menu - select **Create File Share**.</span></span>

    ![Dosya Paylaşımı Oluşturma](media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="4938b-121">Bir metin kutusu altında hello görünür **dosya paylaşımları** klasör.</span><span class="sxs-lookup"><span data-stu-id="4938b-121">A text box will appear below hello **File Shares** folder.</span></span> <span data-ttu-id="4938b-122">Dosya Paylaşımı için Hello adı girin.</span><span class="sxs-lookup"><span data-stu-id="4938b-122">Enter hello name for your file share.</span></span> <span data-ttu-id="4938b-123">Merhaba bkz [adlandırma kuralları paylaşmak](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) bölümünde bir liste için kurallar ve dosya paylaşımları adlandırma kısıtlamaları.</span><span class="sxs-lookup"><span data-stu-id="4938b-123">See hello [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Adlandırma hello paylaşımı](media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="4938b-125">Tuşuna **Enter** Bitti'yi toocreate Merhaba, dosya paylaşımı veya **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="4938b-125">Press **Enter** when done toocreate hello file share, or **Esc** toocancel.</span></span> <span data-ttu-id="4938b-126">Merhaba dosya paylaşımı başarıyla oluşturulduktan sonra uygulamanın altında hello görüntülenecek **dosya paylaşımları** klasörü hello için seçtiğiniz depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="4938b-126">Once hello file share has been successfully created, it will be displayed under hello **File Shares** folder for hello selected storage account.</span></span>

    ![Merhaba yeni paylaşım](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="4938b-128">Dosya paylaşımının içeriğini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="4938b-128">View a file share's contents</span></span>

<span data-ttu-id="4938b-129">Dosya paylaşımları, dosya ve klasörler içerir (klasörler de dosya içerebilir).</span><span class="sxs-lookup"><span data-stu-id="4938b-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="4938b-130">Merhaba aşağıdaki adımları tooview hello bir dosyanın içeriğini Depolama Gezgini (Önizleme) içinde nasıl paylaşmak gösterilmektedir: +</span><span class="sxs-lookup"><span data-stu-id="4938b-130">hello following steps illustrate how tooview hello contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="4938b-131">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="4938b-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="4938b-132">Merhaba sol bölmede, tooview istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="4938b-132">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="4938b-133">Merhaba depolama hesabının genişletin **dosya paylaşımları**.</span><span class="sxs-lookup"><span data-stu-id="4938b-133">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="4938b-134">Sağ hello dosya paylaşımı, tooview istiyor ve - hello bağlam menüsünden - seçin **açık**.</span><span class="sxs-lookup"><span data-stu-id="4938b-134">Right-click hello file share you wish tooview, and - from hello context menu - select **Open**.</span></span> <span data-ttu-id="4938b-135">Ayrıca tooview istediğiniz hello dosya paylaşımı çift tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4938b-135">You can also double-click hello file share you wish tooview.</span></span>

    ![Paylaşımı açma](media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="4938b-137">Merhaba ana bölmede hello dosya paylaşımının içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4938b-137">hello main pane will display hello file share's contents.</span></span>
    
    ![paylaşımın içeriği hello](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="4938b-139">Dosya paylaşımını silme</span><span class="sxs-lookup"><span data-stu-id="4938b-139">Delete a file share</span></span>

<span data-ttu-id="4938b-140">Dosya paylaşımları kolayca oluşturulabilir ve gerektiğinde silinebilir.</span><span class="sxs-lookup"><span data-stu-id="4938b-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="4938b-141">(toosee toodelete tek tek dosyaların başvurmak nasıl toohello bölüm [bir dosya paylaşımında dosyalar yönetme](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="4938b-141">(toosee how toodelete individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="4938b-142">Aşağıdaki adımları hello nasıl toodelete bir dosya paylaşımı Depolama Gezgini (Önizleme) içinde gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4938b-142">hello following steps illustrate how toodelete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="4938b-143">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="4938b-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="4938b-144">Merhaba sol bölmede, tooview istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="4938b-144">In hello left pane, expand hello storage account containing hello file share you wish tooview.</span></span>

3. <span data-ttu-id="4938b-145">Merhaba depolama hesabının genişletin **dosya paylaşımları**.</span><span class="sxs-lookup"><span data-stu-id="4938b-145">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="4938b-146">Sağ hello dosya paylaşımı, toodelete istiyor ve - hello bağlam menüsünden - seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="4938b-146">Right-click hello file share you wish toodelete, and - from hello context menu - select **Delete**.</span></span> <span data-ttu-id="4938b-147">Tuşlarına da basabilirsiniz **silmek** toodelete hello şu anda seçili dosya paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="4938b-147">You can also press **Delete** toodelete hello currently selected file share.</span></span>

    ![Sil](media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="4938b-149">Seçin **Evet** toohello onay iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="4938b-149">Select **Yes** toohello confirmation dialog.</span></span>
    
    ![Onay iletişim kutusu](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="4938b-151">Dosya paylaşımını kopyalama</span><span class="sxs-lookup"><span data-stu-id="4938b-151">Copy a file share</span></span>

<span data-ttu-id="4938b-152">Depolama Gezgini (Önizleme) toocopy bir dosya paylaşımı toohello Pano sağlar ve bu dosya paylaşımına başka bir depolama hesabı yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="4938b-152">Storage Explorer (Preview) enables you toocopy a file share toohello clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="4938b-153">(toosee toocopy tek tek dosyaların başvurmak nasıl toohello bölüm [bir dosya paylaşımında dosyalar yönetme](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="4938b-153">(toosee how toocopy individual files, refer toohello section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="4938b-154">Aşağıdaki adımları hello nasıl toocopy bir dosya paylaşımı bir depolama hesabı tooanother gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4938b-154">hello following steps illustrate how toocopy a file share from one storage account tooanother.</span></span>

1. <span data-ttu-id="4938b-155">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="4938b-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="4938b-156">Merhaba sol bölmede, toocopy istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="4938b-156">In hello left pane, expand hello storage account containing hello file share you wish toocopy.</span></span>

3. <span data-ttu-id="4938b-157">Merhaba depolama hesabının genişletin **dosya paylaşımları**.</span><span class="sxs-lookup"><span data-stu-id="4938b-157">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="4938b-158">Sağ hello dosya paylaşımı, toocopy istiyor ve - hello bağlam menüsünden - seçin **kopyalama dosya paylaşımı**.</span><span class="sxs-lookup"><span data-stu-id="4938b-158">Right-click hello file share you wish toocopy, and - from hello context menu - select **Copy File Share**.</span></span>

    ![Dosya Paylaşımını Kopyala](media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="4938b-160">Hangi içine, toopaste hello dosya paylaşmak istediğiniz - hello bağlam menüsünden - seçin hello istenen "hedef" depolama hesabını sağ tıklatıp **Yapıştır dosya paylaşımı**.</span><span class="sxs-lookup"><span data-stu-id="4938b-160">Right-click hello desired "target" storage account into which you want toopaste hello file share, and - from hello context menu - select **Paste File Share**.</span></span>

    ![Dosya Paylaşımını Yapıştır](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a><span data-ttu-id="4938b-162">Bir dosya paylaşımı için Hello SAS alma</span><span class="sxs-lookup"><span data-stu-id="4938b-162">Get hello SAS for a file share</span></span>

<span data-ttu-id="4938b-163">A [paylaşılan erişim imzası (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) depolama hesabınızda atanmış erişim tooresources sağlar.</span><span class="sxs-lookup"><span data-stu-id="4938b-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="4938b-164">Başka bir deyişle, bir istemci depolama hesabınızdaki izinleri tooobjects süre ve belirtilen bir izin kümesi ile belirli bir süre için hesap erişim tuşlarınızı tooshare gerek kalmadan sınırlı verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4938b-164">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span>

<span data-ttu-id="4938b-165">Merhaba aşağıdaki adımları göstermek toocreate bir dosya için bir SAS nasıl paylaşmak: +</span><span class="sxs-lookup"><span data-stu-id="4938b-165">hello following steps illustrate how toocreate a SAS for a file share:+</span></span>

1. <span data-ttu-id="4938b-166">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="4938b-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="4938b-167">Hello sol bölmesinde, SAS tooget öğrenmek isterseniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="4938b-167">In hello left pane, expand hello storage account containing hello file share for which you wish tooget a SAS.</span></span>

3. <span data-ttu-id="4938b-168">Merhaba depolama hesabının genişletin **dosya paylaşımları**.</span><span class="sxs-lookup"><span data-stu-id="4938b-168">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="4938b-169">Merhaba istenen dosya paylaşımı sağ tıklatın ve - hello bağlam menüsünden - seçin **paylaşılan erişim imzası Al**.</span><span class="sxs-lookup"><span data-stu-id="4938b-169">Right-click hello desired file share, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

    ![Paylaşılan Erişim İmzası Al](media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="4938b-171">Merhaba, **paylaşılan erişim imzası** iletişim kutusunda, hello İlkesi, başlangıç ve sona erme tarihleri, saat dilimini belirtin ve erişim düzeyleri hello kaynak için istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="4938b-171">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

    ![SAS iletişim kutusu](media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="4938b-173">Merhaba SAS seçeneklerini belirtme tamamladığınızda seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="4938b-173">When you're finished specifying hello SAS options, select **Create**.</span></span>

7. <span data-ttu-id="4938b-174">İkinci bir **paylaşılan erişim imzası** iletişim listeleri hello hello URL ile birlikte dosya paylaşımı ve tooaccess kullanabileceğiniz QueryStrings hello depolama kaynağı sonra görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="4938b-174">A second **Shared Access Signature** dialog will then display that lists hello file share along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span> <span data-ttu-id="4938b-175">Seçin **kopya** toocopy toohello Pano istediğiniz sonraki toohello URL.</span><span class="sxs-lookup"><span data-stu-id="4938b-175">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>
    
    ![İkinci SAS iletişim kutusu](media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="4938b-177">İşiniz bittiğinde **Kapat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="4938b-178">Bir dosya paylaşımı için Erişim İlkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="4938b-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="4938b-179">Merhaba aşağıdaki adımları göstermek nasıl toomanage (ekleme ve kaldırma) erişim ilkeleri bir dosya paylaşımı için: +.</span><span class="sxs-lookup"><span data-stu-id="4938b-179">hello following steps illustrate how toomanage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="4938b-180">Merhaba erişim ilkeleri, SAS üzerinden kişiler tanımlı bir süre boyunca tooaccess hello depolama dosya kaynağı kullanabilir URL'ler oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4938b-180">hello Access Policies is used for creating SAS URLs through which people can use tooaccess hello Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="4938b-181">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="4938b-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="4938b-182">Hello sol bölmede, erişim ilkeleri toomanage istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="4938b-182">In hello left pane, expand hello storage account containing hello file share whose access policies you wish toomanage.</span></span>

3. <span data-ttu-id="4938b-183">Merhaba depolama hesabının genişletin **dosya paylaşımları**.</span><span class="sxs-lookup"><span data-stu-id="4938b-183">Expand hello storage account's **File Shares**.</span></span>

4. <span data-ttu-id="4938b-184">Merhaba istenen dosya paylaşımı seçin ve - hello bağlam menüsünden - seçin **erişim ilkelerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="4938b-184">Select hello desired file share, and - from hello context menu - select **Manage Access Policies**.</span></span>

    ![Erişim ilkelerini yönet bağlam menüsü](media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="4938b-186">Merhaba **erişim ilkeleri** iletişim hello seçili dosya paylaşımı için oluşturulmuş tüm erişim ilkeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="4938b-186">hello **Access Policies** dialog will list any access policies already created for hello selected file share.</span></span>
    
    ![Erişim İlkeleri](media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="4938b-188">Merhaba erişim ilkesi yönetim görevi bağlı olarak aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4938b-188">Follow these steps depending on hello access policy management task:</span></span>
    
    - <span data-ttu-id="4938b-189">**Yeni bir erişim ilkesi ekleme** - **Ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="4938b-190">Oluşturduktan sonra hello **erişim ilkeleri** iletişim yeni eklenen hello görüntüler erişim ilkesi (varsayılan ayarlarla).</span><span class="sxs-lookup"><span data-stu-id="4938b-190">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="4938b-191">**Erişim ilkesini düzenleme** - İstediğiniz düzenlemeleri yapıp **Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="4938b-192">**Erişim ilkesini kaldırmak** - seçin **kaldırmak** tooremove istediğiniz sonraki toohello erişim ilkesi.</span><span class="sxs-lookup"><span data-stu-id="4938b-192">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

7. <span data-ttu-id="4938b-193">Merhaba daha önce oluşturduğunuz erişim ilkesi kullanarak yeni bir SAS URL'si oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4938b-193">Create a new SAS URL using hello Access Policy you created earlier:</span></span>
    
    ![SAS alma](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![SAS adı ve özellikleri](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="4938b-196">Bir dosya paylaşımındaki dosyaları yönetme</span><span class="sxs-lookup"><span data-stu-id="4938b-196">Managing files in a file share</span></span>

<span data-ttu-id="4938b-197">Bir dosya paylaşımı oluşturduktan sonra bir dosya toothat dosya paylaşımı karşıya yükleme, bir dosya tooyour yerel bilgisayarda indirin, yerel bilgisayarınıza ve daha pek çok dosya açma.</span><span class="sxs-lookup"><span data-stu-id="4938b-197">Once you've created a file share, you can upload a file toothat file share, download a file tooyour local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="4938b-198">Merhaba aşağıdaki adımları nasıl toomanage hello dosyaları (ve klasörler) içinde bir dosya paylaşımı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4938b-198">hello following steps illustrate how toomanage hello files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="4938b-199">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="4938b-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="4938b-200">Merhaba sol bölmede, toomanage istediğiniz hello dosya paylaşımı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="4938b-200">In hello left pane, expand hello storage account containing hello file share you wish toomanage.</span></span>

3.  <span data-ttu-id="4938b-201">Merhaba depolama hesabının genişletin **dosya paylaşımları**.</span><span class="sxs-lookup"><span data-stu-id="4938b-201">Expand hello storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="4938b-202">Merhaba dosya paylaşımı tooview istediğiniz çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4938b-202">Double-click hello file share you wish tooview.</span></span>

5.  <span data-ttu-id="4938b-203">Merhaba ana bölmede hello dosya paylaşımının içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4938b-203">hello main pane will display hello file share's contents.</span></span>

    ![paylaşımın içeriği hello](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="4938b-205">Merhaba ana bölmede hello dosya paylaşımının içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4938b-205">hello main pane will display hello file share's contents.</span></span>

7.  <span data-ttu-id="4938b-206">Tooperform istediğiniz Hello göreve bağlı olarak aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4938b-206">Follow these steps depending on hello task you wish tooperform:</span></span>

    - <span data-ttu-id="4938b-207">**Dosyaları tooa dosya paylaşımı karşıya yükle**</span><span class="sxs-lookup"><span data-stu-id="4938b-207">**Upload files tooa file share**</span></span>

        <span data-ttu-id="4938b-208">a.</span><span class="sxs-lookup"><span data-stu-id="4938b-208">a.</span></span>  <span data-ttu-id="4938b-209">Merhaba ana bölmede ait araç çubuğunda seçin **karşıya**ve ardından **dosya yükleme** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="4938b-209">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Dosyaları karşıya yükleme](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="4938b-211">b.</span><span class="sxs-lookup"><span data-stu-id="4938b-211">b.</span></span> <span data-ttu-id="4938b-212">Merhaba, **dosyaları karşıya yükleme** iletişim, select hello üç nokta (**...** ) düğmesini hello hello sağ tarafındaki **dosyaları** metin kutusu tooselect hello dosyaları tooupload istiyor.</span><span class="sxs-lookup"><span data-stu-id="4938b-212">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Dosya ekleme](media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="4938b-214">c.</span><span class="sxs-lookup"><span data-stu-id="4938b-214">c.</span></span> <span data-ttu-id="4938b-215">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-215">Select **Upload**.</span></span>

    - <span data-ttu-id="4938b-216">**Bir klasör tooa dosya paylaşımı karşıya yükle**</span><span class="sxs-lookup"><span data-stu-id="4938b-216">**Upload a folder tooa file share**</span></span>
        
        <span data-ttu-id="4938b-217">a.</span><span class="sxs-lookup"><span data-stu-id="4938b-217">a.</span></span> <span data-ttu-id="4938b-218">Merhaba ana bölmede ait araç çubuğunda seçin **karşıya**ve ardından **karşıya yükleme klasörü** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="4938b-218">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Klasörü karşıya yükle menüsü](media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="4938b-220">b.</span><span class="sxs-lookup"><span data-stu-id="4938b-220">b.</span></span> <span data-ttu-id="4938b-221">Merhaba, **karşıya yükleme klasörü** iletişim, select hello üç nokta (**...** ) düğmesini hello hello sağ tarafındaki **klasörü** içeriği tooupload istediğiniz metin kutusu tooselect hello klasörü.</span><span class="sxs-lookup"><span data-stu-id="4938b-221">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        <span data-ttu-id="4938b-222">c.</span><span class="sxs-lookup"><span data-stu-id="4938b-222">c.</span></span> <span data-ttu-id="4938b-223">İsteğe bağlı olarak, hangi hello seçilen klasörün içeriğini karşıya yükleneceği bir hedef klasör belirtin.</span><span class="sxs-lookup"><span data-stu-id="4938b-223">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="4938b-224">Merhaba hedef klasörü yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4938b-224">If hello target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="4938b-225">d.</span><span class="sxs-lookup"><span data-stu-id="4938b-225">d.</span></span> <span data-ttu-id="4938b-226">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-226">Select **Upload**.</span></span>

    - <span data-ttu-id="4938b-227">**Bir dosya tooyour yerel bilgisayarda indirin**</span><span class="sxs-lookup"><span data-stu-id="4938b-227">**Download a file tooyour local computer**</span></span>
        
        <span data-ttu-id="4938b-228">a.</span><span class="sxs-lookup"><span data-stu-id="4938b-228">a.</span></span> <span data-ttu-id="4938b-229">Toodownload istediğiniz hello dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-229">Select hello file you wish toodownload.</span></span>
        
        <span data-ttu-id="4938b-230">b.</span><span class="sxs-lookup"><span data-stu-id="4938b-230">b.</span></span> <span data-ttu-id="4938b-231">Merhaba ana bölmede ait araç çubuğunda seçin **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="4938b-231">On hello main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="4938b-232">c.</span><span class="sxs-lookup"><span data-stu-id="4938b-232">c.</span></span> <span data-ttu-id="4938b-233">Merhaba, **toosave hello dosyasını indirdiğiniz belirt** iletişim kutusunda, indirilen hello dosyasına hello konumu belirtin ve hello toogive istediğiniz adı.</span><span class="sxs-lookup"><span data-stu-id="4938b-233">In hello **Specify where toosave hello downloaded file** dialog, specify hello location where you want hello file downloaded, and hello name you wish toogive it.</span></span>

        <span data-ttu-id="4938b-234">d.</span><span class="sxs-lookup"><span data-stu-id="4938b-234">d.</span></span> <span data-ttu-id="4938b-235">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-235">Select **Save**.</span></span>

    - <span data-ttu-id="4938b-236">**Bir dosyayı yerel bilgisayarınızda açma**</span><span class="sxs-lookup"><span data-stu-id="4938b-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="4938b-237">a.</span><span class="sxs-lookup"><span data-stu-id="4938b-237">a.</span></span>  <span data-ttu-id="4938b-238">Tooopen istediğiniz hello dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-238">Select hello file you wish tooopen.</span></span>
        
        <span data-ttu-id="4938b-239">b.</span><span class="sxs-lookup"><span data-stu-id="4938b-239">b.</span></span>  <span data-ttu-id="4938b-240">Merhaba ana bölmede ait araç çubuğunda seçin **açık**.</span><span class="sxs-lookup"><span data-stu-id="4938b-240">On hello main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="4938b-241">c.</span><span class="sxs-lookup"><span data-stu-id="4938b-241">c.</span></span>  <span data-ttu-id="4938b-242">Merhaba dosyası indirilir ve hello dosyanın temel alınan dosya türü ile ilişkili hello uygulama kullanılarak açılır.</span><span class="sxs-lookup"><span data-stu-id="4938b-242">hello file will be downloaded and opened using hello application associated with hello file's underlying file type.</span></span>

    - <span data-ttu-id="4938b-243">**Bir dosya toohello Panoya Kopyala**</span><span class="sxs-lookup"><span data-stu-id="4938b-243">**Copy a file toohello clipboard**</span></span>

        <span data-ttu-id="4938b-244">a.</span><span class="sxs-lookup"><span data-stu-id="4938b-244">a.</span></span> <span data-ttu-id="4938b-245">Toocopy istediğiniz hello dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-245">Select hello file you wish toocopy.</span></span>

        <span data-ttu-id="4938b-246">b.</span><span class="sxs-lookup"><span data-stu-id="4938b-246">b.</span></span> <span data-ttu-id="4938b-247">Merhaba ana bölmede ait araç çubuğunda seçin **kopya**.</span><span class="sxs-lookup"><span data-stu-id="4938b-247">On hello main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="4938b-248">c.</span><span class="sxs-lookup"><span data-stu-id="4938b-248">c.</span></span> <span data-ttu-id="4938b-249">Hello sol bölmede tooanother dosya paylaşımına gidin ve çift tooview hello ana bölmede içinde.</span><span class="sxs-lookup"><span data-stu-id="4938b-249">In hello left pane, navigate tooanother file share, and double-click it tooview it in hello main pane.</span></span>

        <span data-ttu-id="4938b-250">d.</span><span class="sxs-lookup"><span data-stu-id="4938b-250">d.</span></span> <span data-ttu-id="4938b-251">Merhaba ana bölmede ait araç çubuğunda seçin **Yapıştır** toocreate hello dosyasının bir kopyası.</span><span class="sxs-lookup"><span data-stu-id="4938b-251">On hello main pane's toolbar, select **Paste** toocreate a copy of hello file.</span></span>

    - <span data-ttu-id="4938b-252">**Dosyayı silme**</span><span class="sxs-lookup"><span data-stu-id="4938b-252">**Delete a file**</span></span>

        <span data-ttu-id="4938b-253">a.</span><span class="sxs-lookup"><span data-stu-id="4938b-253">a.</span></span> <span data-ttu-id="4938b-254">Toodelete istediğiniz hello dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="4938b-254">Select hello file you wish toodelete.</span></span>

        <span data-ttu-id="4938b-255">b.</span><span class="sxs-lookup"><span data-stu-id="4938b-255">b.</span></span> <span data-ttu-id="4938b-256">Merhaba ana bölmede ait araç çubuğunda seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="4938b-256">On hello main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="4938b-257">c.</span><span class="sxs-lookup"><span data-stu-id="4938b-257">c.</span></span> <span data-ttu-id="4938b-258">Seçin **Evet** toohello onay iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="4938b-258">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4938b-259">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4938b-259">Next steps</span></span>

- <span data-ttu-id="4938b-260">Görünüm hello [en son Depolama Gezgini (Önizleme) sürüm notları ve videolar](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="4938b-260">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="4938b-261">Nasıl çok öğrenin[Azure BLOB'ları, tabloları, kuyrukları ve dosyaları kullanan uygulamalar oluşturmak](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="4938b-261">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>
