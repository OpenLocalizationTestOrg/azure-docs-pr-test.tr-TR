---
title: "aaaLOB uygulama test ortamı | Microsoft Docs"
description: "Nasıl toocreate bir web tabanlı, iş hattı uygulaması bir karma bulut ortamı için bilgi IT pro veya testi geliştirme."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="70b12-103">Test için karma bulutta web tabanlı LOB uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="70b12-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="70b12-104">Bu konu bir iş (LOB) uygulaması Microsoft Azure üzerinde barındırılan web tabanlı satır test etmek için bir sanal karma bulut ortamı oluşturma konusunda adımları.</span><span class="sxs-lookup"><span data-stu-id="70b12-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="70b12-105">Merhaba sonuçta elde edilen yapılandırma aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="70b12-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="70b12-106">Bu yapılandırma oluşur:</span><span class="sxs-lookup"><span data-stu-id="70b12-106">This configuration consists of:</span></span>

* <span data-ttu-id="70b12-107">(Merhaba sınama laboratuvarı VNet) Azure üzerinde barındırılan sanal şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="70b12-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="70b12-108">(TestVNET) Azure üzerinde barındırılan bir şirket içi sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="70b12-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="70b12-109">VNet-VNet VPN bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="70b12-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="70b12-110">Web tabanlı LOB server, SQL server ve hello TestVNET sanal ağındaki ikincil etki alanı denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="70b12-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="70b12-111">Bu yapılandırma temeli ve, yapabileceğiniz ortak başlangıç noktası sağlar:</span><span class="sxs-lookup"><span data-stu-id="70b12-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="70b12-112">Geliştirme ve azure'da bir SQL Server 2014 veritabanı arka ucu ile Internet Information Services (IIS) üzerinde barındırılan LOB uygulamaları test etme.</span><span class="sxs-lookup"><span data-stu-id="70b12-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="70b12-113">Bu sanal karma bulut tabanlı BT iş yükünü test gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="70b12-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="70b12-114">Bu karma bulut test ortamı kurma üç temel aşamalara toosetting vardır:</span><span class="sxs-lookup"><span data-stu-id="70b12-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="70b12-115">Merhaba benzetimli karma bulut ortamını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="70b12-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="70b12-116">Merhaba SQL server bilgisayarı (SQL1) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="70b12-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="70b12-117">Merhaba LOB sunucusunu (LOB1) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="70b12-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="70b12-118">Bu iş yükünün bir Azure aboneliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="70b12-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="70b12-119">Bir MSDN veya Visual Studio aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="70b12-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="70b12-120">Merhaba üretim LOB uygulaması Azure üzerinde barındırılan bir örnek için bkz **iş kolu uygulamaları** adresindeki mimarisi şeması [Microsoft yazılım mimarisi diyagramları ve planlar](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="70b12-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="70b12-121">1. Aşama: hello benzetimli karma bulut ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="70b12-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="70b12-122">Merhaba oluşturma [benzetimli karma bulut test ortamı](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70b12-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="70b12-123">Bu test ortamı hello Corpnet alt hello APP1 sunucusunda hello varlığını gerektirmediğinden, şimdilik kapanabilir.</span><span class="sxs-lookup"><span data-stu-id="70b12-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="70b12-124">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="70b12-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="70b12-125">2. Aşama: hello SQL server bilgisayarı (SQL1) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70b12-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="70b12-126">Azure portal Hello gerekirse hello DC2 bilgisayarı başlatın.</span><span class="sxs-lookup"><span data-stu-id="70b12-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="70b12-127">Ardından, bir sanal makine, yerel bilgisayarınızda bir Azure PowerShell komut isteminde aşağıdaki komutları için SQL1 oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70b12-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="70b12-128">Önceki toorunning bu komutları hello değişken değerleri ve Kaldır merhaba < ve > karakterleri doldurun.</span><span class="sxs-lookup"><span data-stu-id="70b12-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="70b12-129">SQL1 Hello yerel yönetici hesabı kullanılarak hello Azure portal tooconnect tooSQL1 kullanın.</span><span class="sxs-lookup"><span data-stu-id="70b12-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="70b12-130">Ardından, Windows Güvenlik duvarı kuralları tooallow temel bağlantı test ediliyor ve SQL Server trafiği yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="70b12-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="70b12-131">Bir yönetici düzeyi Windows PowerShell komut isteminde SQL1 bilgisayarında, aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="70b12-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="70b12-132">Merhaba ping komutu 192.168.0.4 IP adresinden dört başarılı yanıt neden olur.</span><span class="sxs-lookup"><span data-stu-id="70b12-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="70b12-133">Merhaba ekleyeceğimize hello sürücü harfi F: olan yeni bir birim olarak SQL1 diskte ek veriler.</span><span class="sxs-lookup"><span data-stu-id="70b12-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="70b12-134">Merhaba sol bölmesinde Sunucu Yöneticisi'nin, **dosya ve depolama hizmetleri**ve ardından **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="70b12-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="70b12-135">Merhaba içeriği bölmesinde hello **diskleri** grubunda **disk 2** (Merhaba ile **bölüm** çok ayarlamak**bilinmeyen**).</span><span class="sxs-lookup"><span data-stu-id="70b12-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="70b12-136">Tıklatın **görevleri**ve ardından **yeni birim**.</span><span class="sxs-lookup"><span data-stu-id="70b12-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="70b12-137">Merhaba Yeni Birim Sihirbazı sayfasında başlamadan önce üzerinde Hello tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="70b12-138">Merhaba Select hello sunucu ve disk sayfasında tıklatın **Disk 2**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="70b12-139">İstendiğinde, tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="70b12-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="70b12-140">Hello hello birim sayfasının hello boyut belirtin, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="70b12-141">Merhaba Ata tooa sürücü harfi veya klasörü sayfasında, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="70b12-142">Merhaba Select dosya sistemi Ayarları sayfasında, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="70b12-143">Merhaba seçimlerini onaylayın sayfasında, tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="70b12-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="70b12-144">Tamamlandığında, tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="70b12-144">When complete, click **Close**.</span></span>

