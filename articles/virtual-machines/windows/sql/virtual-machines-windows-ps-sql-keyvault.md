---
title: "Anahtar kasası (Resource Manager) azure'da Windows vm'lerinde SQL Server ile aaaIntegrate | Microsoft Docs"
description: "Nasıl tooautomate hello Azure anahtar kasası ile kullanmak için SQL Server şifreleme yapılandırma hakkında bilgi edinin. Bu konu, SQL Server sanal makinelerle toouse Azure anahtar kasası tümleştirmeyi Resource Manager ile nasıl oluşturulacağını açıklar."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="cb522-104">SQL Server için Azure anahtar kasası tümleştirme Azure sanal makinelerde (Kaynak Yöneticisi) yapılandırın</span><span class="sxs-lookup"><span data-stu-id="cb522-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb522-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cb522-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="cb522-106">Klasik</span><span class="sxs-lookup"><span data-stu-id="cb522-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="cb522-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cb522-107">Overview</span></span>
<span data-ttu-id="cb522-108">Birden çok SQL Server şifreleme özellikleri vardır, gibi [saydam veri şifreleme (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [sütun düzeyinde şifreleme (Temizle)](https://msdn.microsoft.com/library/ms173744.aspx), ve [yedek şifreleme](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb522-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="cb522-109">Bu formlar şifreleme ve şifreleme için kullandığınız hello şifreleme anahtarlarını saklamak toomanage gerektirir.</span><span class="sxs-lookup"><span data-stu-id="cb522-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="cb522-110">Hello Azure anahtar kasası (AKV) hizmeti tasarlanmış tooimprove hello güvenliği ve yönetimi için güvenli ve yüksek oranda kullanılabilir bir konumda Bu anahtarları ' dir.</span><span class="sxs-lookup"><span data-stu-id="cb522-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="cb522-111">Merhaba [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) SQL Server toouse Bu anahtarları Azure anahtar Kasası'ndan sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb522-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="cb522-112">Şirket içi SQL Server çalıştıran, var. makineleri durumunda olan [şirket içi SQL Server makinenizden tooaccess Azure anahtar kasası izlemeniz adımları](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb522-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="cb522-113">Ancak Azure vm'lerinde SQL Server için hello kullanarak zaman kazanabilirsiniz *Azure anahtar kasası tümleştirmeyi* özelliği.</span><span class="sxs-lookup"><span data-stu-id="cb522-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="cb522-114">Bu özellik etkinleştirildiğinde, otomatik olarak yükler hello SQL Server Bağlayıcısı, hello EKM sağlayıcısı tooaccess Azure anahtar kasası yapılandırır ve hello kimlik bilgisi tooallow oluşturur, tooaccess kasanızı.</span><span class="sxs-lookup"><span data-stu-id="cb522-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="cb522-115">Konumundaki görünüyorsa hello hello adımlarda şirket içi belgelerine daha önce bahsedilen, bu özellik adım 2 ve 3 otomatikleştirir görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb522-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="cb522-116">toodo el ile gerekir hello yalnızca toocreate hello anahtar kasasını ve anahtarları şeydir.</span><span class="sxs-lookup"><span data-stu-id="cb522-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="cb522-117">Buradan, hello tüm Kurulum, SQL VM otomatik hale getirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="cb522-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="cb522-118">Bu özellik, bu kurulum tamamlandıktan sonra veritabanları veya yedeklemeler normal olarak şifreleme T-SQL deyimleri toobegin yürütebilir.</span><span class="sxs-lookup"><span data-stu-id="cb522-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="cb522-119">Etkinleştirme ve yapılandırma AKV tümleştirme</span><span class="sxs-lookup"><span data-stu-id="cb522-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="cb522-120">Sağlama sırasında AKV tümleştirme etkinleştirmek veya var olan VM'ler için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cb522-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="cb522-121">Yeni sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="cb522-121">New VMs</span></span>
<span data-ttu-id="cb522-122">Yeni bir SQL Server sanal makine Resource Manager ile sağlıyorsanız, hello Azure portalı adım tooenable Azure anahtar kasası tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb522-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="cb522-123">Hello Azure anahtar kasası özelliği yalnızca hello Enterprise, Developer ve SQL Server, değerlendirme sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cb522-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![SQL Azure Anahtar Kasası Tümleştirme](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="cb522-125">Sağlama ayrıntılı bilgi için bkz [hello Azure Portal'ın SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="cb522-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="cb522-126">Var olan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="cb522-126">Existing VMs</span></span>
<span data-ttu-id="cb522-127">Var olan SQL Server sanal makineler için SQL Server sanal makine seçin.</span><span class="sxs-lookup"><span data-stu-id="cb522-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="cb522-128">Merhaba seçip **SQL Server yapılandırma** hello bölümünü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="cb522-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Var olan VM'ler için SQL AKV tümleştirme](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="cb522-130">Merhaba, **SQL Server yapılandırma** dikey penceresinde hello tıklatın **Düzenle** hello otomatik anahtar kasası tümleştirme bölümü düğmesini.</span><span class="sxs-lookup"><span data-stu-id="cb522-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![SQL AKV tümleştirme var olan VM'ler için yapılandırma](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="cb522-132">Tamamlandığında, hello tıklatın **Tamam** hello hello alt düğmesinde **SQL Server yapılandırma** dikey toosave değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="cb522-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="cb522-133">Bir şablon kullanarak AKV tümleştirme de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb522-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="cb522-134">Daha fazla bilgi için bkz: [Azure anahtar kasası tümleştirme için Azure Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="cb522-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

