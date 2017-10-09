---
title: "Paylaşılan erişim imzaları - Azure Hdınsight kullanarak aaaRestrict erişim | Microsoft Docs"
description: "Nasıl toouse paylaşılan erişim imzaları toorestrict Hdınsight erişim Azure storage bloblarında depolanır toodata öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="72f0b-103">Azure Storage paylaşılan erişim imzaları toorestrict erişim toodata Hdınsight'ta kullanın</span><span class="sxs-lookup"><span data-stu-id="72f0b-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="72f0b-104">Hdınsight tam erişim toodata hello kümesi ile ilişkili hello Azure depolama hesapları vardır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="72f0b-105">Paylaşılan erişim imzaları hello blob kapsayıcı toorestrict erişim toohello verileri üzerinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72f0b-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="72f0b-106">Örneğin, tooprovide salt okunur erişim toohello verileri.</span><span class="sxs-lookup"><span data-stu-id="72f0b-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="72f0b-107">Paylaşılan erişim imzaları (SAS) toolimit erişim toodata sağlayan bir Azure depolama hesapları özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="72f0b-108">Örneğin, salt okunur erişim toodata sağlama.</span><span class="sxs-lookup"><span data-stu-id="72f0b-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72f0b-109">Apache bırakabilmenizi kullanarak bir çözüm için etki alanına katılmış Hdınsight kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="72f0b-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="72f0b-110">Daha fazla bilgi için bkz: Merhaba [etki alanına katılmış Hdınsight yapılandırma](hdinsight-domain-joined-configure.md) belge.</span><span class="sxs-lookup"><span data-stu-id="72f0b-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="72f0b-111">Hdınsight hello kümesi için tam erişim toohello varsayılan depolama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="72f0b-112">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="72f0b-112">Requirements</span></span>

* <span data-ttu-id="72f0b-113">Bir Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="72f0b-113">An Azure subscription</span></span>
* <span data-ttu-id="72f0b-114">C# veya Python.</span><span class="sxs-lookup"><span data-stu-id="72f0b-114">C# or Python.</span></span> <span data-ttu-id="72f0b-115">C# kod örneği, bir Visual Studio çözümü olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="72f0b-116">Visual Studio 2013, 2015 veya 2017 sürümü olması gerekir</span><span class="sxs-lookup"><span data-stu-id="72f0b-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="72f0b-117">Python 2.7 ya da daha yüksek bir sürüm olması gerekir</span><span class="sxs-lookup"><span data-stu-id="72f0b-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="72f0b-118">Linux tabanlı Hdınsight kümesi veya [Azure PowerShell] [ powershell] -mevcut bir Linux tabanlı kümeniz varsa, Ambari tooadd bir paylaşılan erişim imzası toohello küme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72f0b-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="72f0b-119">Aksi durumda, Azure PowerShell toocreate bir küme kullanın ve küme oluşturma sırasında bir paylaşılan erişim imzası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="72f0b-120">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="72f0b-121">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="72f0b-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="72f0b-122">Örnek dosyalarından hello [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="72f0b-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="72f0b-123">Bu depo hello aşağıdaki öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="72f0b-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="72f0b-124">Hdınsight ile kullanmak için bir depolama kapsayıcısı, depolanan ilke ve SAS oluşturabilirsiniz bir Visual Studio projesi</span><span class="sxs-lookup"><span data-stu-id="72f0b-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="72f0b-125">Hdınsight ile kullanmak için bir depolama kapsayıcısı, depolanan ilke ve SAS oluşturabilirsiniz bir Python komut dosyası</span><span class="sxs-lookup"><span data-stu-id="72f0b-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="72f0b-126">Bir Hdınsight oluşturabilmeniz için bir PowerShell Betiği küme ve toouse hello SAS yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="72f0b-127">Paylaşılan erişim imzaları</span><span class="sxs-lookup"><span data-stu-id="72f0b-127">Shared Access Signatures</span></span>

