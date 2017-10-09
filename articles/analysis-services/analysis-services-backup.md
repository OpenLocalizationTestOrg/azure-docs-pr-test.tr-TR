---
title: "aaaAzure Analysis Services veritabanını yedekleme ve geri yükleme | Microsoft Docs"
description: "Toobackup ve geri yükleme Azure Analiz Hizmetleri nasıl açıklar veritabanı."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="03a4c-103">Yedekleme ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="03a4c-103">Backup and restore</span></span>

<span data-ttu-id="03a4c-104">Azure Analysis Services tablolu model veritabanlarını yedeklemek için çok hello aynı olduğu gibi şirket içi Analysis Services olur.</span><span class="sxs-lookup"><span data-stu-id="03a4c-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="03a4c-105">Merhaba birincil yedekleme dosyalarını depoladığınız farktır.</span><span class="sxs-lookup"><span data-stu-id="03a4c-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="03a4c-106">Tooa kapsayıcısında yedekleme dosyalarını kaydedilmiş bir [Azure depolama hesabı](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="03a4c-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="03a4c-107">Sunucunuz için depolama ayarlarını yapılandırırken oluşturulabilir veya zaten bir depolama hesabı ve kapsayıcı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03a4c-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="03a4c-108">Bir depolama hesabı oluştururken bir ek hizmet ücretlerin alınmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="03a4c-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="03a4c-109">toolearn daha, fazla [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="03a4c-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="03a4c-110">Yedeklemeler bir abf uzantısıyla kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="03a4c-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="03a4c-111">Bellek içi tablolu modeller için model verileri ve meta veriler depolanır.</span><span class="sxs-lookup"><span data-stu-id="03a4c-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="03a4c-112">DirectQuery tablolu modeller için yalnızca model meta verilerini depolanır.</span><span class="sxs-lookup"><span data-stu-id="03a4c-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="03a4c-113">Yedeklemeleri sıkıştırılmış ve, size hello seçeneklere bağlı olarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="03a4c-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="03a4c-114">Depolama ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="03a4c-114">Configure storage settings</span></span>
<span data-ttu-id="03a4c-115">Yedekleme önce tooconfigure depolama ayarlarını sunucunuz için gerekir.</span><span class="sxs-lookup"><span data-stu-id="03a4c-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="03a4c-116">tooconfigure depolama ayarları</span><span class="sxs-lookup"><span data-stu-id="03a4c-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="03a4c-117">Azure portalında > **ayarları**, tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="03a4c-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Yedekleme ayarları](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="03a4c-119">Tıklatın **etkin**, ardından **depolama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="03a4c-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Etkinleştirme](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="03a4c-121">Depolama hesabınızı seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03a4c-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="03a4c-122">Bir kapsayıcı seçin veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03a4c-122">Select a container or create a new one.</span></span>

    ![Kapsayıcı seçin](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="03a4c-124">Yedekleme ayarlarınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="03a4c-124">Save your backup settings.</span></span>

    ![Yedekleme ayarlarını Kaydet](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="03a4c-126">Backup</span><span class="sxs-lookup"><span data-stu-id="03a4c-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="03a4c-127">SSMS kullanarak toobackup</span><span class="sxs-lookup"><span data-stu-id="03a4c-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="03a4c-128">SSMS, bir veritabanına sağ tıklayın > **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="03a4c-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="03a4c-129">İçinde **Backup Database** > **yedekleme dosyası**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="03a4c-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="03a4c-130">Merhaba, **Kaydet dosyası olarak** iletişim kutusunda, hello klasör yolunu doğrulayın ve sonra hello yedekleme dosyası için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="03a4c-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="03a4c-131">Merhaba, **Backup Database** iletişim, seçenekleri belirleyin.</span><span class="sxs-lookup"><span data-stu-id="03a4c-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="03a4c-132">**Dosya izin üzerine** -bu seçenek toooverwrite yedekleme dosyaları hello seçin aynı adı.</span><span class="sxs-lookup"><span data-stu-id="03a4c-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="03a4c-133">Bu seçenek seçilmezse kaydetmekte olduğunuz hello dosya hello aynı zaten bir dosya olarak aynı ad hello olamaz konumu.</span><span class="sxs-lookup"><span data-stu-id="03a4c-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="03a4c-134">**Sıkıştırma uygulamak** -bu seçenek toocompress hello yedekleme dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="03a4c-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="03a4c-135">Sıkıştırılmış yedek dosyaları disk alanından tasarruf, ancak biraz daha yüksek CPU kullanımı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="03a4c-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="03a4c-136">**Yedek dosyayı şifrelemek** -bu seçenek tooencrypt hello yedekleme dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="03a4c-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="03a4c-137">Bu seçenek, bir kullanıcı tarafından sağlanan parola toosecure hello yedekleme dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="03a4c-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="03a4c-138">Merhaba parola hello yedekleme verilerini başka bir yöntemle bir geri yükleme işlemi daha okuma önler.</span><span class="sxs-lookup"><span data-stu-id="03a4c-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="03a4c-139">Tooencrypt yedeklemeler seçerseniz, hello parola güvenli bir yerde saklayın.</span><span class="sxs-lookup"><span data-stu-id="03a4c-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="03a4c-140">Tıklatın **Tamam** toocreate ve hello yedekleme dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="03a4c-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="03a4c-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="03a4c-141">PowerShell</span></span>
<span data-ttu-id="03a4c-142">Kullanım [yedekleme ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="03a4c-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="03a4c-143">Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="03a4c-143">Restore</span></span>
<span data-ttu-id="03a4c-144">Geri yüklerken, yedekleme dosyası, sunucunuz için yapılandırdığınız hello depolama hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="03a4c-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="03a4c-145">Bir şirket içi konumu tooyour depolama hesabından bir yedekleme dosyası toomove gerekiyorsa kullanın [Microsoft Azure Storage Gezgini](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) veya hello [AzCopy](../storage/common/storage-use-azcopy.md) komut satırı yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="03a4c-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="03a4c-146">Bir şirket içi sunucusundan geri yükleme, tüm hello etki alanı kullanıcıları hello modelinin rollerini kaldırın ve bunları eklemeniz gerekir toohello rolleri Azure Active Directory Kullanıcıları olarak yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="03a4c-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="03a4c-147">SSMS kullanarak toorestore</span><span class="sxs-lookup"><span data-stu-id="03a4c-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="03a4c-148">SSMS, bir veritabanına sağ tıklayın > **geri**.</span><span class="sxs-lookup"><span data-stu-id="03a4c-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="03a4c-149">Merhaba, **Backup Database** iletişim, **yedekleme dosyası**, tıklatın **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="03a4c-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="03a4c-150">Merhaba, **veritabanı dosyalarını bulmak** iletişim, select hello dosyasını toorestore.</span><span class="sxs-lookup"><span data-stu-id="03a4c-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="03a4c-151">İçinde **veritabanı geri yükleme**seçin hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="03a4c-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="03a4c-152">Seçeneklerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="03a4c-152">Specify options.</span></span> <span data-ttu-id="03a4c-153">Güvenlik seçenekleri yedekleme yapılırken kullanılan hello yedekleme seçenekleri eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="03a4c-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="03a4c-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="03a4c-154">PowerShell</span></span>

<span data-ttu-id="03a4c-155">Kullanım [geri yükleme ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="03a4c-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="03a4c-156">İlgili bilgiler</span><span class="sxs-lookup"><span data-stu-id="03a4c-156">Related information</span></span>

[<span data-ttu-id="03a4c-157">Azure depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="03a4c-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="03a4c-158">[Yüksek düzey kullanılabilirlik](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="03a4c-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="03a4c-159">Azure Analysis Services yönetme</span><span class="sxs-lookup"><span data-stu-id="03a4c-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