<span data-ttu-id="70b12-145">Merhaba Windows PowerShell komut isteminde şu komutları SQL1 üzerinde çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="70b12-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="70b12-146">Ardından, SQL1 bilgisayarında hello Windows PowerShell isteminde aşağıdaki komutları SQL1 toohello CORP Windows Server Active Directory etki alanına katılın.</span><span class="sxs-lookup"><span data-stu-id="70b12-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="70b12-147">İstendiğinde CORP\User1 hello hesabı kullanmak hello toosupply etki alanı hesap kimlik bilgilerini **Add-Computer** komutu.</span><span class="sxs-lookup"><span data-stu-id="70b12-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="70b12-148">Yeniden başlattıktan sonra hello Azure portal tooconnect tooSQL1 kullanmak *SQL1 hello yerel yönetici hesabı ile*.</span><span class="sxs-lookup"><span data-stu-id="70b12-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="70b12-149">Ardından, SQL Server 2014 toouse hello F: sürücü kullanıcı hesabı izinleri ve yeni veritabanları için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="70b12-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="70b12-150">Merhaba başlangıç ekranından yazın **SQL Server Management**ve ardından **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="70b12-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="70b12-151">İçinde **tooServer bağlanmak**, tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="70b12-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="70b12-152">Merhaba Nesne Gezgini ağaç bölmesinde, **SQL1**ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="70b12-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="70b12-153">Merhaba, **sunucu özellikleri** penceresinde tıklatın **veritabanı ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="70b12-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="70b12-154">Merhaba bulun **veritabanı varsayılan konumları** ve bu değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="70b12-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="70b12-155">İçin **veri**, tür hello yolu **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="70b12-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="70b12-156">İçin **günlük**, tür hello yolu **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="70b12-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="70b12-157">İçin **yedekleme**, tür hello yolu **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="70b12-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="70b12-158">Not: Yalnızca yeni veritabanları bu konumları kullanın.</span><span class="sxs-lookup"><span data-stu-id="70b12-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="70b12-159">Merhaba tıklatın **Tamam** tooclose hello penceresi.</span><span class="sxs-lookup"><span data-stu-id="70b12-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="70b12-160">Merhaba, **Object Explorer** ağaç bölmesinde, açık **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="70b12-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="70b12-161">Sağ **oturumları** ve ardından **yeni oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="70b12-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="70b12-162">İçinde **oturum açma adı**, türü **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="70b12-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="70b12-163">Merhaba üzerinde **sunucu rolleri** sayfasında, **sysadmin**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="70b12-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="70b12-164">Microsoft SQL Server Management Studio'yu kapatın.</span><span class="sxs-lookup"><span data-stu-id="70b12-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="70b12-165">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="70b12-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="70b12-166">3. Aşama: hello LOB sunucusunu (LOB1) yapılandırın</span><span class="sxs-lookup"><span data-stu-id="70b12-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="70b12-167">İlk olarak, bu komutlar hello Azure PowerShell komut isteminde, yerel bilgisayarınızda LOB1 için bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70b12-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="70b12-168">Ardından, hello Azure portal tooconnect tooLOB1 LOB1 hello yerel yönetici hesabını hello kimlik bilgileriyle kullanın.</span><span class="sxs-lookup"><span data-stu-id="70b12-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="70b12-169">Ardından, temel bağlantıyı test etmek için bir Windows Güvenlik duvarı kuralı tooallow trafiği yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="70b12-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="70b12-170">Bir yönetici düzeyi Windows PowerShell komut isteminde LOB1 üzerinde bu komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="70b12-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="70b12-171">Merhaba ping komutu 192.168.0.4 IP adresinden dört başarılı yanıt neden olur.</span><span class="sxs-lookup"><span data-stu-id="70b12-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="70b12-172">Ardından, hello Windows PowerShell komut isteminde aşağıdaki komutları LOB1 toohello CORP Active Directory etki alanına katılın.</span><span class="sxs-lookup"><span data-stu-id="70b12-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="70b12-173">İstendiğinde CORP\User1 hello hesabı kullanmak hello toosupply etki alanı hesap kimlik bilgilerini **Add-Computer** komutu.</span><span class="sxs-lookup"><span data-stu-id="70b12-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="70b12-174">Yeniden başlattıktan sonra hello Azure portal tooconnect tooLOB1 hello CORP\User1 hesap ve parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="70b12-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="70b12-175">Ardından, IIS için LOB1 yapılandırın ve İSTEMCİ1 erişimden sınayın.</span><span class="sxs-lookup"><span data-stu-id="70b12-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="70b12-176">Sunucu Yöneticisi'nden tıklatın **rol ve Özellik Ekle**.</span><span class="sxs-lookup"><span data-stu-id="70b12-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="70b12-177">Merhaba üzerinde **başlamadan önce** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="70b12-178">Merhaba üzerinde **yükleme türünü seçin** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="70b12-179">Merhaba üzerinde **Select hedef sunucu** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="70b12-180">Merhaba üzerinde **sunucu rolleri** sayfasında, **Web sunucusu (IIS)** hello listesinde **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="70b12-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="70b12-181">İstendiğinde, tıklatın **Özellik Ekle**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="70b12-182">Merhaba üzerinde **seçin özellikleri** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="70b12-183">Merhaba üzerinde **Web sunucusu (IIS)** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="70b12-184">Merhaba üzerinde **seçin, rol hizmetlerini** sayfasında, seçin veya iş KOLU uygulamanızı test etmek için gereksinim duyduğunuz hello Hizmetleri için hello onay kutularının işaretini kaldırın ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="70b12-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="70b12-185">Merhaba üzerinde **Yükleme Seçimlerini Onayla** sayfasında, **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="70b12-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="70b12-186">Merhaba bileşenlerin yüklenmesi tamamlanana kadar bekleyin ve ardından **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="70b12-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="70b12-187">Hello Azure portal, toohello İSTEMCİ1 bilgisayarını hello CORP\User1 hesabı kimlik bilgilerinizle bağlanmak ve Internet Explorer'ı başlatın.</span><span class="sxs-lookup"><span data-stu-id="70b12-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="70b12-188">Merhaba adres çubuğuna **http://lob1/** yazıp ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="70b12-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="70b12-189">Merhaba varsayılan IIS 8 web sayfasını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="70b12-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="70b12-190">Bu, geçerli bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="70b12-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="70b12-191">Bu ortam sunulmuştur web tabanlı uygulamanızdan LOB1 ve test işlevlerini İSTEMCİ1 hello Corpnet alt ağda, toodeploy için hazır.</span><span class="sxs-lookup"><span data-stu-id="70b12-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="70b12-192">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="70b12-192">Next step</span></span>
* <span data-ttu-id="70b12-193">Hello kullanarak yeni bir sanal makine Ekle [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70b12-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

