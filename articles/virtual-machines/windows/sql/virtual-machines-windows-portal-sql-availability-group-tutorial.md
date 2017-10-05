---
title: "SQL Server kullanılabilirlik gruplarını - Azure sanal makineleri - Öğreticisi | Microsoft Docs"
description: "Bu öğretici Azure sanal makineler üzerinde bir SQL Server her zaman üzerinde kullanılabilirlik grubu oluşturulacağını gösterir."
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
ms.openlocfilehash: 228ca9ca5fddc493d27bfd6a40df5ee7306d6aa9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a><span data-ttu-id="81f8c-103">Yapılandırma her zaman üzerindeki kullanılabilirlik grubu Azure VM'de el ile</span><span class="sxs-lookup"><span data-stu-id="81f8c-103">Configure Always On Availability Group in Azure VM manually</span></span>

<span data-ttu-id="81f8c-104">Bu öğretici Azure sanal makineler üzerinde bir SQL Server her zaman üzerinde kullanılabilirlik grubu oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-104">This tutorial shows how to create a SQL Server Always On Availability Group on Azure Virtual Machines.</span></span> <span data-ttu-id="81f8c-105">Tam öğretici iki SQL sunucusu üzerindeki veritabanı çoğaltmasıyla bir kullanılabilirlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="81f8c-105">The complete tutorial creates an Availability Group with a database replica on two SQL Servers.</span></span>

<span data-ttu-id="81f8c-106">**Zaman tahmin**: Önkoşullar sağlandığında tamamlanması yaklaşık 30 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="81f8c-106">**Time estimate**: Takes about 30 minutes to complete once the prerequisites are met.</span></span>

<span data-ttu-id="81f8c-107">Aşağıdaki diyagramda, öğreticide yapı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-107">The diagram illustrates what you build in the tutorial.</span></span>

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a><span data-ttu-id="81f8c-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="81f8c-109">Prerequisites</span></span>

