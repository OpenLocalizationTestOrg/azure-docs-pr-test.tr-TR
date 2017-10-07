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
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Test için karma bulutta web tabanlı LOB uygulaması oluşturma
Bu konu bir iş (LOB) uygulaması Microsoft Azure üzerinde barındırılan web tabanlı satır test etmek için bir sanal karma bulut ortamı oluşturma konusunda adımları. Merhaba sonuçta elde edilen yapılandırma aşağıda verilmiştir.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Bu yapılandırma oluşur:

* (Merhaba sınama laboratuvarı VNet) Azure üzerinde barındırılan sanal şirket içi ağ.
* (TestVNET) Azure üzerinde barındırılan bir şirket içi sanal ağ.
* VNet-VNet VPN bağlantısı.
* Web tabanlı LOB server, SQL server ve hello TestVNET sanal ağındaki ikincil etki alanı denetleyicisi.

Bu yapılandırma temeli ve, yapabileceğiniz ortak başlangıç noktası sağlar:

* Geliştirme ve azure'da bir SQL Server 2014 veritabanı arka ucu ile Internet Information Services (IIS) üzerinde barındırılan LOB uygulamaları test etme.
* Bu sanal karma bulut tabanlı BT iş yükünü test gerçekleştirin.

Bu karma bulut test ortamı kurma üç temel aşamalara toosetting vardır:

1. Merhaba benzetimli karma bulut ortamını ayarlama.
2. Merhaba SQL server bilgisayarı (SQL1) yapılandırın.
3. Merhaba LOB sunucusunu (LOB1) yapılandırın.

