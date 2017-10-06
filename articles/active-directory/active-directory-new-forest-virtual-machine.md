---
title: "bir Azure sanal ağı üzerinde bir Active Directory ormanı aaaInstall | Microsoft Docs"
description: "Bir Azure sanal ağ üzerindeki bir sanal makinede (VM) nasıl toocreate yeni bir Active Directory orman açıklayan bir öğretici."
services: active-directory, virtual-network
keywords: "Active directory sanal makine, yükleme active directory ormanı, azure active directory videolarını "
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
tags: 
ms.assetid: eb7170d0-266a-4caa-adce-1855589d65d1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: joflore
ms.openlocfilehash: 08121130777cc3c206d7b5b38974982884dca1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-new-active-directory-forest-on-an-azure-virtual-network"></a>Bir Azure sanal ağ üzerinde yeni bir Active Directory ormanı yüklemek
Bu konuda gösterilmektedir nasıl toocreate yeni bir Windows Server Active Directory bir Azure sanal ağı üzerinde bir sanal makinede (VM) ortamda bir [Azure sanal ağı](../virtual-network/virtual-networks-overview.md). Bu durumda, hello Azure sanal ağı bağlı tooan şirket içi ağ değil.

Bu ilgili konularda ilginizi çekebilir:

* Bu adımları gösteren bir video için bkz [nasıl tooinstall yeni bir Active Directory orman bir Azure sanal ağı](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* İsteğe bağlı olarak yapabileceğiniz [siteden siteye VPN bağlantısını yapılandırma](../vpn-gateway/vpn-gateway-site-to-site-create.md) ve ardından yeni bir orman yüklemek veya bir şirket içi orman tooan Azure sanal ağı genişletir. Bu adımlar için bkz: [bir Azure sanal ağında bir çoğaltma Active Directory etki alanı denetleyicisi yükleme](active-directory-install-replica-active-directory-domain-controller.md).
* Active Directory etki alanı Hizmetleri (AD DS) bir Azure sanal ağ üzerinde yükleme ilgili kavramsal kılavuzlar için bkz: [yönergeleri dağıtma Windows Server Active Directory için Azure sanal makineler üzerinde](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Senaryo diyagramı
Bu senaryoda, dış kullanıcıların etki alanına katılmış sunucuları üzerinde çalışan tooaccess uygulamaları gerekir. Merhaba uygulama sunucusu çalıştırabilir hello VM'ler ve etki alanı denetleyicileri çalıştırma hello VM'ler kendi Azure sanal ağı bulut hizmetinde yüklü yüklenir. Ayrıca kullanılabilirlik geliştirilmiş hataya dayanıklılık için kümesi içinde dahil edilir.

![Azure sanal ağındaki sanal makinelerde Active Directory ormanı ][1] 7

## <a name="how-does-this-differ-from-on-premises"></a>Bu şirket içi nasıl farkı nedir?
Şirket içi Azure üzerinde bir etki alanı denetleyicisi yükleme arasındaki kadar fark değil. Aşağıdaki tablonun hello Hello temel farklar listelenmektedir.

| tooconfigure... | Şirket içi | Azure sanal ağı |
| --- | --- | --- |
| **Merhaba etki alanı denetleyicisi için IP adresi** |Merhaba ağ bağdaştırıcısı özellikleri statik IP adresi atayın |Statik bir IP adresi Hello kümesi AzureStaticVNetIP cmdlet tooassign çalıştırın |
| **DNS istemci çözümleyicisi** |Tercih edilen ve alternatif DNS sunucusu adresi hello üzerinde ağ bağdaştırıcısı etki alanı üyeleri özelliklerini ayarlayın. |DNS sunucusu adresi hello hello sanal ağ özelliklerini ayarlama |
| **Active Directory veritabanı depolama** |İsteğe bağlı olarak C:\ hello varsayılan depolama konumunu değiştirme |Toochange varsayılan depolama C:\ konumdan gerekir |

## <a name="create-an-azure-virtual-network"></a>Bir Azure sanal ağ oluşturma
1. İçinde toohello Klasik Azure portalında oturum açın.
2. Bir sanal ağ oluşturun. Tıklatın **ağlar** > **bir sanal ağ oluşturma**. Tablo toocomplete hello Sihirbazı aşağıdaki hello Hello değerlerini kullanın.

   | Bu sihirbaz sayfasında... | Bu değerleri belirtin |
   | --- | --- |
   |  **Sanal ağ ayrıntıları** |<p>Ad: sanal ağınız için bir ad girin</p><p>Bölge: hello en yakın bölgeyi seçin</p> |
   |  **DNS ve VPN** |<p>DNS sunucusu boş bırakın</p><p>Ya da VPN seçeneği kullanmayın</p> |
   |  **Sanal ağ adres alanları** |<p>Alt ağ adı: alt ağınız için bir ad girin</p><p>Başlangıç IP: <b>10.0.0.0</b></p><p>CIDR: <b>/24 (256)</b></p> |

## <a name="create-vms-toorun-hello-domain-controller-and-dns-server-roles"></a>Sanal makineleri toorun hello etki alanı denetleyicisi ve DNS sunucusu rolleri oluşturun
Aşağıdaki adımları toocreate gerektiğinde VM'ler toohost hello DC rolü hello yineleyin. En az iki sanal DC'leri tooprovide hata toleransı ve artıklık dağıtmanız gerekir. Hello Azure sanal ağı benzer şekilde yapılandırılmış en az iki DC'leri içerir (diğer bir deyişle, çalışma DNS sunucusu, her iki GC'ler oldukları ve ikisi herhangi bir FSMO rolüne vb. tutan) olanlar DC'leri kullanılabilirlik geliştirilmiş hataya dayanıklılık için kümesi çalıştırmanız hello VM'ler yerleştirin.

Kullanıcı Arabirimi, hello yerine Windows PowerShell kullanarak toocreate hello VM'ler bkz [kullanım Azure PowerShell toocreate ve Windows tabanlı sanal makineleri önceden](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Merhaba Klasik Portalı'nda tıklatın **yeni** > **işlem** > **sanal makine** > **Galeri'den**. Değerleri toocomplete hello Sihirbazı aşağıdaki hello kullanın. Başka bir değer önerilen ya da gerekli olmadıkça hello bir ayar için varsayılan değer kabul edin.

   | Bu sihirbaz sayfasında... | Bu değerleri belirtin |
   | --- | --- |
   |  **Bir görüntü seçin** |Windows Server 2012 R2 Datacenter |
   |  **Sanal Makine Yapılandırması** |<p>Sanal makine adı: (örneğin, AzureDC1) tek etiketli bir ad yazın.</p><p>Yeni bir kullanıcı adı: hello bir kullanıcının adını yazın. Bu kullanıcı hello VM hello yerel Yöneticiler grubunun bir üyesi olacaktır. Bu ad toosign toohello VM içinde ilk kez Merhaba gerekir. Yönetici adlı hello yerleşik hesap çalışmaz.</p><p>Yeni Parola/Onayla: bir parola yazın</p> |
   |  **Sanal Makine Yapılandırması** |<p>Bulut hizmeti: Seçin <b>yeni bir bulut hizmeti oluşturma</b> Merhaba ilk VM ve barındıracak daha fazla sanal makineleri oluştururken, aynı hizmet adı bulut seçin DC rolü hello.</p><p>Bulut hizmeti DNS adı: genel olarak benzersiz bir ad belirtin</p><p>Bölge/benzeşim grubu/sanal ağ: hello sanal ağ adı (örneğin, WestUSVNet) belirtin.</p><p>Depolama hesabı: Seçin <b>otomatik olarak oluşturulan depolama hesabı kullan</b> Merhaba ilk VM ve aynı depolama hesabı adı barındıracak daha fazla sanal makineleri oluşturduğunuzda, ardından DC rolü hello.</p><p>Kullanılabilirlik kümesi: Seçin <b>bir kullanılabilirlik kümesi oluştur</b>.</p><p>Kullanılabilirlik kümesi adı: yazın hello kullanılabilirlik oluşturduğunuzda kümesi için bir ad ilk VM hello ve daha fazla sanal makineleri oluşturduğunuzda aynı ad seçin.</p> |
   |  **Sanal Makine Yapılandırması** |<p>Seçin <b>yükleme hello VM Aracısı</b> ve gereksinim duyduğunuz diğer uzantılar.</p> |
2. Disk tooeach hello DC sunucusu rolünü çalıştıracak VM ekleyin. Merhaba ek disk gerekli toostore hello AD veritabanı, günlükler ve SYSVOL ' dir. Başlangıç diski (örneğin, 10 GB) için bir boyut belirtin ve hello bırakın **konak önbelleği tercihi** çok ayarlamak**hiçbiri**. Merhaba adımlar için bkz: [nasıl tooAttach veri diski tooa Windows sanal makine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Toohello VM ilk kez oturum sonra açmak **Sunucu Yöneticisi'ni** > **dosya ve depolama hizmetleri** toocreate NTFS kullanılarak bu disk üzerindeki bir birimi.
4. Statik bir IP adresi hello DC rolü çalıştıracak VM'ler için ayırın. tooreserve bir statik IP adresi, hello Microsoft Web Platformu Yükleyicisi'ı karşıdan yükle ve [Azure PowerShell'i yükleme](/powershell/azure/overview) ve hello kümesi AzureStaticVNetIP cmdlet'ini çalıştırın. Örneğin:

    `Get-AzureVM -ServiceName AzureDC1 -Name AzureDC1 | Set-AzureStaticVNetIP -IPAddress 10.0.0.4 | Update-AzureVM`

Statik bir IP adresi ayarlama hakkında daha fazla bilgi için bkz: [statik iç IP adresi için bir VM yapılandırma](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-windows-server-active-directory"></a>Windows Server Active Directory yükleyin
Kullanmak aynı yordamı çok hello[AD DS'yi yüklemek](https://technet.microsoft.com/library/jj574166.aspx) şirket içi kullanma (diğer bir deyişle, hello kullanıcı Arabirimi, bir yanıt dosyası ya da Windows PowerShell kullanabilirsiniz). Tooprovide yönetici kimlik bilgileri tooinstall yeni bir orman gerekir. toospecify hello konumu hello Active Directory veritabanı, günlükler ve SYSVOL toohello VM ekli hello işletim sistemi sürücüsü toohello ek verileri diskten hello varsayılan depolama konumunu değiştirebilirsiniz.

Merhaba DC yükleme tamamlandıktan sonra toohello VM yeniden bağlanın ve toohello DC üzerinde oturum. Toospecify etki alanı kimlik bilgilerini Hatırla.

## <a name="reset-hello-dns-server-for-hello-azure-virtual-network"></a>Merhaba DNS sunucusu hello Azure sanal ağı için Sıfırla
1. Hello DNS ileticisi hello yeni DC/DNS sunucusu ayarını sıfırlayın.
   1. Sunucu Yöneticisi'nde **Araçları** > **DNS**.
   2. İçinde **DNS Yöneticisi'ni**, hello hello DNS sunucusunun adını sağ tıklatın ve **özellikleri**.
   3. Merhaba üzerinde **İleticiler** sekmesinde hello ileticinin hello IP adresine ve öğesini tıklatın **Düzenle**.  Başlangıç IP adresi seçin ve tıklatın **silmek**.
   4. Tıklatın **Tamam** tooclose hello Düzenleyicisi'ni ve **Tamam** yeniden tooclose hello DNS sunucusu özellikleri.
2. Merhaba sanal ağ Hello DNS sunucusu ayarlarını güncelleştirin.
   1. ' I tıklatın **sanal ağlar** > merhaba sanal ağ oluşturduğunuz çift tıklayın > **yapılandırma** > **DNS sunucuları**, hello adı yazın ve DIP birinin hello Merhaba DC/DNS sunucusu rolü ve tıklatın çalıştıran VM'ler hello **kaydetmek**.
   2. Merhaba VM seçin ve tıklatın **yeniden** tootrigger hello VM tooconfigure DNS Çözümleyicisi ayarları hello hello yeni DNS sunucusunun IP adresine sahip.

## <a name="create-vms-for-domain-members"></a>Etki alanı üyeleri için sanal makineleri oluşturma
1. Uygulama sunucuları olarak adımları toocreate VM'ler toorun aşağıdaki hello yineleyin. Başka bir değer önerilen ya da gerekli olmadıkça hello bir ayar için varsayılan değer kabul edin.

   | Bu sihirbaz sayfasında... | Bu değerleri belirtin |
   | --- | --- |
   |  **Bir görüntü seçin** |Windows Server 2012 R2 Datacenter |
   |  **Sanal Makine Yapılandırması** |<p>Sanal makine adı: (örneğin, AppServer1) tek etiketli bir ad yazın.</p><p>Yeni bir kullanıcı adı: hello bir kullanıcının adını yazın. Bu kullanıcı hello VM hello yerel Yöneticiler grubunun bir üyesi olacaktır. Bu ad toosign toohello VM içinde ilk kez Merhaba gerekir. Yönetici adlı hello yerleşik hesap çalışmaz.</p><p>Yeni Parola/Onayla: bir parola yazın</p> |
   |  **Sanal Makine Yapılandırması** |<p>Bulut hizmeti: Seçin **yeni bir bulut hizmeti oluşturma** Merhaba Merhaba uygulaması ilk VM ve daha fazla sanal makineleri oluştururken aynı hizmet adı bulut seçin barındıracak.</p><p>Bulut hizmeti DNS adı: genel olarak benzersiz bir ad belirtin</p><p>Bölge/benzeşim grubu/sanal ağ: hello sanal ağ adı (örneğin, WestUSVNet) belirtin.</p><p>Depolama hesabı: Seçin **otomatik olarak oluşturulan depolama hesabı kullan** Merhaba Merhaba uygulaması ilk VM ve aynı depolama hesabı adı daha fazla sanal makineleri oluşturduğunuzda seçip barındıracak.</p><p>Kullanılabilirlik kümesi: Seçin **bir kullanılabilirlik kümesi oluştur**.</p><p>Kullanılabilirlik kümesi adı: yazın hello kullanılabilirlik oluşturduğunuzda kümesi için bir ad ilk VM hello ve daha fazla sanal makineleri oluşturduğunuzda aynı ad seçin.</p> |
   |  **Sanal Makine Yapılandırması** |<p>Seçin <b>yükleme hello VM Aracısı</b> ve gereksinim duyduğunuz diğer uzantılar.</p> |
2. Her VM sağlandıktan sonra oturum açın ve toohello etki alanına katılın. İçinde **Sunucu Yöneticisi'ni**, tıklatın **yerel sunucu** > **çalışma grubu** > **Değiştir...** ve ardından **etki alanı** ve şirket içi etki alanınızın türü hello adı. Bir etki alanı kullanıcı kimlik bilgilerini sağlayın ve ardından hello VM toocomplete hello etki alanına katılma yeniden başlatın.

Kullanıcı Arabirimi, hello yerine Windows PowerShell kullanarak toocreate hello VM'ler bkz [kullanım Azure PowerShell toocreate ve Windows tabanlı sanal makineleri önceden](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Windows PowerShell'i kullanma hakkında daha fazla bilgi için bkz: [Azure cmdlet'leri ile çalışmaya başlama](/powershell/azure/overview) ve [Azure Cmdlet başvurusu](/powershell/azure/get-started-azureps).

## <a name="see-also"></a>Ayrıca Bkz.
* [Nasıl tooinstall yeni bir Active Directory orman bir Azure sanal ağı](http://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/How-to-install-a-new-Active-Directory-forest-on-an-Azure-virtual-network)
* [Windows Server Active Directory, Azure sanal makinelerde dağıtmak için yönergeler](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Siteden siteye VPN bağlantısını yapılandırma](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Bir Azure sanal ağındaki bir çoğaltma Active Directory etki alanı denetleyicisi yükleme](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure BT Uzmanı Iaas: (01) sanal makine temelleri](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure BT Uzmanı Iaas: oluşturma (05) sanal ağlar ve şirket içi bağlantılar](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Sanal ağ genel bakış](../virtual-network/virtual-networks-overview.md)
* [Nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure Cmdlet Başvurusu](/powershell/azure/get-started-azureps)
* [Azure VM statik IP adresi kümesi](http://windowsitpro.com/windows-azure/set-azure-vm-static-ip-address)
* [Nasıl tooassign statik IP tooAzure VM](http://www.bhargavs.com/index.php/2014/03/13/how-to-assign-static-ip-to-azure-vm/)
* [Yeni bir Active Directory ormanı yüklemek](https://technet.microsoft.com/library/jj574166.aspx)
* [Giriş tooActive Directory etki alanı Hizmetleri (AD DS) sanallaştırma (düzey 100)](https://technet.microsoft.com/library/hh831734.aspx)

<!--Image references-->
[1]: ./media/active-directory-new-forest-virtual-machine/AD_Forest.png
