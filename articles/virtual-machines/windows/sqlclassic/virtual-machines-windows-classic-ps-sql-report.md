---
title: aaaUse PowerShell tooCreate bir VM ile bir yerel moddaki bir rapor sunucusunda | Microsoft Docs
description: "Bu konuda açıklar ve hello dağıtımını ve SQL Server Reporting Services yerel mod rapor sunucusu bir Azure sanal makine yapılandırmasını size yol göstermektedir. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="e5ee4-103">Bir Azure VM ile bir yerel moddaki bir rapor sunucusunda PowerShell tooCreate kullanın</span><span class="sxs-lookup"><span data-stu-id="e5ee4-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="e5ee4-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e5ee4-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e5ee4-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="e5ee4-107">Bu konuda açıklar ve hello dağıtımını ve SQL Server Reporting Services yerel mod rapor sunucusu bir Azure sanal makine yapılandırmasını size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="e5ee4-108">Merhaba bu belgeyi kullanımda el ile yapılacak adımlar toocreate hello sanal makine ve bir Windows PowerShell Betiği bileşimini hello VM üzerinde tooconfigure Reporting Services adımları.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="e5ee4-109">HTTP veya HTTPs için bir güvenlik duvarı bağlantı noktası açma Hello yapılandırma komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="e5ee4-110">Gerekli olmadığı, **HTTPS** hello rapor sunucusunda **2. adıma geçin**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="e5ee4-111">1. adımda Hello VM oluşturduktan sonra toohello bölüm kullan betik tooconfigure hello report server ve HTTP gidin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="e5ee4-112">Merhaba betiği çalıştırdıktan sonra hello rapor hazır toouse sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="e5ee4-113">Önkoşullar ve varsayımlar</span><span class="sxs-lookup"><span data-stu-id="e5ee4-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="e5ee4-114">**Azure aboneliği**: hello Azure aboneliğinizde kullanılabilir çekirdek sayısı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="e5ee4-115">VM boyutu önerilen hello oluşturursanız **A3**, gereksinim duyduğunuz **4** kullanılabilir çekirdekler.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="e5ee4-116">Bir VM boyutu kullanırsanız **A2**, gereksinim duyduğunuz **2** kullanılabilir çekirdekler.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="e5ee4-117">tooverify hello çekirdek hello Klasik Azure portalı, aboneliğinizde sınırının tıklayın ayarları hello sol bölmesinde ve sonra tıklatın kullanım hello üst menüde.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="e5ee4-118">tooincrease hello çekirdek kotası, kişi [Azure Destek](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="e5ee4-119">VM boyutu bilgi için bkz: [Azure için sanal makine boyutlarını](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="e5ee4-120">**Windows PowerShell komut dosyası**: hello konu Windows PowerShell temel bilgiye sahip olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="e5ee4-121">Windows PowerShell'i kullanma hakkında daha fazla bilgi için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="e5ee4-122">Windows Server'da Windows PowerShell'i başlatma</span><span class="sxs-lookup"><span data-stu-id="e5ee4-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="e5ee4-123">Windows PowerShell ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e5ee4-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="e5ee4-124">1. adım: bir Azure sanal makine sağlama</span><span class="sxs-lookup"><span data-stu-id="e5ee4-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="e5ee4-125">Toohello Klasik Azure portalına göz atın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="e5ee4-126">Tıklatın **sanal makineleri** hello sol bölmede.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![Microsoft azure sanal makineler](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="e5ee4-128">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-128">Click **New**.</span></span>
   
    ![Yeni düğmesi](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="e5ee4-130">Tıklatın **galerisinden**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-130">Click **From Gallery**.</span></span>
   
    ![Galeriden yeni vm](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="e5ee4-132">Tıklatın **SQL Server 2014 RTM Standard – Windows Server 2012 R2** ve hello ok toocontinue'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![ileri](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="e5ee4-134">Merhaba Reporting Services veri abonelikleri özelliği tabanlı gerek duyuyorsanız, **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="e5ee4-135">SQL Server sürümleri ve özellik desteği hakkında daha fazla bilgi için bkz: [hello SQL Server 2012 sürümleri tarafından desteklenen özellikler](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="e5ee4-136">Merhaba üzerinde **sanal makine yapılandırması** sayfasında, aşağıdaki alanları hello düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="e5ee4-137">Varsa birden fazla **sürüm yayın tarihi**, hello en son sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="e5ee4-138">**Sanal makine adı**: hello makine adı hello sonraki yapılandırma sayfasında da hello varsayılan bulut hizmeti DNS adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="e5ee4-139">Merhaba DNS adı hello Azure hizmeti arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="e5ee4-140">Merhaba VM VM için kullanılan hangi hello açıklayan bir bilgisayar adıyla yapılandırmayı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="e5ee4-141">Örneğin ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="e5ee4-142">**Katman**: standart</span><span class="sxs-lookup"><span data-stu-id="e5ee4-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="e5ee4-143">**Boyutu: A3** hello VM boyutu SQL Server iş yükleri için önerilir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="e5ee4-144">Bir VM yalnızca bir rapor sunucusu olarak kullanılıyorsa, büyük bir iş yükü hello rapor sunucusu karşılaştığında sürece, A2 VM boyutunu yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="e5ee4-145">VM fiyatlandırma bilgileri için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="e5ee4-146">**Yeni bir kullanıcı adı**: sağladığınız hello adı hello VM üzerinde bir yönetici olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="e5ee4-147">**Yeni parola** ve **onaylayın**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="e5ee4-148">Bu parola hello yeni yönetici hesabı için kullanılır ve güçlü bir parola kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="e5ee4-149">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-149">Click **Next**.</span></span> <span data-ttu-id="e5ee4-150">![sonraki](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="e5ee4-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="e5ee4-151">Merhaba sonraki sayfada, alanları izleyen hello düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="e5ee4-152">**Bulut hizmeti**: seçin **yeni bir bulut hizmeti oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="e5ee4-153">**Bulut hizmeti DNS adı**: hello Genel DNS adını hello hello VM ile ilişkili bir bulut hizmeti budur.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="e5ee4-154">Merhaba varsayılan adı hello VM adı için yazdığınız hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="e5ee4-155">Hello konu daha sonraki adımlarda güvenilir bir SSL sertifikası oluşturun ve sonra hello DNS adı hello hello değerini kullanılıyorsa "**verilen**" Merhaba sertifika.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="e5ee4-156">**Bölge/benzeşim grubu/sanal ağ**: hello bölgeye en yakın tooyour son kullanıcılar'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="e5ee4-157">**Depolama hesabı**: otomatik olarak oluşturulan depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="e5ee4-158">**Kullanılabilirlik kümesi**: yok.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="e5ee4-159">**Uç noktaları** Koru hello **Uzak Masaüstü** ve **PowerShell** uç noktaları ve HTTP veya HTTPS uç noktası, ortamınıza bağlı olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="e5ee4-160">**HTTP**: Merhaba ortak ve özel bağlantı noktaları varsayılan **80**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="e5ee4-161">Özel bir bağlantı noktası 80 dışında kullanırsanız değiştirme Not **$HTTPport = 80** hello http komut.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="e5ee4-162">**HTTPS**: Merhaba ortak ve özel bağlantı noktaları varsayılan **443**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="e5ee4-163">En iyi güvenlik uygulaması toochange hello özel bağlantı noktası ve, güvenlik duvarı ve hello rapor sunucusu toouse hello özel bağlantı noktası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="e5ee4-164">Uç noktalar hakkında daha fazla bilgi için bkz: [nasıl tooSet bir sanal makine ile iletişim kurma](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="e5ee4-165">Bir bağlantı noktası 443 dışındaki kullanıyorsanız, hello parametre değiştirme Not **$HTTPsport = 443** hello HTTPS komut dosyası olarak.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="e5ee4-166">İleri'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-166">Click next .</span></span> ![ileri](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="e5ee4-168">Merhaba son sayfasında hello Sihirbazı'nın hello varsayılan tutmak **hello VM aracı yükleme** seçili.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="e5ee4-169">Merhaba bu konudaki adımları hello VM Aracısı kullanan değil, ancak bu VM tookeep planlıyorsanız, hello VM aracısı ve uzantılar tooenhance sağlayacak he CM.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="e5ee4-170">Merhaba VM Aracısı hakkında daha fazla bilgi için bkz: [VM aracısı ve uzantılar – Kısım 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="e5ee4-171">Merhaba varsayılan yüklü uzantıları ad çalıştıran biri hello VM masaüstündeki görüntüleyen hello "BGINFO" uzantısı, sistem bilgi ve ücretsiz iç IP gibi sürücü alanı.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="e5ee4-172">Tamamlandı'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-172">Click complete .</span></span> ![Tamam](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="e5ee4-174">Merhaba **durum** VM görüntüler olarak Merhaba, **başlangıç (hazırlama)** hello sağlama işlemi ve ardından görüntüler olarak sırasında **çalıştıran** sağlanmıştır ve kullanıma hazırdır hello VM olduğunda toouse.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="e5ee4-175">2. adım: bir sunucu sertifikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5ee4-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="e5ee4-176">Merhaba rapor sunucusunda HTTPS ihtiyacınız yoksa, şunları yapabilirsiniz **2. adıma geçin** ve toohello bölümüne gidin **betik tooconfigure hello rapor sunucusu ve HTTP kullanma**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="e5ee4-177">Kullanım hello HTTP betik tooquickly hello report server ve hello rapor sunucusu hazır toouse olacak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="e5ee4-178">Sipariş toouse içinde HTTPS hello VM üzerinde güvenilir bir SSL sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="e5ee4-179">Senaryonuza bağlı olarak, hello aşağıdaki iki yöntemden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="e5ee4-180">Geçerli bir SSL sertifikası bir sertifika yetkilisi (CA) tarafından verilen ve Microsoft tarafından güvenilen.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="e5ee4-181">Merhaba CA kök sertifikaları Microsoft kök sertifikası programı hello dağıtılmış gerekli toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="e5ee4-182">Bu program hakkında daha fazla bilgi için bkz: [Windows ve Windows Phone 8 SSL kök sertifika programı (üye CA'lar)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) ve [giriş toohello Microsoft kök sertifikası programı](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="e5ee4-183">Kendinden imzalı bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-183">A self-signed certificate.</span></span> <span data-ttu-id="e5ee4-184">Otomatik olarak imzalanan sertifikalar üretim ortamları için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="e5ee4-185">toouse bir güvenilen sertifika yetkilisi (CA) tarafından oluşturulan bir sertifika</span><span class="sxs-lookup"><span data-stu-id="e5ee4-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="e5ee4-186">**Bir sertifika yetkilisinden hello Web sitesi için bir sunucu sertifikası isteği**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="e5ee4-187">Merhaba Web Sunucusu Sertifika Sihirbazı ya da toogenerate tooa sertifika yetkilisi veya toogenerate bir çevrimiçi sertifika yetkilisi için bir istek göndermek bir sertifika isteği dosyasını (Certreq.txt) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="e5ee4-188">Örneğin, Microsoft Sertifika Hizmetleri Windows Server 2012'de.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="e5ee4-189">Sunucu sertifikanızı tarafından sunulan kimlik güvence düzeyini Merhaba, bağlı olarak birkaç gün tooseveral ay hello sertifika yetkilisi tooapprove için isteğiniz olduğundan ve bir sertifika dosyası Gönder.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="e5ee4-190">Sunucu sertifikaları isteme hakkında daha fazla bilgi için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="e5ee4-191">Kullanım [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="e5ee4-192">Güvenlik araçları tooAdminister Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="e5ee4-193">Güvenlik araçları tooAdminister Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e5ee4-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="e5ee4-194">Merhaba **verilen** hello alanının güvenilir SSL sertifikası olması hello aynı hello **bulut hizmeti DNS adı** sizin için kullanılan yeni VM hello.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="e5ee4-195">**Merhaba sunucu sertifikası hello Web sunucusuna yükleyin**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="e5ee4-196">Merhaba Web bu durumda hello ana rapor sunucusu hello ve Reporting Services yapılandırdığınızda, sonraki adımlarda hello Web sitesi oluşturulur VM sunucusudur.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="e5ee4-197">Merhaba sertifika MMC ek bileşenini kullanarak hello Web sunucusunda hello sunucu sertifikası yükleme hakkında daha fazla bilgi için bkz: [sunucu sertifikasını yüklemeniz](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="e5ee4-198">Bu konuda tooconfigure hello rapor sunucusu dahil toouse hello betik istiyorsanız hello sertifikaları değerini hello **parmak izi** hello komut parametresi olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="e5ee4-199">Ayrıntılar için sonraki bölüme Hello nasıl tooobtain hello üzerinde hello sertifikanın parmak izini bakın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="e5ee4-200">Merhaba sertifika toohello rapor sunucusu atayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="e5ee4-201">Merhaba rapor sunucusunu yapılandırdığınızda hello atama hello sonraki bölümde tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="e5ee4-202">toouse hello sanal makineleri otomatik olarak imzalanan sertifika</span><span class="sxs-lookup"><span data-stu-id="e5ee4-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="e5ee4-203">Merhaba VM hazırlandığında kendinden imzalı bir sertifika hello VM üzerinde oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="e5ee4-204">Merhaba sertifikanın aynı hello VM DNS adı ad hello vardır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="e5ee4-205">Sipariş tooavoid sertifika hataları gerekli hello sertifikanın hello VM kendisi ve ayrıca hello sitenin tüm kullanıcılar tarafından güvenilmiyor.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="e5ee4-206">tootrust hello kök CA'ın hello yerel VM hello sertifika Ekle hello sertifika toohello **güvenilen kök sertifika yetkilileri**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="e5ee4-207">Merhaba, gerekli hello adımları özeti aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="e5ee4-208">Nasıl tootrust hello CA ile ilgili ayrıntılı adımlar için bkz: [sunucu sertifikasını yüklemeniz](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="e5ee4-209">Hello Klasik Azure Portalı ' hello VM seçin ve Bağlan'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="e5ee4-210">Tarayıcı yapılandırmanıza bağlı olarak, istendiğinde toosave toohello VM bağlanmak için bir .rdp dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="e5ee4-212">Merhaba kullanıcı VM adı, kullanıcı adı ve parola hello VM oluştururken yapılandırılmış kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="e5ee4-213">Örneğin, görüntü aşağıdaki hello hello VM adıdır **ssrsnativecloud** ve hello kullanıcı adı **testuser**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![oturum açma bilgileri vm adını içerir](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="e5ee4-215">MMC.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-215">Run mmc.exe.</span></span> <span data-ttu-id="e5ee4-216">Daha fazla bilgi için bkz: [nasıl yapılır: hello MMC ek bileşeni ile sertifikaları görüntüleme](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="e5ee4-217">Merhaba konsol uygulamasındaki **dosya** menüsünde hello eklemek **sertifikaları** ek bileşeninde, select **bilgisayar hesabı** istenir ve ardından **İleri**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="e5ee4-218">Seçin **yerel bilgisayar** toomanage ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="e5ee4-219">Tıklatın **Tamam** genişletin ve ardından hello **sertifikalar - kişisel** düğümleri ve ardından **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="e5ee4-220">Merhaba sertifika sonra hello VM hello DNS adı olarak adlandırılır ve ile biten **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="e5ee4-221">Merhaba sertifika adını sağ tıklatıp **kopya**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="e5ee4-222">Merhaba genişletin **güvenilen kök sertifika yetkilileri** düğümünü ve ardından sağ tıklayarak **sertifikaları** ve ardından **Yapıştır**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="e5ee4-223">Merhaba sertifika adı altında toovalidate, çift tıklayarak **güvenilen kök sertifika yetkilileri** ve hatalar yoktur ve sertifikanızı gördüğünüz doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="e5ee4-224">Bu konuda tooconfigure hello rapor sunucusu dahil toouse hello HTTPS betik istiyorsanız hello sertifikaları değerini hello **parmak izi** hello komut parametresi olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="e5ee4-225">**tooget hello parmak izi değeri**, hello aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="e5ee4-226">Bölümünde de bir PowerShell örnek tooretrieve hello parmak izi yok [betik tooconfigure hello rapor sunucusu ve HTTPS kullanma](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="e5ee4-227">Merhaba sertifika, örneğin ssrsnativecloud.cloudapp.net Hello adına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="e5ee4-228">Merhaba tıklatın **ayrıntıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="e5ee4-229">Tıklatın **parmak izi**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-229">Click **Thumbprint**.</span></span> <span data-ttu-id="e5ee4-230">Merhaba hello parmak izi değerini hello Ayrıntılar alanında, örneğin a6 görüntülenen 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="e5ee4-231">Merhaba parmak izini kopyalayın ve hello değeri daha sonra kullanmak üzere kaydetmek veya hello betik şimdi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="e5ee4-232">(*) Merhaba betiği çalıştırmadan önce hello değer çiftlerini Between hello boşlukları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="e5ee4-233">Örneğin önce not ettiğiniz hello parmak izi şimdi a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f olur.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="e5ee4-234">Merhaba sertifika toohello rapor sunucusu atayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="e5ee4-235">Merhaba rapor sunucusunu yapılandırdığınızda hello atama hello sonraki bölümde tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="e5ee4-236">Otomatik olarak imzalanan bir SSL sertifikası kullanıyorsanız, hello hello sertifikadaki zaten hello VM hello ana bilgisayar adıyla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="e5ee4-237">Bu nedenle, hello hello makinenin DNS zaten genel olarak kaydedilir ve herhangi bir istemciden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="e5ee4-238">3. adım: hello rapor sunucusu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e5ee4-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="e5ee4-239">Bu bölümde bir Reporting Services yerel mod rapor sunucusu olarak hello VM nasıl yapılandıracağınız anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="e5ee4-240">Yöntemleri tooconfigure hello rapor sunucusu aşağıdaki hello birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="e5ee4-241">Merhaba betik tooconfigure hello rapor sunucusu kullanma</span><span class="sxs-lookup"><span data-stu-id="e5ee4-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="e5ee4-242">Yapılandırma Yöneticisi'ni kullanın tooConfigure hello rapor sunucusu.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="e5ee4-243">Daha ayrıntılı adımlar için hello bölümüne bakın [Bağlan toohello sanal makine ve başlangıç hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="e5ee4-244">**Kimlik doğrulama Not:** Windows kimlik doğrulaması kimlik doğrulama yöntemini önerilen hello ve hello varsayılan Reporting Services kimlik doğrulaması olur.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="e5ee4-245">Merhaba VM üzerinde yapılandırılmış olan kullanıcılar Reporting Services erişebilir ve Hizmetleri rolleri tooReporting atanır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="e5ee4-246">Komut dosyası tooconfigure hello report server ve HTTP kullanın</span><span class="sxs-lookup"><span data-stu-id="e5ee4-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="e5ee4-247">toouse hello Windows PowerShell komut dosyası tooconfigure hello rapor sunucusu, aşağıdaki adımları tam hello.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="e5ee4-248">Merhaba yapılandırma HTTP, HTTPS değil içerir:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="e5ee4-249">Hello Klasik Azure Portalı ' hello VM seçin ve Bağlan'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="e5ee4-250">Tarayıcı yapılandırmanıza bağlı olarak, istendiğinde toosave toohello VM bağlanmak için bir .rdp dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="e5ee4-252">Merhaba kullanıcı VM adı, kullanıcı adı ve parola hello VM oluştururken yapılandırılmış kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="e5ee4-253">Örneğin, görüntü aşağıdaki hello hello VM adıdır **ssrsnativecloud** ve hello kullanıcı adı **testuser**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![oturum açma bilgileri vm adını içerir](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="e5ee4-255">Hello VM, açık **Windows PowerShell ISE** yönetici ayrıcalıklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="e5ee4-256">Merhaba PowerShell ISE, Windows server 2012'de varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="e5ee4-257">İŞE hello hello betiğini yapıştırın, hello komut dosyasını değiştirin ve hello betiğini çalıştırmak yerine standart bir Windows PowerShell penceresinde hello ISE kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="e5ee4-258">Windows PowerShell ISE'de hello tıklatın **Görünüm** menüsünü seçin ve ardından **betik bölmesini göster**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="e5ee4-259">Komut dosyası izleyen hello kopyalayıp hello betik hello Windows PowerShell ISE betik bölmesine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="e5ee4-260">Bir HTTP bağlantı noktası 80 dışında hello VM oluşturduysanız hello parametresi $HTTPport değiştirin = 80.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="e5ee4-261">Merhaba komut dosyası şu anda Raporlama Hizmetleri için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="e5ee4-262">Raporlama Hizmetleri için toorun hello betik istiyorsanız, hello yolu toohello ad hello sürüm bölümü çok değiştirin "v11" Merhaba Get-WmiObject deyimi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="e5ee4-263">Merhaba komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-263">Run hello script.</span></span>

<span data-ttu-id="e5ee4-264">**Doğrulama**: hello temel rapor sunucusu işlevselliği çalıştığından, tooverify bkz hello [doğrula hello yapılandırma](#verify-the-configuration) bu konunun ilerleyen bölümlerinde.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="e5ee4-265">Komut dosyası tooconfigure hello rapor sunucusu hem de HTTPS kullanın</span><span class="sxs-lookup"><span data-stu-id="e5ee4-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="e5ee4-266">toouse Windows PowerShell tooconfigure hello rapor sunucusu, aşağıdaki adımları tam hello.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="e5ee4-267">Merhaba yapılandırma, HTTPS değil HTTP içerir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="e5ee4-268">Hello Klasik Azure Portalı ' hello VM seçin ve Bağlan'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="e5ee4-269">Tarayıcı yapılandırmanıza bağlı olarak, istendiğinde toosave toohello VM bağlanmak için bir .rdp dosyası olabilir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="e5ee4-271">Merhaba kullanıcı VM adı, kullanıcı adı ve parola hello VM oluştururken yapılandırılmış kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="e5ee4-272">Örneğin, görüntü aşağıdaki hello hello VM adıdır **ssrsnativecloud** ve hello kullanıcı adı **testuser**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![oturum açma bilgileri vm adını içerir](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="e5ee4-274">Hello VM, açık **Windows PowerShell ISE** yönetici ayrıcalıklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="e5ee4-275">Merhaba PowerShell ISE, Windows server 2012'de varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="e5ee4-276">İŞE hello hello betiğini yapıştırın, hello komut dosyasını değiştirin ve hello betiğini çalıştırmak yerine standart bir Windows PowerShell penceresinde hello ISE kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="e5ee4-277">Windows PowerShell komutunu aşağıdaki hello Çalıştır komut dosyası çalıştırarak tooenable:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="e5ee4-278">Ardından tooverify hello ilkesi aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="e5ee4-279">İçinde **Windows PowerShell ISE**, hello tıklatın **Görünüm** menüsünü seçin ve ardından **betik bölmesini göster**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="e5ee4-280">Aşağıdaki komut dosyası ve hello Windows PowerShell ISE betik bölmesine yapıştırın hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="e5ee4-281">Merhaba değiştirme **$certificatehash** hello komut parametresi:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="e5ee4-282">Bu bir **gerekli** parametresi.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-282">This is a **required** parameter.</span></span> <span data-ttu-id="e5ee4-283">Merhaba önceki adımları hello sertifika değeri kaydetmediyseniz hello sertifika parmak izini yöntemleri toocopy hello sertifika karma değer aşağıdaki hello birini kullanın.:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="e5ee4-284">Hello VM, Windows PowerShell ISE açın ve hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="e5ee4-285">Merhaba çıkış benzer toohello aşağıdaki arar.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="e5ee4-286">Merhaba komut dosyası boş bir satır döndürürse, hello VM örneğin yapılandırılmış bir sertifikaya sahip değilse, hello bölümüne bakın [toouse hello sanal makineleri otomatik olarak imzalanan sertifika](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="e5ee4-287">OR</span><span class="sxs-lookup"><span data-stu-id="e5ee4-287">OR</span></span>
   * <span data-ttu-id="e5ee4-288">VM çalıştırmak mmc.exe hello ve hello eklemek **sertifikaları** ek bileşenini.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="e5ee4-289">Merhaba altında **güvenilen kök sertifika yetkilileri** düğüme çift tıklayın, sertifika adı.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="e5ee4-290">Merhaba otomatik olarak imzalanan sertifikasını hello VM kullanıyorsanız, hello sertifika sonra hello VM hello DNS adı olarak adlandırılır ve ile biten **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="e5ee4-291">Merhaba tıklatın **ayrıntıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="e5ee4-292">Tıklatın **parmak izi**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-292">Click **Thumbprint**.</span></span> <span data-ttu-id="e5ee4-293">Merhaba hello parmak izi değerini hello Ayrıntılar alanında, örneğin af 11 60 b6 4b 28 8 d 89 0a görüntülenen 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="e5ee4-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="e5ee4-294">**Merhaba betiği çalıştırmadan önce**, değer çiftlerini hello Between hello boşlukları Kaldır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="e5ee4-295">Örneğin af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="e5ee4-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="e5ee4-296">Merhaba değiştirme **$httpsport** parametre:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="e5ee4-297">Ardından hello HTTPS uç noktası için 443 numaralı bağlantı noktasını kullandıysanız, tooupdate hello betik bu parametrede gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="e5ee4-298">Aksi durumda VM hello üzerinde hello HTTPS özel uç noktası yapılandırıldığında, seçtiğiniz hello bağlantı noktası değeri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="e5ee4-299">Merhaba değiştirme **$DNSName** parametre:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="e5ee4-300">Merhaba betik bir joker sertifika $DNSName yapılandırılmış = "+".</span><span class="sxs-lookup"><span data-stu-id="e5ee4-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="e5ee4-301">Joker karakter sertifika bağlama için hiçbir istediğiniz tooconfigure bunu yaparsanız, $DNSName Açıklama = "+"ve aşağıdaki satırı, hello tam $DNSNAme başvurusu, ## $DNSName="$server.cloudapp.net hello etkinleştir".</span><span class="sxs-lookup"><span data-stu-id="e5ee4-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="e5ee4-302">Raporlama Hizmetleri için toouse hello sanal makinenin DNS adı istemiyorsanız hello $DNSName değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="e5ee4-303">Merhaba parametreyi kullanırsanız, hello sertifika bu adı kullanmanız gerekir ve bir DNS sunucusundaki genel hello adı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="e5ee4-304">Merhaba komut dosyası şu anda Raporlama Hizmetleri için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="e5ee4-305">Raporlama Hizmetleri için toorun hello betik istiyorsanız, hello yolu toohello ad hello sürüm bölümü çok değiştirin "v11" Merhaba Get-WmiObject deyimi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="e5ee4-306">Merhaba komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-306">Run hello script.</span></span>

<span data-ttu-id="e5ee4-307">**Doğrulama**: hello temel rapor sunucusu işlevselliği çalıştığından, tooverify bkz hello [doğrula hello yapılandırma](#verify-the-connection) bu konunun ilerleyen bölümlerinde.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="e5ee4-308">tooverify hello sertifika bağlama yönetici ayrıcalıklarıyla bir komut istemi açın ve ardından hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="e5ee4-309">Merhaba sonuç hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="e5ee4-310">Yapılandırma Yöneticisi'ni kullanın tooConfigure hello rapor sunucusu</span><span class="sxs-lookup"><span data-stu-id="e5ee4-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="e5ee4-311">Toorun hello PowerShell komut dosyası tooconfigure hello rapor sunucusu istemiyorsanız, bu bölümde toouse hello Reporting Services yerel mod configuration manager tooconfigure hello rapor sunucusu hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="e5ee4-312">Hello Klasik Azure Portalı ' hello VM seçin ve Bağlan'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="e5ee4-313">Merhaba kullanıcı adı ve parola hello VM oluştururken yapılandırılmış kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![tooazure sanal makineye bağlanma](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="e5ee4-315">Windows Update'i çalıştırın ve güncelleştirmeleri toohello VM yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="e5ee4-316">Merhaba VM yeniden başlatılması gerekiyorsa, hello VM yeniden başlatın ve toohello VM hello Klasik Azure Portalı'ndan yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="e5ee4-317">Merhaba Başlat menüsünden hello VM üzerinde yazın **Reporting Services** açarak **Reporting Services Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="e5ee4-318">Merhaba varsayılan değerleri bırakın **sunucu adı** ve **rapor sunucusu örneği**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="e5ee4-319">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-319">Click **Connect**.</span></span>
5. <span data-ttu-id="e5ee4-320">Merhaba sol bölmede **Web hizmeti URL'si**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="e5ee4-321">Varsayılan olarak, RS IP "Tüm atanan" HTTP bağlantı noktası 80 için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="e5ee4-322">tooadd HTTPS:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="e5ee4-323">İçinde **SSL sertifikası**: select hello sertifika [VM adı] örneğin toouse, istediğiniz. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="e5ee4-324">Hiçbir sertifika listelenmiyorsa, hello bölümüne bakın. **2. adım: bir sunucu sertifikası oluşturma** nasıl tooinstall ve güven hello VM sertifikadaki hello hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="e5ee4-325">Altında **SSL bağlantı noktası**: 443'ü seçin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="e5ee4-326">Merhaba VM özel farklı bir bağlantı noktası ile Merhaba HTTPS özel uç noktasını yapılandırdıysanız, bu değer burada kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="e5ee4-327">Tıklatın **Uygula** ve hello işlemi toocomplete için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="e5ee4-328">Merhaba sol bölmede **veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="e5ee4-329">Tıklatın **değiştirme Databas**e.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="e5ee4-330">Tıklatın **yeni bir rapor sunucusu veritabanı oluşturun** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="e5ee4-331">Merhaba varsayılan adı bırakın **sunucu adı**: hello VM adlandırın ve hello varsayılan adı bırakın **kimlik doğrulama türü** olarak **geçerli kullanıcı** – **tümleşik güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="e5ee4-332">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-332">Click **Next**.</span></span>
   4. <span data-ttu-id="e5ee4-333">Merhaba varsayılan adı bırakın **veritabanı adı** olarak **ReportServer** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="e5ee4-334">Merhaba varsayılan adı bırakın **kimlik doğrulama türü** olarak **hizmeti kimlik bilgileri** tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="e5ee4-335">Tıklatın **sonraki** hello üzerinde **Özet** sayfası.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="e5ee4-336">Merhaba Yapılandırma tamamlandığında tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="e5ee4-337">Merhaba sol bölmede **Rapor Yöneticisi URL'si**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="e5ee4-338">Merhaba varsayılan adı bırakın **sanal dizin** olarak **raporları** tıklatıp **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="e5ee4-339">Tıklatın **çıkış** tooclose hello Reporting Services Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="e5ee4-340">4. adım: Windows Güvenlik Duvarı bağlantı noktası Aç</span><span class="sxs-lookup"><span data-stu-id="e5ee4-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="e5ee4-341">Merhaba betikleri tooconfigure hello rapor sunucusu birini kullandıysanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="e5ee4-342">Merhaba betik adım tooopen hello güvenlik duvarı bağlantı noktası dahil.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="e5ee4-343">Merhaba varsayılan bağlantı noktası HTTP için 80 ve HTTPS için 443 numaralı bağlantı noktasını oluştu.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="e5ee4-344">tooconnect uzaktan tooReport Yöneticisi veya hello rapor hello sanal makine sunucuda, bir TCP uç noktası hello VM üzerinde gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="e5ee4-345">Gerekli tooopen hello hello VM'in Güvenlik Duvarı'nda aynı bağlantı noktası olur.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="e5ee4-346">Merhaba VM hazırlandığında hello uç noktası oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="e5ee4-347">Bu bölüm, nasıl tooopen hello üzerinde güvenlik duvarı bağlantı noktasını temel bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="e5ee4-348">Daha fazla bilgi için bkz: [güvenlik duvarını rapor sunucusu erişimi için yapılandırma](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="e5ee4-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="e5ee4-349">Merhaba betik tooconfigure hello rapor sunucusu kullandıysanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="e5ee4-350">Merhaba betik adım tooopen hello güvenlik duvarı bağlantı noktası dahil.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="e5ee4-351">Özel bir bağlantı noktası HTTPS için 443 dışındaki yapılandırdıysanız, komut dosyası uygun şekilde aşağıdaki hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="e5ee4-352">tooopen bağlantı noktası **443** hello Windows Güvenlik Duvarı, hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="e5ee4-353">Yönetici ayrıcalıklarıyla bir Windows PowerShell penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="e5ee4-354">Merhaba VM üzerinde hello HTTPS uç noktası yapılandırıldığında bir bağlantı noktası 443 dışındaki kullandıysanız, komut aşağıdaki hello hello bağlantı noktasını güncelleştirin ve hello komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="e5ee4-355">Merhaba komut tamamlandığında, **Tamam** hello Komut İstemi'nde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="e5ee4-356">başlangıç bağlantı noktası açıldı tooverify bir Windows PowerShell penceresini açın ve komut aşağıdaki çalışma hello açın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="e5ee4-357">Merhaba yapılandırmasını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-357">Verify hello configuration</span></span>
<span data-ttu-id="e5ee4-358">Merhaba temel rapor sunucusu işlevselliği şimdi çalışıyor, tooverify yönetici ayrıcalıklarıyla tarayıcınızı açın ve ardından sunucu ad Rapor Yöneticisi'ni URL'leri Gözat toohello aşağıdaki rapor:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="e5ee4-359">Hello VM, toohello rapor sunucusu URL'si göz atın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="e5ee4-360">Hello VM, toohello Rapor Yöneticisi URL'si göz atın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="e5ee4-361">Yerel bilgisayarınızdan toohello Gözat **uzak** Yöneticisi hello VM üzerinde rapor.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="e5ee4-362">Aşağıdaki uygun şekilde örneğine hello Hello DNS adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="e5ee4-363">İçin bir parola istendiğinde, hello VM hazırlandığında oluşturduğunuz hello yönetici kimlik bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="e5ee4-364">Merhaba kullanıcı adınızdır hello [etki alanı]\[kullanıcı adı] biçiminde hello etki hello VM bilgisayar adını, örneğin ssrsnativecloud\testuser olduğu.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="e5ee4-365">HTTP kullanmıyorsanız**S**, hello kaldırmak **s** hello URL.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="e5ee4-366">VM ek kullanıcılar oluşturma hakkında bilgi için Hello sonraki bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="e5ee4-367">Yerel bilgisayarınızdan toohello uzaktan rapor sunucusu URL'si göz atın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="e5ee4-368">Aşağıdaki uygun şekilde örneğine hello Hello DNS adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="e5ee4-369">HTTPS kullanmıyorsanız hello s hello URL'de kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="e5ee4-370">Kullanıcılar oluşturma ve rolleri atama</span><span class="sxs-lookup"><span data-stu-id="e5ee4-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="e5ee4-371">Rapor sunucusu yapılandırma ve hello doğrulama sonra ortak bir yönetim görevi toocreate bir veya daha fazla kullanıcı sayısıdır ve kullanıcıların tooReporting Hizmetleri rolleri atayın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="e5ee4-372">Daha fazla bilgi için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="e5ee4-373">Bir yerel kullanıcı hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="e5ee4-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="e5ee4-374">[Kullanıcı erişim izni ver tooa rapor sunucusu (Rapor Yöneticisi)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="e5ee4-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="e5ee4-375">Oluşturma ve rol atamalarını yönetme</span><span class="sxs-lookup"><span data-stu-id="e5ee4-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="e5ee4-376">tooCreate ve raporları yayımlama toohello Azure sanal makine</span><span class="sxs-lookup"><span data-stu-id="e5ee4-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="e5ee4-377">Merhaba aşağıdaki tabloda hello seçenekleri kullanılabilir toopublish varolan raporları hello Microsoft Azure sanal makinesi üzerinde barındırılan bir şirket içi bilgisayar toohello rapor sunucusu özetlenmektedir:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="e5ee4-378">**RS.exe betik**: kullanım RS.exe betik toocopy rapor öğeleri ve varolan rapor sunucusu tooyour Microsoft Azure sanal makinesi.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="e5ee4-379">Daha fazla bilgi için hello "yerel mod tooNative modu – Microsoft Azure sanal makinesi" bölümüne bakın [örnek Raporlama Hizmetleri rs.exe betik tooMigrate rapor sunucuları arasında içerik](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="e5ee4-380">**Rapor Oluşturucu**: hello sanal makine içeren hello tıklatın-Microsoft SQL Server Rapor Oluşturucusu sürümünü bir kez.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="e5ee4-381">toostart Rapor Oluşturucu hello hello sanal makinede ilk kez:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="e5ee4-382">Tarayıcınız yönetici ayrıcalıklarıyla başlatın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="e5ee4-383">Merhaba sanal makineye tooreport Yöneticisi bulun ve tıklatın **Rapor Oluşturucu** hello Şeritte.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="e5ee4-384">Daha fazla bilgi için bkz: [yükleme, kaldırma ve destekleyici Rapor Oluşturucusu'nu](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="e5ee4-385">**SQL Server veri araçları: VM**: SQL Server 2012 ile Merhaba VM oluşturduğunuz sonra SQL Server veri araçları hello sanal makinede yüklü ve kullanılan toocreate olabilir **rapor sunucusu projeleri** ve hello sanal raporları Makine.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="e5ee4-386">SQL Server veri araçları hello raporları toohello rapor sunucusu hello sanal makineye yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="e5ee4-387">SQL server 2014 ile Merhaba VM oluşturduysanız, SQL Server veri araçları - BI visual Studio için yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="e5ee4-388">Daha fazla bilgi için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="e5ee4-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="e5ee4-389">Microsoft SQL Server veri araçları - Visual Studio 2013 iş zekası</span><span class="sxs-lookup"><span data-stu-id="e5ee4-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="e5ee4-390">Microsoft SQL Server veri araçları - Visual Studio 2012 için iş zekası</span><span class="sxs-lookup"><span data-stu-id="e5ee4-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="e5ee4-391">SQL Server veri araçları ve SQL Server Business Intelligence (BI SSDT)</span><span class="sxs-lookup"><span data-stu-id="e5ee4-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="e5ee4-392">**SQL Server veri araçları: Uzaktan**: yerel bilgisayarınızda SQL Server veri araçları Raporlama Hizmetleri raporlarını içeren bir Reporting Services projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="e5ee4-393">Merhaba proje tooconnect toohello web hizmeti URL'si yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![SSRS projesi için SSDT proje özellikleri](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="e5ee4-395">**Komut dosyası kullanma**: betik toocopy rapor sunucusu içeriği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="e5ee4-396">Daha fazla bilgi için bkz: [örnek Raporlama Hizmetleri rs.exe betik tooMigrate rapor sunucuları arasında içerik](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="e5ee4-397">Merhaba VM kullanmıyorsanız maliyeti en aza indir</span><span class="sxs-lookup"><span data-stu-id="e5ee4-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="e5ee4-398">toominimize ücretleri için Azure sanal makinelerinizi kullanılmadığı zaman hello VM hello Klasik Azure Portalı'ndan kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="e5ee4-399">Merhaba Windows güç seçenekleri VM tooshut hello VM aşağı içinde kullanırsanız, hala ücretlendirilen hello hello VM için aynı tutar.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="e5ee4-400">tooreduce ücretlendirilen hello Klasik Azure portalı hello VM aşağı tooshut gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5ee4-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="e5ee4-401">Merhaba VM artık ihtiyacınız varsa, ilişkili .vhd dosyaları tooavoid depolama ücretleri hello ve toodelete hello VM unutmayın. Daha fazla bilgi için bkz: hello SSS bölümüne [sanal makineler fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="e5ee4-402">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="e5ee4-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="e5ee4-403">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e5ee4-403">Resources</span></span>
* <span data-ttu-id="e5ee4-404">Tooa tek sunucu dağıtımı için benzer içerik ilgili SQL Server Business Intelligence ve SharePoint 2013'ın bkz [Windows PowerShell'i kullanın tooCreate bir Azure VM ile SQL Server BI ve SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="e5ee4-405">SQL Server Business Intelligence ve SharePoint 2013'ün birden çok sunucu dağıtımı için benzer içerik ilgili tooa bkz [dağıtmak SQL Server Business Intelligence Azure Virtual Machines'de](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="e5ee4-406">SQL Server Business Intelligence Azure sanal makineleri, ilgili toodeployments genel bilgi için bkz [SQL Server Business Intelligence Azure Virtual Machines'de](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="e5ee4-407">Azure işlem ücretleri hello maliyeti hakkında daha fazla bilgi için bkz: hello sanal makineleri sekmesinde [Azure fiyatlandırma hesaplayıcısı](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="e5ee4-408">Topluluk içeriği</span><span class="sxs-lookup"><span data-stu-id="e5ee4-408">Community Content</span></span>
* <span data-ttu-id="e5ee4-409">Nasıl toocreate bir Raporlama Hizmetleri yerel modu rapor sunucusunda komut dosyasını kullanmadan adım adım yönergeler için bkz: [barındırma SQL Raporlama hizmeti Azure sanal makine üzerinde](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="e5ee4-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="e5ee4-410">Azure vm'lerinde SQL Server için bağlantılar tooother kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e5ee4-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="e5ee4-411">SQL Server üzerinde Azure sanal makinelere genel bakış</span><span class="sxs-lookup"><span data-stu-id="e5ee4-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