<span data-ttu-id="72f0b-128">Paylaşılan erişim imzaları iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="72f0b-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="72f0b-129">Geçici: hello başlangıç saati, sona erme saati ve SAS tüm belirtilen SAS URI'sini hello üzerinde hello izinlerini.</span><span class="sxs-lookup"><span data-stu-id="72f0b-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="72f0b-130">Erişim ilkesinde saklanan: depolanmış erişim ilkesi, bir blob kapsayıcısını gibi bir kaynak kapsayıcısı üzerinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="72f0b-131">Bir ilke bir veya daha fazla paylaşılan erişim imzalar için kullanılan toomanage kısıtlamaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="72f0b-132">Bir SAS depolanmış erişim ilkesi ile ilişkilendirdiğinizde, hello SAS hello kısıtlamaları devralır - hello başlangıç saati, sona erme saati ve izinleri - depolanan hello erişim ilkesi için tanımlı.</span><span class="sxs-lookup"><span data-stu-id="72f0b-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="72f0b-133">Merhaba fark hello iki formlar arasında önemli bir senaryo için önemlidir: iptal.</span><span class="sxs-lookup"><span data-stu-id="72f0b-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="72f0b-134">Merhaba SAS edinir herkes, kimin istenen bağımsız olarak toobegin ile kullanabilmesi için bir SAS bir URL ' dir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="72f0b-135">Bir SAS yayımlandığını, hello world herkes tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="72f0b-136">Dağıtılan bir SAS dört özelliklerinden biri işlem yapılana kadar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="72f0b-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="72f0b-137">SAS ulaşıldığında hello üzerinde belirtilen hello bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="72f0b-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="72f0b-138">SAS ulaşıldığında hello tarafından başvurulan depolanan hello erişim ilkesinde belirtilen hello bitiş saati.</span><span class="sxs-lookup"><span data-stu-id="72f0b-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="72f0b-139">Merhaba aşağıdaki senaryolara neden hello sona erme saati toobe ulaştı:</span><span class="sxs-lookup"><span data-stu-id="72f0b-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="72f0b-140">Merhaba süre geçti.</span><span class="sxs-lookup"><span data-stu-id="72f0b-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="72f0b-141">depolanan hello erişim ilkesi değiştirilmiş toohave bir sona erme hello geçmiş saattir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="72f0b-142">Merhaba sona erme saati değiştirme tek yönlü toorevoke hello SAS olur.</span><span class="sxs-lookup"><span data-stu-id="72f0b-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="72f0b-143">Merhaba, başka bir şekilde toorevoke hello SAS SAS silinir, hello tarafından başvurulan erişim ilkesi depolanır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="72f0b-144">Depolanan hello erişim ilkesi ile aynı adı, için tüm SAS belirteci hello yeniden yapıyorsanız hello önceki ilke (Merhaba sona erme saati hello üzerinde SAS değil geçtiyse) geçerli olur.</span><span class="sxs-lookup"><span data-stu-id="72f0b-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="72f0b-145">Toorevoke hello SAS düşünüyorsanız, hello erişim ilkesi hello gelecekteki içinde bir sona erme saati ile yeniden farklı bir ad emin toouse olması.</span><span class="sxs-lookup"><span data-stu-id="72f0b-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="72f0b-146">kullanılan toocreate hello SAS olduğu hello hesap anahtarını yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="72f0b-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="72f0b-147">Başlangıç anahtarı yeniden oluşturuluyor hello önceki anahtar toofail kimlik doğrulaması kullanan tüm uygulamalar neden olur.</span><span class="sxs-lookup"><span data-stu-id="72f0b-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="72f0b-148">Tüm bileşenleri toohello yeni anahtarı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72f0b-149">Paylaşılan erişim imzası URI hello hesabı anahtar kullanılan toocreate hello imza ile ilişkili ve hello depolanmış erişim ilkesi (varsa) ilişkili.</span><span class="sxs-lookup"><span data-stu-id="72f0b-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="72f0b-150">Hiçbir depolanmış erişim ilkesi belirtilirse, hello yalnızca yolu toorevoke paylaşılan erişim imzası toochange hello hesap anahtardır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="72f0b-151">Her zaman depolanmış erişim ilkeleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="72f0b-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="72f0b-152">Depolanan ilkelerde kullanırken imzaları iptal etmek veya gerektiği gibi hello sona erme tarihini uzatmak.</span><span class="sxs-lookup"><span data-stu-id="72f0b-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="72f0b-153">Bu belgedeki Hello adımları depolanmış erişim ilkeleri toogenerate SAS kullanın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="72f0b-154">Paylaşılan erişim imzaları ile ilgili daha fazla bilgi için bkz: [anlama hello SAS modelini](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="72f0b-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="72f0b-155">Depolanan ilke ve C kullanarak SAS oluşturma\#</span><span class="sxs-lookup"><span data-stu-id="72f0b-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="72f0b-156">Merhaba çözümü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="72f0b-157">Çözüm Gezgini'nde hello üzerinde sağ **SASToken** proje ve seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="72f0b-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="72f0b-158">Seçin **ayarları** ve girişleri aşağıdaki hello değerlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="72f0b-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="72f0b-159">StorageConnectionString: hello bağlantı dizesi toocreate istediğiniz hello depolama hesabı için depolanan ilke ve SAS için.</span><span class="sxs-lookup"><span data-stu-id="72f0b-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="72f0b-160">Hello biçiminde olmalıdır `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` nerede `myaccount` depolama hesabınız hello adıdır ve `mykey` hello depolama hesabı için hello anahtarıdır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="72f0b-161">ContainerName: toorestrict erişmek istediğiniz hello depolama hesabındaki hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="72f0b-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="72f0b-162">SASPolicyName: hello adı toouse hello için ilke toocreate depolanır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="72f0b-163">FileToUpload: karşıya yüklenen toohello kapsayıcı hello yolu tooa dosya.</span><span class="sxs-lookup"><span data-stu-id="72f0b-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="72f0b-164">Merhaba projesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-164">Run hello project.</span></span> <span data-ttu-id="72f0b-165">Merhaba SAS oluşturulduktan sonra metin aşağıdaki bilgileri benzer toohello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="72f0b-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="72f0b-166">Merhaba SAS İlkesi belirteci, depolama hesabı adı ve kapsayıcı adını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="72f0b-167">Hdınsight kümenizle hello depolama hesabını ilişkilendirerek bu değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="72f0b-168">Depolanan ilke ve Python kullanarak SAS oluşturma</span><span class="sxs-lookup"><span data-stu-id="72f0b-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="72f0b-169">Merhaba SASToken.py dosyasını açın ve aşağıdaki değerleri hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="72f0b-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="72f0b-170">İlke\_ad: hello adı toouse hello için depolanan ilke toocreate.</span><span class="sxs-lookup"><span data-stu-id="72f0b-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="72f0b-171">Depolama\_hesap\_ad: hello depolama hesabınızın adını.</span><span class="sxs-lookup"><span data-stu-id="72f0b-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="72f0b-172">Depolama\_hesap\_anahtarı: hello depolama hesabının hello anahtarı.</span><span class="sxs-lookup"><span data-stu-id="72f0b-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="72f0b-173">Depolama\_kapsayıcı\_ad: toorestrict erişmek istediğiniz hello depolama hesabındaki hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="72f0b-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="72f0b-174">örnek\_dosya\_yol: karşıya yüklenen toohello kapsayıcıdır hello yol tooa dosyası.</span><span class="sxs-lookup"><span data-stu-id="72f0b-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="72f0b-175">Merhaba komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-175">Run hello script.</span></span> <span data-ttu-id="72f0b-176">Metin hello betik tamamlandığında aşağıdaki hello SAS belirteci benzer toohello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="72f0b-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="72f0b-177">Merhaba SAS İlkesi belirteci, depolama hesabı adı ve kapsayıcı adını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="72f0b-178">Hdınsight kümenizle hello depolama hesabını ilişkilendirerek bu değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="72f0b-179">Hdınsight ile Merhaba SAS kullanma</span><span class="sxs-lookup"><span data-stu-id="72f0b-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="72f0b-180">Bir Hdınsight kümesi oluştururken, bir birincil depolama hesabı belirtmeniz gerekir ve isteğe bağlı olarak ek depolama hesapları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72f0b-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="72f0b-181">Depolama ekleme bu yöntemlerin her ikisi de tam erişim toohello depolama hesapları ve kullanılan kapsayıcıları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="72f0b-182">toouse bir paylaşılan erişim imzası toolimit erişim tooa kapsayıcı ekleme özel giriş toohello **çekirdek site** hello küme yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="72f0b-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="72f0b-183">İçin **Windows tabanlı** veya **Linux tabanlı** Hdınsight kümeleri, PowerShell kullanarak küme oluşturma sırasında hello giriş ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72f0b-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="72f0b-184">İçin **Linux tabanlı** Hdınsight kümeleri, Ambari kullanarak küme oluşturulduktan sonra başlangıç yapılandırmasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="72f0b-185">Merhaba SAS kullanan bir küme oluşturun</span><span class="sxs-lookup"><span data-stu-id="72f0b-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="72f0b-186">SAS hello dahil bu kullanımları hello Hdınsight kümesi oluşturma örneği `CreateCluster` hello havuzun dizin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="72f0b-187">Bunu, aşağıdaki kullanım hello adımları toouse:</span><span class="sxs-lookup"><span data-stu-id="72f0b-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="72f0b-188">Açık hello `CreateCluster\HDInsightSAS.ps1` dosyasını bir metin düzenleyicisinde ve değerleri hello belge hello başında aşağıdaki hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="72f0b-189">Örneğin, değiştirme `'mycluster'` toohello adı hello kümesinin toocreate istiyor.</span><span class="sxs-lookup"><span data-stu-id="72f0b-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="72f0b-190">Merhaba SAS değerleri, bir depolama hesabı ve SAS belirteci oluştururken hello önceki adımlardan hello değerler eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="72f0b-191">Merhaba değerlerinin değiştiğini sonra hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="72f0b-192">Yeni bir Azure PowerShell komut istemini açın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="72f0b-193">Azure PowerShell ile ilgili bilginiz veya yüklemediyseniz, bkz: [yükleyin ve Azure PowerShell yapılandırma][powershell].</span><span class="sxs-lookup"><span data-stu-id="72f0b-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="72f0b-194">Merhaba isteminden komutu tooauthenticate tooyour Azure aboneliği aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="72f0b-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="72f0b-195">İstendiğinde, Azure aboneliğinizin hello hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="72f0b-196">Hesabınızın birden çok Azure aboneliği ile ilişkili ise, toouse gerekebilir `Select-AzureRmSubscription` tooselect hello abonelik toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="72f0b-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="72f0b-197">Dizinleri toohello Hello satırından değiştirmek `CreateCluster` hello HDInsightSAS.ps1 dosyasını içeren dizini.</span><span class="sxs-lookup"><span data-stu-id="72f0b-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="72f0b-198">Toorun hello komut aşağıdaki hello kullanın</span><span class="sxs-lookup"><span data-stu-id="72f0b-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="72f0b-199">Merhaba kaynak grubu ve depolama hesapları oluşturur gibi hello komut dosyası çalışırken Çıktı toohello PowerShell istemi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="72f0b-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="72f0b-200">İstendiğinde tooenter hello HTTP kullanıcı hello Hdınsight kümesi için var.</span><span class="sxs-lookup"><span data-stu-id="72f0b-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="72f0b-201">Kullanılan toosecure HTTP/s erişimini toohello küme hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="72f0b-202">Linux tabanlı bir küme oluşturuyorsanız, bir SSH kullanıcı hesabı adı ve parola istenir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="72f0b-203">Bu hesap, toohello kümedeki kullanılan tooremotely günlüktür.</span><span class="sxs-lookup"><span data-stu-id="72f0b-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="72f0b-204">Merhaba HTTP/s veya SSH kullanıcı adı ve parola istendiğinde, hello aşağıdaki ölçütleri karşılayan bir parola sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="72f0b-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="72f0b-205">En az 10 karakter uzunluğunda olmalıdır</span><span class="sxs-lookup"><span data-stu-id="72f0b-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="72f0b-206">En az bir rakam içermelidir</span><span class="sxs-lookup"><span data-stu-id="72f0b-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="72f0b-207">En az bir alfasayısal olmayan karakter içermelidir</span><span class="sxs-lookup"><span data-stu-id="72f0b-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="72f0b-208">En az bir büyük veya küçük harf içermelidir</span><span class="sxs-lookup"><span data-stu-id="72f0b-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="72f0b-209">Bir süre bu komut dosyası toocomplete genellikle yaklaşık 15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="72f0b-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="72f0b-210">Herhangi bir hata olmadan Hello betik tamamlandığında, hello küme oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="72f0b-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="72f0b-211">Merhaba SAS ile var olan bir küme kullanın</span><span class="sxs-lookup"><span data-stu-id="72f0b-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="72f0b-212">Varolan bir Linux tabanlı kümeniz varsa, hello SAS toohello ekleyebilirsiniz **çekirdek site** hello aşağıdaki adımları kullanarak yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="72f0b-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="72f0b-213">Kümeniz için Hello Ambari web kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="72f0b-214">Hello için bu sayfayı https://YOURCLUSTERNAME.azurehdinsight.net adresidir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="72f0b-215">İstendiğinde, toohello küme hello yönetici adı (Yönetici) kullanarak kimlik doğrulaması ve ne zaman kullanılan parola hello küme oluşturma.</span><span class="sxs-lookup"><span data-stu-id="72f0b-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="72f0b-216">Sol hello Ambari web kullanıcı Arabirimi tarafı hello seçin **HDFS** seçip hello **yapılandırmalar** hello sayfasının hello ortasında sekmesi.</span><span class="sxs-lookup"><span data-stu-id="72f0b-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="72f0b-217">Select hello **Gelişmiş** sekmesini tıklatın ve ardından hello bulana kadar kaydırın **özel çekirdek site** bölümü.</span><span class="sxs-lookup"><span data-stu-id="72f0b-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="72f0b-218">Merhaba genişletin **özel çekirdek site** bölümünde, sonra kaydırma toohello uç ve select hello **Özellik Ekle...**  bağlantı.</span><span class="sxs-lookup"><span data-stu-id="72f0b-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="72f0b-219">Kullanım hello aşağıdaki değerleri Merhaba **anahtar** ve **değeri** alanlar:</span><span class="sxs-lookup"><span data-stu-id="72f0b-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="72f0b-220">**Anahtar**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="72f0b-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="72f0b-221">**Değer**: hello önceden çalıştırdığınız C# veya Python uygulama tarafından döndürülen SAS hello</span><span class="sxs-lookup"><span data-stu-id="72f0b-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="72f0b-222">Değiştir **CONTAINERNAME** hello kapsayıcı adı ile Merhaba C# veya SAS uygulaması ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="72f0b-223">Değiştir **STORAGEACCOUNTNAME** , kullandığınız hello depolama hesabı adı ile.</span><span class="sxs-lookup"><span data-stu-id="72f0b-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="72f0b-224">Hello tıklatın **Ekle** toosave bu anahtar ve değer düğmesine tıklayın ve ardından hello **kaydetmek** düğmesini toosave hello yapılandırma değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="72f0b-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="72f0b-225">İstendiğinde, ("SAS depolama erişim örneğin ekleme") hello değişiklik açıklamasını ekleyin ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="72f0b-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="72f0b-226">Tıklatın **Tamam** zaman hello değişiklikleri tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="72f0b-227">Merhaba değişiklik uygulanmadan önce birkaç hizmeti yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="72f0b-228">Merhaba Ambari web kullanıcı Arabirimi, seçin **HDFS** sol hello ve ardından hello listeden **yeniden tüm** hello gelen **hizmet eylemleri** hello sağdaki listede aşağı açılır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="72f0b-229">İstendiğinde, seçin **bakım Modu'nu** ve select yeniden tüm __Conform ".</span><span class="sxs-lookup"><span data-stu-id="72f0b-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="72f0b-230">MapReduce2 ve YARN için bu işlemi yineleyin.</span><span class="sxs-lookup"><span data-stu-id="72f0b-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="72f0b-231">Merhaba hizmetleri yeniden başlattıktan sonra her birini seçin ve hello bakım modundan devre dışı bırakma **hizmet eylemleri** açılır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="72f0b-232">Kısıtlı erişim test</span><span class="sxs-lookup"><span data-stu-id="72f0b-232">Test restricted access</span></span>

