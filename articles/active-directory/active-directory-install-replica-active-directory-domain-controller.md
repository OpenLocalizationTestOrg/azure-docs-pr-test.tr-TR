---
title: "bir çoğaltma Active Directory etki alanı denetleyicisi azure'da aaaInstall | Microsoft Docs"
description: "Bir Azure sanal makinesi üzerinde nasıl tooinstall bir şirket içi Active Directory etki alanı denetleyicisinden orman açıklar Öğreticisi."
services: virtual-network
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8c9ebf1b-289a-4dd6-9567-a946450005c0
ms.service: virtual-network
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 74876fce2ca2a29f02c2828f9b3a21227248233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-replica-active-directory-domain-controller-in-an-azure-virtual-network"></a>Bir Azure sanal ağındaki bir çoğaltma Active Directory etki alanı denetleyicisi yükleme
Bu konuda gösterilmektedir nasıl bir Azure sanal ağı Azure sanal makinelerle (VM'ler) şirket içi Active Directory etki alanı için tooinstall ek etki alanı denetleyicileri (olarak da bilinen çoğaltma DC'ler).

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.

Bu ilgili konularda ilginizi çekebilir:

* Bu gibi durumlarda, yeni bir Active Directory ormanı isteğe bağlı olarak bir Azure sanal ağ üzerinde yükleyebilirsiniz. Bu adımlar için bkz: [bir Azure sanal ağ üzerinde yeni bir Active Directory ormanı yüklemek](active-directory-new-forest-virtual-machine.md).
* Active Directory etki alanı Hizmetleri (AD DS) bir Azure sanal ağ üzerinde yükleme ilgili kavramsal kılavuzlar için bkz: [yönergeleri dağıtma Windows Server Active Directory için Azure sanal makineler üzerinde](https://msdn.microsoft.com/library/azure/jj156090.aspx).

## <a name="scenario-diagram"></a>Senaryo diyagramı
Bu senaryoda, dış kullanıcıların etki alanına katılmış sunucuları üzerinde çalışan tooaccess uygulamaları gerekir. Merhaba hello uygulama sunucusu çalıştırabilir ve çoğaltma DC'leri hello VM'ler bir Azure sanal ağında yüklenir. Merhaba sanal ağ bağlantılı toohello şirket içi ağ tarafından olabilir bir [siteden siteye VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) hello aşağıda gösterildiği gibi bağlantı diyagramı veya kullanabilirsiniz [ExpressRoute](../expressroute/expressroute-locations-providers.md) daha hızlı bağlantı.

Merhaba uygulama sunucuları ve hello DC'leri dağıtıldığı ayrı bulut Hizmetleri içinde toodistribute işlem işleme ve içinde [kullanılabilirlik kümeleri](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) geliştirilmiş hataya dayanıklılık için.
Hello DC'leri Active Directory çoğaltmasını kullanarak birbiriyle ve şirket içi DC'leri ile çoğaltılır. Hiçbir eşitleme araçları gereklidir.

![Bir Azure sanal PF çoğaltma Active Directory etki alanı denetleyicisi diyagram][1]

## <a name="create-an-active-directory-site-for-hello-azure-virtual-network"></a>Hello Azure sanal ağı için bir Active Directory sitesi oluşturun
İyi bir fikir toocreate Active Directory'de hello ağ bölgeyi karşılık gelen toohello sanal ağ temsil eden bir site değil. Kimlik doğrulama, çoğaltma ve diğer DC Konum işlemleri en iyi duruma getirme yardımcı olur. Merhaba aşağıdaki adımlarda açıklanmaktadır nasıl toocreate bir site ve daha fazla arka plan için bkz: [yeni bir Site Ekleme](https://technet.microsoft.com/library/cc781496.aspx).

1. Active Directory Siteleri ve Hizmetleri'ni açmak: **Sunucu Yöneticisi'ni** > **Araçları** > **Active Directory Siteleri ve Hizmetleri**.
2. Bir Azure sanal ağı oluşturulduğu site toorepresent hello bölgesi oluşturun: tıklatın **siteleri** > **eylem** > **yeni site** > türü Hello Azure ABD Batı gibi hello yeni sitenin adını > bir site bağlantısı seçin > **Tamam**.
3. Bir alt ağ oluşturun ve yeni bir site hello ile ilişkilendirin: çift **siteleri** > sağ tıklayın **alt ağlar** > **yeni bir alt ağ** > merhaba IP adres aralığı yazın Merhaba sanal ağa (örneğin, 10.1.0.0/16 hello senaryo diyagramındaki) > seçin hello yeni Azure sitesi > **Tamam**.

## <a name="create-an-azure-virtual-network"></a>Bir Azure sanal ağ oluşturma
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **yeni** > **Ağ Hizmetleri** > **sanal ağ**  >  **Özel Oluştur** ve kullanım hello aşağıdaki değerleri toocomplete hello Sihirbazı.

   | Bu sihirbaz sayfasında... | Bu değerleri belirtin |
   | --- | --- |
   |  **Sanal ağ ayrıntıları** |<p>Ad: WestUSVNet gibi hello sanal ağ için bir ad yazın.</p><p>Bölge: hello en yakın bölgeyi seçin.</p> |
   |  **DNS ve VPN bağlantısı** |<p>DNS sunucuları: hello adını ve bir veya daha fazla şirket içi DNS sunucusunun IP adresini belirtin.</p><p>Bağlantı: Seçin **siteden siteye VPN bağlantısını yapılandırma**.</p><p>Yerel ağ: yeni bir yerel ağ belirtin.</p><p>ExpressRoute yerine bir VPN kullanıyorsanız bkz [bir ExpressRoute bağlantı Exchange sağlayıcısı aracılığıyla yapılandırmayı](../expressroute/expressroute-locations-providers.md).</p> |
   |  **Siteden siteye bağlantı** |<p>Ad: hello şirket içi ağ için bir ad yazın.</p><p>VPN cihazı IP adresi: toohello sanal ağa bağlanması hello aygıt hello ortak IP adresini belirtin. Merhaba VPN cihazı bir NAT'nin arkasında olamaz</p><p>Adres: şirket içi ağınız (örneğin, hello senaryo diyagramı 192.168.0.0/16) hello adres aralıklarını belirtin.</p> |
   |  **Sanal ağ adres alanları** |<p>Adres alanı: hello Azure sanal ağı (örneğin, 10.1.0.0/16 hello senaryo diyagramındaki) toorun istediğiniz VM'ler için başlangıç IP adresi aralığı belirtin. Bu adres aralığı hello şirket içi ağın hello adres aralığı ile örtüşemez.</p><p>Alt ağları: bir ad ve adres hello uygulama sunucuları için bir alt ağ belirtin (gibi ön uç, 10.1.1.0/24) ve hello DC'ler için (arka uç gibi 10.1.2.0/24).</p><p>Tıklatın **ağ geçidi alt ağı eklemek**.</p> |
2. Ardından, hello sanal ağ geçidi toocreate güvenli bir siteden siteye VPN bağlantısı yapılandıracaksınız. Bkz: [bir sanal ağ geçidi yapılandırma](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) hello yönergeler için.
3. Merhaba yeni bir sanal ağ ve bir şirket içi VPN cihazı arasında Hello siteden siteye VPN bağlantısı oluşturun. Bkz: [bir sanal ağ geçidi yapılandırma](../vpn-gateway/vpn-gateway-configure-vpn-gateway-mp.md) hello yönergeler için.

## <a name="create-azure-vms-for-hello-dc-roles"></a>Azure VM'ler için hello DC rolleri oluşturabilir.
Aşağıdaki adımları toocreate gerektiğinde VM'ler toohost hello DC rolü hello yineleyin. En az iki sanal DC'leri tooprovide hata toleransı ve artıklık dağıtmanız gerekir. Hello Azure sanal ağı benzer şekilde yapılandırılmış en az iki DC'leri içerir (diğer bir deyişle, çalışma DNS sunucusu, her iki GC'ler oldukları ve ikisi herhangi bir FSMO rolüne vb. tutan) olanlar DC'leri kullanılabilirlik geliştirilmiş hataya dayanıklılık için kümesi çalıştırmanız hello VM'ler yerleştirin.
Kullanıcı Arabirimi, hello yerine Windows PowerShell kullanarak toocreate hello VM'ler bkz [kullanım Azure PowerShell toocreate ve Windows tabanlı sanal makineleri önceden](../virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), tıklatın **yeni** > **işlem** > **sanal makine**  >  **Galerisinden**. Değerleri toocomplete hello Sihirbazı aşağıdaki hello kullanın. Başka bir değer önerilen ya da gerekli olmadıkça hello bir ayar için varsayılan değer kabul edin.

   | Bu sihirbaz sayfasında... | Bu değerleri belirtin |
   | --- | --- |
   |  **Bir görüntü seçin** |Windows Server 2012 R2 Datacenter |
   |  **Sanal Makine Yapılandırması** |<p>Sanal makine adı: (örneğin, AzureDC1) tek etiketli bir ad yazın.</p><p>Yeni bir kullanıcı adı: hello bir kullanıcının adını yazın. Bu kullanıcı hello VM hello yerel Yöneticiler grubunun bir üyesi olacaktır. Bu ad toosign toohello VM içinde ilk kez Merhaba gerekir. Yönetici adlı hello yerleşik hesap çalışmaz.</p><p>Yeni Parola/Onayla: bir parola yazın</p> |
   |  **Sanal Makine Yapılandırması** |<p>Bulut hizmeti: Seçin <b>yeni bir bulut hizmeti oluşturma</b> Merhaba ilk VM ve barındıracak daha fazla sanal makineleri oluştururken, aynı hizmet adı bulut seçin DC rolü hello.</p><p>Bulut hizmeti DNS adı: genel olarak benzersiz bir ad belirtin</p><p>Bölge/benzeşim grubu/sanal ağ: hello sanal ağ adı (örneğin, WestUSVNet) belirtin.</p><p>Depolama hesabı: Seçin <b>otomatik olarak oluşturulan depolama hesabı kullan</b> Merhaba ilk VM ve aynı depolama hesabı adı barındıracak daha fazla sanal makineleri oluşturduğunuzda, ardından DC rolü hello.</p><p>Kullanılabilirlik kümesi: Seçin <b>bir kullanılabilirlik kümesi oluştur</b>.</p><p>Kullanılabilirlik kümesi adı: yazın hello kullanılabilirlik oluşturduğunuzda kümesi için bir ad ilk VM hello ve daha fazla sanal makineleri oluşturduğunuzda aynı ad seçin.</p> |
   |  **Sanal Makine Yapılandırması** |<p>Seçin <b>yükleme hello VM Aracısı</b> ve gereksinim duyduğunuz diğer uzantılar.</p> |