<span data-ttu-id="81f8c-110">Öğretici, SQL Server Always On kullanılabilirlik grupları temel bilgilere sahip varsayar.</span><span class="sxs-lookup"><span data-stu-id="81f8c-110">The tutorial assumes you have a basic understanding of SQL Server Always On Availability Groups.</span></span> <span data-ttu-id="81f8c-111">Daha fazla bilgi için bkz: [genel bakış, Always On kullanılabilirlik grupları (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span><span class="sxs-lookup"><span data-stu-id="81f8c-111">If you need more information, see [Overview of Always On Availability Groups (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).</span></span>

<span data-ttu-id="81f8c-112">Aşağıdaki tabloda bu öğreticiye başlamadan önce tamamlamanız gereken önkoşulları listeler:</span><span class="sxs-lookup"><span data-stu-id="81f8c-112">The following table lists the prerequisites that you need to complete before starting this tutorial:</span></span>

|  |<span data-ttu-id="81f8c-113">Gereksinim</span><span class="sxs-lookup"><span data-stu-id="81f8c-113">Requirement</span></span> |<span data-ttu-id="81f8c-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="81f8c-114">Description</span></span> |
|----- |----- |----- |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | <span data-ttu-id="81f8c-116">İki SQL sunucuları</span><span class="sxs-lookup"><span data-stu-id="81f8c-116">Two SQL Servers</span></span> | <span data-ttu-id="81f8c-117">-Bir Azure kullanılabilirlik kümesine</span><span class="sxs-lookup"><span data-stu-id="81f8c-117">- In an Azure availability set</span></span> <br/> <span data-ttu-id="81f8c-118">-Tek bir etki alanı</span><span class="sxs-lookup"><span data-stu-id="81f8c-118">- In a single domain</span></span> <br/> <span data-ttu-id="81f8c-119">-Yük Devretme Kümelemesi özelliği yüklü olan</span><span class="sxs-lookup"><span data-stu-id="81f8c-119">- With Failover Clustering feature installed</span></span> |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| <span data-ttu-id="81f8c-121">Windows Server</span><span class="sxs-lookup"><span data-stu-id="81f8c-121">Windows Server</span></span> | <span data-ttu-id="81f8c-122">Küme Tanık dosya paylaşımı</span><span class="sxs-lookup"><span data-stu-id="81f8c-122">File share for cluster witness</span></span> |  
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="81f8c-124">SQL Server hizmet hesabı</span><span class="sxs-lookup"><span data-stu-id="81f8c-124">SQL Server service account</span></span> | <span data-ttu-id="81f8c-125">Etki alanı hesabı</span><span class="sxs-lookup"><span data-stu-id="81f8c-125">Domain account</span></span> |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="81f8c-127">SQL Server Aracısı hizmet hesabı</span><span class="sxs-lookup"><span data-stu-id="81f8c-127">SQL Server Agent service account</span></span> | <span data-ttu-id="81f8c-128">Etki alanı hesabı</span><span class="sxs-lookup"><span data-stu-id="81f8c-128">Domain account</span></span> |  
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="81f8c-130">Güvenlik Duvarı bağlantı noktalarını açın</span><span class="sxs-lookup"><span data-stu-id="81f8c-130">Firewall ports open</span></span> | <span data-ttu-id="81f8c-131">-SQL Server: **1433** varsayılan örnek için</span><span class="sxs-lookup"><span data-stu-id="81f8c-131">- SQL Server: **1433** for default instance</span></span> <br/> <span data-ttu-id="81f8c-132">-Veritabanı yansıtma uç noktası: **5022** veya tüm kullanılabilir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="81f8c-132">- Database mirroring endpoint: **5022** or any available port</span></span> <br/> <span data-ttu-id="81f8c-133">-Azure yük dengeleyici araştırmasını: **59999** veya tüm kullanılabilir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="81f8c-133">- Azure load balancer probe: **59999** or any available port</span></span> |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="81f8c-135">Yük Devretme Kümelemesi özelliği Ekle</span><span class="sxs-lookup"><span data-stu-id="81f8c-135">Add Failover Clustering Feature</span></span> | <span data-ttu-id="81f8c-136">Bu özellik, her iki SQL sunucuları gerektirir</span><span class="sxs-lookup"><span data-stu-id="81f8c-136">Both SQL Servers require this feature</span></span> |
|![Kare](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|<span data-ttu-id="81f8c-138">Yükleme etki alanı hesabı</span><span class="sxs-lookup"><span data-stu-id="81f8c-138">Installation domain account</span></span> | <span data-ttu-id="81f8c-139">-Her bir SQL Server yerel yönetici</span><span class="sxs-lookup"><span data-stu-id="81f8c-139">- Local administrator on each SQL Server</span></span> <br/> <span data-ttu-id="81f8c-140">-Her SQL Server örneği için SQL Server sysadmin sabit sunucu rolünün üyesi</span><span class="sxs-lookup"><span data-stu-id="81f8c-140">- Member of SQL Server sysadmin fixed server role for each instance of SQL Server</span></span>  |


<span data-ttu-id="81f8c-141">Öğreticiye başlamadan önce şunları gerçekleştirmeniz [tamamlamak Azure sanal makinelerinde Always On kullanılabilirlik grupları oluşturmak için Önkoşullar](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span><span class="sxs-lookup"><span data-stu-id="81f8c-141">Before you begin the tutorial, you need to [Complete prerequisites for creating Always On Availability Groups in Azure Virtual Machines](virtual-machines-windows-portal-sql-availability-group-prereq.md).</span></span> <span data-ttu-id="81f8c-142">Bu Önkoşullar zaten tamamladıysanız, atlayabilirsiniz [küme oluşturma](#CreateCluster).</span><span class="sxs-lookup"><span data-stu-id="81f8c-142">If these prerequisites are completed already, you can jump to [Create Cluster](#CreateCluster).</span></span>


<span data-ttu-id="81f8c-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="81f8c-143"><!--**Procedure**: *This is the first “step”. Make titles H2’s and short and clear – H2’s appear in the right pane on the web page and are important for navigation.*-->

<a name="CreateCluster"></a>
## Create the cluster</span></span>

<span data-ttu-id="81f8c-144">Önkoşullar tamamlandıktan sonra ilk adım iki SQL Server'lar içeren Windows Server Yük devretme kümesi ve bir Tanık oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-144">After the prerequisites are completed, the first step is to create a Windows Server Failover Cluster that includes two SQL Severs and a witness server.</span></span>  

1. <span data-ttu-id="81f8c-145">RDP SQL sunucuları ve Tanık sunucu üzerindeki bir yönetici olan bir etki alanı hesabı kullanarak ilk SQL Server.</span><span class="sxs-lookup"><span data-stu-id="81f8c-145">RDP to the first SQL Server using a domain account that is an administrator on both SQL Servers and the witness server.</span></span>

   >[!TIP]
   ><span data-ttu-id="81f8c-146">İzlediyseniz [önkoşul belgesi](virtual-machines-windows-portal-sql-availability-group-prereq.md), adlı bir hesap oluşturulan **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-146">If you followed the [prerequisites document](virtual-machines-windows-portal-sql-availability-group-prereq.md), you created an account called **CORP\Install**.</span></span> <span data-ttu-id="81f8c-147">Bu hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-147">Use this account.</span></span>

2. <span data-ttu-id="81f8c-148">İçinde **Sunucu Yöneticisi'ni** Pano, select **Araçları**ve ardından **yük devretme kümesi Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-148">In the **Server Manager** dashboard, select **Tools**, and then click **Failover Cluster Manager**.</span></span>
3. <span data-ttu-id="81f8c-149">Sol bölmesinde, **yük devretme kümesi Yöneticisi**ve ardından **bir küme oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-149">In the left pane, right-click **Failover Cluster Manager**, and then click **Create a Cluster**.</span></span>
   <span data-ttu-id="81f8c-150">![Küme oluşturma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span><span class="sxs-lookup"><span data-stu-id="81f8c-150">![Create Cluster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)</span></span>
4. <span data-ttu-id="81f8c-151">Küme oluşturma Sihirbazı'nda, aşağıdaki tablodaki ayarları sayfalarında adımla tek düğümlü bir küme oluşturun:</span><span class="sxs-lookup"><span data-stu-id="81f8c-151">In the Create Cluster Wizard, create a one-node cluster by stepping through the pages with the settings in the following table:</span></span>

   | <span data-ttu-id="81f8c-152">Sayfa</span><span class="sxs-lookup"><span data-stu-id="81f8c-152">Page</span></span> | <span data-ttu-id="81f8c-153">Ayarlar</span><span class="sxs-lookup"><span data-stu-id="81f8c-153">Settings</span></span> |
   | --- | --- |
   | <span data-ttu-id="81f8c-154">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="81f8c-154">Before You Begin</span></span> |<span data-ttu-id="81f8c-155">Varsayılanları kullanın</span><span class="sxs-lookup"><span data-stu-id="81f8c-155">Use defaults</span></span> |
   | <span data-ttu-id="81f8c-156">Sunucuları seçin</span><span class="sxs-lookup"><span data-stu-id="81f8c-156">Select Servers</span></span> |<span data-ttu-id="81f8c-157">İlk SQL Server adı yazın **sunucu adını girin** tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-157">Type the first SQL Server name in **Enter server name** and click **Add**.</span></span> |
   | <span data-ttu-id="81f8c-158">Doğrulama uyarısı</span><span class="sxs-lookup"><span data-stu-id="81f8c-158">Validation Warning</span></span> |<span data-ttu-id="81f8c-159">Seçin **ı bu küme için Microsoft desteğine gereksiniminiz ve bu nedenle doğrulama testlerini çalıştırmak istemiyorsanız Hayır. Sonraki tıkladığınızda, kümeyi oluşturmaya devam**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-159">Select **No. I do not require support from Microsoft for this cluster, and therefore do not want to run the validation tests. When I click Next, continue Creating the cluster**.</span></span> |
   | <span data-ttu-id="81f8c-160">Kümeyi yönetmek için erişim noktası</span><span class="sxs-lookup"><span data-stu-id="81f8c-160">Access Point for Administering the Cluster</span></span> |<span data-ttu-id="81f8c-161">Bir küme adı yazın, örneğin **SQLAGCluster1** içinde **küme adı**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-161">Type a cluster name, for example **SQLAGCluster1** in **Cluster Name**.</span></span>|
   | <span data-ttu-id="81f8c-162">Onay</span><span class="sxs-lookup"><span data-stu-id="81f8c-162">Confirmation</span></span> |<span data-ttu-id="81f8c-163">Depolama alanları kullanmadığınız sürece varsayılan ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-163">Use defaults unless you are using Storage Spaces.</span></span> <span data-ttu-id="81f8c-164">Bu tablonun altındaki nota bakın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-164">See the note following this table.</span></span> |

### <a name="set-the-cluster-ip-address"></a><span data-ttu-id="81f8c-165">Küme IP adresi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="81f8c-165">Set the cluster IP address</span></span>

1. <span data-ttu-id="81f8c-166">İçinde **yük devretme kümesi Yöneticisi**, aşağı kaydırarak **küme çekirdek kaynakları** ve küme Ayrıntıları'nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-166">In **Failover Cluster Manager**, scroll down to **Cluster Core Resources** and expand the cluster details.</span></span> <span data-ttu-id="81f8c-167">Her ikisi de görmelisiniz **adı** ve **IP adresi** kaynaklarında **başarısız** durumu.</span><span class="sxs-lookup"><span data-stu-id="81f8c-167">You should see both the **Name** and the **IP Address** resources in the **Failed** state.</span></span> <span data-ttu-id="81f8c-168">Küme makine aynı IP adresine atandığından IP adresi kaynağı çevrimiçi duruma getirilemiyor, bu nedenle, yinelenen bir adresi.</span><span class="sxs-lookup"><span data-stu-id="81f8c-168">The IP address resource cannot be brought online because the cluster is assigned the same IP address as the machine itself, therefore it is a duplicate address.</span></span>

2. <span data-ttu-id="81f8c-169">Başarısız sağ **IP adresi** kaynak ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-169">Right-click the failed **IP Address** resource, and then click **Properties**.</span></span>

   ![Küme Özellikleri](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. <span data-ttu-id="81f8c-171">Seçin **statik IP adresi** ve kullanılabilir bir SQL Server adresi metin kutusuna olduğu alt ağ adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-171">Select **Static IP Address** and specify an available address from subnet where the SQL Server is in the Address text box.</span></span> <span data-ttu-id="81f8c-172">Ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-172">Then, click **OK**.</span></span>
4. <span data-ttu-id="81f8c-173">İçinde **küme çekirdek kaynakları** bölümünde, küme adını sağ tıklatın ve **çevrimiçine**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-173">In the **Cluster Core Resources** section, right-click cluster name and click **Bring Online**.</span></span> <span data-ttu-id="81f8c-174">Daha sonra her iki kaynağın çevrimiçi olana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-174">Then, wait until both resources are online.</span></span> <span data-ttu-id="81f8c-175">Küme Adı kaynağını çevrimiçi olduğunda, DC sunucusuna yeni bir AD bilgisayar hesabı ile güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-175">When the cluster name resource comes online, it updates the DC server with a new AD computer account.</span></span> <span data-ttu-id="81f8c-176">Kullanılabilirlik grubu kümelenmiş hizmet daha sonra çalıştırmak için bu AD hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-176">Use this AD account to run the Availability Group clustered service later.</span></span>

### <span data-ttu-id="81f8c-177"><a name="addNode"></a>Kümeye bir SQL Server ekleyin</span><span class="sxs-lookup"><span data-stu-id="81f8c-177"><a name="addNode"></a>Add the other SQL Server to cluster</span></span>

<span data-ttu-id="81f8c-178">Bir SQL Server kümeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-178">Add the other SQL Server to the cluster.</span></span>

1. <span data-ttu-id="81f8c-179">Tarayıcı ağacında kümeye sağ tıklayın ve **düğüm Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-179">In the browser tree, right-click the cluster and click **Add Node**.</span></span>

    ![Düğümü kümeye ekleme](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. <span data-ttu-id="81f8c-181">İçinde **Düğüm Ekleme Sihirbazı'nı**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-181">In the **Add Node Wizard**, click **Next**.</span></span> <span data-ttu-id="81f8c-182">İçinde **sunucuları Seç** sayfasında, ikinci SQL Server ekleyin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-182">In the **Select Servers** page, add the second SQL Server.</span></span> <span data-ttu-id="81f8c-183">Sunucu adı yazın **sunucu adını girin** ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-183">Type the server name in **Enter server name** and then click **Add**.</span></span> <span data-ttu-id="81f8c-184">İşiniz bittiğinde tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-184">When you are done, click **Next**.</span></span>

1. <span data-ttu-id="81f8c-185">İçinde **doğrulama uyarısı** sayfasında, **Hayır** (bir üretim senaryosunda, doğrulama testleri gerçekleştirmeniz gerekir).</span><span class="sxs-lookup"><span data-stu-id="81f8c-185">In the **Validation Warning** page, click **No** (in a production scenario you should perform the validation tests).</span></span> <span data-ttu-id="81f8c-186">Ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-186">Then, click **Next**.</span></span>

8. <span data-ttu-id="81f8c-187">İçinde **onay** depolama alanları kullanıyorsanız sayfasında, etiketli onay kutusunun işaretini **tüm uygun depolama kümeye ekleyin.**</span><span class="sxs-lookup"><span data-stu-id="81f8c-187">In the **Confirmation** page if you are using Storage Spaces, clear the checkbox labeled **Add all eligible storage to the cluster.**</span></span>

   ![Düğüm onay Ekle](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   ><span data-ttu-id="81f8c-189">Depolama alanları kullanma ve değil işaretini **tüm uygun depolamayı kümeye eklemek**, Windows Kümeleme işlemi sırasında sanal diskleri ayırır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-189">If you are using Storage Spaces and do not uncheck **Add all eligible storage to the cluster**, Windows detaches the virtual disks during the clustering process.</span></span> <span data-ttu-id="81f8c-190">Sonuç olarak, depolama alanları kümeden kaldırılana kadar Disk Yöneticisi'nde veya Explorer görünmez ve PowerShell kullanarak yeniden.</span><span class="sxs-lookup"><span data-stu-id="81f8c-190">As a result, they do not appear in Disk Manager or Explorer until the storage spaces are removed from the cluster and reattached using PowerShell.</span></span> <span data-ttu-id="81f8c-191">Depolama alanları, birden çok diskleri depolama havuzları için gruplar.</span><span class="sxs-lookup"><span data-stu-id="81f8c-191">Storage Spaces groups multiple disks in to storage pools.</span></span> <span data-ttu-id="81f8c-192">Daha fazla bilgi için bkz: [depolama alanları](https://technet.microsoft.com/library/hh831739).</span><span class="sxs-lookup"><span data-stu-id="81f8c-192">For more information, see [Storage Spaces](https://technet.microsoft.com/library/hh831739).</span></span>

1. <span data-ttu-id="81f8c-193">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-193">Click **Next**.</span></span>

1. <span data-ttu-id="81f8c-194">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-194">Click **Finish**.</span></span>

   <span data-ttu-id="81f8c-195">Yük Devretme Kümesi Yöneticisi'ni gösterir kümenizi yeni bir düğüm ve içinde listeler **düğümleri** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="81f8c-195">Failover Cluster Manager shows that your cluster has a new node and lists it in the **Nodes** container.</span></span>

10. <span data-ttu-id="81f8c-196">Uzak Masaüstü oturumunu kapatmak.</span><span class="sxs-lookup"><span data-stu-id="81f8c-196">Log out of the remote desktop session.</span></span>

### <a name="add-a-cluster-quorum-file-share"></a><span data-ttu-id="81f8c-197">Bir küme çekirdek dosya paylaşımı Ekle</span><span class="sxs-lookup"><span data-stu-id="81f8c-197">Add a cluster quorum file share</span></span>

<span data-ttu-id="81f8c-198">Bu örnekte, Küme çekirdeğini oluşturmak için bir dosya paylaşımı Windows kümesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-198">In this example the Windows cluster uses a file share to create a cluster quorum.</span></span> <span data-ttu-id="81f8c-199">Bu öğretici, bir düğüm ve dosya paylaşımı çoğunluğu çekirdek kullanır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-199">This tutorial uses a Node and File Share Majority quorum.</span></span> <span data-ttu-id="81f8c-200">Daha fazla bilgi için bkz: [yük devretme kümesindeki çekirdek yapılandırmalarını anlama](http://technet.microsoft.com/library/cc731739.aspx).</span><span class="sxs-lookup"><span data-stu-id="81f8c-200">For more information, see [Understanding Quorum Configurations in a Failover Cluster](http://technet.microsoft.com/library/cc731739.aspx).</span></span>

1. <span data-ttu-id="81f8c-201">Uzak Masaüstü oturumu ile dosya paylaşımı tanığı üye sunucuya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-201">Connect to the file share witness member server with a remote desktop session.</span></span>

1. <span data-ttu-id="81f8c-202">Üzerinde **Sunucu Yöneticisi'ni**, tıklatın **Araçları**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-202">On **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="81f8c-203">Açık **Bilgisayar Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-203">Open **Computer Management**.</span></span>

1. <span data-ttu-id="81f8c-204">Tıklatın **paylaşılan klasörleri**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-204">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="81f8c-205">Sağ **paylaşımları**, tıklatıp **yeni paylaşım...** .</span><span class="sxs-lookup"><span data-stu-id="81f8c-205">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="81f8c-207">Kullanım **bir paylaşılan klasör oluşturma Sihirbazı** bir paylaşımı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-207">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="81f8c-208">Üzerinde **klasör yolu**, tıklatın **Gözat** bulun ve paylaşılan klasör için bir yol oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81f8c-208">On **Folder Path**, click **Browse** and locate or create a path for the shared folder.</span></span> <span data-ttu-id="81f8c-209">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-209">Click **Next**.</span></span>

1. <span data-ttu-id="81f8c-210">İçinde **adı, açıklama ve ayarları** paylaşım adını ve yolunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-210">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="81f8c-211">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-211">Click **Next**.</span></span>

1. <span data-ttu-id="81f8c-212">Üzerinde **paylaşılan klasör izinlerini** ayarlamak **izinleri Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-212">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="81f8c-213">Tıklatın **özel...** .</span><span class="sxs-lookup"><span data-stu-id="81f8c-213">Click **Custom...**.</span></span>

1. <span data-ttu-id="81f8c-214">Üzerinde **izinleri Özelleştir**, tıklatın **Ekle...** .</span><span class="sxs-lookup"><span data-stu-id="81f8c-214">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="81f8c-215">Kümeyi oluşturmak için kullanılan hesabın tam denetime sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="81f8c-215">Make sure that the account used to create the cluster has full control.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. <span data-ttu-id="81f8c-217">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-217">Click **OK**.</span></span>

1. <span data-ttu-id="81f8c-218">İçinde **paylaşılan klasör izinlerini**, tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-218">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="81f8c-219">Tıklatın **son** yeniden.</span><span class="sxs-lookup"><span data-stu-id="81f8c-219">Click **Finish** again.</span></span>  

1. <span data-ttu-id="81f8c-220">Sunucunun dışında oturum</span><span class="sxs-lookup"><span data-stu-id="81f8c-220">Log out of the server</span></span>

### <a name="configure-cluster-quorum"></a><span data-ttu-id="81f8c-221">Küme çekirdeğini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="81f8c-221">Configure cluster quorum</span></span>

<span data-ttu-id="81f8c-222">Ardından, Küme çekirdeğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-222">Next, set the cluster quorum.</span></span>

1. <span data-ttu-id="81f8c-223">İlk küme düğümüne Uzak Masaüstü kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-223">Connect to the first cluster node with remote desktop.</span></span>

1. <span data-ttu-id="81f8c-224">İçinde **yük devretme kümesi Yöneticisi**, kümeye sağ tıklayın, fareyle **diğer eylemler**, tıklatıp **küme çekirdek ayarlarını yapılandır...** .</span><span class="sxs-lookup"><span data-stu-id="81f8c-224">In **Failover Cluster Manager**, right-click the cluster, point to **More Actions**, and click **Configure Cluster Quorum Settings...**.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. <span data-ttu-id="81f8c-226">İçinde **küme çekirdeği Yapılandırma Sihirbazı**, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-226">In **Configure Cluster Quorum Wizard**, click **Next**.</span></span>

1. <span data-ttu-id="81f8c-227">İçinde **çekirdek yapılandırma seçeneğini**, seçin **çekirdek tanığı Seç**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-227">In **Select Quorum Configuration Option**, choose **Select the quorum witness**, and click **Next**.</span></span>

1. <span data-ttu-id="81f8c-228">Üzerinde **çekirdek tanığı Seç**, tıklatın **bir dosya paylaşımı tanığı Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-228">On **Select Quorum Witness**, click **Configure a file share witness**.</span></span>

   >[!TIP]
   ><span data-ttu-id="81f8c-229">Windows Server 2016 bulut Tanık destekler.</span><span class="sxs-lookup"><span data-stu-id="81f8c-229">Windows Server 2016 supports a cloud witness.</span></span> <span data-ttu-id="81f8c-230">Bu tür bir Tanık seçerseniz, bir dosya gerekmez paylaşımı tanığını.</span><span class="sxs-lookup"><span data-stu-id="81f8c-230">If you choose this type of witness, you do not need a file share witness.</span></span> <span data-ttu-id="81f8c-231">Daha fazla bilgi için bkz: [bir yük devretme kümesi için bir bulut tanığı dağıtmak](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="81f8c-231">For more information, see [Deploy a cloud witness for a Failover Cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span> <span data-ttu-id="81f8c-232">Bu öğretici, önceki işletim sistemleri tarafından desteklenen bir dosya paylaşımı tanığı kullanır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-232">This tutorial uses a file share witness, which is supported by previous operating systems.</span></span>

1. <span data-ttu-id="81f8c-233">Üzerinde **dosya paylaşımı Tanığını Yapılandır**, oluşturduğunuz paylaşımının yolu yazın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-233">On **Configure File Share Witness**, type the path for the share you created.</span></span> <span data-ttu-id="81f8c-234">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-234">Click **Next**.</span></span>

1. <span data-ttu-id="81f8c-235">Ayarları doğrulayın **onay**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-235">Verify the settings on **Confirmation**.</span></span> <span data-ttu-id="81f8c-236">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-236">Click **Next**.</span></span>

1. <span data-ttu-id="81f8c-237">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-237">Click **Finish**.</span></span>

<span data-ttu-id="81f8c-238">Küme Çekirdek kaynakları dosya paylaşım tanığı ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-238">The cluster core resources are configured with a file share witness.</span></span>

## <a name="enable-availability-groups"></a><span data-ttu-id="81f8c-239">Kullanılabilirlik gruplarını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="81f8c-239">Enable Availability Groups</span></span>

<span data-ttu-id="81f8c-240">Ardından, **AlwaysOn Kullanılabilirlik grupları** özelliği.</span><span class="sxs-lookup"><span data-stu-id="81f8c-240">Next, enable the **AlwaysOn Availability Groups** feature.</span></span> <span data-ttu-id="81f8c-241">Her iki SQL sunucularında bu adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-241">Do these steps on both SQL Servers.</span></span>

1. <span data-ttu-id="81f8c-242">Gelen **Başlat** ekranında, başlatma **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-242">From the **Start** screen, launch **SQL Server Configuration Manager**.</span></span>
2. <span data-ttu-id="81f8c-243">Tarayıcı ağacında tıklayın **SQL Server Hizmetleri**, sonra sağ **SQL Server (MSSQLSERVER)** 'ı tıklatın ve hizmeti **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-243">In the browser tree, click **SQL Server Services**, then right-click the **SQL Server (MSSQLSERVER)** service and click **Properties**.</span></span>
3. <span data-ttu-id="81f8c-244">Tıklatın **AlwaysOn yüksek kullanılabilirlik** sekmesini ve ardından **etkinleştirmek AlwaysOn Kullanılabilirlik grupları**aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="81f8c-244">Click the **AlwaysOn High Availability** tab, then select **Enable AlwaysOn Availability Groups**, as follows:</span></span>

    ![AlwaysOn Kullanılabilirlik gruplarını etkinleştir](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. <span data-ttu-id="81f8c-246">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-246">Click **Apply**.</span></span> <span data-ttu-id="81f8c-247">Tıklatın **Tamam** açılan iletişim kutusunda.</span><span class="sxs-lookup"><span data-stu-id="81f8c-247">Click **OK** in the pop-up dialog.</span></span>

5. <span data-ttu-id="81f8c-248">SQL Server hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-248">Restart the SQL Server service.</span></span>

<span data-ttu-id="81f8c-249">Diğer SQL Server'da bu adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-249">Repeat these steps on the other SQL Server.</span></span>

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for the database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for the instance of SQL Server that is used to synchronize the database replicas in the Availability Groups on that instance.

On both SQL Servers, open the firewall for the TCP port for the database mirroring endpoint.

1. On the first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In the left pane, select **Inbound Rules**. On the right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For the port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In the **Action** page, keep **Allow the connection** selected and click **Next**.
6. In the **Profile** page, accept the default settings and click **Next**.
7. In the **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in the **Name** text box, then click **Finish**.

Repeat these steps on the second SQL Server.
-------------------------->

## <a name="create-a-database-on-the-first-sql-server"></a><span data-ttu-id="81f8c-250">İlk SQL Server'da bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="81f8c-250">Create a database on the first SQL Server</span></span>

1. <span data-ttu-id="81f8c-251">İlk SQL Server sysadmin sabit sunucu rolünün üyesi olan bir etki alanı hesabı ile için RDP dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-251">Launch the RDP file to the first SQL Server with a domain account that is a member of sysadmin fixed server role.</span></span>
1. <span data-ttu-id="81f8c-252">SQL Server Management Studio'yu açın ve ilk SQL sunucusuna bağlanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-252">Open SQL Server Management Studio and connect to the first SQL Server.</span></span>
7. <span data-ttu-id="81f8c-253">İçinde **Object Explorer**, sağ **veritabanları** tıklatıp **yeni veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-253">In **Object Explorer**, right-click **Databases** and click **New Database**.</span></span>
8. <span data-ttu-id="81f8c-254">İçinde **veritabanı adı**, türü **MyDB1**, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-254">In **Database name**, type **MyDB1**, then click **OK**.</span></span>

### <span data-ttu-id="81f8c-255"><a name="backupshare"></a>Bir yedekleme paylaşımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="81f8c-255"><a name="backupshare"></a> Create a backup share</span></span>

1. <span data-ttu-id="81f8c-256">İlk SQL sunucusuna **Sunucu Yöneticisi'ni**, tıklatın **Araçları**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-256">On the first SQL Server in **Server Manager**, click **Tools**.</span></span> <span data-ttu-id="81f8c-257">Açık **Bilgisayar Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-257">Open **Computer Management**.</span></span>

1. <span data-ttu-id="81f8c-258">Tıklatın **paylaşılan klasörleri**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-258">Click **Shared Folders**.</span></span>

1. <span data-ttu-id="81f8c-259">Sağ **paylaşımları**, tıklatıp **yeni paylaşım...** .</span><span class="sxs-lookup"><span data-stu-id="81f8c-259">Right-click **Shares**, and click **New Share...**.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   <span data-ttu-id="81f8c-261">Kullanım **bir paylaşılan klasör oluşturma Sihirbazı** bir paylaşımı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-261">Use **Create a Shared Folder Wizard** to create a share.</span></span>

1. <span data-ttu-id="81f8c-262">Üzerinde **klasör yolu**, tıklatın **Gözat** bulun ve veritabanı yedekleme paylaşılan klasörü için bir yol oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81f8c-262">On **Folder Path**, click **Browse** and locate or create a path for the database backup shared folder.</span></span> <span data-ttu-id="81f8c-263">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-263">Click **Next**.</span></span>

1. <span data-ttu-id="81f8c-264">İçinde **adı, açıklama ve ayarları** paylaşım adını ve yolunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-264">In **Name, Description, and Settings** verify the share name and path.</span></span> <span data-ttu-id="81f8c-265">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-265">Click **Next**.</span></span>

1. <span data-ttu-id="81f8c-266">Üzerinde **paylaşılan klasör izinlerini** ayarlamak **izinleri Özelleştir**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-266">On **Shared Folder Permissions** set **Customize permissions**.</span></span> <span data-ttu-id="81f8c-267">Tıklatın **özel...** .</span><span class="sxs-lookup"><span data-stu-id="81f8c-267">Click **Custom...**.</span></span>

1. <span data-ttu-id="81f8c-268">Üzerinde **izinleri Özelleştir**, tıklatın **Ekle...** .</span><span class="sxs-lookup"><span data-stu-id="81f8c-268">On **Customize Permissions**, click **Add...**.</span></span>

1. <span data-ttu-id="81f8c-269">SQL Server ve SQL Server Aracısı hizmet hesapları her iki sunucu için tam denetim olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="81f8c-269">Make sure that the SQL Server and SQL Server Agent service accounts for both servers have full control.</span></span>

   ![Yeni paylaşım](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. <span data-ttu-id="81f8c-271">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-271">Click **OK**.</span></span>

1. <span data-ttu-id="81f8c-272">İçinde **paylaşılan klasör izinlerini**, tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-272">In **Shared Folder Permissions**, click **Finish**.</span></span> <span data-ttu-id="81f8c-273">Tıklatın **son** yeniden.</span><span class="sxs-lookup"><span data-stu-id="81f8c-273">Click **Finish** again.</span></span>  

### <a name="take-a-full-backup-of-the-database"></a><span data-ttu-id="81f8c-274">Tam veritabanı yedeklemesi alın</span><span class="sxs-lookup"><span data-stu-id="81f8c-274">Take a full backup of the database</span></span>

<span data-ttu-id="81f8c-275">Günlük zinciri başlatmak için yeni veritabanını yedeklemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-275">You need to back up the new database to initialize the log chain.</span></span> <span data-ttu-id="81f8c-276">Yeni veritabanının bir yedeğini almazsanız, bir kullanılabilirlik grubuna eklenemez.</span><span class="sxs-lookup"><span data-stu-id="81f8c-276">If you do not take a backup of the new database, it cannot be included in an Availability Group.</span></span>

1. <span data-ttu-id="81f8c-277">İçinde **Object Explorer**, veritabanına sağ tıklayın, fareyle **görevleri...** , tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-277">In **Object Explorer**, right-click the database, point to **Tasks...**, click **Back Up**.</span></span>

1. <span data-ttu-id="81f8c-278">Tıklatın **Tamam** varsayılan yedekleme konumuna tam yedekleme olabilmesi için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-278">Click **OK** to take a full backup to the default backup location.</span></span>

## <a name="create-the-availability-group"></a><span data-ttu-id="81f8c-279">Kullanılabilirlik grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="81f8c-279">Create the Availability Group</span></span>
<span data-ttu-id="81f8c-280">Artık aşağıdaki adımları kullanarak bir kullanılabilirlik grubu yapılandırmak hazırsınız:</span><span class="sxs-lookup"><span data-stu-id="81f8c-280">You are now ready to configure an Availability Group using the following steps:</span></span>

* <span data-ttu-id="81f8c-281">İlk SQL Server'da bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="81f8c-281">Create a database on the first SQL Server.</span></span>
* <span data-ttu-id="81f8c-282">Tam yedekleme ve veritabanının işlem günlüğü yedeklemesi gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="81f8c-282">Take both a full backup and a transaction log backup of the database</span></span>
* <span data-ttu-id="81f8c-283">Tam geri yükleme ve yedeklemeleri ikinci bir SQL Server ile oturum **NORECOVERY** seçeneği</span><span class="sxs-lookup"><span data-stu-id="81f8c-283">Restore the full and log backups to the second SQL Server with the **NORECOVERY** option</span></span>
* <span data-ttu-id="81f8c-284">Kullanılabilirlik grubu oluşturun (**AG1**) zaman uyumlu tamamlama, otomatik yük devretme ve okunabilir ikincil çoğaltmalarda</span><span class="sxs-lookup"><span data-stu-id="81f8c-284">Create the Availability Group (**AG1**) with synchronous commit, automatic failover, and readable secondary replicas</span></span>

### <a name="create-the-availability-group"></a><span data-ttu-id="81f8c-285">Kullanılabilirlik grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="81f8c-285">Create the Availability Group:</span></span>

1. <span data-ttu-id="81f8c-286">Uzak Masaüstü oturumu üzerinde ilk SQL Server.</span><span class="sxs-lookup"><span data-stu-id="81f8c-286">On remote desktop session to the first SQL Server.</span></span> <span data-ttu-id="81f8c-287">İçinde **Object Explorer** SSMS, sağ **AlwaysOn yüksek kullanılabilirlik** tıklatıp **yeni Kullanılabilirlik Grubu Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-287">In **Object Explorer** in SSMS, right-click **AlwaysOn High Availability** and click **New Availability Group Wizard**.</span></span>

    ![Yeni kullanılabilirlik grubu sihirbazını başlat](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. <span data-ttu-id="81f8c-289">İçinde **giriş** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-289">In the **Introduction** page, click **Next**.</span></span> <span data-ttu-id="81f8c-290">İçinde **kullanılabilirlik grubu adı belirtin** sayfasında, kullanılabilirlik grubu için bir ad yazın, örneğin **AG1**, **kullanılabilirlik grubu adının**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-290">In the **Specify Availability Group Name** page, type a name for the Availability Group, for example **AG1**, in **Availability group name**.</span></span> <span data-ttu-id="81f8c-291">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-291">Click **Next**.</span></span>

    ![Yeni AG Sihirbazı, AG adını belirtin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. <span data-ttu-id="81f8c-293">İçinde **seçin veritabanları** sayfasında Veritabanınızı seçin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-293">In the **Select Databases** page, select your database and click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="81f8c-294">En az bir tam yedekleme hedeflenen birincil Çoğaltmada uyguladığınız için veritabanı bir kullanılabilirlik grubu için Önkoşullar karşılıyor.</span><span class="sxs-lookup"><span data-stu-id="81f8c-294">The database meets the prerequisites for an Availability Group because you have taken at least one full backup on the intended primary replica.</span></span>

   ![Yeni AG Sihirbazı, veritabanlarını seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. <span data-ttu-id="81f8c-296">İçinde **çoğaltmaları belirle** sayfasında, **eklemek çoğaltma**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-296">In the **Specify Replicas** page, click **Add Replica**.</span></span>

   ![Yeni AG Sihirbazı, çoğaltmaları belirtin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. <span data-ttu-id="81f8c-298">**Sunucuya Bağlan** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-298">The **Connect to Server** dialog pops up.</span></span> <span data-ttu-id="81f8c-299">İkinci sunucunun adını yazın **sunucu adı**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-299">Type the name of the second server in **Server name**.</span></span> <span data-ttu-id="81f8c-300">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-300">Click **Connect**.</span></span>

   <span data-ttu-id="81f8c-301">Geri **çoğaltmaları belirle** sayfasında, listelenen ikinci sunucu artık görmelisiniz **kullanılabilirlik çoğaltmalarının**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-301">Back in the **Specify Replicas** page, you should now see the second server listed in **Availability Replicas**.</span></span> <span data-ttu-id="81f8c-302">Çoğaltmaların aşağıdaki gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-302">Configure the replicas as follows.</span></span>

   ![Yeni AG Sihirbazı, çoğaltmaları belirtin (tam)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. <span data-ttu-id="81f8c-304">Tıklatın **uç noktaları** yansıtma uç noktası bu kullanılabilirlik grubu için veritabanı görmek için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-304">Click **Endpoints** to see the database mirroring endpoint for this Availability Group.</span></span> <span data-ttu-id="81f8c-305">Ayarlarken kullandığınız aynı bağlantı noktasını [veritabanı yansıtma uç noktaları için güvenlik duvarı kuralı](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="81f8c-305">Use the same port that you used when you set the [firewall rule for database mirroring endpoints](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

    ![Yeni AG Sihirbazı, ilk veri eşitlemeyi seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. <span data-ttu-id="81f8c-307">İçinde **ilk veri eşitlemesi** sayfasında **tam** ve paylaşılan bir ağ konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-307">In the **Select Initial Data Synchronization** page, select **Full** and specify a shared network location.</span></span> <span data-ttu-id="81f8c-308">Konum, [oluşturduğunuz yedekleme paylaşımı](#backupshare).</span><span class="sxs-lookup"><span data-stu-id="81f8c-308">For the location, use the [backup share that you created](#backupshare).</span></span> <span data-ttu-id="81f8c-309">Olduğu, örnekte **\\\\\<ilk SQL Server\>\Backup\**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-309">In the example it was, **\\\\\<First SQL Server\>\Backup\**.</span></span> <span data-ttu-id="81f8c-310">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-310">Click **Next**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="81f8c-311">Tam eşitleme veritabanı SQL Server'ın ilk örneğinin üzerinde tam yedeğini alır ve ikinci örneğine geri yükler.</span><span class="sxs-lookup"><span data-stu-id="81f8c-311">Full synchronization takes a full backup of the database on the first instance of SQL Server and restores it to the second instance.</span></span> <span data-ttu-id="81f8c-312">Büyük veritabanları için tam eşitleme önerilmez uzun bir süre devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-312">For large databases, full synchronization is not recommended because it may take a long time.</span></span> <span data-ttu-id="81f8c-313">El ile veritabanının bir yedeğini almak ve onunla geri yükleme bu kez azaltabilir `NO RECOVERY`.</span><span class="sxs-lookup"><span data-stu-id="81f8c-313">You can reduce this time by manually taking a backup of the database and restoring it with `NO RECOVERY`.</span></span> <span data-ttu-id="81f8c-314">Veritabanı zaten ile geri yüklenirse `NO RECOVERY` ikinci SQL kullanılabilirlik grubu yapılandırmadan önce sunucuda seçin **yalnızca katmak**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-314">If the database is already restored with `NO RECOVERY` on the second SQL Server before configuring the Availability Group, choose **Join only**.</span></span> <span data-ttu-id="81f8c-315">Kullanılabilirlik grubu yapılandırdıktan sonra yedekleyin istiyorsanız seçin **ilk veri eşitlemeyi atla**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-315">If you want to take the backup after configuring the Availability Group, choose **Skip initial data synchronization**.</span></span>

    ![Yeni AG Sihirbazı, ilk veri eşitlemeyi seçin](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. <span data-ttu-id="81f8c-317">İçinde **doğrulama** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-317">In the **Validation** page, click **Next**.</span></span> <span data-ttu-id="81f8c-318">Bu sayfa aşağıdaki görüntüye benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="81f8c-318">This page should look similar to the following image:</span></span>

    ![Yeni AG Sihirbazı, doğrulama](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    ><span data-ttu-id="81f8c-320">Bir kullanılabilirlik grubu dinleyicisi yapılandırılmadığı için dinleyici yapılandırması için bir uyarı yok.</span><span class="sxs-lookup"><span data-stu-id="81f8c-320">There is a warning for the listener configuration because you have not configured an Availability Group listener.</span></span> <span data-ttu-id="81f8c-321">Azure sanal makinelerde, dinleyiciyi Azure yük dengeleyici oluşturduktan sonra oluşturduğundan bu uyarıyı yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f8c-321">You can ignore this warning because on Azure virtual machines you create the listener after creating the Azure load balancer.</span></span>

10. <span data-ttu-id="81f8c-322">İçinde **Özet** sayfasında, **son**, ardından yeni Kullanılabilirlik Grubu Sihirbazı'nı yapılandırırken bekleyin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-322">In the **Summary** page, click **Finish**, then wait while the wizard configures the new Availability Group.</span></span> <span data-ttu-id="81f8c-323">İçinde **ilerleme** tıklayabilirsiniz sayfasında **daha fazla ayrıntı** ayrıntılı ilerleme durumunu görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-323">In the **Progress** page, you can click **More details** to view the detailed progress.</span></span> <span data-ttu-id="81f8c-324">Sihirbaz tamamlandıktan sonra İnceleme **sonuçları** sayfa kullanılabilirlik grubu başarıyla oluşturulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-324">Once the wizard is finished, inspect the **Results** page to verify that the Availability Group is successfully created.</span></span>

     ![Yeni AG Sihirbazı, sonuçlar](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. <span data-ttu-id="81f8c-326">Tıklatın **Kapat** sihirbazdan çıkmak için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-326">Click **Close** to exit the wizard.</span></span>

### <a name="check-the-availability-group"></a><span data-ttu-id="81f8c-327">Kullanılabilirlik grubu denetleyin</span><span class="sxs-lookup"><span data-stu-id="81f8c-327">Check the Availability Group</span></span>

1. <span data-ttu-id="81f8c-328">İçinde **Object Explorer**, genişletin **AlwaysOn yüksek kullanılabilirlik**, ardından **kullanılabilirlik grupları**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-328">In **Object Explorer**, expand **AlwaysOn High Availability**, then expand **Availability Groups**.</span></span> <span data-ttu-id="81f8c-329">Bu kapsayıcıda yeni kullanılabilirlik grubu görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="81f8c-329">You should now see the new Availability Group in this container.</span></span> <span data-ttu-id="81f8c-330">Kullanılabilirlik grubunu sağ tıklatın ve **Göster Pano**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-330">Right-click the Availability Group and click **Show Dashboard**.</span></span>

   ![AG panosunu Göster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   <span data-ttu-id="81f8c-332">**AlwaysOn panosunu** şuna benzer görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-332">Your **AlwaysOn Dashboard** should look similar to this.</span></span>

   ![AG Panosu](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   <span data-ttu-id="81f8c-334">Çoğaltmalar, yük devretme modu her çoğaltma ve eşitleme durumu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f8c-334">You can see the replicas, the failover mode of each replica and the synchronization state.</span></span>

2. <span data-ttu-id="81f8c-335">İçinde **yük devretme kümesi Yöneticisi**, kümenizi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-335">In **Failover Cluster Manager**, click your cluster.</span></span> <span data-ttu-id="81f8c-336">Seçin **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-336">Select **Roles**.</span></span> <span data-ttu-id="81f8c-337">Kullandığınız kullanılabilirlik grubu adı küme üzerinde bir rolüdür.</span><span class="sxs-lookup"><span data-stu-id="81f8c-337">The Availability Group name you used is a role on the cluster.</span></span> <span data-ttu-id="81f8c-338">Bu kullanılabilirlik grubu dinleyici yapılandırmadı olduğundan istemci bağlantıları için bir IP adresi yok.</span><span class="sxs-lookup"><span data-stu-id="81f8c-338">That Availability Group does not have an IP address for client connections, because you did not configure a listener.</span></span> <span data-ttu-id="81f8c-339">Bir Azure yük dengeleyici oluşturduktan sonra dinleyicisi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-339">You will configure the listener after you create an Azure load balancer.</span></span>

   ![Yük Devretme Kümesi Yöneticisi'nde AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > <span data-ttu-id="81f8c-341">Kullanılabilirlik grubu yük devretme kümesi Yöneticisi'nden üzerinden vermesine çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-341">Do not try to fail over the Availability Group from the Failover Cluster Manager.</span></span> <span data-ttu-id="81f8c-342">Tüm yük devretme işlemlerini içinden gerçekleştirilmelidir **AlwaysOn panosunu** SSMS içinde.</span><span class="sxs-lookup"><span data-stu-id="81f8c-342">All failover operations should be performed from within **AlwaysOn Dashboard** in SSMS.</span></span> <span data-ttu-id="81f8c-343">Daha fazla bilgi için bkz: [kısıtlamaları üzerinde kullanarak yük devretme kümesi Yöneticisi kullanılabilirlik grupları ile](https://msdn.microsoft.com/library/ff929171.aspx).</span><span class="sxs-lookup"><span data-stu-id="81f8c-343">For more information, see [Restrictions on Using The Failover Cluster Manager with Availability Groups](https://msdn.microsoft.com/library/ff929171.aspx).</span></span>
    >

<span data-ttu-id="81f8c-344">Bu noktada, çoğaltmalar SQL Server'ın iki örneği üzerinde kullanılabilirlik grubuyla sahip.</span><span class="sxs-lookup"><span data-stu-id="81f8c-344">At this point, you have an Availability Group with replicas on two instances of SQL Server.</span></span> <span data-ttu-id="81f8c-345">Kullanılabilirlik grubu örnekleri arasında taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f8c-345">You can move the Availability Group between instances.</span></span> <span data-ttu-id="81f8c-346">Dinleyici olmadığı için kullanılabilirlik grubu için henüz bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="81f8c-346">You cannot connect to the Availability Group yet because you do not have a listener.</span></span> <span data-ttu-id="81f8c-347">Azure sanal makinelerinde dinleyicisi bir yük dengeleyici gerektirir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-347">In Azure virtual machines, the listener requires a load balancer.</span></span> <span data-ttu-id="81f8c-348">Sonraki adım, Azure yük dengeleyici oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-348">The next step is to create the load balancer in Azure.</span></span>

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a><span data-ttu-id="81f8c-349">Bir Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="81f8c-349">Create an Azure load balancer</span></span>

<span data-ttu-id="81f8c-350">Azure sanal makinelerde SQL Server kullanılabilirlik grubu yük dengeleyici gerektirir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-350">On Azure virtual machines, a SQL Server Availability Group requires a load balancer.</span></span> <span data-ttu-id="81f8c-351">Yük Dengeleyici için kullanılabilirlik grubu dinleyici IP adresini tutar.</span><span class="sxs-lookup"><span data-stu-id="81f8c-351">The load balancer holds the IP address for the Availability Group listener.</span></span> <span data-ttu-id="81f8c-352">Bu bölümde Azure portalında yük dengeleyici oluşturma özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-352">This section summarizes how to create the load balancer in the Azure portal.</span></span>

1. <span data-ttu-id="81f8c-353">Azure Portal'da, burada SQL sunucularınızı ve tıklatın Kaynak grubuna gidin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-353">In the Azure portal, go to the resource group where your SQL Servers are and click **+ Add**.</span></span>
2. <span data-ttu-id="81f8c-354">Arama **yük dengeleyici**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-354">Search for **Load Balancer**.</span></span> <span data-ttu-id="81f8c-355">Microsoft tarafından yayımlanan yük dengeleyici seçin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-355">Choose the load balancer published by Microsoft.</span></span>

   ![Yük Devretme Kümesi Yöneticisi'nde AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  <span data-ttu-id="81f8c-357">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-357">Click **Create**.</span></span>
3. <span data-ttu-id="81f8c-358">Yük Dengeleyici için aşağıdaki parametreleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-358">Configure the following parameters for the load balancer.</span></span>

   | <span data-ttu-id="81f8c-359">Ayar</span><span class="sxs-lookup"><span data-stu-id="81f8c-359">Setting</span></span> | <span data-ttu-id="81f8c-360">Alan</span><span class="sxs-lookup"><span data-stu-id="81f8c-360">Field</span></span> |
   | --- | --- |
   | <span data-ttu-id="81f8c-361">**Ad**</span><span class="sxs-lookup"><span data-stu-id="81f8c-361">**Name**</span></span> |<span data-ttu-id="81f8c-362">Yük Dengeleyici için bir metin adı kullanın örneğin **sqlLB**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-362">Use a text name for the load balancer, for example **sqlLB**.</span></span> |
   | <span data-ttu-id="81f8c-363">**Tür**</span><span class="sxs-lookup"><span data-stu-id="81f8c-363">**Type**</span></span> |<span data-ttu-id="81f8c-364">İç</span><span class="sxs-lookup"><span data-stu-id="81f8c-364">Internal</span></span> |
   | <span data-ttu-id="81f8c-365">**Sanal ağ**</span><span class="sxs-lookup"><span data-stu-id="81f8c-365">**Virtual network**</span></span> |<span data-ttu-id="81f8c-366">Azure sanal ağı adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-366">Use the name of the Azure virtual network.</span></span> |
   | <span data-ttu-id="81f8c-367">**Alt ağ**</span><span class="sxs-lookup"><span data-stu-id="81f8c-367">**Subnet**</span></span> |<span data-ttu-id="81f8c-368">Sanal makine alt ağ adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-368">Use the name of the subnet that the virtual machine is in.</span></span>  |
   | <span data-ttu-id="81f8c-369">**IP adresi ataması**</span><span class="sxs-lookup"><span data-stu-id="81f8c-369">**IP address assignment**</span></span> |<span data-ttu-id="81f8c-370">Statik</span><span class="sxs-lookup"><span data-stu-id="81f8c-370">Static</span></span> |
   | <span data-ttu-id="81f8c-371">**IP adresi**</span><span class="sxs-lookup"><span data-stu-id="81f8c-371">**IP address**</span></span> |<span data-ttu-id="81f8c-372">Kullanılabilir bir alt ağ adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-372">Use an available address from subnet.</span></span> |
   | <span data-ttu-id="81f8c-373">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="81f8c-373">**Subscription**</span></span> |<span data-ttu-id="81f8c-374">Aynı abonelikte sanal makine olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-374">Use the same subscription as the virtual machine.</span></span> |
   | <span data-ttu-id="81f8c-375">**Konum**</span><span class="sxs-lookup"><span data-stu-id="81f8c-375">**Location**</span></span> |<span data-ttu-id="81f8c-376">Aynı konumda sanal makine olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-376">Use the same location as the virtual machine.</span></span> |

   <span data-ttu-id="81f8c-377">Azure portal dikey penceresinde aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="81f8c-377">The Azure portal blade should look like this:</span></span>

   ![Yük Dengeleyici oluşturma](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. <span data-ttu-id="81f8c-379">Tıklatın **oluşturma**, yük dengeleyici oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-379">Click **Create**, to create the load balancer.</span></span>

<span data-ttu-id="81f8c-380">Yük Dengeleyici yapılandırmak için bir arka uç havuzu, bir araştırma oluşturmak ve Yük Dengeleme kuralları ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-380">To configure the load balancer, you need to create a backend pool, a probe, and set the load balancing rules.</span></span> <span data-ttu-id="81f8c-381">Bunlar Azure portalında yapın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-381">Do these in the Azure portal.</span></span>

### <a name="add-backend-pool"></a><span data-ttu-id="81f8c-382">Arka uç havuzu ekleme</span><span class="sxs-lookup"><span data-stu-id="81f8c-382">Add backend pool</span></span>

1. <span data-ttu-id="81f8c-383">Azure portalında kullanılabilirlik grubuna gidin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-383">In the Azure portal, go to your availability group.</span></span> <span data-ttu-id="81f8c-384">Yeni oluşturulan yük dengeleyici görmek için görünümü yenilemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-384">You might need to refresh the view to see the newly created load balancer.</span></span>

   ![Yük Dengeleyici kaynak grubunda bulunamadı](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. <span data-ttu-id="81f8c-386">Yük Dengeleyici tıklatın, **arka uç havuzları**, tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-386">Click the load balancer, click **Backend pools**, and click **+Add**.</span></span> <span data-ttu-id="81f8c-387">Arka uç havuzu aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="81f8c-387">Set the backend pool as follows:</span></span>

   | <span data-ttu-id="81f8c-388">Ayar</span><span class="sxs-lookup"><span data-stu-id="81f8c-388">Setting</span></span> | <span data-ttu-id="81f8c-389">Açıklama</span><span class="sxs-lookup"><span data-stu-id="81f8c-389">Description</span></span> | <span data-ttu-id="81f8c-390">Örnek</span><span class="sxs-lookup"><span data-stu-id="81f8c-390">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="81f8c-391">**Ad**</span><span class="sxs-lookup"><span data-stu-id="81f8c-391">**Name**</span></span> | <span data-ttu-id="81f8c-392">Bir metin yazın</span><span class="sxs-lookup"><span data-stu-id="81f8c-392">Type a text name</span></span> | <span data-ttu-id="81f8c-393">SQLLBBE</span><span class="sxs-lookup"><span data-stu-id="81f8c-393">SQLLBBE</span></span>
   | <span data-ttu-id="81f8c-394">**İle ilişkili**</span><span class="sxs-lookup"><span data-stu-id="81f8c-394">**Associated to**</span></span> | <span data-ttu-id="81f8c-395">Listeden seçin</span><span class="sxs-lookup"><span data-stu-id="81f8c-395">Pick from list</span></span> | <span data-ttu-id="81f8c-396">Kullanılabilirlik kümesi</span><span class="sxs-lookup"><span data-stu-id="81f8c-396">Availability set</span></span>
   | <span data-ttu-id="81f8c-397">**Kullanılabilirlik kümesi**</span><span class="sxs-lookup"><span data-stu-id="81f8c-397">**Availability set**</span></span> | <span data-ttu-id="81f8c-398">SQL Server Vm'lerinin bulunan kullanılabilirlik kümesi adını kullanın</span><span class="sxs-lookup"><span data-stu-id="81f8c-398">Use a name of the availability set that your SQL Server VMs are in</span></span> | <span data-ttu-id="81f8c-399">sqlAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="81f8c-399">sqlAvailabilitySet</span></span> |
   | <span data-ttu-id="81f8c-400">**Sanal makineler**</span><span class="sxs-lookup"><span data-stu-id="81f8c-400">**Virtual machines**</span></span> |<span data-ttu-id="81f8c-401">İki Azure SQL Server VM adı</span><span class="sxs-lookup"><span data-stu-id="81f8c-401">The two Azure SQL Server VM names</span></span> | <span data-ttu-id="81f8c-402">SQLServer-0, sqlserver-1</span><span class="sxs-lookup"><span data-stu-id="81f8c-402">sqlserver-0, sqlserver-1</span></span>

1. <span data-ttu-id="81f8c-403">Arka uç havuzu için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-403">Type the name for the back end pool.</span></span>

1. <span data-ttu-id="81f8c-404">Tıklatın **+ bir sanal makine Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-404">Click **+ Add a virtual machine**.</span></span>

1. <span data-ttu-id="81f8c-405">Kullanılabilirlik kümesi için SQL sunucusu olduğundan emin kullanılabilirlik kümesi'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-405">For the availability set, choose the availability set that the SQL Servers are in.</span></span>

1. <span data-ttu-id="81f8c-406">Sanal makineler için SQL Server'ların ikisi de içerir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-406">For virtual machines, include both of the SQL Servers.</span></span> <span data-ttu-id="81f8c-407">Dosya paylaşımı tanığı sunucusu içermez.</span><span class="sxs-lookup"><span data-stu-id="81f8c-407">Do not include the file share witness server.</span></span>

1. <span data-ttu-id="81f8c-408">Tıklatın **Tamam** arka uç havuzu oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-408">Click **OK** to create the backend pool.</span></span>

### <a name="set-the-probe"></a><span data-ttu-id="81f8c-409">Araştırma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="81f8c-409">Set the probe</span></span>

1. <span data-ttu-id="81f8c-410">Yük Dengeleyici tıklatın, **sistem durumu araştırmalarının**, tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-410">Click the load balancer, click **Health probes**, and click **+Add**.</span></span>

1. <span data-ttu-id="81f8c-411">Sistem durumu araştırma aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="81f8c-411">Set the health probe as follows:</span></span>

   | <span data-ttu-id="81f8c-412">Ayar</span><span class="sxs-lookup"><span data-stu-id="81f8c-412">Setting</span></span> | <span data-ttu-id="81f8c-413">Açıklama</span><span class="sxs-lookup"><span data-stu-id="81f8c-413">Description</span></span> | <span data-ttu-id="81f8c-414">Örnek</span><span class="sxs-lookup"><span data-stu-id="81f8c-414">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="81f8c-415">**Ad**</span><span class="sxs-lookup"><span data-stu-id="81f8c-415">**Name**</span></span> | <span data-ttu-id="81f8c-416">Metin</span><span class="sxs-lookup"><span data-stu-id="81f8c-416">Text</span></span> | <span data-ttu-id="81f8c-417">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="81f8c-417">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="81f8c-418">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="81f8c-418">**Protocol**</span></span> | <span data-ttu-id="81f8c-419">TCP seçin</span><span class="sxs-lookup"><span data-stu-id="81f8c-419">Choose TCP</span></span> | <span data-ttu-id="81f8c-420">TCP</span><span class="sxs-lookup"><span data-stu-id="81f8c-420">TCP</span></span> |
   | <span data-ttu-id="81f8c-421">**Bağlantı Noktası**</span><span class="sxs-lookup"><span data-stu-id="81f8c-421">**Port**</span></span> | <span data-ttu-id="81f8c-422">Kullanılmayan bir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="81f8c-422">Any unused port</span></span> | <span data-ttu-id="81f8c-423">59999</span><span class="sxs-lookup"><span data-stu-id="81f8c-423">59999</span></span> |
   | <span data-ttu-id="81f8c-424">**Aralığı**</span><span class="sxs-lookup"><span data-stu-id="81f8c-424">**Interval**</span></span>  | <span data-ttu-id="81f8c-425">Saniye cinsinden araştırma girişimleri arasındaki süre</span><span class="sxs-lookup"><span data-stu-id="81f8c-425">The amount of time between probe attempts in seconds</span></span> |<span data-ttu-id="81f8c-426">5</span><span class="sxs-lookup"><span data-stu-id="81f8c-426">5</span></span> |
   | <span data-ttu-id="81f8c-427">**Sağlıksız durum eşiği.**</span><span class="sxs-lookup"><span data-stu-id="81f8c-427">**Unhealthy threshold**</span></span> | <span data-ttu-id="81f8c-428">Sağlıksız olarak kabul edilmesi bir sanal makine için oluşması gereken arka arkaya araştırma hatası sayısı</span><span class="sxs-lookup"><span data-stu-id="81f8c-428">The number of consecutive probe failures that must occur for a virtual machine to be considered unhealthy</span></span>  | <span data-ttu-id="81f8c-429">2</span><span class="sxs-lookup"><span data-stu-id="81f8c-429">2</span></span> |

1. <span data-ttu-id="81f8c-430">Tıklatın **Tamam** durumu araştırması ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-430">Click **OK** to set the health probe.</span></span>

### <a name="set-the-load-balancing-rules"></a><span data-ttu-id="81f8c-431">Yük Dengeleme kuralları ayarlama</span><span class="sxs-lookup"><span data-stu-id="81f8c-431">Set the load balancing rules</span></span>

1. <span data-ttu-id="81f8c-432">Yük Dengeleyici tıklatın, **Yük Dengeleme kuralları**, tıklatıp **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-432">Click the load balancer, click **Load balancing rules**, and click **+Add**.</span></span>

1. <span data-ttu-id="81f8c-433">Yük Dengeleme kuralları aşağıdaki gibi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-433">Set the load balancing rules as follows.</span></span>
   | <span data-ttu-id="81f8c-434">Ayar</span><span class="sxs-lookup"><span data-stu-id="81f8c-434">Setting</span></span> | <span data-ttu-id="81f8c-435">Açıklama</span><span class="sxs-lookup"><span data-stu-id="81f8c-435">Description</span></span> | <span data-ttu-id="81f8c-436">Örnek</span><span class="sxs-lookup"><span data-stu-id="81f8c-436">Example</span></span>
   | --- | --- |---
   | <span data-ttu-id="81f8c-437">**Ad**</span><span class="sxs-lookup"><span data-stu-id="81f8c-437">**Name**</span></span> | <span data-ttu-id="81f8c-438">Metin</span><span class="sxs-lookup"><span data-stu-id="81f8c-438">Text</span></span> | <span data-ttu-id="81f8c-439">SQLAlwaysOnEndPointListener</span><span class="sxs-lookup"><span data-stu-id="81f8c-439">SQLAlwaysOnEndPointListener</span></span> |
   | <span data-ttu-id="81f8c-440">**Ön uç IP adresi**</span><span class="sxs-lookup"><span data-stu-id="81f8c-440">**Frontend IP address**</span></span> | <span data-ttu-id="81f8c-441">Adres seçin</span><span class="sxs-lookup"><span data-stu-id="81f8c-441">Choose an address</span></span> |<span data-ttu-id="81f8c-442">Yük Dengeleyici oluşturduğunuz sırada oluşturduğunuz adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-442">Use the address that you created when you created the load balancer.</span></span> |
   | <span data-ttu-id="81f8c-443">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="81f8c-443">**Protocol**</span></span> | <span data-ttu-id="81f8c-444">TCP seçin</span><span class="sxs-lookup"><span data-stu-id="81f8c-444">Choose TCP</span></span> |<span data-ttu-id="81f8c-445">TCP</span><span class="sxs-lookup"><span data-stu-id="81f8c-445">TCP</span></span> |
   | <span data-ttu-id="81f8c-446">**Bağlantı Noktası**</span><span class="sxs-lookup"><span data-stu-id="81f8c-446">**Port**</span></span> | <span data-ttu-id="81f8c-447">Bağlantı noktası için SQL Server örneğini kullan</span><span class="sxs-lookup"><span data-stu-id="81f8c-447">Use the port for the SQL Server instance</span></span> | <span data-ttu-id="81f8c-448">1433</span><span class="sxs-lookup"><span data-stu-id="81f8c-448">1433</span></span> |
   | <span data-ttu-id="81f8c-449">**Arka uç bağlantı noktası**</span><span class="sxs-lookup"><span data-stu-id="81f8c-449">**Backend Port**</span></span> | <span data-ttu-id="81f8c-450">Kayan IP için doğrudan sunucu dönüş ayarladığınızda, bu alan kullanılmıyor</span><span class="sxs-lookup"><span data-stu-id="81f8c-450">This field is not used when Floating IP is set for direct server return</span></span> | <span data-ttu-id="81f8c-451">1433</span><span class="sxs-lookup"><span data-stu-id="81f8c-451">1433</span></span> |
   | <span data-ttu-id="81f8c-452">**Araştırma**</span><span class="sxs-lookup"><span data-stu-id="81f8c-452">**Probe**</span></span> |<span data-ttu-id="81f8c-453">Araştırması için belirtilen adı</span><span class="sxs-lookup"><span data-stu-id="81f8c-453">The name you specified for the probe</span></span> | <span data-ttu-id="81f8c-454">SQLAlwaysOnEndPointProbe</span><span class="sxs-lookup"><span data-stu-id="81f8c-454">SQLAlwaysOnEndPointProbe</span></span> |
   | <span data-ttu-id="81f8c-455">**Oturum kalıcılığı**</span><span class="sxs-lookup"><span data-stu-id="81f8c-455">**Session Persistence**</span></span> | <span data-ttu-id="81f8c-456">Açılan liste</span><span class="sxs-lookup"><span data-stu-id="81f8c-456">Drop down list</span></span> | <span data-ttu-id="81f8c-457">**Yok**</span><span class="sxs-lookup"><span data-stu-id="81f8c-457">**None**</span></span> |
   | <span data-ttu-id="81f8c-458">**Boşta kalma zaman aşımı**</span><span class="sxs-lookup"><span data-stu-id="81f8c-458">**Idle Timeout**</span></span> | <span data-ttu-id="81f8c-459">Bir TCP bağlantısı açık tutmak için dakika</span><span class="sxs-lookup"><span data-stu-id="81f8c-459">Minutes to keep a TCP connection open</span></span> | <span data-ttu-id="81f8c-460">4</span><span class="sxs-lookup"><span data-stu-id="81f8c-460">4</span></span> |
   | <span data-ttu-id="81f8c-461">**Kayan IP (doğrudan sunucu dönüşü)**</span><span class="sxs-lookup"><span data-stu-id="81f8c-461">**Floating IP (direct server return)**</span></span> | |<span data-ttu-id="81f8c-462">Etkin</span><span class="sxs-lookup"><span data-stu-id="81f8c-462">Enabled</span></span> |

   > [!WARNING]
   > <span data-ttu-id="81f8c-463">Doğrudan sunucu dönüşü oluşturma sırasında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-463">Direct server return is set during creation.</span></span> <span data-ttu-id="81f8c-464">Değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="81f8c-464">It cannot be changed.</span></span>

1. <span data-ttu-id="81f8c-465">Tıklatın **Tamam** Yük Dengeleme kuralları ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="81f8c-465">Click **OK** to set the load balancing rules.</span></span>

## <span data-ttu-id="81f8c-466"><a name="configure-listener"></a>Dinleyici yapılandırın</span><span class="sxs-lookup"><span data-stu-id="81f8c-466"><a name="configure-listener"></a> Configure the listener</span></span>

<span data-ttu-id="81f8c-467">Sonraki bir şey yapmak için yük devretme kümesinde bir kullanılabilirlik grubu dinleyicisi yapılandırmaktır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-467">The next thing to do is to configure an Availability Group listener on the failover cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="81f8c-468">Bu öğretici bir ILB IP adresi ile tek bir dinleyicisi - oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-468">This tutorial shows how to create a single listener - with one ILB IP address.</span></span> <span data-ttu-id="81f8c-469">Bir veya daha fazla IP adresi kullanarak bir veya daha fazla dinleyicileri oluşturmak için bkz: [oluşturma kullanılabilirlik grubu dinleyici ve yük dengeleyici | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="81f8c-469">To create one or more listeners using one or more IP addresses, see [Create Availability Group listener and load balancer | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a><span data-ttu-id="81f8c-470">Set dinleyicisi bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="81f8c-470">Set listener port</span></span>

<span data-ttu-id="81f8c-471">SQL Server Management Studio'da dinleyicisi bağlantı noktası ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-471">In SQL Server Management Studio, set the listener port.</span></span>

1. <span data-ttu-id="81f8c-472">SQL Server Management Studio'yu başlatın ve birincil kopyaya bağlanın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-472">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="81f8c-473">Gidin **AlwaysOn yüksek kullanılabilirlik** | **kullanılabilirlik grupları** | **kullanılabilirlik grubu dinleyicileri**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-473">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span>

1. <span data-ttu-id="81f8c-474">Yük Devretme Kümesi Yöneticisi'nde oluşturulan dinleyici adı görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="81f8c-474">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="81f8c-475">Dinleyici adına sağ tıklatın ve **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-475">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="81f8c-476">İçinde **bağlantı noktası** kutusunda, daha önce kullandığınız $EndpointPort kullanarak için kullanılabilirlik grubu dinleyici bağlantı noktası numarası belirtin (1433 olduğu varsayılan), ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="81f8c-476">In the **Port** box, specify the port number for the Availability Group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

<span data-ttu-id="81f8c-477">Artık Azure sanal makinelerde Kaynak Yöneticisi modunda çalışan bir SQL Server kullanılabilirlik grubu vardır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-477">You now have a SQL Server Availability Group in Azure virtual machines running in Resource Manager mode.</span></span>

## <a name="test-connection-to-listener"></a><span data-ttu-id="81f8c-478">Dinleyici bağlantıyı sınayın</span><span class="sxs-lookup"><span data-stu-id="81f8c-478">Test connection to listener</span></span>

<span data-ttu-id="81f8c-479">Bağlantıyı sınamak için:</span><span class="sxs-lookup"><span data-stu-id="81f8c-479">To test the connection:</span></span>

1. <span data-ttu-id="81f8c-480">RDP bir SQL Server'a aynı sanal ağda bulunan, ancak çoğaltma kendisine ait değil.</span><span class="sxs-lookup"><span data-stu-id="81f8c-480">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="81f8c-481">Bir SQL Server kümesinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="81f8c-481">You can use the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="81f8c-482">Kullanım **sqlcmd** yardımcı programını kullanarak bağlantıyı sınayın.</span><span class="sxs-lookup"><span data-stu-id="81f8c-482">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="81f8c-483">Örneğin, aşağıdaki komut dosyasını oluşturur. bir **sqlcmd** Windows kimlik doğrulaması dinleyicisiyle aracılığıyla birincil çoğaltma bağlantısı:</span><span class="sxs-lookup"><span data-stu-id="81f8c-483">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>

    ```
    sqlcmd -S <listenerName> -E
    ```

    <span data-ttu-id="81f8c-484">Dinleyici varsayılan dışında bir bağlantı noktası kullanıyorsa (1433) bağlantı noktası, bağlantı dizesinde bağlantı noktasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="81f8c-484">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="81f8c-485">Örneğin, aşağıdaki sqlcmd komut bir dinleyici bağlantı noktası 1435 bağlanır:</span><span class="sxs-lookup"><span data-stu-id="81f8c-485">For example, the following sqlcmd command connects to a listener at port 1435:</span></span>

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="81f8c-486">SQL Server'ın hangi örneğinin birincil çoğaltmayı barındıran için SQLCMD bağlantı otomatik olarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="81f8c-486">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span>

> [!TIP]
> <span data-ttu-id="81f8c-487">Belirttiğiniz bağlantı noktasının Güvenlik Duvarı'nı her iki SQL sunucularının açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="81f8c-487">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="81f8c-488">Her iki sunucuyu kullandığınız TCP bağlantı noktası için bir gelen kuralı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="81f8c-488">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="81f8c-489">Daha fazla bilgi için bkz: [Ekle veya Düzenle güvenlik duvarı kuralı](http://technet.microsoft.com/library/cc753558.aspx).</span><span class="sxs-lookup"><span data-stu-id="81f8c-489">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span>
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by the way” info, an Important is info users need to complete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is the second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note the format for documenting the UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult to maintain. Highlight areas you are referring to in red.*-->

<!--**No. of steps**: *Make sure the number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want to go on.*-->

## <a name="next-steps"></a><span data-ttu-id="81f8c-490">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81f8c-490">Next steps</span></span>

- <span data-ttu-id="81f8c-491">[İkinci bir kullanılabilirlik grubu için yük dengeleyici için IP adresi eklemek](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span><span class="sxs-lookup"><span data-stu-id="81f8c-491">[Add an IP address to a load balancer for a second availability group](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).</span></span>