<span data-ttu-id="72f0b-233">sınırlı tooverify erişim, aşağıdaki yöntemleri kullanın hello:</span><span class="sxs-lookup"><span data-stu-id="72f0b-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="72f0b-234">İçin **Windows tabanlı** Hdınsight kümeleri, Uzak Masaüstü tooconnect toohello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="72f0b-235">Daha fazla bilgi için bkz: [bağlanmak, RDP kullanarak tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="72f0b-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="72f0b-236">Bağlantı kurulduktan sonra hello kullan **Hadoop komut satırı** hello Masaüstü tooopen bir komut istemi simgesi.</span><span class="sxs-lookup"><span data-stu-id="72f0b-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="72f0b-237">İçin **Linux tabanlı** Hdınsight kümeleri, SSH tooconnect toohello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="72f0b-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="72f0b-238">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="72f0b-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="72f0b-239">Toohello küme bağlandıktan sonra yalnızca okuma ve liste öğeleri hello SAS depolama hesabındaki yapabilecekleriniz adımları tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="72f0b-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="72f0b-240">Merhaba kapsayıcısının toolist hello içeriği hello isteminden komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="72f0b-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="72f0b-241">Değiştir **SASCONTAINER** hello SAS depolama hesabı için oluşturulan hello kapsayıcı hello adı.</span><span class="sxs-lookup"><span data-stu-id="72f0b-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="72f0b-242">Değiştir **SASACCOUNTNAME** SAS hello için kullanılan hello depolama hesabının hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="72f0b-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="72f0b-243">Merhaba listesi hello kapsayıcı ve SAS oluşturulduğunda karşıya hello dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="72f0b-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="72f0b-244">Kullanım hello aşağıdaki hello hello dosyasının içeriğini okuyabilirsiniz tooverify komutu.</span><span class="sxs-lookup"><span data-stu-id="72f0b-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="72f0b-245">Hello yerine **SASCONTAINER** ve **SASACCOUNTNAME** hello önceki adımda olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="72f0b-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="72f0b-246">Değiştir **FILENAME** hello önceki komutta gösterilen hello dosyasının hello adıyla:</span><span class="sxs-lookup"><span data-stu-id="72f0b-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="72f0b-247">Bu komut hello hello dosyasının içeriğini listeler.</span><span class="sxs-lookup"><span data-stu-id="72f0b-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="72f0b-248">Komut toodownload hello dosya toohello yerel dosya sistemi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="72f0b-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="72f0b-249">İndirmeler hello adlı tooa yerel dosyası bu komut **testdosyası.txt**.</span><span class="sxs-lookup"><span data-stu-id="72f0b-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="72f0b-250">Kullanım hello aşağıdaki adlı tooupload hello yerel dosya tooa yeni dosya komutu **testupload.txt** hello SAS depolama üzerinde:</span><span class="sxs-lookup"><span data-stu-id="72f0b-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="72f0b-251">Metin aşağıdaki ileti benzer toohello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="72f0b-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="72f0b-252">Merhaba depolama konumu okuma + liste yalnızca olduğundan bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="72f0b-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="72f0b-253">Merhaba varsayılan depolama yazılabilir olduğundan hello kümesi için komut tooput hello verileri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="72f0b-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="72f0b-254">Bu süre, hello işlemi başarıyla tamamlanmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="72f0b-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="72f0b-255">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="72f0b-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="72f0b-256">Bir görev iptal edildi</span><span class="sxs-lookup"><span data-stu-id="72f0b-256">A task was canceled</span></span>

