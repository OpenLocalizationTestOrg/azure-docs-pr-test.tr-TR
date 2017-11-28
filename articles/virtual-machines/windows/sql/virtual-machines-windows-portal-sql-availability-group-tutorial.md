---
title: "aaaSQL Server kullanılabilirlik gruplarını - Azure sanal makineleri - Öğreticisi | Microsoft Docs"
description: "Bu öğreticide gösterilmiştir nasıl toocreate bir SQL Server her zaman üzerinde kullanılabilirlik grubu Azure sanal makineler üzerinde."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="a2a36-103">Yapılandırma her zaman üzerindeki kullanılabilirlik grubu Azure VM'de el ile</span><span class="sxs-lookup"><span data-stu-id="a2a36-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="a2a36-104">Bu öğreticide gösterilmiştir nasıl toocreate bir SQL Server her zaman üzerinde kullanılabilirlik grubu Azure sanal makineler üzerinde.</span><span class="sxs-lookup"><span data-stu-id="a2a36-104">This tutorial shows how toocreate a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="a2a36-105">Merhaba tam öğretici iki SQL sunucusu üzerindeki veritabanı çoğaltmasıyla bir kullanılabilirlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a2a36-105">hello complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="a2a36-106">**Zaman tahmin**: hello Önkoşullar sağlandığında yaklaşık 30 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-106">**Time estimate**: Takes about 30 minutes toocomplete once hello prerequisites are met.</span></span>

<span data-ttu-id="a2a36-107">Merhaba diyagram hello öğreticide yapı gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-107">hello diagram illustrates what you build in hello tutorial.</span></span>

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="a2a36-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a2a36-109">Prerequisites</span></span>

