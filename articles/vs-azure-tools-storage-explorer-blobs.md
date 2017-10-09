---
title: "Depolama Gezgini (Önizleme) ile aaaManage Azure Blob Storage kaynaklarını | Microsoft Docs"
description: "Azure Blob kapsayıcılar ve Bloblar Depolama Gezgini (Önizleme) ile yönetme"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="a1a1a-103">Depolama Gezgini (Önizleme) ile Azure Blob Storage kaynaklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="a1a1a-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="a1a1a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a1a1a-104">Overview</span></span>
<span data-ttu-id="a1a1a-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) büyük miktarda gelen herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış veriyi depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-105">[Azure Blob Storage](storage/blobs/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span>
<span data-ttu-id="a1a1a-106">Blob Depolama tooexpose verileri kullanabileceğiniz genel olarak toohello world veya toostore uygulama verilerini özel olarak.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-106">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span> <span data-ttu-id="a1a1a-107">Bu makalede, bilgi edineceksiniz nasıl toouse Depolama Gezgini (Önizleme) toowork blob kapsayıcılar ve bloblar ile.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-107">In this article, you'll learn how toouse Storage Explorer (Preview) toowork with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1a1a-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a1a1a-108">Prerequisites</span></span>
<span data-ttu-id="a1a1a-109">Bu makaledeki toocomplete hello adımları, hello aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="a1a1a-109">toocomplete hello steps in this article, you'll need hello following:</span></span>

* [<span data-ttu-id="a1a1a-110">Depolama Gezgini (önizleme) indirip yükleme</span><span class="sxs-lookup"><span data-stu-id="a1a1a-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="a1a1a-111">Tooa Azure depolama hesabı veya hizmetine bağlanmak</span><span class="sxs-lookup"><span data-stu-id="a1a1a-111">Connect tooa Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="a1a1a-112">Bir blob kapsayıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="a1a1a-112">Create a blob container</span></span>
<span data-ttu-id="a1a1a-113">Tüm BLOB'lar BLOB'ları yalnızca mantıksal bir gruplandırması olan bir blob kapsayıcısında bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="a1a1a-114">Bir hesapta sınırsız sayıda kapsayıcı olabilir ve her kapsayıcı sınırsız sayıda BLOB depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="a1a1a-115">Merhaba aşağıdaki adımları göstermek nasıl toocreate bir blob kapsayıcısına Depolama Gezgini (Önizleme).</span><span class="sxs-lookup"><span data-stu-id="a1a1a-115">hello following steps illustrate how toocreate a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="a1a1a-116">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="a1a1a-117">Merhaba sol bölmede toocreate hello blob kapsayıcısı içinde istediğiniz hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-117">In hello left pane, expand hello storage account within which you wish toocreate hello blob container.</span></span>
3. <span data-ttu-id="a1a1a-118">Sağ **Blob kapsayıcıları**ve - hello bağlam menüsünden - seçin **Blob kapsayıcısı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-118">Right-click **Blob Containers**, and - from hello context menu - select **Create Blob Container**.</span></span>

   ![BLOB kapsayıcıları bağlam menüsü oluşturma][0]
4. <span data-ttu-id="a1a1a-120">Bir metin kutusu altında hello görünür **Blob kapsayıcıları** klasör.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-120">A text box will appear below hello **Blob Containers** folder.</span></span> <span data-ttu-id="a1a1a-121">Blob kapsayıcısı için Hello ad girin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-121">Enter hello name for your blob container.</span></span> <span data-ttu-id="a1a1a-122">Merhaba bkz [kapsayıcı adlandırma kurallarını](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) bölümünde bir liste için kurallar ve blob kapsayıcı adlandırma kısıtlamaları.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-122">See hello [Container naming rules](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![BLOB kapsayıcıları metin kutusu oluşturma][1]
5. <span data-ttu-id="a1a1a-124">Tuşuna **Enter** toocreate hello blob kapsayıcısı, tamamlandığında veya **Esc** toocancel.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-124">Press **Enter** when done toocreate hello blob container, or **Esc** toocancel.</span></span> <span data-ttu-id="a1a1a-125">Merhaba blob kapsayıcısı başarıyla oluşturulduktan sonra uygulamanın altında hello görüntülenecek **Blob kapsayıcıları** klasörü hello için seçtiğiniz depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-125">Once hello blob container has been successfully created, it will be displayed under hello **Blob Containers** folder for hello selected storage account.</span></span>

   ![Blob kapsayıcısı oluşturuldu][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="a1a1a-127">Bir blob kapsayıcının içeriğini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a1a1a-127">View a blob container's contents</span></span>
<span data-ttu-id="a1a1a-128">BLOB kapsayıcıları, blobları ve (Ayrıca BLOB içerebilir) klasörleri içerir.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="a1a1a-129">Merhaba aşağıdaki adımları göstermek nasıl Depolama Gezgini (Önizleme) bir blob kapsayıcısına tooview Merhaba içeriğine:</span><span class="sxs-lookup"><span data-stu-id="a1a1a-129">hello following steps illustrate how tooview hello contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="a1a1a-130">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="a1a1a-131">Merhaba sol bölmede, tooview istediğiniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-131">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="a1a1a-132">Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-132">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="a1a1a-133">Sağ hello blob kapsayıcısı, tooview istiyor ve - hello bağlam menüsünden - seçin **açık Blob kapsayıcı Düzenleyicisi**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-133">Right-click hello blob container you wish tooview, and - from hello context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="a1a1a-134">Ayrıca tooview istediğiniz hello blob kapsayıcısı çift tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-134">You can also double-click hello blob container you wish tooview.</span></span>

   ![Açık blob kapsayıcı Düzenleyicisi bağlam menüsü][19]
5. <span data-ttu-id="a1a1a-136">Merhaba ana bölmede hello blob kapsayıcısının içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-136">hello main pane will display hello blob container's contents.</span></span>

   ![BLOB kapsayıcı Düzenleyicisi][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="a1a1a-138">Bir blob kapsayıcısından silin</span><span class="sxs-lookup"><span data-stu-id="a1a1a-138">Delete a blob container</span></span>
<span data-ttu-id="a1a1a-139">BLOB kapsayıcıları kolayca oluşturulur ve gerektiğinde silinir.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="a1a1a-140">(nasıl toodelete tek BLOB, toosee toohello bölümüne başvurun [blob kapsayıcısı içinde BLOB'ları yönetme](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="a1a1a-140">(toosee how toodelete individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="a1a1a-141">Merhaba aşağıdaki adımları göstermek nasıl toodelete bir blob kapsayıcısına Depolama Gezgini (Önizleme):</span><span class="sxs-lookup"><span data-stu-id="a1a1a-141">hello following steps illustrate how toodelete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="a1a1a-142">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="a1a1a-143">Merhaba sol bölmede, tooview istediğiniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-143">In hello left pane, expand hello storage account containing hello blob container you wish tooview.</span></span>
3. <span data-ttu-id="a1a1a-144">Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-144">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="a1a1a-145">Sağ hello blob kapsayıcısı, toodelete istiyor ve - hello bağlam menüsünden - seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-145">Right-click hello blob container you wish toodelete, and - from hello context menu - select **Delete**.</span></span>
   <span data-ttu-id="a1a1a-146">Tuşlarına da basabilirsiniz **silmek** toodelete hello şu anda seçili blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-146">You can also press **Delete** toodelete hello currently selected blob container.</span></span>

   ![BLOB kapsayıcı bağlam menüsü Sil][4]
5. <span data-ttu-id="a1a1a-148">Seçin **Evet** toohello onay iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-148">Select **Yes** toohello confirmation dialog.</span></span>

   ![BLOB kapsayıcı onay Sil][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="a1a1a-150">Bir blob kapsayıcısını kopyalayın</span><span class="sxs-lookup"><span data-stu-id="a1a1a-150">Copy a blob container</span></span>
<span data-ttu-id="a1a1a-151">Depolama Gezgini (Önizleme) toocopy bir blob kapsayıcı toohello Pano ve kapsayıcı içinde başka bir depolama hesabı blob sonra Yapıştır sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-151">Storage Explorer (Preview) enables you toocopy a blob container toohello clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="a1a1a-152">(nasıl toocopy tek BLOB, toosee toohello bölümüne başvurun [blob kapsayıcısı içinde BLOB'ları yönetme](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="a1a1a-152">(toosee how toocopy individual blobs, refer toohello section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="a1a1a-153">Aşağıdaki adımları hello nasıl toocopy bir blob kapsayıcısından bir depolama hesabı tooanother gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-153">hello following steps illustrate how toocopy a blob container from one storage account tooanother.</span></span>

1. <span data-ttu-id="a1a1a-154">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="a1a1a-155">Merhaba sol bölmede, toocopy istediğiniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-155">In hello left pane, expand hello storage account containing hello blob container you wish toocopy.</span></span>
3. <span data-ttu-id="a1a1a-156">Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-156">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="a1a1a-157">Sağ hello blob kapsayıcısı, toocopy istiyor ve - hello bağlam menüsünden - seçin **kopyalama Blob kapsayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-157">Right-click hello blob container you wish toocopy, and - from hello context menu - select **Copy Blob Container**.</span></span>

   ![Kopya blob kapsayıcı bağlam menüsü][6]
5. <span data-ttu-id="a1a1a-159">Hangi içine, toopaste hello blob kapsayıcısı istediğiniz - hello bağlam menüsünden - seçin hello istenen "hedef" depolama hesabını sağ tıklatıp **Yapıştır Blob kapsayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-159">Right-click hello desired "target" storage account into which you want toopaste hello blob container, and - from hello context menu - select **Paste Blob Container**.</span></span>

   ![Yapıştır blob kapsayıcı bağlam menüsü][7]

## <a name="get-hello-sas-for-a-blob-container"></a><span data-ttu-id="a1a1a-161">Blob kapsayıcısı için Hello SAS alma</span><span class="sxs-lookup"><span data-stu-id="a1a1a-161">Get hello SAS for a blob container</span></span>
<span data-ttu-id="a1a1a-162">A [paylaşılan erişim imzası (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) depolama hesabınızda atanmış erişim tooresources sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-162">A [shared access signature (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) provides delegated access tooresources in your storage account.</span></span>
<span data-ttu-id="a1a1a-163">Başka bir deyişle, bir istemci depolama hesabınızdaki izinleri tooobjects süre ve belirtilen bir izin kümesi ile belirli bir süre için hesap erişim tuşlarınızı paylaşmak zorunda kalmadan sınırlı verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-163">This means that you can grant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="a1a1a-164">Merhaba aşağıdaki adımları göstermek nasıl toocreate bir blob kapsayıcı için bir SAS:</span><span class="sxs-lookup"><span data-stu-id="a1a1a-164">hello following steps illustrate how toocreate a SAS for a blob container:</span></span>

1. <span data-ttu-id="a1a1a-165">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="a1a1a-166">Hello sol bölmesinde, SAS tooget öğrenmek isterseniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-166">In hello left pane, expand hello storage account containing hello blob container for which you wish tooget a SAS.</span></span>
3. <span data-ttu-id="a1a1a-167">Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-167">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="a1a1a-168">Merhaba istenen blob kapsayıcısına sağ tıklayın ve - hello bağlam menüsünden - seçin **paylaşılan erişim imzası Al**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-168">Right-click hello desired blob container, and - from hello context menu - select **Get Shared Access Signature**.</span></span>

   ![SAS bağlam menüsü Al][8]
5. <span data-ttu-id="a1a1a-170">Merhaba, **paylaşılan erişim imzası** iletişim kutusunda, hello İlkesi, başlangıç ve sona erme tarihleri, saat dilimini belirtin ve erişim düzeyleri hello kaynak için istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-170">In hello **Shared Access Signature** dialog, specify hello policy, start and expiration dates, time zone, and access levels you want for hello resource.</span></span>

   ![SAS seçenekleri Al][9]
6. <span data-ttu-id="a1a1a-172">Merhaba SAS seçeneklerini belirtme tamamladığınızda seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-172">When you're finished specifying hello SAS options, select **Create**.</span></span>
7. <span data-ttu-id="a1a1a-173">İkinci bir **paylaşılan erişim imzası** iletişim listeleri hello hello URL yanı sıra blob kapsayıcısı ve tooaccess kullanabileceğiniz QueryStrings hello depolama kaynağı sonra görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-173">A second **Shared Access Signature** dialog will then display that lists hello blob container along with hello URL and QueryStrings you can use tooaccess hello storage resource.</span></span>
   <span data-ttu-id="a1a1a-174">Seçin **kopya** toocopy toohello Pano istediğiniz sonraki toohello URL.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-174">Select **Copy** next toohello URL you wish toocopy toohello clipboard.</span></span>

   ![SAS URL'leri Kopyala][10]
8. <span data-ttu-id="a1a1a-176">İşiniz bittiğinde **Kapat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="a1a1a-177">Blob kapsayıcısı için erişim ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="a1a1a-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="a1a1a-178">Merhaba aşağıdaki adımları göstermek nasıl toomanage (ekleme ve kaldırma) erişim ilkeleri blob kapsayıcısı için:</span><span class="sxs-lookup"><span data-stu-id="a1a1a-178">hello following steps illustrate how toomanage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="a1a1a-179">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="a1a1a-180">Merhaba sol bölmede hello depolama hesabı erişim ilkeleri toomanage istediğiniz hello blob kapsayıcısı içeren genişletin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-180">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="a1a1a-181">Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-181">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="a1a1a-182">Merhaba istenen blob kapsayıcısı seçip - hello bağlam menüsünden - **erişim ilkelerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-182">Select hello desired blob container, and - from hello context menu - select **Manage Access Policies**.</span></span>

   ![Erişim ilkelerini yönet bağlam menüsü][11]
5. <span data-ttu-id="a1a1a-184">Merhaba **erişim ilkeleri** iletişim hello seçili blob kapsayıcısı için oluşturulmuş tüm erişim ilkeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-184">hello **Access Policies** dialog will list any access policies already created for hello selected blob container.</span></span>

   ![Erişim ilkesi seçenekleri][12]        
6. <span data-ttu-id="a1a1a-186">Merhaba erişim ilkesi yönetim görevi bağlı olarak aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a1a1a-186">Follow these steps depending on hello access policy management task:</span></span>

   * <span data-ttu-id="a1a1a-187">**Yeni bir erişim ilkesi ekleme** - **Ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="a1a1a-188">Oluşturduktan sonra hello **erişim ilkeleri** iletişim yeni eklenen hello görüntüler erişim ilkesi (varsayılan ayarlarla).</span><span class="sxs-lookup"><span data-stu-id="a1a1a-188">Once generated, hello **Access Policies** dialog will display hello newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="a1a1a-189">**Bir erişim ilkesi Düzenle** - istenen tüm düzenlemeleri yapın ve seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="a1a1a-190">**Erişim ilkesini kaldırmak** - seçin **kaldırmak** tooremove istediğiniz sonraki toohello erişim ilkesi.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-190">**Remove an access policy** - Select **Remove** next toohello access policy you wish tooremove.</span></span>

## <a name="set-hello-public-access-level-for-a-blob-container"></a><span data-ttu-id="a1a1a-191">Blob kapsayıcısı için Hello genel erişim düzeyini ayarlama</span><span class="sxs-lookup"><span data-stu-id="a1a1a-191">Set hello Public Access Level for a blob container</span></span>
<span data-ttu-id="a1a1a-192">Varsayılan olarak, her blob kapsayıcısı çok ayarlanır "Genel erişim yok".</span><span class="sxs-lookup"><span data-stu-id="a1a1a-192">By default, every blob container is set too"No public access".</span></span>

<span data-ttu-id="a1a1a-193">Merhaba aşağıdaki adımları nasıl toospecify genel erişim gösteren bir blob kapsayıcısı için düzeyi.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-193">hello following steps illustrate how toospecify a public access level for a blob container.</span></span>

1. <span data-ttu-id="a1a1a-194">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="a1a1a-195">Merhaba sol bölmede hello depolama hesabı erişim ilkeleri toomanage istediğiniz hello blob kapsayıcısı içeren genişletin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-195">In hello left pane, expand hello storage account containing hello blob container whose access policies you wish toomanage.</span></span>
3. <span data-ttu-id="a1a1a-196">Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-196">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="a1a1a-197">Merhaba istenen blob kapsayıcısı seçip - hello bağlam menüsünden - **genel erişim düzeyi ayarlanan**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-197">Select hello desired blob container, and - from hello context menu - select **Set Public Access Level**.</span></span>

   ![Genel erişim düzeyi bağlam menüsü Ayarla][13]
5. <span data-ttu-id="a1a1a-199">Merhaba, **kapsayıcısı genel erişim düzeyi ayarlanan** iletişim kutusunda, istenen hello erişim düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-199">In hello **Set Container Public Access Level** dialog, specify hello desired access level.</span></span>

   ![Genel erişim düzeyi seçeneklerini ayarlama][14]
6. <span data-ttu-id="a1a1a-201">**Uygula**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="a1a1a-202">Blob kapsayıcısı içinde BLOB'ları yönetme</span><span class="sxs-lookup"><span data-stu-id="a1a1a-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="a1a1a-203">Bir blob kapsayıcısını oluşturduktan sonra bir blob toothat blob kapsayıcı karşıya yükleme, bir blob tooyour yerel bilgisayarda indirin, yerel bilgisayarınıza ve çok daha fazlasını bir blob açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-203">Once you've created a blob container, you can upload a blob toothat blob container, download a blob tooyour local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="a1a1a-204">Aşağıdaki adımları hello nasıl toomanage hello BLOB'lar (ve klasörler) bir blob kapsayıcısına gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-204">hello following steps illustrate how toomanage hello blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="a1a1a-205">Depolama Gezgini’ni (Önizleme) açın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="a1a1a-206">Merhaba sol bölmede, toomanage istediğiniz hello blob kapsayıcısı içeren hello depolama hesabı'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-206">In hello left pane, expand hello storage account containing hello blob container you wish toomanage.</span></span>
3. <span data-ttu-id="a1a1a-207">Merhaba depolama hesabının genişletin **Blob kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-207">Expand hello storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="a1a1a-208">Merhaba blob kapsayıcısı tooview istediğiniz çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-208">Double-click hello blob container you wish tooview.</span></span>
5. <span data-ttu-id="a1a1a-209">Merhaba ana bölmede hello blob kapsayıcısının içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-209">hello main pane will display hello blob container's contents.</span></span>

   ![Görünüm blob kapsayıcısı][3]
6. <span data-ttu-id="a1a1a-211">Merhaba ana bölmede hello blob kapsayıcısının içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-211">hello main pane will display hello blob container's contents.</span></span>
7. <span data-ttu-id="a1a1a-212">Tooperform istediğiniz Hello göreve bağlı olarak aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a1a1a-212">Follow these steps depending on hello task you wish tooperform:</span></span>

   * <span data-ttu-id="a1a1a-213">**Dosyaları tooa blob kapsayıcısı karşıya yükle**</span><span class="sxs-lookup"><span data-stu-id="a1a1a-213">**Upload files tooa blob container**</span></span>

     1. <span data-ttu-id="a1a1a-214">Merhaba ana bölmede ait araç çubuğunda seçin **karşıya**ve ardından **dosya yükleme** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-214">On hello main pane's toolbar, select **Upload**, and then **Upload Files** from hello drop-down menu.</span></span>

        ![Dosya menüsü karşıya yükle][15]
     2. <span data-ttu-id="a1a1a-216">Merhaba, **dosyaları karşıya yükleme** iletişim, select hello üç nokta (**...** ) düğmesini hello hello sağ tarafındaki **dosyaları** metin kutusu tooselect hello dosyaları tooupload istiyor.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-216">In hello **Upload files** dialog, select hello ellipsis (**…**) button on hello right side of hello **Files** text box tooselect hello file(s) you wish tooupload.</span></span>

        ![Karşıya yükleme seçenekleri dosyaları][16]
     3. <span data-ttu-id="a1a1a-218">Merhaba türünü belirtin **Blob türü**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-218">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="a1a1a-219">Merhaba makale [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) çeşitli blob türü hello hello arasındaki farklar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-219">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="a1a1a-220">İsteğe bağlı olarak, içine hello seçili dosyaları karşıya yükleneceği bir hedef klasör belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-220">Optionally, specify a target folder into which hello selected file(s) will be uploaded.</span></span> <span data-ttu-id="a1a1a-221">Merhaba hedef klasörü yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-221">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="a1a1a-222">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-222">Select **Upload**.</span></span>
   * <span data-ttu-id="a1a1a-223">**Bir klasör tooa blob kapsayıcı karşıya yükle**</span><span class="sxs-lookup"><span data-stu-id="a1a1a-223">**Upload a folder tooa blob container**</span></span>

     1. <span data-ttu-id="a1a1a-224">Merhaba ana bölmede ait araç çubuğunda seçin **karşıya**ve ardından **karşıya yükleme klasörü** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-224">On hello main pane's toolbar, select **Upload**, and then **Upload Folder** from hello drop-down menu.</span></span>

        ![Klasörü karşıya yükle menüsü][17]
     2. <span data-ttu-id="a1a1a-226">Merhaba, **karşıya yükleme klasörü** iletişim, select hello üç nokta (**...** ) düğmesini hello hello sağ tarafındaki **klasörü** içeriği tooupload istediğiniz metin kutusu tooselect hello klasörü.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-226">In hello **Upload folder** dialog, select hello ellipsis (**…**) button on hello right side of hello **Folder** text box tooselect hello folder whose contents you wish tooupload.</span></span>

        ![Klasör Seçenekleri karşıya yükle][18]
     3. <span data-ttu-id="a1a1a-228">Merhaba türünü belirtin **Blob türü**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-228">Specify hello type of **Blob type**.</span></span> <span data-ttu-id="a1a1a-229">Merhaba makale [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) çeşitli blob türü hello hello arasındaki farklar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-229">hello article [Get started with Azure Blob storage using .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains hello differences between hello various blob types.</span></span>
     4. <span data-ttu-id="a1a1a-230">İsteğe bağlı olarak, hangi hello seçilen klasörün içeriğini karşıya yükleneceği bir hedef klasör belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-230">Optionally, specify a target folder into which hello selected folder's contents will be uploaded.</span></span> <span data-ttu-id="a1a1a-231">Merhaba hedef klasörü yoksa, oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-231">If hello target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="a1a1a-232">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-232">Select **Upload**.</span></span>
   * <span data-ttu-id="a1a1a-233">**Bir blob tooyour yerel bilgisayarda indirin**</span><span class="sxs-lookup"><span data-stu-id="a1a1a-233">**Download a blob tooyour local computer**</span></span>

     1. <span data-ttu-id="a1a1a-234">Merhaba blob toodownload istediğiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-234">Select hello blob you wish toodownload.</span></span>
     2. <span data-ttu-id="a1a1a-235">Merhaba ana bölmede ait araç çubuğunda seçin **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-235">On hello main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="a1a1a-236">Merhaba, **toosave hello blob indirdiğiniz belirt** iletişim kutusunda, indirilen hello blob hello konumu belirtin ve hello toogive istediğiniz adı.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-236">In hello **Specify where toosave hello downloaded blob** dialog, specify hello location where you want hello blob downloaded, and hello name you wish toogive it.</span></span>  
     4. <span data-ttu-id="a1a1a-237">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-237">Select **Save**.</span></span>
   * <span data-ttu-id="a1a1a-238">**Yerel bilgisayarınızda bir blob açın**</span><span class="sxs-lookup"><span data-stu-id="a1a1a-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="a1a1a-239">Merhaba blob tooopen istediğiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-239">Select hello blob you wish tooopen.</span></span>
     2. <span data-ttu-id="a1a1a-240">Merhaba ana bölmede ait araç çubuğunda seçin **açık**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-240">On hello main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="a1a1a-241">Merhaba blob indirilir ve hello blob'un temel alınan dosya türü ile ilişkili hello uygulama kullanılarak açılır.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-241">hello blob will be downloaded and opened using hello application associated with hello blob's underlying file type.</span></span>
   * <span data-ttu-id="a1a1a-242">**Bir blob toohello Panoya Kopyala**</span><span class="sxs-lookup"><span data-stu-id="a1a1a-242">**Copy a blob toohello clipboard**</span></span>

     1. <span data-ttu-id="a1a1a-243">Merhaba blob toocopy istediğiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-243">Select hello blob you wish toocopy.</span></span>
     2. <span data-ttu-id="a1a1a-244">Merhaba ana bölmede ait araç çubuğunda seçin **kopya**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-244">On hello main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="a1a1a-245">Merhaba sol bölmede tooanother blob kapsayıcısı gidin ve çift tooview hello ana bölmede içinde.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-245">In hello left pane, navigate tooanother blob container, and double-click it tooview it in hello main pane.</span></span>
     4. <span data-ttu-id="a1a1a-246">Merhaba ana bölmede ait araç çubuğunda seçin **Yapıştır** toocreate hello blob kopyalama.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-246">On hello main pane's toolbar, select **Paste** toocreate a copy of hello blob.</span></span>
   * <span data-ttu-id="a1a1a-247">**Bir blob Sil**</span><span class="sxs-lookup"><span data-stu-id="a1a1a-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="a1a1a-248">Merhaba blob toodelete istediğiniz seçin.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-248">Select hello blob you wish toodelete.</span></span>
     2. <span data-ttu-id="a1a1a-249">Merhaba ana bölmede ait araç çubuğunda seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-249">On hello main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="a1a1a-250">Seçin **Evet** toohello onay iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="a1a1a-250">Select **Yes** toohello confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1a1a-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1a1a-251">Next steps</span></span>
* <span data-ttu-id="a1a1a-252">Görünüm hello [en son Depolama Gezgini (Önizleme) sürüm notları ve videolar](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="a1a1a-252">View hello [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="a1a1a-253">Nasıl çok öğrenin[Azure BLOB'ları, tabloları, kuyrukları ve dosyaları kullanan uygulamalar oluşturmak](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="a1a1a-253">Learn how too[create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