<span data-ttu-id="72f0b-257">**Belirtiler**: hello PowerShell Betiği kullanılarak bir küme oluştururken, hello aşağıdaki hata iletisini alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="72f0b-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="72f0b-258">**Neden**: Merhaba yönetici/HTTP kullanıcı hello küme veya (Linux tabanlı kümelerde) için bir parola kullanıyorsanız, bu hata oluşabilir hello SSH kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="72f0b-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="72f0b-259">**Çözümleme**: hello aşağıdaki ölçütleri karşılayan bir parola kullanın:</span><span class="sxs-lookup"><span data-stu-id="72f0b-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="72f0b-260">En az 10 karakter uzunluğunda olmalıdır</span><span class="sxs-lookup"><span data-stu-id="72f0b-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="72f0b-261">En az bir rakam içermelidir</span><span class="sxs-lookup"><span data-stu-id="72f0b-261">Must contain at least one digit</span></span>
* <span data-ttu-id="72f0b-262">En az bir alfasayısal olmayan karakter içermelidir</span><span class="sxs-lookup"><span data-stu-id="72f0b-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="72f0b-263">En az bir büyük veya küçük harf içermelidir</span><span class="sxs-lookup"><span data-stu-id="72f0b-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="72f0b-264">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72f0b-264">Next steps</span></span>

<span data-ttu-id="72f0b-265">Sizin için artık öğrendiğinize tooadd sınırlı erişimli depolama tooyour Hdınsight kümesi diğer yolları toowork kümenizdeki veri ile nasıl bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="72f0b-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="72f0b-266">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="72f0b-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="72f0b-267">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="72f0b-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="72f0b-268">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="72f0b-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