Bu iş yükünün bir Azure aboneliği gerektirir. Bir MSDN veya Visual Studio aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Merhaba üretim LOB uygulaması Azure üzerinde barındırılan bir örnek için bkz **iş kolu uygulamaları** adresindeki mimarisi şeması [Microsoft yazılım mimarisi diyagramları ve planlar](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>1. Aşama: hello benzetimli karma bulut ortamını ayarlama
Merhaba oluşturma [benzetimli karma bulut test ortamı](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Bu test ortamı hello Corpnet alt hello APP1 sunucusunda hello varlığını gerektirmediğinden, şimdilik kapanabilir.

Bu, geçerli bir yapılandırmadır.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>2. Aşama: hello SQL server bilgisayarı (SQL1) yapılandırma
Azure portal Hello gerekirse hello DC2 bilgisayarı başlatın.

Ardından, bir sanal makine, yerel bilgisayarınızda bir Azure PowerShell komut isteminde aşağıdaki komutları için SQL1 oluşturun. Önceki toorunning bu komutları hello değişken değerleri ve Kaldır merhaba < ve > karakterleri doldurun.

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

SQL1 Hello yerel yönetici hesabı kullanılarak hello Azure portal tooconnect tooSQL1 kullanın.

Ardından, Windows Güvenlik duvarı kuralları tooallow temel bağlantı test ediliyor ve SQL Server trafiği yapılandırın. Bir yönetici düzeyi Windows PowerShell komut isteminde SQL1 bilgisayarında, aşağıdaki komutları çalıştırın.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

Merhaba ping komutu 192.168.0.4 IP adresinden dört başarılı yanıt neden olur.

Merhaba ekleyeceğimize hello sürücü harfi F: olan yeni bir birim olarak SQL1 diskte ek veriler.

1. Merhaba sol bölmesinde Sunucu Yöneticisi'nin, **dosya ve depolama hizmetleri**ve ardından **diskleri**.
2. Merhaba içeriği bölmesinde hello **diskleri** grubunda **disk 2** (Merhaba ile **bölüm** çok ayarlamak**bilinmeyen**).
3. Tıklatın **görevleri**ve ardından **yeni birim**.
4. Merhaba Yeni Birim Sihirbazı sayfasında başlamadan önce üzerinde Hello tıklatın **sonraki**.
5. Merhaba Select hello sunucu ve disk sayfasında tıklatın **Disk 2**ve ardından **sonraki**. İstendiğinde, tıklatın **Tamam**.
6. Hello hello birim sayfasının hello boyut belirtin, tıklatın **sonraki**.
7. Merhaba Ata tooa sürücü harfi veya klasörü sayfasında, tıklatın **sonraki**.
8. Merhaba Select dosya sistemi Ayarları sayfasında, tıklatın **sonraki**.
9. Merhaba seçimlerini onaylayın sayfasında, tıklatın **oluşturma**.
10. Tamamlandığında, tıklayın **Kapat**.

Merhaba Windows PowerShell komut isteminde şu komutları SQL1 üzerinde çalıştırın:

    md f:\Data
    md f:\Log
    md f:\Backup

Ardından, SQL1 bilgisayarında hello Windows PowerShell isteminde aşağıdaki komutları SQL1 toohello CORP Windows Server Active Directory etki alanına katılın.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

İstendiğinde CORP\User1 hello hesabı kullanmak hello toosupply etki alanı hesap kimlik bilgilerini **Add-Computer** komutu.

Yeniden başlattıktan sonra hello Azure portal tooconnect tooSQL1 kullanmak *SQL1 hello yerel yönetici hesabı ile*.

Ardından, SQL Server 2014 toouse hello F: sürücü kullanıcı hesabı izinleri ve yeni veritabanları için yapılandırın.

1. Merhaba başlangıç ekranından yazın **SQL Server Management**ve ardından **SQL Server 2014 Management Studio**.
2. İçinde **tooServer bağlanmak**, tıklatın **Bağlan**.
3. Merhaba Nesne Gezgini ağaç bölmesinde, **SQL1**ve ardından **özellikleri**.
4. Merhaba, **sunucu özellikleri** penceresinde tıklatın **veritabanı ayarlarını**.
5. Merhaba bulun **veritabanı varsayılan konumları** ve bu değerleri ayarlayın: 
   * İçin **veri**, tür hello yolu **f:\Data**.
   * İçin **günlük**, tür hello yolu **f:\Log**.
   * İçin **yedekleme**, tür hello yolu **f:\Backup**.
   * Not: Yalnızca yeni veritabanları bu konumları kullanın.
6. Merhaba tıklatın **Tamam** tooclose hello penceresi.
7. Merhaba, **Object Explorer** ağaç bölmesinde, açık **güvenlik**.
8. Sağ **oturumları** ve ardından **yeni oturum açma**.
9. İçinde **oturum açma adı**, türü **CORP\User1**.
10. Merhaba üzerinde **sunucu rolleri** sayfasında, **sysadmin**ve ardından **Tamam**.
11. Microsoft SQL Server Management Studio'yu kapatın.

Bu, geçerli bir yapılandırmadır.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>3. Aşama: hello LOB sunucusunu (LOB1) yapılandırın
İlk olarak, bu komutlar hello Azure PowerShell komut isteminde, yerel bilgisayarınızda LOB1 için bir sanal makine oluşturun.

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

Ardından, hello Azure portal tooconnect tooLOB1 LOB1 hello yerel yönetici hesabını hello kimlik bilgileriyle kullanın.

Ardından, temel bağlantıyı test etmek için bir Windows Güvenlik duvarı kuralı tooallow trafiği yapılandırın. Bir yönetici düzeyi Windows PowerShell komut isteminde LOB1 üzerinde bu komutları çalıştırın.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

Merhaba ping komutu 192.168.0.4 IP adresinden dört başarılı yanıt neden olur.

Ardından, hello Windows PowerShell komut isteminde aşağıdaki komutları LOB1 toohello CORP Active Directory etki alanına katılın.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

İstendiğinde CORP\User1 hello hesabı kullanmak hello toosupply etki alanı hesap kimlik bilgilerini **Add-Computer** komutu.

Yeniden başlattıktan sonra hello Azure portal tooconnect tooLOB1 hello CORP\User1 hesap ve parola kullanın.

Ardından, IIS için LOB1 yapılandırın ve İSTEMCİ1 erişimden sınayın.

1. Sunucu Yöneticisi'nden tıklatın **rol ve Özellik Ekle**.
2. Merhaba üzerinde **başlamadan önce** sayfasında, **sonraki**.
3. Merhaba üzerinde **yükleme türünü seçin** sayfasında, **sonraki**.
4. Merhaba üzerinde **Select hedef sunucu** sayfasında, **sonraki**.
5. Merhaba üzerinde **sunucu rolleri** sayfasında, **Web sunucusu (IIS)** hello listesinde **rolleri**.
6. İstendiğinde, tıklatın **Özellik Ekle**ve ardından **sonraki**.
7. Merhaba üzerinde **seçin özellikleri** sayfasında, **sonraki**.
8. Merhaba üzerinde **Web sunucusu (IIS)** sayfasında, **sonraki**.
9. Merhaba üzerinde **seçin, rol hizmetlerini** sayfasında, seçin veya iş KOLU uygulamanızı test etmek için gereksinim duyduğunuz hello Hizmetleri için hello onay kutularının işaretini kaldırın ve ardından **sonraki**.
10. Merhaba üzerinde **Yükleme Seçimlerini Onayla** sayfasında, **yükleme**.
11. Merhaba bileşenlerin yüklenmesi tamamlanana kadar bekleyin ve ardından **Kapat**.
12. Hello Azure portal, toohello İSTEMCİ1 bilgisayarını hello CORP\User1 hesabı kimlik bilgilerinizle bağlanmak ve Internet Explorer'ı başlatın.
13. Merhaba adres çubuğuna **http://lob1/** yazıp ENTER tuşuna basın. Merhaba varsayılan IIS 8 web sayfasını görmeniz gerekir.

Bu, geçerli bir yapılandırmadır.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Bu ortam sunulmuştur web tabanlı uygulamanızdan LOB1 ve test işlevlerini İSTEMCİ1 hello Corpnet alt ağda, toodeploy için hazır.

## <a name="next-step"></a>Sonraki adım
* Hello kullanarak yeni bir sanal makine Ekle [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