<span data-ttu-id="a2a36-110">SQL Server Always On kullanılabilirlik grupları temel bir anlayış Hello öğretici varsayar.</span><span class="sxs-lookup"><span data-stu-id="a2a36-110">hello tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="a2a36-111">Daha fazla bilgi için bkz: [genel bakış, Always On kullanılabilirlik grupları (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2a36-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="a2a36-112">Merhaba aşağıdaki tabloda bu öğreticiye başlamadan önce toocomplete gereken hello önkoşulları listeler:</span><span class="sxs-lookup"><span data-stu-id="a2a36-112">hello following table lists hello prerequisites that you need toocomplete before starting this tutorial:</span></span>

|  |<span data-ttu-id="a2a36-113">Gereksinim</span><span class="sxs-lookup"><span data-stu-id="a2a36-113">Requirement</span></span> |<span data-ttu-id="a2a36-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a2a36-114">Description</span></span> |
|----- |----- |----- |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="a2a36-116">İki SQL sunucuları</span><span class="sxs-lookup"><span data-stu-id="a2a36-116">Two SQL Servers</span></span> | <span data-ttu-id="a2a36-117">-Bir Azure kullanılabilirlik kümesine</span><span class="sxs-lookup"><span data-stu-id="a2a36-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="a2a36-118">-Tek bir etki alanı</span><span class="sxs-lookup"><span data-stu-id="a2a36-118">- In a single domain</span></span> <br/> <span data-ttu-id="a2a36-119">-Yük Devretme Kümelemesi özelliği yüklü olan</span><span class="sxs-lookup"><span data-stu-id="a2a36-119">- With Failover Clustering feature installed</span></span> |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="a2a36-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="a2a36-121">Windows Server</span></span> | <span data-ttu-id="a2a36-122">Küme Tanık dosya paylaşımı</span><span class="sxs-lookup"><span data-stu-id="a2a36-122">File share for cluster witness</span></span> |  
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="a2a36-124">SQL Server hizmet hesabı</span><span class="sxs-lookup"><span data-stu-id="a2a36-124">SQL Server service account</span></span> | <span data-ttu-id="a2a36-125">Etki alanı hesabı</span><span class="sxs-lookup"><span data-stu-id="a2a36-125">Domain account</span></span> |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="a2a36-127">SQL Server Aracısı hizmet hesabı</span><span class="sxs-lookup"><span data-stu-id="a2a36-127">SQL Server Agent service account</span></span> | <span data-ttu-id="a2a36-128">Etki alanı hesabı</span><span class="sxs-lookup"><span data-stu-id="a2a36-128">Domain account</span></span> |  
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="a2a36-130">Güvenlik Duvarı bağlantı noktalarını açın</span><span class="sxs-lookup"><span data-stu-id="a2a36-130">Firewall ports open</span></span> | <span data-ttu-id="a2a36-131">-SQL Server: **1433** varsayılan örnek için</span><span class="sxs-lookup"><span data-stu-id="a2a36-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="a2a36-132">-Veritabanı yansıtma uç noktası: **5022** veya tüm kullanılabilir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="a2a36-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="a2a36-133">-Azure yük dengeleyici araştırmasını: **59999** veya tüm kullanılabilir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="a2a36-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="a2a36-135">Yük Devretme Kümelemesi özelliği Ekle</span><span class="sxs-lookup"><span data-stu-id="a2a36-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="a2a36-136">Bu özellik, her iki SQL sunucuları gerektirir</span><span class="sxs-lookup"><span data-stu-id="a2a36-136">Both SQL Servers require this feature</span></span> |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="a2a36-138">Yükleme etki alanı hesabı</span><span class="sxs-lookup"><span data-stu-id="a2a36-138">Installation domain account</span></span> | <span data-ttu-id="a2a36-139">-Her bir SQL Server yerel yönetici</span><span class="sxs-lookup"><span data-stu-id="a2a36-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="a2a36-140">-Her SQL Server örneği için SQL Server sysadmin sabit sunucu rolünün üyesi</span><span class="sxs-lookup"><span data-stu-id="a2a36-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="a2a36-141">Merhaba öğreticiye başlamadan önce çok ihtiyacınız[tamamlamak Azure sanal makinelerinde Always On kullanılabilirlik grupları oluşturmak için Önkoşullar](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="a2a36-141">Before you begin hello tutorial, you need too[Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="a2a36-142">Bu Önkoşullar zaten tamamladıysanız, sizin çok atlayabilirsiniz[küme oluşturma](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="a2a36-142">If these prerequisites are completed already, you can jump too[Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="a2a36-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Merhaba kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2a36-143"><!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create hello cluster</span></span>

<span data-ttu-id="a2a36-144">Hello Önkoşullar tamamlandıktan sonra hello ilk toocreate iki SQL Server'lar içeren Windows Server Yük devretme kümesi ve bir Tanık adımdır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-144">After hello prerequisites are completed, hello first step is toocreate a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="a2a36-145">RDP toohello SQL sunucuları ve hello Tanık sunucu üzerindeki bir yönetici olan bir etki alanı hesabı kullanarak ilk SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a2a36-145">RDP toohello first SQL Server using a domain account that is an administrator on both SQL Servers and hello witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="a2a36-146">Merhaba izlediyseniz [önkoşul belgesi](virtual-machines-windows-portal-sql-availability-group-prereq.md), adlı bir hesap oluşturulan **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-146">If you followed hello [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="a2a36-147">Bu hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-147">Use this account.</span></span>

2. <span data-ttu-id="a2a36-148">Merhaba, **Sunucu Yöneticisi'ni** Pano, select **Araçları**ve ardından **yük devretme kümesi Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-148">In hello **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="a2a36-149">Merhaba sol bölmesinde, **yük devretme kümesi Yöneticisi**ve ardından **bir küme oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-149">In hello left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="a2a36-150">![Küme oluşturma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="a2a36-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="a2a36-151">Buna küme oluşturma Sihirbazı'nı Merhaba, aşağıdaki tablonun hello hello ayarlarla hello sayfalarıyla adımla tek düğümlü bir küme oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a2a36-151">In hello Create Cluster Wizard, create a one-node cluster by stepping through hello pages with hello settings in hello following table:</span></span>

   | <span data-ttu-id="a2a36-152">Sayfa</span><span class="sxs-lookup"><span data-stu-id="a2a36-152">Page</span></span> | <span data-ttu-id="a2a36-153">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="a2a36-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="a2a36-154">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a2a36-154">Before You Begin</span></span> |<span data-ttu-id="a2a36-155">Varsayılanları kullanın</span><span class="sxs-lookup"><span data-stu-id="a2a36-155">Use defaults</span></span> |
   | <span data-ttu-id="a2a36-156">Sunucuları seçin</span><span class="sxs-lookup"><span data-stu-id="a2a36-156">Select Servers</span></span> |<span data-ttu-id="a2a36-157">İlk SQL Server adı türü hello **sunucu adını girin** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-157">Type hello first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="a2a36-158">Doğrulama uyarısı</span><span class="sxs-lookup"><span data-stu-id="a2a36-158">Validation Warning</span></span> |<span data-ttu-id="a2a36-159">Seçin **ı bu küme için Microsoft desteğine gereksiniminiz ve bu nedenle toorun hello doğrulama istemiyorsanız Hayır sınar. Sonraki tıkladığınızda, hello küme oluşturmaya devam etmek**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want toorun hello validation tests. When I click Next, continue Creating hello cluster**.</span></span> |
   | <span data-ttu-id="a2a36-160">Yönetme hello küme için erişim noktası</span><span class="sxs-lookup"><span data-stu-id="a2a36-160">Access Point for Administering hello Cluster</span></span> |<span data-ttu-id="a2a36-161">Bir küme adı yazın, örneğin **SQLAGCluster1** içinde **küme adı**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="a2a36-162">Onay</span><span class="sxs-lookup"><span data-stu-id="a2a36-162">Confirmation</span></span> |<span data-ttu-id="a2a36-163">Depolama alanları kullanmadığınız sürece varsayılan ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="a2a36-164">Bu tablodan sonraki hello nota bakın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-164">See hello note following this table.</span></span> |

### <a name="set-hello-cluster-ip-address"></a><span data-ttu-id="a2a36-165">Merhaba küme IP adresi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a2a36-165">Set hello cluster IP address</span></span>

1. <span data-ttu-id="a2a36-166">İçinde **yük devretme kümesi Yöneticisi**, çok ilerleyin**küme çekirdek kaynakları** ve hello küme Ayrıntıları'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-166">In **Failover Cluster Manager**, scroll down too**Cluster Core Resources** and expand hello cluster details.</span></span> <span data-ttu-id="a2a36-167">Her iki hello görmelisiniz **adı** ve hello **IP adresi** hello kaynaklarında **başarısız** durumu.</span><span class="sxs-lookup"><span data-stu-id="a2a36-167">You should see both hello **Name** and hello **IP Address** resources in hello **Failed** state.</span></span> <span data-ttu-id="a2a36-168">Merhaba küme hello atandığından hello IP adresi kaynağı çevrimiçi duruma getirilemiyor aynı IP adresi hello makine olarak kendisi, bu nedenle, bir yinelenen adresidir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-168">hello IP address resource cannot be brought online because hello cluster is assigned hello same IP address as hello machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="a2a36-169">Başarısız sağ hello **IP adresi** kaynak ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-169">Right-click hello failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Küme Özellikleri](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="a2a36-171">Seçin **statik IP adresi** ve kullanılabilir bir hello SQL Server hello adresi metin kutusuna olduğu alt ağ adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-171">Select **Static IP Address** and specify an available address from subnet where hello SQL Server is in hello Address text box.</span></span> <span data-ttu-id="a2a36-172">Ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="a2a36-173">Merhaba, **küme çekirdek kaynakları** bölümünde, küme adını sağ tıklatın ve **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-173">In hello **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="a2a36-174">Daha sonra her iki kaynağın çevrimiçi olana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="a2a36-175">Merhaba küme adı kaynağını çevrimiçi olduğunda hello DC sunucusuna yeni bir AD bilgisayar hesabı ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-175">When hello cluster name resource comes online, it updates hello DC server with a new AD computer account.</span></span> <span data-ttu-id="a2a36-176">Bu AD hesabı toorun hello daha sonra kullanılabilirlik grubu kümelenmiş hizmet kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-176">Use this AD account toorun hello Availability Group clustered service later.</span></span>

### <span data-ttu-id="a2a36-177"><a name="addNode"></a>Ekleme diğer SQL Server toocluster hello</span><span class="sxs-lookup"><span data-stu-id="a2a36-177"><a name="addNode"></a>Add hello other SQL Server toocluster</span></span>

<span data-ttu-id="a2a36-178">Ekleme diğer SQL Server toohello küme hello.</span><span class="sxs-lookup"><span data-stu-id="a2a36-178">Add hello other SQL Server toohello cluster.</span></span>

1. <span data-ttu-id="a2a36-179">Merhaba tarayıcı ağacında hello kümeye sağ tıklayın ve **düğüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-179">In hello browser tree, right-click hello cluster and click **Add Node**.</span></span>

    ![Küme düğümü toohello Ekle](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="a2a36-181">Merhaba, **Düğüm Ekleme Sihirbazı'nı**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-181">In hello **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="a2a36-182">Merhaba, **sunucuları Seç** sayfasında, eklemek ikinci SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="a2a36-182">In hello **Select Servers** page, add hello second SQL Server.</span></span> <span data-ttu-id="a2a36-183">Tür hello sunucu adı **sunucu adını girin** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-183">Type hello server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="a2a36-184">İşiniz bittiğinde tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="a2a36-185">Merhaba, **doğrulama uyarısı** sayfasında, **Hayır** (bir üretim senaryosunda, hello doğrulama testleri gerçekleştirmeniz gerekir).</span><span class="sxs-lookup"><span data-stu-id="a2a36-185">In hello **Validation Warning** page, click **No** (in a production scenario you should perform hello validation tests).</span></span> <span data-ttu-id="a2a36-186">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="a2a36-187">Merhaba, **onay** depolama alanları, etiketli Temizle hello onay kutusunu kullanıyorsanız, sayfa **tüm uygun depolama toohello küme ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="a2a36-187">In hello **Confirmation** page if you are using Storage Spaces, clear hello checkbox labeled **Add all eligible storage toohello cluster.**</span></span>

   ![Düğüm onay Ekle](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="a2a36-189">Depolama alanları kullanma ve değil işaretini **tüm uygun depolama toohello küme eklemek**, Windows hello kümeleme işlemi sırasında hello sanal diskler ayırır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage toohello cluster**, Windows detaches hello virtual disks during hello clustering process.</span></span> <span data-ttu-id="a2a36-190">Sonuç olarak, hello depolama alanları hello kümeden kaldırılana kadar Disk Yöneticisi'nde veya Explorer görünmez ve PowerShell kullanarak yeniden.</span><span class="sxs-lookup"><span data-stu-id="a2a36-190">As a result, they do not appear in Disk Manager or Explorer until hello storage spaces are removed from hello cluster and reattached using PowerShell.</span></span> <span data-ttu-id="a2a36-191">Depolama alanları, birden çok disk toostorage havuzlarında gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-191">Storage Spaces groups multiple disks in toostorage pools.</span></span> <span data-ttu-id="a2a36-192">Daha fazla bilgi için bkz: [depolama alanları](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="a2a36-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="a2a36-193">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-193">Click **Next**.</span></span>

1. <span data-ttu-id="a2a36-194">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-194">Click **Finish**.</span></span>

   <span data-ttu-id="a2a36-195">Yük Devretme Kümesi Yöneticisi'ni gösterir kümenizi yeni bir düğüm ve hello listeler **düğümleri** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="a2a36-195">Failover Cluster Manager shows that your cluster has a new node and lists it in hello **Nodes** container.</span></span>

10. <span data-ttu-id="a2a36-196">Merhaba Uzak Masaüstü oturumunu kapatmak.</span><span class="sxs-lookup"><span data-stu-id="a2a36-196">Log out of hello remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="a2a36-197">Bir küme çekirdek dosya paylaşımı Ekle</span><span class="sxs-lookup"><span data-stu-id="a2a36-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="a2a36-198">Bu örnekte, bir dosya paylaşımı toocreate Küme çekirdeğini hello Windows kümesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-198">In this example hello Windows cluster uses a file share toocreate a cluster quorum.</span></span> <span data-ttu-id="a2a36-199">Bu öğretici, bir düğüm ve dosya paylaşımı çoğunluğu çekirdek kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="a2a36-200">Daha fazla bilgi için bkz: [yük devretme kümesindeki çekirdek yapılandırmalarını anlama](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2a36-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="a2a36-201">Toohello dosya paylaşımı tanığı üye sunucusu ile Uzak Masaüstü oturumu bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-201">Connect toohello file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="a2a36-202">Üzerinde **Sunucu Yöneticisi'ni**, tıklatın **Araçları**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="a2a36-203">Açık **Bilgisayar Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="a2a36-204">Tıklatın **paylaşılan klasörleri**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="a2a36-205">Sağ **paylaşımları**, tıklatıp **yeni paylaşım...** .</span><span class="sxs-lookup"><span data-stu-id="a2a36-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="a2a36-207">Kullanım **bir paylaşılan klasör oluşturma Sihirbazı** toocreate bir paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="a2a36-207">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="a2a36-208">Üzerinde **klasör yolu**, tıklatın **Gözat** ve bulun veya hello paylaşılan klasör için bir yol oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2a36-208">On **Folder Path**, click **Browse** and locate or create a path for hello shared folder.</span></span> <span data-ttu-id="a2a36-209">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-209">Click **Next**.</span></span>

1. <span data-ttu-id="a2a36-210">İçinde **adı, açıklama ve ayarları** hello paylaşım adını ve yolunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-210">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="a2a36-211">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-211">Click **Next**.</span></span>

1. <span data-ttu-id="a2a36-212">Üzerinde **paylaşılan klasör izinlerini** ayarlamak **izinleri Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="a2a36-213">Tıklatın **özel...** .</span><span class="sxs-lookup"><span data-stu-id="a2a36-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="a2a36-214">Üzerinde **izinleri Özelleştir**, tıklatın **Ekle...** .</span><span class="sxs-lookup"><span data-stu-id="a2a36-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="a2a36-215">Tam Denetim bu hello kullanılan hesap toocreate hello küme olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2a36-215">Make sure that hello account used toocreate hello cluster has full control.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="a2a36-217">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-217">Click **OK**.</span></span>

1. <span data-ttu-id="a2a36-218">İçinde **paylaşılan klasör izinlerini**, tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="a2a36-219">Tıklatın **son** yeniden.</span><span class="sxs-lookup"><span data-stu-id="a2a36-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="a2a36-220">Merhaba sunucu dışında oturum</span><span class="sxs-lookup"><span data-stu-id="a2a36-220">Log out of hello server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="a2a36-221">Küme çekirdeğini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a2a36-221">Configure cluster quorum</span></span>

<span data-ttu-id="a2a36-222">Ardından, hello Küme çekirdeğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-222">Next, set hello cluster quorum.</span></span>

1. <span data-ttu-id="a2a36-223">Toohello ilk küme düğümüne Uzak Masaüstü'nü bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-223">Connect toohello first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="a2a36-224">İçinde **yük devretme kümesi Yöneticisi**, hello kümeye sağ tıklayın, çok noktası**diğer eylemler**, tıklatıp **küme çekirdek ayarlarını yapılandır...** .</span><span class="sxs-lookup"><span data-stu-id="a2a36-224">In **Failover Cluster Manager**, right-click hello cluster, point too**More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="a2a36-226">İçinde **küme çekirdeği Yapılandırma Sihirbazı**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="a2a36-227">İçinde **çekirdek yapılandırma seçeneğini**, seçin **hello çekirdek tanığı Seç**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-227">In **Select Quorum Configuration Option**, choose **Select hello quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="a2a36-228">Üzerinde **çekirdek tanığı Seç**, tıklatın **bir dosya paylaşımı tanığı Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="a2a36-229">Windows Server 2016 bulut Tanık destekler.</span><span class="sxs-lookup"><span data-stu-id="a2a36-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="a2a36-230">Bu tür bir Tanık seçerseniz, bir dosya gerekmez paylaşımı tanığını.</span><span class="sxs-lookup"><span data-stu-id="a2a36-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="a2a36-231">Daha fazla bilgi için bkz: [bir yük devretme kümesi için bir bulut tanığı dağıtmak](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="a2a36-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="a2a36-232">Bu öğretici, önceki işletim sistemleri tarafından desteklenen bir dosya paylaşımı tanığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="a2a36-233">Üzerinde **dosya paylaşımı Tanığını Yapılandır**, oluşturduğunuz hello paylaşımı için hello yolunu yazın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-233">On **Configure File Share Witness**, type hello path for hello share you created.</span></span> <span data-ttu-id="a2a36-234">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-234">Click **Next**.</span></span>

1. <span data-ttu-id="a2a36-235">Hello ayarlarını doğrulayın **onay**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-235">Verify hello settings on **Confirmation**.</span></span> <span data-ttu-id="a2a36-236">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-236">Click **Next**.</span></span>

1. <span data-ttu-id="a2a36-237">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-237">Click **Finish**.</span></span>

<span data-ttu-id="a2a36-238">Merhaba küme çekirdek kaynakları dosya paylaşım tanığı ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-238">hello cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="a2a36-239">Kullanılabilirlik gruplarını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a2a36-239">Enable Availability Groups</span></span>

<span data-ttu-id="a2a36-240">Ardından, hello etkinleştirmek **AlwaysOn Kullanılabilirlik grupları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="a2a36-240">Next, enable hello **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="a2a36-241">Her iki SQL sunucularında bu adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="a2a36-242">Merhaba gelen **Başlat** ekranında, başlatma **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-242">From hello **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="a2a36-243">Merhaba tarayıcı ağacında tıklayın **SQL Server Hizmetleri**, hello sağ tıklatın **SQL Server (MSSQLSERVER)** 'ı tıklatın ve hizmeti **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-243">In hello browser tree, click **SQL Server Services**, then right-click hello **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="a2a36-244">Merhaba tıklatın **AlwaysOn yüksek kullanılabilirlik** sekmesini ve ardından **etkinleştirmek AlwaysOn Kullanılabilirlik grupları**aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="a2a36-244">Click hello **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![AlwaysOn Kullanılabilirlik gruplarını etkinleştir](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="a2a36-246">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-246">Click **Apply**.</span></span> <span data-ttu-id="a2a36-247">Tıklatın **Tamam** hello açılan iletişim kutusunda.</span><span class="sxs-lookup"><span data-stu-id="a2a36-247">Click **OK** in hello pop-up dialog.</span></span>

5. <span data-ttu-id="a2a36-248">Merhaba SQL Server hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-248">Restart hello SQL Server service.</span></span>

<span data-ttu-id="a2a36-249">Diğer SQL Server hello bu adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-249">Repeat these steps on hello other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a><span data-ttu-id="a2a36-250">Bir veritabanı üzerinde hello oluşturmak ilk SQL Server</span><span class="sxs-lookup"><span data-stu-id="a2a36-250">Create a database on hello first SQL Server</span></span>

1. <span data-ttu-id="a2a36-251">Başlatma hello RDP dosyası toohello ilk SQL Server ile bir etki alanı hesabı başka bir deyişle bir üyesi sysadmin sabit sunucu rolü.</span><span class="sxs-lookup"><span data-stu-id="a2a36-251">Launch hello RDP file toohello first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="a2a36-252">SQL Server Management Studio'yu açın ve toohello bağlanın ilk SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a2a36-252">Open SQL Server Management Studio and connect toohello first SQL Server.</span></span>
7. <span data-ttu-id="a2a36-253">İçinde **Object Explorer**, sağ **veritabanları** tıklatıp **yeni veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="a2a36-254">İçinde **veritabanı adı**, türü **MyDB1**, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="a2a36-255"><a name="backupshare"></a>Bir yedekleme paylaşımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="a2a36-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="a2a36-256">Üzerinde ilk SQL Server'da hello **Sunucu Yöneticisi'ni**, tıklatın **Araçları**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-256">On hello first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="a2a36-257">Açık **Bilgisayar Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="a2a36-258">Tıklatın **paylaşılan klasörleri**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="a2a36-259">Sağ **paylaşımları**, tıklatıp **yeni paylaşım...** .</span><span class="sxs-lookup"><span data-stu-id="a2a36-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="a2a36-261">Kullanım **bir paylaşılan klasör oluşturma Sihirbazı** toocreate bir paylaşımı.</span><span class="sxs-lookup"><span data-stu-id="a2a36-261">Use **Create a Shared Folder Wizard** toocreate a share.</span></span>

1. <span data-ttu-id="a2a36-262">Üzerinde **klasör yolu**, tıklatın **Gözat** ve bulun veya hello veritabanı yedekleme paylaşılan klasörü için bir yol oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2a36-262">On **Folder Path**, click **Browse** and locate or create a path for hello database backup shared folder.</span></span> <span data-ttu-id="a2a36-263">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-263">Click **Next**.</span></span>

1. <span data-ttu-id="a2a36-264">İçinde **adı, açıklama ve ayarları** hello paylaşım adını ve yolunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-264">In **Name, Description, and Settings** verify hello share name and path.</span></span> <span data-ttu-id="a2a36-265">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-265">Click **Next**.</span></span>

1. <span data-ttu-id="a2a36-266">Üzerinde **paylaşılan klasör izinlerini** ayarlamak **izinleri Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="a2a36-267">Tıklatın **özel...** .</span><span class="sxs-lookup"><span data-stu-id="a2a36-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="a2a36-268">Üzerinde **izinleri Özelleştir**, tıklatın **Ekle...** .</span><span class="sxs-lookup"><span data-stu-id="a2a36-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="a2a36-269">Her iki sunucuyu Hello SQL Server ve SQL Server Aracısı hizmet hesaplarını tam denetime sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2a36-269">Make sure that hello SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="a2a36-271">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-271">Click **OK**.</span></span>

1. <span data-ttu-id="a2a36-272">İçinde **paylaşılan klasör izinlerini**, tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="a2a36-273">Tıklatın **son** yeniden.</span><span class="sxs-lookup"><span data-stu-id="a2a36-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-hello-database"></a><span data-ttu-id="a2a36-274">Tam hello veritabanı yedek alın</span><span class="sxs-lookup"><span data-stu-id="a2a36-274">Take a full backup of hello database</span></span>

<span data-ttu-id="a2a36-275">Merhaba yeni veritabanı tooinitialize hello günlük zinciri yukarı tooback gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-275">You need tooback up hello new database tooinitialize hello log chain.</span></span> <span data-ttu-id="a2a36-276">Merhaba yeni veritabanının bir yedeğini almazsanız, bir kullanılabilirlik grubuna eklenemez.</span><span class="sxs-lookup"><span data-stu-id="a2a36-276">If you do not take a backup of hello new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="a2a36-277">İçinde **Object Explorer**, hello veritabanını sağ tıklatın, çok noktası**görevleri...** , tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-277">In **Object Explorer**, right-click hello database, point too**Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="a2a36-278">Tıklatın **Tamam** tootake tam yedekleme toohello varsayılan yedekleme konumu.</span><span class="sxs-lookup"><span data-stu-id="a2a36-278">Click **OK** tootake a full backup toohello default backup location.</span></span>

## <a name="create-hello-availability-group"></a><span data-ttu-id="a2a36-279">Merhaba kullanılabilirlik grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2a36-279">Create hello Availability Group</span></span>
<span data-ttu-id="a2a36-280">Aşağıdaki hello kullanarak bir kullanılabilirlik grubu adımları hazır tooconfigure sunulmuştur:</span><span class="sxs-lookup"><span data-stu-id="a2a36-280">You are now ready tooconfigure an Availability Group using hello following steps:</span></span>

* <span data-ttu-id="a2a36-281">Bir veritabanı üzerinde hello oluşturmak ilk SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a2a36-281">Create a database on hello first SQL Server.</span></span>
* <span data-ttu-id="a2a36-282">Tam yedekleme ve hello veritabanının işlem günlüğü yedeklemesi gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="a2a36-282">Take both a full backup and a transaction log backup of hello database</span></span>
* <span data-ttu-id="a2a36-283">Tam geri yükleme hello ve SQL Server ile Merhaba ikinci günlük yedekleri toohello **NORECOVERY** seçeneği</span><span class="sxs-lookup"><span data-stu-id="a2a36-283">Restore hello full and log backups toohello second SQL Server with hello **NORECOVERY** option</span></span>
* <span data-ttu-id="a2a36-284">Merhaba kullanılabilirlik grubu oluşturun (**AG1**) zaman uyumlu tamamlama, otomatik yük devretme ve okunabilir ikincil çoğaltmalarda</span><span class="sxs-lookup"><span data-stu-id="a2a36-284">Create hello Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-hello-availability-group"></a><span data-ttu-id="a2a36-285">Merhaba kullanılabilirlik grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a2a36-285">Create hello Availability Group:</span></span>

1. <span data-ttu-id="a2a36-286">Uzak Masaüstü oturumu toohello üzerinde ilk SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a2a36-286">On remote desktop session toohello first SQL Server.</span></span> <span data-ttu-id="a2a36-287">İçinde **Object Explorer** SSMS, sağ **AlwaysOn yüksek kullanılabilirlik** tıklatıp **yeni Kullanılabilirlik Grubu Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Yeni kullanılabilirlik grubu sihirbazını başlat](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="a2a36-289">Merhaba, **giriş** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-289">In hello **Introduction** page, click **Next**.</span></span> <span data-ttu-id="a2a36-290">Merhaba, **kullanılabilirlik grubu adı belirtin** sayfasında, hello kullanılabilirlik grubu için bir ad yazın, örneğin **AG1**, **kullanılabilirlik grubu adının**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-290">In hello **Specify Availability Group Name** page, type a name for hello Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="a2a36-291">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-291">Click **Next**.</span></span>

    ![Yeni AG Sihirbazı, AG adını belirtin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="a2a36-293">Merhaba, **veritabanlarını seçin** sayfasında Veritabanınızı seçin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-293">In hello **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="a2a36-294">en az bir tam yedekleme hello hedeflenen birincil Çoğaltmada uyguladığınız için hello veritabanı bir kullanılabilirlik grubu için hello önkoşulları karşıladığını.</span><span class="sxs-lookup"><span data-stu-id="a2a36-294">hello database meets hello prerequisites for an Availability Group because you have taken at least one full backup on hello intended primary replica.</span></span>

   ![Yeni AG Sihirbazı, veritabanlarını seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="a2a36-296">Merhaba, **çoğaltmaları belirle** sayfasında, **eklemek çoğaltma**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-296">In hello **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Yeni AG Sihirbazı, çoğaltmaları belirtin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="a2a36-298">Merhaba **tooServer bağlanmak** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-298">hello **Connect tooServer** dialog pops up.</span></span> <span data-ttu-id="a2a36-299">Merhaba ikinci sunucusunun türü hello adı **sunucu adı**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-299">Type hello name of hello second server in **Server name**.</span></span> <span data-ttu-id="a2a36-300">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-300">Click **Connect**.</span></span>

   <span data-ttu-id="a2a36-301">Merhaba edilene **çoğaltmaları belirle** sayfasında, listelenen hello ikinci sunucu artık görmelisiniz **kullanılabilirlik çoğaltmalarının**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-301">Back in hello **Specify Replicas** page, you should now see hello second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="a2a36-302">Merhaba çoğaltmaları şu şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-302">Configure hello replicas as follows.</span></span>

   ![Yeni AG Sihirbazı, çoğaltmaları belirtin (tam)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="a2a36-304">Tıklatın **uç noktaları** toosee hello veritabanı yansıtma uç noktası bu kullanılabilirlik grubu için.</span><span class="sxs-lookup"><span data-stu-id="a2a36-304">Click **Endpoints** toosee hello database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="a2a36-305">Aynı bağlantı noktası hello ayarlarken kullandığınız kullanım hello [veritabanı yansıtma uç noktaları için güvenlik duvarı kuralı](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="a2a36-305">Use hello same port that you used when you set hello [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Yeni AG Sihirbazı, ilk veri eşitlemeyi seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="a2a36-307">Merhaba, **ilk veri eşitlemesi** sayfasında **tam** ve paylaşılan bir ağ konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-307">In hello **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="a2a36-308">Merhaba Hello konumu için kullanmanız [oluşturduğunuz yedekleme paylaşımı](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="a2a36-308">For hello location, use hello [backup share that you created](#backupshare).</span></span> <span data-ttu-id="a2a36-309">Merhaba örnekte olduğu, **\\\\\<ilk SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-309">In hello example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="a2a36-310">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="a2a36-311">Tam eşitleme hello veritabanı hello ilk SQL Server örneği üzerinde tam yedeğini alır ve toohello ikinci örneği geri yükler.</span><span class="sxs-lookup"><span data-stu-id="a2a36-311">Full synchronization takes a full backup of hello database on hello first instance of SQL Server and restores it toohello second instance.</span></span> <span data-ttu-id="a2a36-312">Büyük veritabanları için tam eşitleme önerilmez uzun bir süre devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="a2a36-313">El ile Merhaba veritabanının bir yedeğini almak ve onunla geri yükleme bu kez azaltabilir `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="a2a36-313">You can reduce this time by manually taking a backup of hello database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="a2a36-314">Merhaba veritabanı zaten ile geri yüklenirse `NO RECOVERY` hello ikinci SQL Server kullanılabilirlik grubu hello yapılandırmadan önce seçin **yalnızca katmak**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-314">If hello database is already restored with `NO RECOVERY` on hello second SQL Server before configuring hello Availability Group, choose **Join only**.</span></span> <span data-ttu-id="a2a36-315">Merhaba kullanılabilirlik grubu yapılandırdıktan sonra tootake hello yedekleme istiyorsanız, tercih **ilk veri eşitlemeyi atla**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-315">If you want tootake hello backup after configuring hello Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Yeni AG Sihirbazı, ilk veri eşitlemeyi seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="a2a36-317">Merhaba, **doğrulama** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-317">In hello **Validation** page, click **Next**.</span></span> <span data-ttu-id="a2a36-318">Bu sayfayı benzer toohello görüntü aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="a2a36-318">This page should look similar toohello following image:</span></span>

    ![Yeni AG Sihirbazı, doğrulama](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="a2a36-320">Bir kullanılabilirlik grubu dinleyicisi yapılandırılmadığı için hello dinleyici yapılandırması için bir uyarı yok.</span><span class="sxs-lookup"><span data-stu-id="a2a36-320">There is a warning for hello listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="a2a36-321">Azure sanal makinelerde, hello dinleyicisi hello Azure yük dengeleyici oluşturduktan sonra oluşturduğundan bu uyarıyı yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a36-321">You can ignore this warning because on Azure virtual machines you create hello listener after creating hello Azure load balancer.</span></span>

10. <span data-ttu-id="a2a36-322">Merhaba, **Özet** sayfasında, **son**, Başlangıç Sihirbazı'nı yapılandırırken bekleyin hello sonra yeni kullanılabilirlik grubu.</span><span class="sxs-lookup"><span data-stu-id="a2a36-322">In hello **Summary** page, click **Finish**, then wait while hello wizard configures hello new Availability Group.</span></span> <span data-ttu-id="a2a36-323">Merhaba, **ilerleme** tıklayabilirsiniz sayfasında, **daha fazla ayrıntı** tooview hello ayrıntılı devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="a2a36-323">In hello **Progress** page, you can click **More details** tooview hello detailed progress.</span></span> <span data-ttu-id="a2a36-324">Merhaba Sihirbaz tamamlandıktan sonra hello incelemek **sonuçları** kullanılabilirlik grubu hello sayfa tooverify başarıyla oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a2a36-324">Once hello wizard is finished, inspect hello **Results** page tooverify that hello Availability Group is successfully created.</span></span>

     ![Yeni AG Sihirbazı, sonuçlar](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="a2a36-326">Tıklatın **Kapat** tooexit hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="a2a36-326">Click **Close** tooexit hello wizard.</span></span>

### <a name="check-hello-availability-group"></a><span data-ttu-id="a2a36-327">Onay hello kullanılabilirlik grubu</span><span class="sxs-lookup"><span data-stu-id="a2a36-327">Check hello Availability Group</span></span>

1. <span data-ttu-id="a2a36-328">İçinde **Object Explorer**, genişletin **AlwaysOn yüksek kullanılabilirlik**, ardından **kullanılabilirlik grupları**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="a2a36-329">Artık görmelisiniz bu kapsayıcıda yeni kullanılabilirlik grubu hello.</span><span class="sxs-lookup"><span data-stu-id="a2a36-329">You should now see hello new Availability Group in this container.</span></span> <span data-ttu-id="a2a36-330">Merhaba kullanılabilirlik grubunu sağ tıklatın ve **Göster Pano**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-330">Right-click hello Availability Group and click **Show Dashboard**.</span></span>

   ![AG panosunu Göster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="a2a36-332">**AlwaysOn panosunu** benzer toothis görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-332">Your **AlwaysOn Dashboard** should look similar toothis.</span></span>

   ![AG Panosu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="a2a36-334">Merhaba çoğaltmalar, her çoğaltma ve hello eşitleme durumunun hello yük devretme modu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a36-334">You can see hello replicas, hello failover mode of each replica and hello synchronization state.</span></span>

2. <span data-ttu-id="a2a36-335">İçinde **yük devretme kümesi Yöneticisi**, kümenizi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="a2a36-336">Seçin **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-336">Select **Roles**.</span></span> <span data-ttu-id="a2a36-337">kullandığınız hello kullanılabilirlik grubu adını hello kümede bir roldür.</span><span class="sxs-lookup"><span data-stu-id="a2a36-337">hello Availability Group name you used is a role on hello cluster.</span></span> <span data-ttu-id="a2a36-338">Bu kullanılabilirlik grubu dinleyici yapılandırmadı olduğundan istemci bağlantıları için bir IP adresi yok.</span><span class="sxs-lookup"><span data-stu-id="a2a36-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="a2a36-339">Bir Azure yük dengeleyici oluşturduktan sonra hello dinleyicisi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-339">You will configure hello listener after you create an Azure load balancer.</span></span>

   ![Yük Devretme Kümesi Yöneticisi'nde AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="a2a36-341">Toofail hello yük devretme kümesi Yöneticisi'nden hello kullanılabilirlik grubu üzerinden çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-341">Do not try toofail over hello Availability Group from hello Failover Cluster Manager.</span></span> <span data-ttu-id="a2a36-342">Tüm yük devretme işlemlerini içinden gerçekleştirilmelidir **AlwaysOn panosunu** SSMS içinde.</span><span class="sxs-lookup"><span data-stu-id="a2a36-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="a2a36-343">Daha fazla bilgi için bkz: [kullanma kısıtlamaları hello yük devretme kümesi Yöneticisi kullanılabilirlik grupları ile](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2a36-343">For more information, see [Restrictions on Using hello Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="a2a36-344">Bu noktada, çoğaltmalar SQL Server'ın iki örneği üzerinde kullanılabilirlik grubuyla sahip.</span><span class="sxs-lookup"><span data-stu-id="a2a36-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="a2a36-345">Merhaba kullanılabilirlik grubu örnekleri arasında taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a36-345">You can move hello Availability Group between instances.</span></span> <span data-ttu-id="a2a36-346">Dinleyici olmadığından toohello kullanılabilirlik grubu henüz bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="a2a36-346">You cannot connect toohello Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="a2a36-347">Azure sanal makinelerinde hello dinleyicisi bir yük dengeleyici gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-347">In Azure virtual machines, hello listener requires a load balancer.</span></span> <span data-ttu-id="a2a36-348">Merhaba sonraki toocreate hello yük dengeleyici Azure adımdır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-348">hello next step is toocreate hello load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="a2a36-349">Bir Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2a36-349">Create an Azure load balancer</span></span>

<span data-ttu-id="a2a36-350">Azure sanal makinelerde SQL Server kullanılabilirlik grubu yük dengeleyici gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="a2a36-351">Merhaba yük dengeleyici hello kullanılabilirlik grubu dinleyicisi için başlangıç IP adresi tutar.</span><span class="sxs-lookup"><span data-stu-id="a2a36-351">hello load balancer holds hello IP address for hello Availability Group listener.</span></span> <span data-ttu-id="a2a36-352">Bu bölümde, nasıl toocreate hello yük dengeleyici hello Azure portal'ın özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-352">This section summarizes how toocreate hello load balancer in hello Azure portal.</span></span>

1. <span data-ttu-id="a2a36-353">Burada, SQL sunucuları ve tıklatın toohello kaynak grubu Hello Azure portal, Git **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-353">In hello Azure portal, go toohello resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="a2a36-354">Arama **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="a2a36-355">Microsoft tarafından yayımlanan hello yük dengeleyici seçin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-355">Choose hello load balancer published by Microsoft.</span></span>

   ![Yük Devretme Kümesi Yöneticisi'nde AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="a2a36-357">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-357">Click **Create**.</span></span>
3. <span data-ttu-id="a2a36-358">Şu parametreler hello yük dengeleyici için hello yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-358">Configure hello following parameters for hello load balancer.</span></span>

   | <span data-ttu-id="a2a36-359">Ayar</span><span class="sxs-lookup"><span data-stu-id="a2a36-359">Setting</span></span> | <span data-ttu-id="a2a36-360">Alan</span><span class="sxs-lookup"><span data-stu-id="a2a36-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="a2a36-361">**Ad**</span><span class="sxs-lookup"><span data-stu-id="a2a36-361">**Name**</span></span> |<span data-ttu-id="a2a36-362">Hello yük dengeleyici için bir metin adı kullanın örneğin **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-362">Use a text name for hello load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="a2a36-363">**Tür**</span><span class="sxs-lookup"><span data-stu-id="a2a36-363">**Type**</span></span> |<span data-ttu-id="a2a36-364">İç</span><span class="sxs-lookup"><span data-stu-id="a2a36-364">Internal</span></span> |
   | <span data-ttu-id="a2a36-365">**Sanal ağ**</span><span class="sxs-lookup"><span data-stu-id="a2a36-365">**Virtual network**</span></span> |<span data-ttu-id="a2a36-366">Hello Azure sanal ağı Hello adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-366">Use hello name of hello Azure virtual network.</span></span> |
   | <span data-ttu-id="a2a36-367">**Alt ağ**</span><span class="sxs-lookup"><span data-stu-id="a2a36-367">**Subnet**</span></span> |<span data-ttu-id="a2a36-368">Sanal makine hello hello alt ağın kullanım hello adı kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="a2a36-368">Use hello name of hello subnet that hello virtual machine is in.</span></span>  |
   | <span data-ttu-id="a2a36-369">**IP adresi ataması**</span><span class="sxs-lookup"><span data-stu-id="a2a36-369">**IP address assignment**</span></span> |<span data-ttu-id="a2a36-370">Statik</span><span class="sxs-lookup"><span data-stu-id="a2a36-370">Static</span></span> |
   | <span data-ttu-id="a2a36-371">**IP adresi**</span><span class="sxs-lookup"><span data-stu-id="a2a36-371">**IP address**</span></span> |<span data-ttu-id="a2a36-372">Kullanılabilir bir alt ağ adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="a2a36-373">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="a2a36-373">**Subscription**</span></span> |<span data-ttu-id="a2a36-374">Kullanım hello aynı abonelik hello sanal makine olarak.</span><span class="sxs-lookup"><span data-stu-id="a2a36-374">Use hello same subscription as hello virtual machine.</span></span> |
   | <span data-ttu-id="a2a36-375">**Konum**</span><span class="sxs-lookup"><span data-stu-id="a2a36-375">**Location**</span></span> |<span data-ttu-id="a2a36-376">Kullanım hello aynı konumu hello sanal makine olarak.</span><span class="sxs-lookup"><span data-stu-id="a2a36-376">Use hello same location as hello virtual machine.</span></span> |

   <span data-ttu-id="a2a36-377">Azure portal dikey penceresinde Hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="a2a36-377">hello Azure portal blade should look like this:</span></span>

   ![Yük Dengeleyici oluşturma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="a2a36-379">Tıklatın **oluşturma**, toocreate hello yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="a2a36-379">Click **Create**, toocreate hello load balancer.</span></span>

<span data-ttu-id="a2a36-380">tooconfigure hello yük dengeleyici, toocreate bir arka uç havuzu, araştırma ve kümesi hello Yük Dengeleme kuralları gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-380">tooconfigure hello load balancer, you need toocreate a backend pool, a probe, and set hello load balancing rules.</span></span> <span data-ttu-id="a2a36-381">Bu hello Azure portal yapın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-381">Do these in hello Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="a2a36-382">Arka uç havuzu ekleme</span><span class="sxs-lookup"><span data-stu-id="a2a36-382">Add backend pool</span></span>

1. <span data-ttu-id="a2a36-383">Hello Azure portal, tooyour kullanılabilirlik grubu gidin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-383">In hello Azure portal, go tooyour availability group.</span></span> <span data-ttu-id="a2a36-384">Toorefresh hello görünüm toosee hello yeni oluşturulan yük dengeleyici gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-384">You might need toorefresh hello view toosee hello newly created load balancer.</span></span>

   ![Yük Dengeleyici kaynak grubunda bulunamadı](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="a2a36-386">Merhaba yük dengeleyici tıklatın, **arka uç havuzları**, tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-386">Click hello load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="a2a36-387">Merhaba arka uç havuzu aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a2a36-387">Set hello backend pool as follows:</span></span>

   | <span data-ttu-id="a2a36-388">Ayar</span><span class="sxs-lookup"><span data-stu-id="a2a36-388">Setting</span></span> | <span data-ttu-id="a2a36-389">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a2a36-389">Description</span></span> | <span data-ttu-id="a2a36-390">Örnek</span><span class="sxs-lookup"><span data-stu-id="a2a36-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="a2a36-391">**Ad**</span><span class="sxs-lookup"><span data-stu-id="a2a36-391">**Name**</span></span> | <span data-ttu-id="a2a36-392">Bir metin yazın</span><span class="sxs-lookup"><span data-stu-id="a2a36-392">Type a text name</span></span> | <span data-ttu-id="a2a36-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="a2a36-393">SQLLBBE</span></span>
   | <span data-ttu-id="a2a36-394">**İle ilişkili**</span><span class="sxs-lookup"><span data-stu-id="a2a36-394">**Associated to**</span></span> | <span data-ttu-id="a2a36-395">Listeden seçin</span><span class="sxs-lookup"><span data-stu-id="a2a36-395">Pick from list</span></span> | <span data-ttu-id="a2a36-396">Kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="a2a36-396">Availability set</span></span>
   | <span data-ttu-id="a2a36-397">**Kullanılabilirlik kümesi**</span><span class="sxs-lookup"><span data-stu-id="a2a36-397">**Availability set**</span></span> | <span data-ttu-id="a2a36-398">SQL Server Vm'lerinin bulunan hello kullanılabilirlik kümesi adını kullanın</span><span class="sxs-lookup"><span data-stu-id="a2a36-398">Use a name of hello availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="a2a36-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="a2a36-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="a2a36-400">**Sanal makineler**</span><span class="sxs-lookup"><span data-stu-id="a2a36-400">**Virtual machines**</span></span> |<span data-ttu-id="a2a36-401">Merhaba iki Azure SQL Server VM adları</span><span class="sxs-lookup"><span data-stu-id="a2a36-401">hello two Azure SQL Server VM names</span></span> | <span data-ttu-id="a2a36-402">SQLServer-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="a2a36-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="a2a36-403">Merhaba hello arka uç havuzu için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-403">Type hello name for hello back end pool.</span></span>

1. <span data-ttu-id="a2a36-404">Tıklatın **+ bir sanal makine Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="a2a36-405">Merhaba kullanılabilirlik kümesi için SQL sunucusu olduğundan bu hello hello kullanılabilirlik kümesi'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-405">For hello availability set, choose hello availability set that hello SQL Servers are in.</span></span>

1. <span data-ttu-id="a2a36-406">Sanal makineler için ikisi de hello SQL sunucuları içerir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-406">For virtual machines, include both of hello SQL Servers.</span></span> <span data-ttu-id="a2a36-407">Merhaba dosya paylaşımı tanığı sunucusu içermez.</span><span class="sxs-lookup"><span data-stu-id="a2a36-407">Do not include hello file share witness server.</span></span>

1. <span data-ttu-id="a2a36-408">Tıklatın **Tamam** toocreate hello arka uç havuzu.</span><span class="sxs-lookup"><span data-stu-id="a2a36-408">Click **OK** toocreate hello backend pool.</span></span>

### <a name="set-hello-probe"></a><span data-ttu-id="a2a36-409">Kümesi hello araştırması</span><span class="sxs-lookup"><span data-stu-id="a2a36-409">Set hello probe</span></span>

1. <span data-ttu-id="a2a36-410">Merhaba yük dengeleyici tıklatın, **sistem durumu araştırmalarının**, tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-410">Click hello load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="a2a36-411">Merhaba durumu araştırması aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a2a36-411">Set hello health probe as follows:</span></span>

   | <span data-ttu-id="a2a36-412">Ayar</span><span class="sxs-lookup"><span data-stu-id="a2a36-412">Setting</span></span> | <span data-ttu-id="a2a36-413">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a2a36-413">Description</span></span> | <span data-ttu-id="a2a36-414">Örnek</span><span class="sxs-lookup"><span data-stu-id="a2a36-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="a2a36-415">**Ad**</span><span class="sxs-lookup"><span data-stu-id="a2a36-415">**Name**</span></span> | <span data-ttu-id="a2a36-416">Metin</span><span class="sxs-lookup"><span data-stu-id="a2a36-416">Text</span></span> | <span data-ttu-id="a2a36-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="a2a36-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="a2a36-418">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="a2a36-418">**Protocol**</span></span> | <span data-ttu-id="a2a36-419">TCP seçin</span><span class="sxs-lookup"><span data-stu-id="a2a36-419">Choose TCP</span></span> | <span data-ttu-id="a2a36-420">TCP</span><span class="sxs-lookup"><span data-stu-id="a2a36-420">TCP</span></span> |
   | <span data-ttu-id="a2a36-421">**Bağlantı Noktası**</span><span class="sxs-lookup"><span data-stu-id="a2a36-421">**Port**</span></span> | <span data-ttu-id="a2a36-422">Kullanılmayan bir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="a2a36-422">Any unused port</span></span> | <span data-ttu-id="a2a36-423">59999</span><span class="sxs-lookup"><span data-stu-id="a2a36-423">59999</span></span> |
   | <span data-ttu-id="a2a36-424">**Aralığı**</span><span class="sxs-lookup"><span data-stu-id="a2a36-424">**Interval**</span></span>  | <span data-ttu-id="a2a36-425">saniye cinsinden araştırma arasındaki süre miktarı Hello çalışır</span><span class="sxs-lookup"><span data-stu-id="a2a36-425">hello amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="a2a36-426">5</span><span class="sxs-lookup"><span data-stu-id="a2a36-426">5</span></span> |
   | <span data-ttu-id="a2a36-427">**Sağlıksız durum eşiği.**</span><span class="sxs-lookup"><span data-stu-id="a2a36-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="a2a36-428">Merhaba sağlıksız kabul bir sanal makine toobe için oluşması gereken arka arkaya araştırma hatası sayısı</span><span class="sxs-lookup"><span data-stu-id="a2a36-428">hello number of consecutive probe failures that must occur for a virtual machine toobe considered unhealthy</span></span>  | <span data-ttu-id="a2a36-429">2</span><span class="sxs-lookup"><span data-stu-id="a2a36-429">2</span></span> |

1. <span data-ttu-id="a2a36-430">Tıklatın **Tamam** tooset hello durumu araştırması.</span><span class="sxs-lookup"><span data-stu-id="a2a36-430">Click **OK** tooset hello health probe.</span></span>

### <a name="set-hello-load-balancing-rules"></a><span data-ttu-id="a2a36-431">Merhaba Yük Dengeleme kuralları ayarlama</span><span class="sxs-lookup"><span data-stu-id="a2a36-431">Set hello load balancing rules</span></span>

1. <span data-ttu-id="a2a36-432">Merhaba yük dengeleyici tıklatın, **Yük Dengeleme kuralları**, tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-432">Click hello load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="a2a36-433">Merhaba Yük Dengeleme kuralları aşağıdaki gibi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-433">Set hello load balancing rules as follows.</span></span>
   | <span data-ttu-id="a2a36-434">Ayar</span><span class="sxs-lookup"><span data-stu-id="a2a36-434">Setting</span></span> | <span data-ttu-id="a2a36-435">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a2a36-435">Description</span></span> | <span data-ttu-id="a2a36-436">Örnek</span><span class="sxs-lookup"><span data-stu-id="a2a36-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="a2a36-437">**Ad**</span><span class="sxs-lookup"><span data-stu-id="a2a36-437">**Name**</span></span> | <span data-ttu-id="a2a36-438">Metin</span><span class="sxs-lookup"><span data-stu-id="a2a36-438">Text</span></span> | <span data-ttu-id="a2a36-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="a2a36-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="a2a36-440">**Ön uç IP adresi**</span><span class="sxs-lookup"><span data-stu-id="a2a36-440">**Frontend IP address**</span></span> | <span data-ttu-id="a2a36-441">Adres seçin</span><span class="sxs-lookup"><span data-stu-id="a2a36-441">Choose an address</span></span> |<span data-ttu-id="a2a36-442">Merhaba yük dengeleyici oluşturduğunuz sırada oluşturduğunuz hello adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-442">Use hello address that you created when you created hello load balancer.</span></span> |
   | <span data-ttu-id="a2a36-443">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="a2a36-443">**Protocol**</span></span> | <span data-ttu-id="a2a36-444">TCP seçin</span><span class="sxs-lookup"><span data-stu-id="a2a36-444">Choose TCP</span></span> |<span data-ttu-id="a2a36-445">TCP</span><span class="sxs-lookup"><span data-stu-id="a2a36-445">TCP</span></span> |
   | <span data-ttu-id="a2a36-446">**Bağlantı Noktası**</span><span class="sxs-lookup"><span data-stu-id="a2a36-446">**Port**</span></span> | <span data-ttu-id="a2a36-447">Merhaba SQL Server örneği için başlangıç bağlantı noktası kullanma</span><span class="sxs-lookup"><span data-stu-id="a2a36-447">Use hello port for hello SQL Server instance</span></span> | <span data-ttu-id="a2a36-448">1433</span><span class="sxs-lookup"><span data-stu-id="a2a36-448">1433</span></span> |
   | <span data-ttu-id="a2a36-449">**Arka uç bağlantı noktası**</span><span class="sxs-lookup"><span data-stu-id="a2a36-449">**Backend Port**</span></span> | <span data-ttu-id="a2a36-450">Kayan IP için doğrudan sunucu dönüş ayarladığınızda, bu alan kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="a2a36-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="a2a36-451">1433</span><span class="sxs-lookup"><span data-stu-id="a2a36-451">1433</span></span> |
   | <span data-ttu-id="a2a36-452">**Araştırma**</span><span class="sxs-lookup"><span data-stu-id="a2a36-452">**Probe**</span></span> |<span data-ttu-id="a2a36-453">Merhaba araştırması için belirtilen hello adı</span><span class="sxs-lookup"><span data-stu-id="a2a36-453">hello name you specified for hello probe</span></span> | <span data-ttu-id="a2a36-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="a2a36-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="a2a36-455">**Oturum kalıcılığı**</span><span class="sxs-lookup"><span data-stu-id="a2a36-455">**Session Persistence**</span></span> | <span data-ttu-id="a2a36-456">Açılan liste</span><span class="sxs-lookup"><span data-stu-id="a2a36-456">Drop down list</span></span> | <span data-ttu-id="a2a36-457">**Yok**</span><span class="sxs-lookup"><span data-stu-id="a2a36-457">**None**</span></span> |
   | <span data-ttu-id="a2a36-458">**Boşta kalma zaman aşımı**</span><span class="sxs-lookup"><span data-stu-id="a2a36-458">**Idle Timeout**</span></span> | <span data-ttu-id="a2a36-459">Bir TCP bağlantı açmak dakika tookeep</span><span class="sxs-lookup"><span data-stu-id="a2a36-459">Minutes tookeep a TCP connection open</span></span> | <span data-ttu-id="a2a36-460">4</span><span class="sxs-lookup"><span data-stu-id="a2a36-460">4</span></span> |
   | <span data-ttu-id="a2a36-461">**Kayan IP (doğrudan sunucu dönüşü)**</span><span class="sxs-lookup"><span data-stu-id="a2a36-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="a2a36-462">Etkin</span><span class="sxs-lookup"><span data-stu-id="a2a36-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="a2a36-463">Doğrudan sunucu dönüşü oluşturma sırasında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-463">Direct server return is set during creation.</span></span> <span data-ttu-id="a2a36-464">Değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="a2a36-464">It cannot be changed.</span></span>

1. <span data-ttu-id="a2a36-465">Tıklatın **Tamam** tooset hello Yük Dengeleme kuralları.</span><span class="sxs-lookup"><span data-stu-id="a2a36-465">Click **OK** tooset hello load balancing rules.</span></span>

## <span data-ttu-id="a2a36-466"><a name="configure-listener"></a>Merhaba dinleyicisini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a2a36-466"><a name="configure-listener"></a> Configure hello listener</span></span>

<span data-ttu-id="a2a36-467">Merhaba sonraki şey toodo tooconfigure hello yük devretme kümesindeki bir kullanılabilirlik grubu dinleyicisi ' dir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-467">hello next thing toodo is tooconfigure an Availability Group listener on hello failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a2a36-468">Bu öğretici nasıl toocreate tek bir dinleyici - bir ILB'nin IP adresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-468">This tutorial shows how toocreate a single listener - with one ILB IP address.</span></span> <span data-ttu-id="a2a36-469">bir veya daha fazla IP adresi kullanarak bir veya daha fazla dinleyicileri toocreate bakın [oluşturma kullanılabilirlik grubu dinleyici ve yük dengeleyici | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2a36-469">toocreate one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="a2a36-470">Set dinleyicisi bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="a2a36-470">Set listener port</span></span>

<span data-ttu-id="a2a36-471">SQL Server Management Studio'da hello dinleyicisi bağlantı noktası ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-471">In SQL Server Management Studio, set hello listener port.</span></span>

1. <span data-ttu-id="a2a36-472">SQL Server Management Studio'yu başlatın ve toohello birincil çoğaltma bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a2a36-472">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="a2a36-473">Çok gidin**AlwaysOn yüksek kullanılabilirlik** | **kullanılabilirlik grupları** | **kullanılabilirlik grubu dinleyicileri**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-473">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="a2a36-474">Yük Devretme Kümesi Yöneticisi'nde oluşturulan hello dinleyici adı görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a2a36-474">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="a2a36-475">Merhaba dinleyicisi adını sağ tıklatıp **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-475">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="a2a36-476">Merhaba, **bağlantı noktası** kutusunda, daha önce kullandığınız $EndpointPort hello kullanarak hello hello kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (1433 olduğu hello varsayılan), ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a2a36-476">In hello **Port** box, specify hello port number for hello Availability Group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

<span data-ttu-id="a2a36-477">Artık Azure sanal makinelerde Kaynak Yöneticisi modunda çalışan bir SQL Server kullanılabilirlik grubu vardır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-toolistener"></a><span data-ttu-id="a2a36-478">Test bağlantısı toolistener</span><span class="sxs-lookup"><span data-stu-id="a2a36-478">Test connection toolistener</span></span>

<span data-ttu-id="a2a36-479">tootest hello bağlantısı:</span><span class="sxs-lookup"><span data-stu-id="a2a36-479">tootest hello connection:</span></span>

1. <span data-ttu-id="a2a36-480">RDP tooa hello SQL Server aynı sanal ağ, ancak kendi hello çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="a2a36-480">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="a2a36-481">Kullanabileceğiniz diğer SQL Server hello kümedeki hello.</span><span class="sxs-lookup"><span data-stu-id="a2a36-481">You can use hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="a2a36-482">Kullanım **sqlcmd** yardımcı programı tootest hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="a2a36-482">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="a2a36-483">Örneğin, komut dosyası izleyen hello kurar bir **sqlcmd** bağlantı toohello birincil çoğaltma Windows kimlik doğrulaması ile Merhaba dinleyicisi aracılığıyla:</span><span class="sxs-lookup"><span data-stu-id="a2a36-483">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="a2a36-484">Merhaba dinleyicisi dışında bir bağlantı noktası kullanıyorsa, varsayılan hello (1433) bağlantı noktası, başlangıç bağlantı noktası başlangıç bağlantı dizesinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="a2a36-484">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="a2a36-485">Örneğin, hello aşağıdaki sqlcmd komut tooa dinleyicisi bağlantı noktası 1435 bağlanır:</span><span class="sxs-lookup"><span data-stu-id="a2a36-485">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="a2a36-486">Merhaba SQLCMD bağlantı toowhichever örneğini SQL Server konakları hello birincil çoğaltma otomatik olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="a2a36-486">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="a2a36-487">Belirttiğiniz başlangıç bağlantı noktası hem SQL sunucuları hello güvenlik duvarı açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a2a36-487">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="a2a36-488">Her iki sunucuyu hello kullandığınız TCP bağlantı noktası için bir gelen kuralı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a2a36-488">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="a2a36-489">Daha fazla bilgi için bkz: [Ekle veya Düzenle güvenlik duvarı kuralı](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2a36-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a><span data-ttu-id="a2a36-490">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2a36-490">Next steps</span></span>

- <span data-ttu-id="a2a36-491">[İkinci bir kullanılabilirlik grubu için bir IP adresi tooa yük dengeleyici eklemek](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="a2a36-491">[Add an IP address tooa load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
