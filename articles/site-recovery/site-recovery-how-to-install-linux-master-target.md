---
title: "aaaHow tooinstall Azure tooon içi yük devretme için bir Linux ana hedef sunucusu | Microsoft Docs"
description: "Linux sanal makine yeniden korumayı önce bir Linux ana hedef sunucusu gerekir. Bilgi nasıl tooinstall biri."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="387cf-104">Bir Linux ana hedef sunucu yükle</span><span class="sxs-lookup"><span data-stu-id="387cf-104">Install a Linux master target server</span></span>
<span data-ttu-id="387cf-105">Sanal makinelerinizi başarısız olduktan sonra geri hello sanal makineleri toohello şirket içi site başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="387cf-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="387cf-106">geri toofail, tooreprotect hello sanal makine Azure toohello şirket içi siteden gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="387cf-107">Bu işlem için bir şirket içi ana hedef sunucusu tooreceive hello trafiği gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="387cf-108">Windows sanal makinesi korumalı sanal makineniz olması durumunda, bir Windows ana hedef gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="387cf-109">Bir Linux sanal makine için bir Linux ana hedef gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="387cf-110">Okuma hello aşağıdaki adımları toolearn nasıl hedef toocreate ve yükleme bir Linux ana.</span><span class="sxs-lookup"><span data-stu-id="387cf-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="387cf-111">Merhaba 9.10.0 ana hedef sunucusu sürümünden itibaren hello son ana hedef sunucusu, yalnızca bir Ubuntu 16.04 sunucusunda yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="387cf-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="387cf-112">Yeni yüklemeler CentOS6.6 sunucularda izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="387cf-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="387cf-113">Ancak, tooupgrade eski ana hedef sunucularınızı hello 9.10.0 sürümünü kullanarak devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="387cf-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="387cf-114">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="387cf-114">Overview</span></span>
<span data-ttu-id="387cf-115">Bu makalede nasıl tooinstall bir Linux ana hedef için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="387cf-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="387cf-116">POST yorumlarınızı ve sorularınızı bu makalenin veya hello hello sonunda [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="387cf-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="387cf-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="387cf-117">Prerequisites</span></span>

