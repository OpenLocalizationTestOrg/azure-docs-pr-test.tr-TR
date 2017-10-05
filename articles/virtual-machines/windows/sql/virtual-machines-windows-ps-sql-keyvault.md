---
title: "Anahtar kasası (Resource Manager) azure'da Windows sanal makineleri üzerinde SQL Server ile tümleştirme | Microsoft Docs"
description: "Azure anahtar kasası ile kullanmak için SQL Server şifrelemesi yapılandırmasını öğrenin. Bu konu, Resource Manager ile oluşturulan SQL Server sanal makineleri ile Azure anahtar kasası tümleştirmeyi kullanımı açıklanmaktadır."
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
ms.openlocfilehash: 32b9564fa5c9ca6864ade343fda309b2c3edf123
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="ff0fd-104">SQL Server için Azure anahtar kasası tümleştirme Azure sanal makinelerde (Kaynak Yöneticisi) yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ff0fd-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff0fd-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ff0fd-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="ff0fd-106">Klasik</span><span class="sxs-lookup"><span data-stu-id="ff0fd-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ff0fd-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ff0fd-107">Overview</span></span>
<span data-ttu-id="ff0fd-108">Birden çok SQL Server şifreleme özellikleri vardır, gibi [saydam veri şifreleme (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [sütun düzeyinde şifreleme (Temizle)](https://msdn.microsoft.com/library/ms173744.aspx), ve [yedek şifreleme](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff0fd-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="ff0fd-109">Bu formlar şifreleme, şifreleme için kullandığınız şifreleme anahtarlarını depolamak ve yönetmek gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-109">These forms of encryption require you to manage and store the cryptographic keys you use for encryption.</span></span> <span data-ttu-id="ff0fd-110">Azure anahtar kasası (AKV) hizmeti bu anahtarların güvenli ve yüksek oranda kullanılabilir bir konumda yönetim ve güvenlik artırmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-110">The Azure Key Vault (AKV) service is designed to improve the security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="ff0fd-111">[SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) SQL Server'ın bu anahtarları Azure anahtar kasası kullanmaya sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-111">The [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server to use these keys from Azure Key Vault.</span></span>

<span data-ttu-id="ff0fd-112">Şirket içi SQL Server çalıştıran, var. makineleri durumunda olan [Azure anahtar kasası, şirket içi SQL Server makineden erişmek için izlemeniz adımları](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff0fd-112">If you running SQL Server with on-premises machines, there are [steps you can follow to access Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="ff0fd-113">Ancak Azure vm'lerinde SQL Server için kullanarak zaman kazanabilirsiniz *Azure anahtar kasası tümleştirmeyi* özelliği.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-113">But for SQL Server in Azure VMs, you can save time by using the *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="ff0fd-114">Bu özellik etkinleştirildiğinde, otomatik olarak SQL Server Bağlayıcısı'nı yükler, Azure anahtar kasası erişmek için EKM sağlayıcısına yapılandırır ve kasanızı erişmesine izin vermek için kimlik bilgisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-114">When this feature is enabled, it automatically installs the SQL Server Connector, configures the EKM provider to access Azure Key Vault, and creates the credential to allow you to access your vault.</span></span> <span data-ttu-id="ff0fd-115">Yukarıda açıklanan şirket içi belgelerindeki adımları sırasında görünüyorsa, bu özellik adım 2 ve 3 otomatikleştirir görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-115">If you looked at the steps in the previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="ff0fd-116">Anahtar kasasını ve anahtarları hala el ile yapmanız gerekir tek şey oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-116">The only thing you would still need to do manually is to create the key vault and keys.</span></span> <span data-ttu-id="ff0fd-117">Buradan, tüm Kurulum, SQL VM otomatik hale getirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-117">From there, the entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="ff0fd-118">Bu özellik, bu kurulum tamamlandıktan sonra veritabanları veya yedeklemeler normal olarak şifreleme başlamak için T-SQL deyimlerini yürütebilir.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-118">Once this feature has completed this setup, you can execute T-SQL statements to begin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="ff0fd-119">Etkinleştirme ve yapılandırma AKV tümleştirme</span><span class="sxs-lookup"><span data-stu-id="ff0fd-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="ff0fd-120">Sağlama sırasında AKV tümleştirme etkinleştirmek veya var olan VM'ler için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="ff0fd-121">Yeni sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="ff0fd-121">New VMs</span></span>
<span data-ttu-id="ff0fd-122">Yeni bir SQL Server sanal makine Resource Manager ile sağlıyorsanız, Azure portalında Azure anahtar kasası tümleştirmeyi etkinleştirmek için bir adım sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, the Azure portal provides a step to enable Azure Key Vault integration.</span></span> <span data-ttu-id="ff0fd-123">Azure anahtar kasası özelliği yalnızca Enterprise, Developer ve değerlendirme sürümleri SQL Server için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-123">The Azure Key Vault feature is available only for the Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![SQL Azure Anahtar Kasası Tümleştirme](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="ff0fd-125">Sağlama ayrıntılı bilgi için bkz [Azure Portal'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ff0fd-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="ff0fd-126">Var olan sanal makineleri</span><span class="sxs-lookup"><span data-stu-id="ff0fd-126">Existing VMs</span></span>
<span data-ttu-id="ff0fd-127">Var olan SQL Server sanal makineler için SQL Server sanal makine seçin.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="ff0fd-128">Ardından **SQL Server yapılandırma** bölümünü **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-128">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Var olan VM'ler için SQL AKV tümleştirme](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="ff0fd-130">İçinde **SQL Server yapılandırma** dikey penceresinde tıklatın **Düzenle** otomatik anahtar kasası tümleştirme bölümdeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-130">In the **SQL Server configuration** blade, click the **Edit** button in the Automated Key Vault integration section.</span></span>

![SQL AKV tümleştirme var olan VM'ler için yapılandırma](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="ff0fd-132">Tamamlandığında, tıklatın **Tamam** alt düğmesinde **SQL Server yapılandırma** yaptığınız değişiklikleri kaydetmek için dikey.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-132">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="ff0fd-133">Bir şablon kullanarak AKV tümleştirme de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff0fd-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="ff0fd-134">Daha fazla bilgi için bkz: [Azure anahtar kasası tümleştirme için Azure Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="ff0fd-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

