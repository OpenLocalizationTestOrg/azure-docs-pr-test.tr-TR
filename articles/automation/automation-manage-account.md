---
title: "Azure Otomasyonu hesabı aaaManage | Microsoft Docs"
description: "Bu makalede nasıl toomanage hello Otomasyon hesabınızın sertifika yenileme, silme ve yanlış yapılandırılması gibi yapılandırma açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="c41bf-103">Azure Otomasyonu hesabını yönetme</span><span class="sxs-lookup"><span data-stu-id="c41bf-103">Manage Azure Automation account</span></span>
<span data-ttu-id="c41bf-104">Belirli bir noktada, Automation hesabınız süresi dolmadan önce toorenew hello sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="c41bf-104">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="c41bf-105">Bu farklı çalıştır hesabı hello tehlikeye düşünüyorsanız, silin ve yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c41bf-105">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="c41bf-106">Bu bölümde ele alınmaktadır nasıl tooperform bu işlemler.</span><span class="sxs-lookup"><span data-stu-id="c41bf-106">This section discusses how tooperform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="c41bf-107">Otomatik olarak imzalanan sertifika yenileme</span><span class="sxs-lookup"><span data-stu-id="c41bf-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="c41bf-108">hello farklı çalıştır hesabı için oluşturulan hello otomatik olarak imzalanan sertifika oluşturma başlangıç tarihinden itibaren bir yıl süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="c41bf-108">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="c41bf-109">Sertifikayı süresi dolmadan önce herhangi bir zamanda yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c41bf-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="c41bf-110">Yenilediğinizde, yukarı veya etkin olarak çalışan sıraya ve bu farklı çalıştır hesabını hello ile kimlik doğrulaması runbook'ları olumsuz etkilenmez tutulan tooensure hello geçerli geçerli sertifika yok.</span><span class="sxs-lookup"><span data-stu-id="c41bf-110">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="c41bf-111">Merhaba sertifika sona erme tarihini kadar geçerli kalır.</span><span class="sxs-lookup"><span data-stu-id="c41bf-111">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="c41bf-112">Automation farklı çalıştır hesabı toouse, kuruluş sertifika yetkiliniz tarafından verilen bir sertifika yapılandırdıktan ve bu seçeneği kullanırsanız, hello Kurumsal Sertifika tarafından otomatik olarak imzalanan bir sertifika kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="c41bf-112">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="c41bf-113">toorenew hello sertifika, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="c41bf-113">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="c41bf-114">Hello Azure portal, hello Automation hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="c41bf-114">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="c41bf-115">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde hello **hesap özellikleri** bölmesi altında **hesap ayarlarını**seçin **farklı çalıştır hesapları**.</span><span class="sxs-lookup"><span data-stu-id="c41bf-115">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Otomasyon hesabı özellikleri bölmesi](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="c41bf-117">Merhaba üzerinde **farklı çalıştır hesapları** ya da hello Çalıştır hesabı veya toorenew hello sertifika için istediğiniz hello Klasik farklı çalıştır hesabı olarak özellikleri dikey penceresinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="c41bf-117">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="c41bf-118">Merhaba üzerinde **özellikleri** hello dikey penceresinde seçili hesabı'na tıklayın **yenileme sertifika**.</span><span class="sxs-lookup"><span data-stu-id="c41bf-118">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Farklı Çalıştır hesabının sertifikasını yenileme](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="c41bf-120">Merhaba sertifika yenileme sırasında altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c41bf-120">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="c41bf-121">Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını silme</span><span class="sxs-lookup"><span data-stu-id="c41bf-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="c41bf-122">Bu bölümde açıklanmıştır nasıl toodelete ve bir farklı çalıştır veya Klasik farklı çalıştır hesabını yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c41bf-122">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="c41bf-123">Bu eylemi gerçekleştirdiğinizde, hello Otomasyon hesabı korunur.</span><span class="sxs-lookup"><span data-stu-id="c41bf-123">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="c41bf-124">Bir farklı çalıştır veya Klasik farklı çalıştır hesabını sildikten sonra hello Azure portalında yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c41bf-124">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="c41bf-125">Hello Azure portal, hello Automation hesabını açın.</span><span class="sxs-lookup"><span data-stu-id="c41bf-125">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="c41bf-126">Merhaba üzerinde **Otomasyon hesabı** dikey penceresinde hello hesap Özellikler bölmesinde, **farklı çalıştır hesapları**.</span><span class="sxs-lookup"><span data-stu-id="c41bf-126">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="c41bf-127">Merhaba üzerinde **farklı çalıştır hesapları** özellikleri dikey penceresinde, seçin ya da hello Çalıştır hesabı veya Klasik farklı çalıştır hesabı toodelete istiyor.</span><span class="sxs-lookup"><span data-stu-id="c41bf-127">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="c41bf-128">Ardından, hello **özellikleri** hello dikey penceresinde seçili hesabı'na tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="c41bf-128">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Farklı Çalıştır hesabını silme](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="c41bf-130">Merhaba hesap silindi, ancak altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="c41bf-130">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="c41bf-131">Merhaba hesabı silindikten sonra bunu hello üzerinde yeniden oluşturabilirsiniz **farklı çalıştır hesapları** hello seçerek özellikler dikey penceresini oluşturma seçeneği **Azure farklı çalıştır hesabını**.</span><span class="sxs-lookup"><span data-stu-id="c41bf-131">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Merhaba Automation farklı çalıştır hesabını yeniden oluşturun](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="c41bf-133">Yanlış yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c41bf-133">Misconfiguration</span></span>
<span data-ttu-id="c41bf-134">Merhaba Çalıştır veya Klasik farklı çalıştır hesabı toofunction için gereken bazı yapılandırma öğeleri düzgün silinmiş veya yanlış ilk kurulum sırasında oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c41bf-134">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="c41bf-135">Merhaba öğeleri içerir:</span><span class="sxs-lookup"><span data-stu-id="c41bf-135">hello items include:</span></span>

* <span data-ttu-id="c41bf-136">Sertifika varlığı</span><span class="sxs-lookup"><span data-stu-id="c41bf-136">Certificate asset</span></span>
* <span data-ttu-id="c41bf-137">Bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="c41bf-137">Connection asset</span></span>
* <span data-ttu-id="c41bf-138">Farklı Çalıştır hesabı hello katkıda bulunan rolü ' kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="c41bf-138">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="c41bf-139">Azure AD'de hizmet sorumlusu veya uygulama</span><span class="sxs-lookup"><span data-stu-id="c41bf-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="c41bf-140">Hello önceki ve diğer örnekleri yanlış hello Otomasyon hesabı hello değiştirir ve durumunu görüntüler algılar *tamamlanmamış* hello üzerinde **farklı çalıştır hesapları** hello özellikleri dikey penceresi hesabı.</span><span class="sxs-lookup"><span data-stu-id="c41bf-140">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![Tamamlanmamış Farklı Çalıştır hesabı yapılandırma durumu](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="c41bf-142">Merhaba farklı çalıştır hesabı seçin, hesap hello **özellikleri** bölmesi hello aşağıdaki hata iletisini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="c41bf-142">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Tamamlanmamış Farklı Çalıştır yapılandırma uyarısı iletisi](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="c41bf-144">.</span><span class="sxs-lookup"><span data-stu-id="c41bf-144">.</span></span>

<span data-ttu-id="c41bf-145">Bu farklı çalıştır hesabı sorunları hızla, silme ve hello hesabını yeniden oluşturmayı da çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c41bf-145">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c41bf-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c41bf-146">Next steps</span></span>
* <span data-ttu-id="c41bf-147">Hizmet sorumluları hakkında daha fazla bilgi için çok başvuran[uygulama ve hizmet sorumlusu nesneleri](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="c41bf-147">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="c41bf-148">Azure automation'da rol tabanlı erişim denetimi hakkında daha fazla bilgi için çok başvuran[Azure automation'da rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="c41bf-148">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="c41bf-149">Sertifikalar ve Azure hizmetleri hakkında daha fazla bilgi için çok başvuran[Azure Cloud Services sertifikalarına genel bakış](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="c41bf-149">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