* <span data-ttu-id="387cf-118">toochoose hello hangi toodeploy hello ana hedef konakta belirlemek hello geri dönme toobe tooan mevcut şirket içi sanal makine ya da tooa yeni bir sanal makine geçiyor durumunda.</span><span class="sxs-lookup"><span data-stu-id="387cf-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="387cf-119">Mevcut bir sanal makine için erişim toohello veri depolarına hello sanal makinenin hello ana hedefinin hello konak olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="387cf-120">Merhaba şirket içi sanal makine yoksa hello geri dönme sanal makine aynı hello ana hedefi olarak konağı hello oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="387cf-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="387cf-121">Herhangi bir ESXi ana tooinstall hello ana hedef seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="387cf-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="387cf-122">Merhaba ana hedef hello işlem sunucusu ve hello yapılandırma sunucusu ile iletişim kurabilen bir ağ üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="387cf-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="387cf-123">Merhaba ana hedef Hello sürümü eşit tooor önceki sürümlerinden hello hello işlem sunucusu ve hello yapılandırma sunucusu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="387cf-124">Örneğin, hello yapılandırma sunucusu Hello sürümü 9,4 ise hello ana hedef hello sürümü 9,4 veya 9.3 ancak değil 9.5 olabilir.</span><span class="sxs-lookup"><span data-stu-id="387cf-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="387cf-125">Merhaba ana hedef yalnızca bir VMware sanal makine ve bir fiziksel sunucuya yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="387cf-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="387cf-126">Merhaba ana hedef toohello boyutlandırma yönergelerine göre oluşturma</span><span class="sxs-lookup"><span data-stu-id="387cf-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="387cf-127">Merhaba ana hedef boyutlandırma yönergeleri izleyerek hello uygun şekilde oluşturun:</span><span class="sxs-lookup"><span data-stu-id="387cf-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="387cf-128">**RAM**: 6 GB veya daha fazla</span><span class="sxs-lookup"><span data-stu-id="387cf-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="387cf-129">**İşletim sistemi disk boyutu**: 100 GB veya daha fazla (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="387cf-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="387cf-130">**Saklama sürücüsünün için ek disk boyutu**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="387cf-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="387cf-131">**CPU çekirdekleri**: 4 çekirdek ya da daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="387cf-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="387cf-132">Merhaba aşağıdaki tekrar desteklenen Ubuntu desteklenir.</span><span class="sxs-lookup"><span data-stu-id="387cf-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="387cf-133">Çekirdek serisi</span><span class="sxs-lookup"><span data-stu-id="387cf-133">Kernel Series</span></span>  |<span data-ttu-id="387cf-134">Yukarı çok desteği</span><span class="sxs-lookup"><span data-stu-id="387cf-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="387cf-135">4.4</span><span class="sxs-lookup"><span data-stu-id="387cf-135">4.4</span></span>      |<span data-ttu-id="387cf-136">4.4.0-81-Generic</span><span class="sxs-lookup"><span data-stu-id="387cf-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="387cf-137">4.8</span><span class="sxs-lookup"><span data-stu-id="387cf-137">4.8</span></span>      |<span data-ttu-id="387cf-138">4.8.0-56-Generic</span><span class="sxs-lookup"><span data-stu-id="387cf-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="387cf-139">4.10</span><span class="sxs-lookup"><span data-stu-id="387cf-139">4.10</span></span>     |<span data-ttu-id="387cf-140">4.10.0-24-Generic</span><span class="sxs-lookup"><span data-stu-id="387cf-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="387cf-141">Merhaba ana hedef sunucusu dağıtma</span><span class="sxs-lookup"><span data-stu-id="387cf-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="387cf-142">Ubuntu 16.04.2 yükleme en az</span><span class="sxs-lookup"><span data-stu-id="387cf-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="387cf-143">Merhaba adımları tooinstall hello Ubuntu 16.04.2 64-bit işletim sistemi aşağıdaki hello alın.</span><span class="sxs-lookup"><span data-stu-id="387cf-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="387cf-144">**1. adım:** Git toohello [bağlantı karşıdan](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) ve hello en yakın yansıtma seçin, bir Ubuntu 16.04.2 en az 64-bit ISO indirme alanından.</span><span class="sxs-lookup"><span data-stu-id="387cf-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="387cf-145">Merhaba DVD sürücüsüne bir Ubuntu 16.04.2 en az 64-bit ISO tutmak ve hello sistem başlatın.</span><span class="sxs-lookup"><span data-stu-id="387cf-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="387cf-146">**2. adım:** seçin **İngilizce** tercih edilen dili ve ardından olarak **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Dil Seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="387cf-148">**3. adım:** seçin **yükleme Ubuntu Server**ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Ubuntu Server yüklemesi seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="387cf-150">**4. adım:** seçin **İngilizce** tercih edilen dili ve ardından olarak **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![İngilizce tercih ettiğiniz dili seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="387cf-152">**5. adım:** seçin hello hello uygun seçeneği **saat dilimi** Seçenekler listesinde ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Merhaba doğru saat dilimini seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="387cf-154">**6. adım:** seçin **Hayır** (varsayılan seçenek hello) ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Merhaba klavye yapılandırın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="387cf-156">**7. adım:** seçin **İngilizce (ABD)** gibi hello hello klavye kaynak ülke ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![ABD kaynak hello ülkeyi seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="387cf-158">**8. adım:** seçin **İngilizce (ABD)** hello klavye düzeni ve ardından olarak **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![ABD İngilizcesi hello klavye düzeni seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="387cf-160">**9. adım:** sunucunuzun hello için hello ana bilgisayar adı girin **ana bilgisayar adı** kutusuna ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="387cf-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Sunucunuz için Hello ana bilgisayar adı girin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="387cf-162">**10. adım:** toocreate bir kullanıcı hesabı hello kullanıcı adı girin ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="387cf-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Bir kullanıcı hesabı oluşturun](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="387cf-164">**11. adım:** hello yeni kullanıcı hesabının hello parolasını girin ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="387cf-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Merhaba parolayı girin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="387cf-166">**12. adım:** hello hello yeni bir kullanıcı parolasını onaylayın ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="387cf-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Merhaba parolaları onaylayın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="387cf-168">**13. adım:** seçin **Hayır** (varsayılan seçenek hello) ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Kullanıcılar ve parolaları ayarlama](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="387cf-170">**14. adım:** görüntülenen hello saat dilimi doğru ise, seçin **Evet** (varsayılan seçenek hello) ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="387cf-171">tooreconfigure seçin, saat dilimi **Hayır**.</span><span class="sxs-lookup"><span data-stu-id="387cf-171">tooreconfigure your time zone, select **No**.</span></span>

![Başlangıç saati yapılandırın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="387cf-173">**15. adım:** bölümleme yöntemi seçenekleri hello seçin **destekli - tüm disk kullanmak**ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Yöntem seçeneği bölümleme hello seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="387cf-175">**16. adım:** seçin hello hello uygun diskten **seçin disk toopartition** seçenekleri ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Başlangıç diski seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="387cf-177">**17. adım:** seçin **Evet** toowrite hello değişiklikleri toodisk ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Merhaba değişiklikleri toodisk yazma](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="387cf-179">**Adım 18:** hello varsayılan seçeneği seçin, **devam**ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Merhaba varsayılan seçeneği seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="387cf-181">**19. adım:** hello sisteminizdeki yükseltmeler yönetmek için uygun seçeneği belirleyin ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Yükseltme nasıl toomanage seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="387cf-183">Hello Azure Site Recovery ana hedef sunucusu hello Ubuntu çok belirli bir sürümünü gerektirdiğinden, tooensure hello sanal makine için yükseltme devre dışı bırakıldı, hello çekirdek gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="387cf-184">Etkinleştirilirse, normal bir yükseltme hello ana hedef sunucusu toomalfunction neden.</span><span class="sxs-lookup"><span data-stu-id="387cf-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="387cf-185">Merhaba seçtiğinizden emin olun **otomatik güncelleştirme** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="387cf-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="387cf-186">**20. adım:** varsayılan seçenekleri seçin.</span><span class="sxs-lookup"><span data-stu-id="387cf-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="387cf-187">SSH bağlantısı için openSSH istiyorsanız hello seçin **OpenSSH server** seçeneğini ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="387cf-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Yazılımı seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="387cf-189">**21. adım:** seçin **Evet**ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Yükleme oturumu hello kaz önyükleme yükleyicisi](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="387cf-191">**22. adım:** seçin hello hello önyükleme yükleyicisi yükleme için uygun aygıt (tercihen **/dev/sda**) ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="387cf-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Önyükleme yükleyicisi yükleme için bir cihaz seçin](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="387cf-193">**23. adım:** seçin **devam**ve ardından **Enter** toofinish hello yükleme.</span><span class="sxs-lookup"><span data-stu-id="387cf-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Merhaba yüklemeyi tamamlama](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="387cf-195">Hello yükleme tamamlandıktan sonra toohello VM hello yeni kullanıcı kimlik bilgileriyle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="387cf-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="387cf-196">(Çok başvuran**adım 10** daha fazla bilgi için.)</span><span class="sxs-lookup"><span data-stu-id="387cf-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="387cf-197">Ekran tooset hello kök aşağıdaki hello açıklanan hello kullanıcı parolası adımlar.</span><span class="sxs-lookup"><span data-stu-id="387cf-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="387cf-198">Ardından kök kullanıcı olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="387cf-198">Then sign in as ROOT user.</span></span>

![Merhaba kök kullanıcı parolasını ayarlayın](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="387cf-200">Merhaba makine yapılandırması için bir ana hedef sunucusu olarak hazırlama</span><span class="sxs-lookup"><span data-stu-id="387cf-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="387cf-201">Ardından, bir ana hedef sunucusu gibi hello makine yapılandırması için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="387cf-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="387cf-202">bir Linux sanal makinedeki her bir SCSI sabit disk için tooget hello ID'yi etkinleştirmek hello **disk. EnableUUID = TRUE** parametre.</span><span class="sxs-lookup"><span data-stu-id="387cf-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="387cf-203">Bu parametre, Al hello aşağıdaki adımları tooenable:</span><span class="sxs-lookup"><span data-stu-id="387cf-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="387cf-204">Sanal makineyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="387cf-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="387cf-205">Merhaba sanal makine hello sol bölmede Hello girişini sağ tıklatın ve ardından **ayarlarını Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="387cf-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="387cf-206">Select hello **seçenekleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="387cf-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="387cf-207">Merhaba sol bölmesinde seçin **Gelişmiş** > **genel**seçip hello **yapılandırma parametrelerini** hello hello ekranın sağ alt bölümünün düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="387cf-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Seçenekler sekmesi](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="387cf-209">Merhaba **yapılandırma parametrelerini** seçeneği kullanılamaz hello makine çalışırken.</span><span class="sxs-lookup"><span data-stu-id="387cf-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="387cf-210">Bu sekme etkin toomake hello sanal makineyi kapatın.</span><span class="sxs-lookup"><span data-stu-id="387cf-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="387cf-211">Olan bir satır olup olmadığını görmek **disk. EnableUUID** zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="387cf-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="387cf-212">Başlangıç değeri varsa ve çok ayarlanır**False**, hello değeri çok değiştirmek**doğru**.</span><span class="sxs-lookup"><span data-stu-id="387cf-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="387cf-213">(Merhaba değerleri büyük küçük harfe duyarlı değildir.)</span><span class="sxs-lookup"><span data-stu-id="387cf-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="387cf-214">Başlangıç değeri varsa ve çok ayarlanır**True**seçin **iptal**.</span><span class="sxs-lookup"><span data-stu-id="387cf-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="387cf-215">Merhaba değer yoksa seçin **Satır Ekle**.</span><span class="sxs-lookup"><span data-stu-id="387cf-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="387cf-216">Merhaba Ad sütununda eklemek **disk. EnableUUID**ve ardından hello değeri çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="387cf-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![Olup olmadığını denetleme disk. EnableUUID zaten var.](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="387cf-218">Çekirdek yükseltmeler devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="387cf-218">Disable kernel upgrades</span></span>

<span data-ttu-id="387cf-219">Azure Site Recovery ana hedef sunucusu hello Ubuntu çok belirli bir sürümünü gerektirir, hello çekirdek yükseltmeler hello sanal makine için devre dışı emin olun.</span><span class="sxs-lookup"><span data-stu-id="387cf-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="387cf-220">Çekirdek yükseltmeler etkinleştirilirse, normal bir yükseltme hello ana hedef sunucusu toomalfunction neden.</span><span class="sxs-lookup"><span data-stu-id="387cf-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="387cf-221">İndirme ve ek paketler yükleme</span><span class="sxs-lookup"><span data-stu-id="387cf-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="387cf-222">Internet bağlantısı toodownload varsa ve ek paketler yükleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="387cf-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="387cf-223">Internet bağlantısı yoksa, toomanually gereken bu RPM paketleri bulun ve bunları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="387cf-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="387cf-224">Kurulum için Hello yükleyici Al</span><span class="sxs-lookup"><span data-stu-id="387cf-224">Get hello installer for setup</span></span>

<span data-ttu-id="387cf-225">Ana hedef Internet bağlantısı varsa, aşağıdaki adımları toodownload hello yükleyici hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="387cf-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="387cf-226">Aksi takdirde hello yükleyici hello işlem sunucusundan kopyalayın ve ardından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="387cf-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="387cf-227">Merhaba ana hedef yükleme paketleri indirin</span><span class="sxs-lookup"><span data-stu-id="387cf-227">Download hello master target installation packages</span></span>

<span data-ttu-id="387cf-228">[Merhaba son Linux ana hedef yükleme BITS karşıdan yükleme](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="387cf-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="387cf-229">toodownload Linux, türü kullanarak:</span><span class="sxs-lookup"><span data-stu-id="387cf-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="387cf-230">Karşıdan yükle ve giriş dizininizde hello yükleyici sıkıştırmasını emin olun.</span><span class="sxs-lookup"><span data-stu-id="387cf-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="387cf-231">Çok sıkıştırmasını açın,**/usr/yerel**, sonra da hello yükleme başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="387cf-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="387cf-232">Merhaba işlem sunucusundan erişim hello yükleyici</span><span class="sxs-lookup"><span data-stu-id="387cf-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="387cf-233">Merhaba işlem sunucusunda çok Git**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="387cf-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="387cf-234">Merhaba işlem sunucusundan Hello gerekli yükleyici dosyasını kopyalayın ve kaydedileceği **latestlinuxmobsvc.tar.gz** giriş dizininizdeki.</span><span class="sxs-lookup"><span data-stu-id="387cf-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="387cf-235">Özel yapılandırma değişikliklerini uygula</span><span class="sxs-lookup"><span data-stu-id="387cf-235">Apply custom configuration changes</span></span>

<span data-ttu-id="387cf-236">tooapply özel yapılandırma değişiklikleri, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="387cf-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="387cf-237">Aşağıdaki komut toountar hello ikili hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="387cf-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Merhaba komutu toorun ekran görüntüsü](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="387cf-239">Çalışma hello aşağıdaki toogive izni komutu.</span><span class="sxs-lookup"><span data-stu-id="387cf-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="387cf-240">Toorun hello komut aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="387cf-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="387cf-241">Yalnızca bir kez Hello betik hello sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="387cf-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="387cf-242">Merhaba sunucuyu kapatın.</span><span class="sxs-lookup"><span data-stu-id="387cf-242">Shut down hello server.</span></span> <span data-ttu-id="387cf-243">Bir disk ekledikten sonra ardından hello sunucu hello sonraki bölümde açıklandığı gibi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="387cf-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="387cf-244">Bir bekletme disk toohello Linux ana hedef sanal makine Ekle</span><span class="sxs-lookup"><span data-stu-id="387cf-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="387cf-245">Aşağıdaki adımları toocreate saklama diskinin hello kullan:</span><span class="sxs-lookup"><span data-stu-id="387cf-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="387cf-246">Yeni bir 1 TB disk toohello Linux ana hedef sanal makine ekleyin ve sonra hello makine başlatın.</span><span class="sxs-lookup"><span data-stu-id="387cf-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="387cf-247">Kullanım hello **çok yollu -üm** toolearn hello çok yollu kimliği hello saklama diskinin komutu.</span><span class="sxs-lookup"><span data-stu-id="387cf-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![Merhaba saklama diskinin Hello çok yollu kimliği](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="387cf-249">Merhaba sürücüyü biçimlendirmek ve ardından bir dosya sistemi hello yeni sürücüde oluşturun.</span><span class="sxs-lookup"><span data-stu-id="387cf-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Merhaba sürücüsünde bir dosya sistemi oluşturma](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="387cf-251">Merhaba dosya sistemi oluşturduktan sonra hello saklama diskinin bağlayın.</span><span class="sxs-lookup"><span data-stu-id="387cf-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Bağlama hello saklama diskinin](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="387cf-253">Merhaba oluşturma **fstab** hello sistem her başlatıldığında giriş toomount hello bekletme sürücüsü.</span><span class="sxs-lookup"><span data-stu-id="387cf-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="387cf-254">Seçin **Ekle** hello dosyasını düzenleyerek toobegin.</span><span class="sxs-lookup"><span data-stu-id="387cf-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="387cf-255">Yeni bir satır oluşturun ve ardından metin aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="387cf-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="387cf-256">Merhaba disk çok yollu kimliği vurgulanmış hello çok yollu kimliği hello önceki komutundan göre düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="387cf-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="387cf-257">** /dev/Eşleyici/ <Retention disks multipath id> /mnt/bekletme ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="387cf-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="387cf-258">Seçin **Esc**ve ardından **: wq** (yazma ve çıkın) tooclose hello Düzenleyicisi penceresini.</span><span class="sxs-lookup"><span data-stu-id="387cf-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="387cf-259">Merhaba ana hedef yükleyin</span><span class="sxs-lookup"><span data-stu-id="387cf-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="387cf-260">Merhaba ana hedef sunucusu Hello sürümü eşit tooor önceki sürümlerinden hello hello işlem sunucusu ve hello yapılandırma sunucusu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="387cf-261">Bu koşul karşılanmazsa, yeniden koruma başarılı olur, ancak çoğaltma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="387cf-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="387cf-262">Merhaba ana hedef sunucusunu yüklemeden önce bu hello denetleyin **/etc/hosts** dosya hello sanal makinedeki tüm ağ bağdaştırıcıları ile ilişkili hello yerel ana bilgisayar adı toohello IP adreslerini eşlemek giriş içerir.</span><span class="sxs-lookup"><span data-stu-id="387cf-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="387cf-263">Merhaba parola alanından kopyalama **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** hello yapılandırma sunucusundaki.</span><span class="sxs-lookup"><span data-stu-id="387cf-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="387cf-264">Olarak Kaydet **passphrase.txt** hello çalıştırarak aynı yerel dizine hello komutu aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="387cf-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="387cf-265">Örnek:</span><span class="sxs-lookup"><span data-stu-id="387cf-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="387cf-266">Merhaba yapılandırma sunucunun IP adresini not edin.</span><span class="sxs-lookup"><span data-stu-id="387cf-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="387cf-267">Merhaba sonraki adımda ihtiyaç.</span><span class="sxs-lookup"><span data-stu-id="387cf-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="387cf-268">Komut tooinstall hello ana hedef sunucusu aşağıdaki hello çalıştırın ve hello sunucu hello yapılandırma sunucusuna kaydedin.</span><span class="sxs-lookup"><span data-stu-id="387cf-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="387cf-269">Örnek:</span><span class="sxs-lookup"><span data-stu-id="387cf-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="387cf-270">Merhaba betik tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="387cf-270">Wait until hello script finishes.</span></span> <span data-ttu-id="387cf-271">Merhaba ana hedef başarıyla kaydederse, hello ana hedef üzerinde hello listelenen **Site Recovery altyapısı** hello portal sayfası.</span><span class="sxs-lookup"><span data-stu-id="387cf-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="387cf-272">Merhaba ana hedef etkileşimli bir yükleme kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="387cf-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="387cf-273">Çalışma hello aşağıdaki tooinstall hello ana hedef komutu.</span><span class="sxs-lookup"><span data-stu-id="387cf-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="387cf-274">Merhaba Aracısı rolü için seçin **ana hedef**.</span><span class="sxs-lookup"><span data-stu-id="387cf-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="387cf-275">Yükleme için Hello varsayılan konum seçin ve ardından **Enter** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="387cf-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Ana hedef yüklemesi için varsayılan konumu seçme](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="387cf-277">Merhaba yükleme tamamlandıktan sonra hello yapılandırma sunucusu hello komut satırını kullanarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="387cf-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="387cf-278">Hello hello yapılandırma sunucusu IP adresini not alın.</span><span class="sxs-lookup"><span data-stu-id="387cf-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="387cf-279">Merhaba sonraki adımda ihtiyaç.</span><span class="sxs-lookup"><span data-stu-id="387cf-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="387cf-280">Komut tooinstall hello ana hedef sunucusu aşağıdaki hello çalıştırın ve hello sunucu hello yapılandırma sunucusuna kaydedin.</span><span class="sxs-lookup"><span data-stu-id="387cf-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="387cf-281">Örnek:</span><span class="sxs-lookup"><span data-stu-id="387cf-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="387cf-282">Merhaba betik tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="387cf-282">Wait until hello script finishes.</span></span> <span data-ttu-id="387cf-283">Merhaba ana hedef kayıtlı başarıyla ise, hello ana hedef üzerinde hello listelenen **Site Recovery altyapısı** hello portal sayfası.</span><span class="sxs-lookup"><span data-stu-id="387cf-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="387cf-284">Merhaba ana hedef yükseltme</span><span class="sxs-lookup"><span data-stu-id="387cf-284">Upgrade hello master target</span></span>

<span data-ttu-id="387cf-285">Merhaba yükleyiciyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="387cf-285">Run hello installer.</span></span> <span data-ttu-id="387cf-286">Bu hello aracı hello ana hedefte yüklü otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="387cf-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="387cf-287">tooupgrade, select **Y**.  Merhaba Kurulum tamamlandıktan sonra komutu aşağıdaki hello kullanarak yüklü hello ana hedef hello sürümünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="387cf-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="387cf-288">Bu hello görebilirsiniz **sürüm** alan hello sürüm hello ana hedef sayısını verir.</span><span class="sxs-lookup"><span data-stu-id="387cf-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="387cf-289">VMware araçları hello ana hedef sunucusuna yükleyin</span><span class="sxs-lookup"><span data-stu-id="387cf-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="387cf-290">Böylece hello veri depolarına bulabilir tooinstall VMware araçları hello ana hedefte gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="387cf-291">Merhaba Araçlar yüklü değilse hello yeniden koruma ekran hello veri depolarında listelenmiyor.</span><span class="sxs-lookup"><span data-stu-id="387cf-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="387cf-292">Merhaba VMware araçları yüklendikten sonra toorestart gerekir.</span><span class="sxs-lookup"><span data-stu-id="387cf-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="387cf-293">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="387cf-293">Next steps</span></span>
<span data-ttu-id="387cf-294">Merhaba yükleme ve kaydetme hello ana hedefinin finsihed olduğunda hello ana hedef üzerinde hello görünür görebilirsiniz **ana hedef** bölümüne **Site Recovery altyapısı**, hello altında yapılandırma sunucusu genel bakış.</span><span class="sxs-lookup"><span data-stu-id="387cf-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="387cf-295">Şimdi devam edebilmeniz [yükü](site-recovery-how-to-reprotect.md), ardından yeniden çalışma.</span><span class="sxs-lookup"><span data-stu-id="387cf-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="387cf-296">Genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="387cf-296">Common issues</span></span>

* <span data-ttu-id="387cf-297">Bir ana hedef gibi tüm yönetim bileşenleri üzerinde depolama VMotion'ı kapatmanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="387cf-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="387cf-298">Merhaba ana hedef sonra başarılı bir yeniden koruma taşınırsa hello sanal makine disklerini (VMDKs) ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="387cf-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="387cf-299">Bu durumda, yeniden çalışma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="387cf-299">In this case, failback fails.</span></span>

* <span data-ttu-id="387cf-300">Merhaba ana hedef tüm anlık görüntüleri hello sanal makineye sahip olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="387cf-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="387cf-301">Anlık görüntüler varsa, yeniden çalışma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="387cf-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="387cf-302">Toosome özel NIC yapılandırmaları bazı müşterilerin en son başlatma sırasında hello ağ arabirimi devre dışıdır ve hello ana hedef Aracısı başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="387cf-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="387cf-303">Aşağıdaki özelliklere bu hello doğru ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="387cf-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="387cf-304">Bu özellikler hello Ethernet, dosyanın /etc/sysconfig/network-scripts/ifcfg kartı denetleyin-eth *.</span><span class="sxs-lookup"><span data-stu-id="387cf-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="387cf-305">BOOTPROTO dhcp =</span><span class="sxs-lookup"><span data-stu-id="387cf-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="387cf-306">ONBOOT = Evet</span><span class="sxs-lookup"><span data-stu-id="387cf-306">ONBOOT=yes</span></span>
