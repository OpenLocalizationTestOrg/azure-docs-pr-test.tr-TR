---
title: "Azure Otomasyonu hesabını yönetme | Microsoft Docs"
description: "Bu makalede sertifika yenileme, silme ve yanlış yapılandırılma gibi Otomasyon hesabınızın yapılandırmasını yönetme işlemleri açıklanmaktadır."
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
ms.openlocfilehash: 41efdbcacede74bac038342688362ff480cadc7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-automation-account"></a><span data-ttu-id="bfc1b-103">Azure Otomasyonu hesabını yönetme</span><span class="sxs-lookup"><span data-stu-id="bfc1b-103">Manage Azure Automation account</span></span>
<span data-ttu-id="bfc1b-104">Otomasyon hesabınızın süresi dolmadan önce sertifikayı yenilemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-104">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="bfc1b-105">Farklı Çalıştır hesabının tehlikede olduğunu düşünüyorsanız, hesabı silip yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-105">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="bfc1b-106">Bu bölümde bu işlemlerin nasıl gerçekleştirileceği ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-106">This section discusses how to perform these operations.</span></span>

## <a name="self-signed-certificate-renewal"></a><span data-ttu-id="bfc1b-107">Otomatik olarak imzalanan sertifika yenileme</span><span class="sxs-lookup"><span data-stu-id="bfc1b-107">Self-signed certificate renewal</span></span>
<span data-ttu-id="bfc1b-108">Farklı Çalıştır hesabı için oluşturduğunuz otomatik olarak imzalanan sertifikanın süresi, oluşturulduktan bir yıl sonra dolar.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-108">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="bfc1b-109">Sertifikayı süresi dolmadan önce herhangi bir zamanda yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-109">You can renew it at any time before it expires.</span></span> <span data-ttu-id="bfc1b-110">Sertifikayı yenilediğinizde, sıraya alınmış ya da o anda çalışan ve Farklı Çalıştır hesabı ile kimliği doğrulanmış runbook’ların olumsuz yönde etkilenmemesi için geçerli sertifika saklanır.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-110">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="bfc1b-111">Sertifika, sona erme tarihine kadar geçerliliğini sürdürür.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-111">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="bfc1b-112">Otomasyon Farklı Çalıştır hesabınızı, kuruluş sertifika yetkiliniz tarafından yayınlanan bir sertifika kullanmak üzere yapılandırdıysanız ve bu seçeneği kullanırsanız, kurumsal sertifika otomatik olarak imzalanan bir sertifikayla değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-112">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="bfc1b-113">Sertifikayı yenilemek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="bfc1b-113">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="bfc1b-114">Azure portalında Otomasyon hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-114">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="bfc1b-115">**Otomasyon Hesabı** dikey penceresindeki **Hesap özellikleri** bölmesinin **Hesap Ayarları** altında **Farklı Çalıştır Hesapları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-115">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Otomasyon hesabı özellikleri bölmesi](media/automation-manage-account/automation-account-properties-pane.png)
3. <span data-ttu-id="bfc1b-117">**Farklı Çalıştır Hesapları** özellikleri dikey penceresinde sertifikasını yenilemek istediğiniz Farklı Çalıştır Hesabını veya Klasik Farklı Çalıştır Hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-117">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="bfc1b-118">Seçili hesabın **Özellikler** dikey penceresinde **Sertifikayı yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-118">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Farklı Çalıştır hesabının sertifikasını yenileme](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="bfc1b-120">Sertifika yenilenirken menünün **Bildirimler** öğesi altında ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-120">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

## <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="bfc1b-121">Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını silme</span><span class="sxs-lookup"><span data-stu-id="bfc1b-121">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="bfc1b-122">Bu bölümde bir Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını silip yeniden oluşturma işlemi açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-122">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="bfc1b-123">Bu eylemi gerçekleştirdiğinizde Otomasyon hesabı korunur.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-123">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="bfc1b-124">Farklı Çalıştır veya Klasik Farklı Çalıştır hesabını sildikten sonra Azure portalında yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-124">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="bfc1b-125">Azure portalında Otomasyon hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-125">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="bfc1b-126">**Otomasyon Hesabı** dikey penceresindeki hesap özellikleri bölmesinde **Farklı Çalıştır Hesapları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-126">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="bfc1b-127">**Farklı Çalıştır Hesapları** özellikleri dikey penceresinde silmek istediğiniz Farklı Çalıştır Hesabını veya Klasik Farklı Çalıştır Hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-127">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="bfc1b-128">Ardından, seçili hesabın **Özellikler** dikey penceresinde **Sil**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-128">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Farklı Çalıştır hesabını silme](media/automation-manage-account/automation-account-delete-runas.png)

4. <span data-ttu-id="bfc1b-130">Hesap silinirken menünün **Bildirimler** öğesi altında ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-130">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="bfc1b-131">Hesap silindikten sonra **Farklı Çalıştır Hesapları** özellikler dikey penceresinde **Azure Farklı Çalıştır Hesabı** seçeneğini belirleyerek hesabı yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-131">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Otomasyon Farklı Çalıştır hesabını yeniden oluşturma](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a><span data-ttu-id="bfc1b-133">Yanlış yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bfc1b-133">Misconfiguration</span></span>
<span data-ttu-id="bfc1b-134">İlk kurulum sırasında, Farklı Çalıştır veya Klasik Farklı Çalıştır hesabının düzgün çalışması için gerekli olan bazıları silinmiş veya düzgün oluşturulmamış olabilir.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-134">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="bfc1b-135">Bu öğeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bfc1b-135">The items include:</span></span>

* <span data-ttu-id="bfc1b-136">Sertifika varlığı</span><span class="sxs-lookup"><span data-stu-id="bfc1b-136">Certificate asset</span></span>
* <span data-ttu-id="bfc1b-137">Bağlantı varlığı</span><span class="sxs-lookup"><span data-stu-id="bfc1b-137">Connection asset</span></span>
* <span data-ttu-id="bfc1b-138">Farklı Çalıştır hesabının katkıda bulunan rolünden kaldırılması</span><span class="sxs-lookup"><span data-stu-id="bfc1b-138">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="bfc1b-139">Azure AD'de hizmet sorumlusu veya uygulama</span><span class="sxs-lookup"><span data-stu-id="bfc1b-139">Service principal or application in Azure AD</span></span>

<span data-ttu-id="bfc1b-140">Yanlış yapılandırmanın önceki ve diğer örneklerinde, Otomasyon hesabı değişiklikleri algılar ve hesabın **Farklı Çalıştır Hesapları** özellikleri dikey penceresinde *Tamamlanmadı* durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-140">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![Tamamlanmamış Farklı Çalıştır hesabı yapılandırma durumu](media/automation-manage-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="bfc1b-142">Farklı Çalıştır hesabını seçtiğinizde hesabın **Özellikler** bölmesinde aşağıdaki hata iletisi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="bfc1b-142">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Tamamlanmamış Farklı Çalıştır yapılandırma uyarısı iletisi](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="bfc1b-144">.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-144">.</span></span>

<span data-ttu-id="bfc1b-145">Hesabı silip yeniden oluşturarak Farklı Çalıştır hesabıyla ilgili bu sorunları hızlı bir şekilde çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bfc1b-145">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfc1b-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bfc1b-146">Next steps</span></span>
* <span data-ttu-id="bfc1b-147">Hizmet Sorumluları hakkında daha fazla bilgi için bkz. [Uygulama Nesneleri ve Hizmet Sorumlusu Nesneleri](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="bfc1b-147">For more information about Service Principals, refer to [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="bfc1b-148">Azure Automation’da Rol Tabanlı Erişim Denetimi hakkında daha fazla bilgi için bkz. [Azure Automation’da rol tabanlı erişim denetimi](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="bfc1b-148">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="bfc1b-149">Sertifikalar ve Azure hizmetleri hakkında daha fazla bilgi için bkz. [Azure Cloud Services sertifikalarına genel bakış](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="bfc1b-149">For more information about certificates and Azure services, refer to [Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>