2. Disk tooeach hello DC sunucusu rolünü çalıştıracak VM ekleyin. Merhaba ek disk gerekli toostore hello AD veritabanı, günlükler ve SYSVOL ' dir. Başlangıç diski (örneğin, 10 GB) için bir boyut belirtin ve hello bırakın **konak önbelleği tercihi** çok ayarlamak**hiçbiri**. Merhaba adımlar için bkz: [nasıl tooAttach veri diski tooa Windows sanal makine](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Toohello VM ilk kez oturum sonra açmak **Sunucu Yöneticisi'ni** > **dosya ve depolama hizmetleri** toocreate NTFS kullanılarak bu disk üzerindeki bir birimi.
4. Statik bir IP adresi hello DC rolü çalıştıracak VM'ler için ayırın. tooreserve bir statik IP adresi, hello Microsoft Web Platformu Yükleyicisi'ı karşıdan yükle ve [Azure PowerShell'i yükleme](/powershell/azure/overview) ve hello kümesi AzureStaticVNetIP cmdlet'ini çalıştırın. Örneğin:

    ' Get-AzureVM - ServiceName AzureDC1-ad AzureDC1 | Set-AzureStaticVNetIP - IPADDRESS 10.0.0.4 | Update-AzureVM

Statik bir IP adresi ayarlama hakkında daha fazla bilgi için bkz: [statik iç IP adresi için bir VM yapılandırma](../virtual-network/virtual-networks-reserved-private-ip.md).

## <a name="install-ad-ds-on-azure-vms"></a>Azure VM'ler üzerinde AD DS'yi yüklemek
Tooa VM oturum ve şirket içi ağınızda arasında hello siteden siteye VPN veya ExpressRoute bağlantı tooresources bağlantı sahip olduğunuzu doğrulayın. Daha sonra AD DS hello Azure Vm'leri üzerinde yükleyin. (Kullanıcı Arabirimi, Windows PowerShell veya bir yanıt dosyası) şirket içi ağınızda tooinstall ek DC kullanmak işlemin aynısını kullanabilirsiniz. AD DS'yi yüklemek gibi yeni bir birim hello hello AD veritabanı, günlükler ve SYSVOL hello konumu için belirttiğinizden emin olun. AD DS yüklemesi üzerinde Yenileyici gerekirse bkz [Active Directory etki alanı hizmetlerini yükleme (düzey 100)](https://technet.microsoft.com/library/hh472162.aspx) veya [varolan bir etki alanında (Düzey 200) kopya Windows Server 2012 etki alanı denetleyicisi yükleme](https://technet.microsoft.com/library/jj574134.aspx).

## <a name="reconfigure-dns-server-for-hello-virtual-network"></a>Merhaba sanal ağınızın DNS sunucusu yeniden yapılandırın
1. Merhaba, [Azure portal](https://portal.azure.com), hello, **arama kaynakları** kutusuna *sanal ağlar*, ardından **sanal ağları (Klasik)** içinde Merhaba arama sonuçları. Merhaba sanal ağ, Hello adına tıklayın ve ardından [hello DNS sunucusu IP adreslerini sanal ağınız için yeniden](../virtual-network/virtual-network-manage-network.md#dns-servers) toouse hello statik IP adresleri atanan toohello bir şirket içi DNS hello IP adreslerini yerine çoğaltma DC'leri sunucuları.
2. Tüm hello çoğaltma DC VM'ler hello sanal ağda yapılandırıldığından hello sanal ağdaki toouse DNS sunucularıyla tooensure tıklatın **sanal makineleri**hello durum sütunu her VM için tıklatın ve ardından **yeniden başlatın** . Merhaba VM görüntüleyene kadar bekleyin **çalıştıran** toosign içine denemeden önce belirtin.

## <a name="create-vms-for-application-servers"></a>Uygulama sunucuları için sanal makineleri oluşturma
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

## <a name="additional-resources"></a>Ek kaynaklar
* [Windows Server Active Directory, Azure sanal makinelerde dağıtmak için yönergeler](https://msdn.microsoft.com/library/azure/jj156090.aspx)
* [Nasıl tooupload var olan Hyper-V etki alanı denetleyicileri tooAzure Azure PowerShell kullanarak şirket içi](http://support.microsoft.com/kb/2904015)
* [Bir Azure sanal ağ üzerinde yeni bir Active Directory ormanı yüklemek](active-directory-new-forest-virtual-machine.md)
* [Azure Sanal Ağ](../virtual-network/virtual-networks-overview.md)
* [Microsoft Azure BT Uzmanı Iaas: (01) sanal makine temelleri](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure BT Uzmanı Iaas: oluşturma (05) sanal ağlar ve şirket içi bağlantılar](http://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)
* [Azure PowerShell](/powershell/azure/overview)
* [Azure yönetim cmdlet'leri](/powershell/module/azurerm.compute/#virtual_machines)

<!--Image references-->
[1]: ./media/active-directory-install-replica-active-directory-domain-controller/ReplicaDCsOnAzureVNet.png
