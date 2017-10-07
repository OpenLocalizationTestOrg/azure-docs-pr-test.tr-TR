---
title: "Dağıtımı Windows Server Active Directory için Azure sanal makineler üzerinde aaaGuidelines | Microsoft Docs"
description: "Toodeploy AD etki alanı Hizmetleri ve şirket içi, AD Federasyon Hizmetleri nasıl bilgi Azure sanal makinelerde nasıl çalıştıklarını biliyorsanız."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>Windows Server Active Directory Azure sanal makinelerde dağıtmak için yönergeler
Bu makalede hello dağıtma Windows Server Active Directory etki alanı Hizmetleri (AD DS) ve Active Directory Federasyon Hizmetleri (AD FS) Microsoft Azure sanal makinelerde dağıtmak ve şirket arasındaki önemli farklar açıklanmaktadır.

## <a name="scope-and-audience"></a>Kapsam ve hedef kitle
Merhaba makale olanlar zaten içi Active Directory dağıtımı ile karşılaştı yöneliktir. Microsoft Azure sanal makineleri/Azure sanal ağlar ve geleneksel şirket içi Active Directory dağıtımlarında Active Directory dağıtımı arasında hello farklılıkları kapsar. Azure sanal makineler ve Azure sanal ağlar bir altyapı olarak-bilgi işlem kaynakları hello bulutta kuruluşlar tooleverage sunan hizmet (Iaas) parçasıdır.

Olmayanlar için AD dağıtımı ile tanıdık, hello bkz [AD DS dağıtım kılavuzu](https://technet.microsoft.com/library/cc753963) veya [AD FS dağıtımınızı planlama](https://technet.microsoft.com/library/dn151324.aspx) uygun şekilde.

Bu makalede hello okuyucu kavramları aşağıdaki hello ile alışkın olduğu varsayılmaktadır:

* Windows Server AD DS dağıtım ve Yönetimi
* Dağıtım ve DNS toosupport bir Windows Server AD DS altyapısının yapılandırma
* Windows Server AD FS dağıtımı ve Yönetimi
* Dağıtma, yapılandırma ve Windows Server AD FS belirteçleri tüketebileceği bağlı olan taraf uygulamaları (Web siteleri ve web Hizmetleri) yönetme
* Genel sanal makine kavramlar, gibi nasıl tooconfigure sanal bir makine, sanal diskler ve sanal ağlar

Bu makale, hangi Windows Server AD DS veya AD FS kısmen dağıtılan şirket içi ve kısmen Azure sanal makinelerinde dağıtılan bir karma dağıtım senaryosu için hello gereksinimleri vurgular. Merhaba belge ilk Windows Server AD DS ve AD FS ile şirket içi ve tasarım ve dağıtım etkileyen önemli karar noktaları Azure sanal makinelerde çalışan arasındaki kritik farklar hello kapsar. Merhaba kağıt Hello kalanında her hello karar noktaları daha fazla ayrıntı ve nasıl tooapply hello yönergeleri toovarious dağıtım senaryoları için yönergeleri verilmektedir.

Bu makalede hello yapılandırmasını tartışılmaz [Azure Active Directory](http://azure.microsoft.com/services/active-directory/), bulut uygulamaları için kimlik yönetimi ve erişim denetimi özellikleri sağlayan REST tabanlı bir hizmet olduğu. Azure Active Directory (Azure AD) ve Windows Server AD DS olan, ancak tasarlanmış toowork birlikte tooprovide bugünün karma BT için bir kimlik ve erişim yönetimi çözümü ortamları ve modern uygulamalar. toohelp ve Windows Server AD DS ve Azure AD arasındaki ilişkileri hello farkları anlamak, hello aşağıdakileri göz önünde bulundurun:

1. Azure tooextend kullanırken, Windows Server AD DS hello bulutta Azure sanal makinelerde, şirket içi veri merkezi hello bulutunu çalıştırabilirsiniz.
2. Kullanıcılar tek oturum açma tooSoftware olarak-hizmet (SaaS) uygulamalarınızı Azure AD toogive kullanabilir. Örneğin, Microsoft Office 365 bu teknolojisini kullanır ve Azure veya Bulut platformlarıyla üzerinde çalışan uygulamalar de kullanabilirsiniz.
3. Facebook, Google, Microsoft ve hello Bulut veya şirket içi barındırılan diğer kimlik sağlayıcıları tooapplications kimliklerden kullanarak Azure AD (kendi erişim denetimi hizmeti) toolet kullanıcılar oturum kullanabilir.

Bu farklılıklar hakkında daha fazla bilgi için bkz: [Azure kimlik](fundamentals-identity.md).

## <a name="related-resources"></a>İlgili kaynaklar
İndirme ve hello çalıştırma [Azure Sanal Makine Hazırlık Değerlendirmesi](https://www.microsoft.com/download/details.aspx?id=40898). Merhaba değerlendirme otomatik olarak şirket içi ortamınız inceleyin ve üzerinde hello göre özelleştirilmiş bir rapor oluşturmak Kılavuzu hello ortamı tooAzure geçirdiğinizde bu konuda toohelp bulundu.

Ayrıca ilk hello öğreticileri, kılavuzları ve aşağıdaki konularda hello kapak videolar gözden geçirmenizi öneririz:

* [Hello Azure Portal Cloud-Only sanal ağ yapılandırma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [Siteden siteye VPN hello Azure Portal yapılandırma](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Bir Azure sanal ağ üzerinde yeni bir Active Directory ormanı yüklemek](active-directory-new-forest-virtual-machine.md)
* [Azure üzerinde Active Directory etki alanı Denetleyicisi'nin çoğaltmasını yükleme](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure BT Uzmanı Iaas: (01) sanal makine temelleri](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure BT Uzmanı Iaas: oluşturma (05) sanal ağlar ve şirket içi bağlantılar](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>Giriş
Hello Azure sanal makinelerde Windows Server Active Directory dağıtmak için temel gereksinimler çok az farklılıklar şirket içi sanal makinelerin (ve toosome ölçüde, fiziksel makineler,) dağıtılması nedeniyle. Örneğin, hello Azure sanal makinelerde dağıtmak hello etki alanı denetleyicileri (DC'ler) bir varolan çoğaltmaları varsa Windows Server AD DS, durumunun şirket etki alanında/ormanda şirket içi ve ardından hello Azure dağıtımı büyük ölçüde kabul hello aynı şekilde diğer herhangi bir ek Windows Server Active Directory site davranır. Diğer bir deyişle, alt ağlar oluşturulmuş bir site, Windows Server AD DS tanımlanmalıdır, hello alt ağlar toothat site bağlı ve uygun site bağlantıları kullanarak tooother siteler bağlı. Ancak, ortak tooall Azure olan bazı farklar vardır dağıtımları ve bazıları according toohello belirli dağıtım senaryosu farklılık gösterir. İki temel farklar aşağıda özetlenen:

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>Azure sanal makine bağlantısı toohello şirket içi kurumsal ağ gerekebilir.
Azure sanal geri tooan şirket içi kurumsal ağ gerektiren bir site siteye içeren Azure sanal ağı veya site noktası sanal özel ağ (VPN) makineler bağlanma bileşeni mümkün tooseamlessly bağlanmak Azure sanal makineleri ve Şirket içi makineler. Bu VPN bileşen ayrıca şirket içi etki alanı üyesi bilgisayarlar tooaccess, etki alanı denetleyicilerini özel olarak Azure sanal makinelerinde barındırılan bir Windows Server Active Directory etki alanı sağlayabilir. Önemli toonote ancak olduğundan, Merhaba, VPN başarısız, kimlik doğrulaması ve Windows Server Active Directory bağımlı diğer işlemleri de başarısız olacak. Kullanıcıların mevcut önbelleğe alınmış kimlik bilgilerini, tüm-eşler kullanarak mümkün toosign olabilir ya da toobe verilen veya eski duruma gelmiş henüz hangi biletleri için istemci-sunucu kimlik doğrulama girişimlerini sahip başarısız olur.

Bkz: [sanal ağ](http://azure.microsoft.com/documentation/services/virtual-network/) video tanıtımı ve de dahil olmak üzere adım adım öğreticiler listesi için [hello Azure portalında bir siteden siteye VPN yapılandırma](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Ayrıca, Windows Server Active Directory ile şirket içi ağ bağlantısına sahip olmayan bir Azure sanal ağı dağıtabilir. Bu konudaki Hello yönergeleri, ancak, IP adresi, önemli tooWindows sunucu özelliklerini sağladığından, Azure sanal ağı kullanılan varsayalım.
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>Statik IP adreslerini Azure PowerShell ile yapılandırılması gerekir.
Dinamik adresleri varsayılan olarak ayrılan ancak hello kümesi AzureStaticVNetIP cmdlet tooassign statik bir IP adresi kullanın. Hizmet onarma ve VM kapatma/restart aracılığıyla kalıcı statik bir IP adresi ayarlar. Daha fazla bilgi için bkz: [sanal makineler için statik iç IP adresi](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/).

## <a name="BKMK_Glossary"></a>Terimleri ve tanımları
Merhaba, bu makaledeki başvuran çeşitli Azure teknolojileri koşullarına kapsamlı olmayan listesi aşağıdadır.

* **Azure sanal makineleri**: Geleneksel neredeyse tüm çalışan toodeploy Vm'leri müşterilerin sağlayan Azure Iaas Sunumda hello şirket içi sunucu iş yükü.
* **Azure sanal ağı**: oluşturabilir ve Azure sanal ağları yönetin ve bunları güvenli bir şekilde bağlayabilirsiniz müşteriler sağlayan Azure hizmetinde tootheir kendi ağ hello şirket içi ağ altyapısı sanal özel ağ (VPN) kullanarak.
* **Sanal IP adresi**: bir internet'e yönelik IP adresi başka bir deyişle değil ilişkili tooa belirli bilgisayar veya ağ arabirim kartı. Bulut hizmetleri yeniden yönlendirilen tooan Azure VM olan ağ trafiğini almak için bir sanal IP adresi atanır. Bir sanal IP adresi, bir veya daha fazla Azure sanal makineler içeren bir bulut-hizmeti özelliğidir. Ayrıca bir Azure sanal ağı bir veya daha fazla bulut hizmeti içerebileceğini unutmayın. Sanal IP adresleri yerel Yük Dengeleme yetenekleri sağlar.
* **Dinamik IP adresi**: Bu, yalnızca dahili kullanım içindir hello IP adresidir. Bu bir statik IP adresi olarak (Merhaba kümesi AzureStaticVNetIP cmdlet'ini kullanarak) hello DC/DNS sunucusu rolleri barındıran sanal makineleri için yapılandırılması gerekir.
* **Hizmet düzeltme**: içinde Azure otomatik olarak döndüren hizmet tooa çalışan durum yeniden hello hizmet algılandıktan sonra hello işlemi başarısız oldu. Düzeltme hizmet kullanılabilirliğini ve esnekliğini destekleyen Azure hello yönlerini biridir. Olası olsa da, bir VM üzerinde çalışan bir DC için olay iyileştirme hizmet aşağıdaki hello sonuç benzer tooan planlanmamış yeniden başlatma, ancak birkaç yan etkileri var:
  
  * Merhaba VM sanal ağ bağdaştırıcısı Hello değiştirir
  * Merhaba hello sanal ağ bağdaştırıcısının MAC adresini değiştirir
  * Merhaba hello VM işlemci/CPU Kimliğini değiştirir
  * Merhaba hello sanal ağ bağdaştırıcısının IP yapılandırması hello VM ekli tooa sanal ağ ve hello VM'ın IP adresi statik sürece değiştirmez.
  
  Bu davranışların hiçbiri hiçbir bağımlılık hello MAC adresi veya işlemci/CPU Kimliği olmadığı ve Azure ile ilgili tüm Windows Server Active Directory dağıtımlarında toobe yukarıda açıklandığı şekilde bir Azure sanal ağ üzerinde çalıştırmak için önerilen için Windows Server Active Directory etkiler .

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>Güvenli toovirtualize Windows Server Active Directory etki alanı denetleyicileri mi?
Azure sanal makinelerde Windows Server Active Directory DCs dağıtmaya DC'leri şirket içi bir sanal makinede çalışan olarak aynı yönergeleri konu toohello olduğu. Yedekleme ve geri yükleme DC'ler için yönergeleri takip sürece sanallaştırılmış DC'ler çalıştıran güvenli bir uygulamadır. Kısıtlamaları ve sanallaştırılmış DC'ler çalıştırmak için yönergeleri hakkında daha fazla bilgi için bkz: [Hyper-v çalıştıran etki alanı denetleyicileri](https://technet.microsoft.com/library/dd363553).

Hiper yöneticilere sağlamak veya Windows Server Active Directory dahil olmak üzere birçok dağıtılmış sistemler için sorunlara neden olabilecek teknolojiler trivialize. Örneğin, bir fiziksel sunucuda bir disk kopyalama veya desteklenmeyen yöntemleri tooroll geri hello SANs ve benzeri kullanarak da dahil, bir sunucu durumunu kullanabilirsiniz ancak, bir fiziksel sunucuda bunu bir hiper yönetici, bir sanal makine anlık görüntü geri daha çok daha zordur. Azure hello aynı sonuçlanabilir işlevselliği sunar istenmeyen koşulu. Örneğin, DC'lerin VHD dosyalarını benzer durum toousing anlık görüntü geri yükleme özellikler bunları geri sağladığından düzenli yedeklemeler gerçekleştirmek yerine kopyalamanız gerekir değil.

Bu tür düzeyine toopermanently divergent durumları arasında DC'leri açabilir USN balonları tanıtır. Sorunları gibi neden olabilir:

* Kalan nesneler
* Tutarsız parolaları
* Tutarsız öznitelik değerleri
* Merhaba şema yöneticisini geri alınması durumunda şema uyuşmazlığı

DC'lerin nasıl etkilediği hakkında daha fazla bilgi için bkz: [USN ve USN geri alma](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback).

Windows Server 2012 ile başlayan [ek güvenlik önlemleri tooAD DS yerleşik](https://technet.microsoft.com/library/hh831734.aspx). Hello temel hiper yönetici platformunun VM-Generationıd'yi destekleyen sürece bu korumalar, sanallaştırılmış etki alanı denetleyicileri hello daha önce bahsedilen sorunlara karşı korunmasına yardımcı olmak. Azure, Windows Server 2012 ya da daha sonra Azure sanal makineleri çalıştıran etki alanı denetleyicileri hello ek güvenlik önlemleri sahip VM-Generationıd'yi destekleyen.

> [!NOTE]
> Kapatılır ve hello yerine hello konuk işletim sistemi içinde Azure'da hello etki alanı denetleyicisi rolünü çalıştıran bir VM yeniden **Kapat** hello Azure Portalı hakkında seçeneği. Bugün, bir VM aşağı hello portal tooshut kullanarak serbest hello VM toobe neden olur. Deallocated VM ücretlerinin yansıtılmasını değil hello avantajına sahiptir, ancak bir DC için istenmeyen olduğu da hello VM-Generationıd, sıfırlar. Merhaba VM-Generationıd sıfırladığınızda hello Invocationıd hello AD DS veritabanının da sıfırlanır, hello RID havuzu atılır ve SYSVOL'ü yetkisiz olarak işaretlenmiş. Daha fazla bilgi için bkz: [giriş tooActive Directory etki alanı Hizmetleri (AD DS) sanallaştırma](https://technet.microsoft.com/library/hh831734.aspx) ve [güvenli şekilde sanallaştırılmasını DFSR](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx).
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>Neden Azure sanal makineler üzerinde Windows Server AD DS dağıtma?
Çoğu Windows Server AD DS dağıtım senaryoları dağıtım Azure Vm'lerinde olarak uymaktadır. Örneğin, şirket tooauthenticate kullanıcılar Asya'da uzak bir konumdaki gereken Avrupa'da olduğunu varsayalım. Merhaba şirket daha önce Windows Server Active Directory DC'leri Asya'da maliyet toohello toodeploy dağıtılmamış bunları ve sınırlı uzmanlık toomanage hello sunucuları dağıtım sonrası. Sonuç olarak, kimlik doğrulama isteklerini Asya Avrupa'da DC'ler tarafından yetersiz sonuçlarıyla sunulur. Bu durumda, bir DC hello Asya'da Azure veri merkezi içinde çalıştırılması gereken belirtilen bir VM üzerinde dağıtabilirsiniz. Bu DC tooan toohello uzaktaki kimlik doğrulama performansını artırır doğrudan bağlı Azure sanal ağı ekleniyor.

Azure ayrıca bir yedek toootherwise maliyetli olağanüstü durum kurtarma (DR) siteler olarak çok uygundur. Merhaba nispeten düşük az sayıda etki alanı denetleyicileri ve Azure üzerinde tek bir sanal ağa barındırma maliyetli çekici alternatif temsil eder.

Son olarak, bir ağ uygulaması, Windows Server Active Directory gerektiriyor, ancak şirket içi ağ veya şirket Windows Server Active Directory hello hello üzerinde hiçbir bağımlılık içeriyor SharePoint gibi Azure üzerinde toodeploy isteyebilirsiniz. Bu durumda, ayrı bir ormanda Azure toomeet hello SharePoint üzerinde dağıtma sunucunun gereksinimleri en iyi. Yeniden bağlantı toohello şirket içi ağ ve kurumsal Active Directory'ye hello gerektiren ağ uygulamaları dağıtma de desteklenir.

> [!NOTE]
> Bir katman 3 bağlantısı sağlar olduğundan, bir Azure sanal ağı ve bir şirket içi ağ arasında bağlantı Azure sanal makineleri Azure üzerinde çalışan şirket içi tooleverage DC'leri çalıştıran üye sunucuları da etkinleştirebilirsiniz sağlar VPN bileşeni hello sanal ağ. Ancak hello VPN kullanılamıyorsa, arasındaki iletişimi bilgisayarların şirket içi ve Azure tabanlı etki alanı denetleyicileri, kimlik doğrulama ve diğer çeşitli hatalar çalışmayacaktır.  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>Arasında veya şirket içinde Azure sanal makineler üzerinde Windows Server Active Directory etki alanı denetleyicileri dağıtma çelişir
* Tek bir VM'ye birden fazla içerir hiçbir Windows Server Active Directory dağıtım senaryosu için gerekli toouse bir Azure sanal ağ IP adresi tutarlılığını değil. Bu kılavuz DC'leri bir Azure sanal ağ üzerinde çalıştırıyorsanız varsaydığını unutmayın.
* İle şirket içi DC'leri gibi statik IP adresleri önerilir. Statik bir IP adresi yalnızca Azure PowerShell kullanarak yapılandırılabilir. Bkz: [VM'ler için statik iç IP adresi](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) daha fazla ayrıntı için. İzleme sistemleri ya da statik IP adresi yapılandırması hello konuk işletim sistemi içinde denetle diğer çözümleri varsa, aynı statik IP adresi toohello ağ bağdaştırıcısı özelliklerini hello VM hello atayabilirsiniz. Ancak, hello ağ bağdaştırıcısının hello VM hizmet onarma uğradığında veya hello Portalı'nda kapatılır ve adresini serbest bıraktı atılacak unutmayın. Bu durumda, hello statik IP adresi hello Konuk içinde toobe gerekir sıfırlayın.
* Bir sanal ağ üzerinde sanal makineleri dağıtma kapsıyor (gerektiren bağlantı geri tooan şirket içi ağ veya değil); Merhaba sanal ağ yalnızca bu olanağı sağlar. Azure ile şirket içi ağınız arasında özel iletişim için bir sanal ağ oluşturmanız gerekir. Toodeploy hello şirket içi ağ üzerindeki bir VPN uç noktası gerekir. Merhaba VPN Azure toohello şirket içi ağ bağlantısı açıldı. Daha fazla bilgi için bkz: [Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md) ve [hello Azure portalı bir siteden siteye VPN yapılandırma](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Bir seçenek çok[bir noktadan siteye VPN Oluştur](../vpn-gateway/vpn-gateway-point-to-site-create.md) kullanılabilir tooconnect ayrı Windows tabanlı bilgisayarlar olan doğrudan tooan Azure sanal ağı.
> 
> 

* Olup bir sanal oluşturduğunuz bağımsız olarak değil, Azure ücretleri çıkış trafiği ancak değil giriş için ağ veya. Windows Server Active Directory Tasarım seçeneklerinin çeşitliliğine ne kadar çıkış trafiği bir dağıtım tarafından oluşturulan etkileyebilir. Giden çoğaltmıyor çünkü Örneğin, bir salt okunur etki alanı denetleyicisi dağıtma (RODC) çıkış trafiği sınırlar. Ancak toodeploy RODC gereken hello gerek tooperform karşı ağırlıklı toobe hello karar yazma işlemleri hello DC ve hello karşı [Uyumluluk](https://technet.microsoft.com/library/cc755190) uygulamaları ve Hizmetleri hello sitedeki ile RODC'ler sahip. Trafiği ücretlere hakkında daha fazla bilgi için bkz: [Azure bir bakışta fiyatlandırma](http://azure.microsoft.com/pricing/).
* Azure üzerinde hangi sunucu kaynakları toouse VM'ler şirket içi, RAM, disk boyutu vb. gibi üzerinde tam denetim varken önceden yapılandırılmış sunucu boyutları listesinden seçmeniz gerekir. Bir DC için bir veri diski ekleme toohello işletim sistemi diski sipariş toostore hello Windows Server Active Directory veritabanındaki gerekli değildir.

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>Azure sanal makinelerde Windows Server AD FS dağıtabilir miyim?
Evet, Azure sanal makinelerde Windows Server AD FS dağıtabilir ve hello [AD FS dağıtımı için en iyi uygulamaları](https://technet.microsoft.com/library/dn151324.aspx) şirket içi Uygula eşit olarak Azure üzerinde tooAD FS dağıtımı. Ancak bazı hello en iyi uygulamalar gibi Yük Dengeleme ve yüksek kullanılabilirlik ne AD FS kendisini sunar ötesinde teknolojileri gerektirir. Merhaba temel altyapısı tarafından sağlanmalıdır. Şimdi bu en iyi uygulamaları gözden geçirin ve nasıl bunlar Azure Vm'leri ve Azure sanal ağını kullanarak elde edilebilir bakın.

1. **Güvenlik belirteci hizmeti (STS) sunucuları hiçbir zaman kullanıma doğrudan toohello Internet.**
   
    Merhaba STS güvenlik belirteçleri olduğundan bu önemlidir. AD FS sunucuları ile değerlendirilmelidir gibi sonucu olarak STS sunucuları aynı hello bir etki alanı denetleyicisi olarak koruma düzeyi. Bir STS riske kötü amaçlı kullanıcılar olası seçme toorelying taraf uygulamalarını ve diğer STS sunucuların güvenen kuruluşlardaki talepleri içeren hello özelliği tooissue erişim belirteçleri varsa.
2. **Active Directory etki alanı denetleyicileri aynı ağ hello AD FS sunucuları hello içindeki tüm kullanıcı etki alanları için dağıtın.**
   
    AD FS sunucuları, Active Directory etki alanı Hizmetleri tooauthenticate kullanıcılar kullanın. Aynı ağ hello AD FS sunucuları hello toodeploy etki alanı denetleyicilerinde önerilir. Bu durumda arasında hello bağlantı hello Azure ağ ve şirket içi ağınıza bozuluyor ve daha düşük gecikme süresi ve oturum açma performans artışı sağlar iş sürekliliği sağlar.
3. **Yüksek kullanılabilirlik ve hello Yük Dengeleme için birden çok AD FS düğüme dağıtın.**
   
    Görev açısından kritik güvenlik belirteçleri sıklıkla olmayan gerektiren hello uygulamalar için çoğu durumda, AD FS sağlayan bir uygulama hello başarısızlığını kabul edilebilir değil. Sonuç olarak, ve AD FS artık hello kritik yol tooaccessing iş açısından önemli uygulamaları içinde bulunduğu için başlangıç AD FS hizmeti birden çok AD FS proxy'si ve AD FS sunucuları yüksek oranda kullanılabilir olması gerekir. istekler, yük dengeleyici tooachieve dağıtımını genellikle dağıtılan hello AD FS proxy ve hello AD FS sunucuları önünde.
4. **İnternet erişimi için bir veya daha fazla Web uygulaması proxy'si düğümleri dağıtın.**
   
    Kullanıcıların hello AD FS hizmeti tarafından korunan tooaccess uygulamaları gerektiğinde Merhaba AD FS hizmeti gereksinimlerini toobe kullanılabilir Internet hello. Bu işlem, başlangıç Web uygulaması proxy'si hizmeti dağıtarak sağlanır. Yüksek kullanılabilirlik ve Yük Dengeleme hello amacıyla bir düğümü birden çok toodeploy önemle tavsiye edilir.
5. **Merhaba Web uygulaması proxy'si düğümleri toointernal ağ kaynaklarına erişimi kısıtlayın.**
   
    gelen tooallow dış kullanıcılar tooaccess AD FS Internet Merhaba, toodeploy Web uygulaması proxy'si düğümleri (veya Windows Server'ın önceki sürümlerindeki AD FS Proxy) gerekir. Merhaba düğümleri doğrudan olan Web uygulaması proxy toohello Internet açık. Bunlar gerekli toobe etki alanına katılmış değildir ve bunlar yalnızca toohello AD FS sunucularına TCP bağlantı noktaları 443 ve 80 erişmesi. Bu iletişim tooall önerilir diğer bilgisayarlarda (özellikle de etki alanı denetleyicileri) engellenir.
   
    Genellikle arşivlenmiş şirket içi DMZ yoluyla budur. Güvenlik duvarları işlemi toorestrict hello DMZ toohello şirket içi ağ trafiğinden beyaz liste modu (diğer bir deyişle, hello trafiğinden belirtilen IP adresleri ve bağlantı noktaları izin verilir ve diğer tüm trafik engellendi üzerinden belirtilen yalnızca) kullanın.

Merhaba Aşağıdaki diyagramda geleneksel gösterir şirket içi AD FS dağıtımı.

![Geleneksel şirket içi Active Directory Federasyon Hizmetleri dağıtım diyagramı](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

Ancak, Azure yerel, tam özellikli bir güvenlik duvarı yetenek sağlanmadığı için diğer seçenekleri kullanılan toobe toorestrict trafiği gerekir. Merhaba aşağıdaki tabloda her bir seçeneğin ve avantajları ve dezavantajları gösterilmektedir.

| Seçenek | Avantajı | Olumsuz |
| --- | --- | --- |
| [Azure ağ ACL'leri](../virtual-network/virtual-networks-acl.md) |Daha az maliyetli ve daha basit ilk yapılandırma |Yeni Vm'leri toohello dağıtım eklenirse ek ağ ACL yapılandırması gerekli |
| [Barracuda NG güvenlik duvarı](https://www.barracuda.com/products/ngfirewall) |Beyaz liste modu işlem ve ağ ACL yapılandırma gerektirir |Artan maliyetini ve karmaşıklığını ilk kurulumu |

Merhaba üst düzey adımları toodeploy AD FS bu durumda aşağıdaki gibidir:

1. VPN kullanarak şirket içi bağlantılar ile bir sanal ağ oluşturma veya [ExpressRoute](http://azure.microsoft.com/services/expressroute/).
2. Etki alanı denetleyicilerini hello sanal ağda dağıtın. Bu adım isteğe bağlıdır ancak önerilir.
3. AD FS sunucularında etki alanına katılmış hello sanal ağ dağıtın.
4. Oluşturma bir [iç yük dengeli kümesi](http://azure.microsoft.com/blog/internal-load-balancing/) hello AD FS sunucularını içerir ve hello sanal ağ (dinamik bir IP adresi) içinde yeni bir özel IP adresi kullanır.
   
   1. DNS toocreate hello FQDN toopoint toohello özel (dinamik) IP adresi hello iç yük dengeli küme güncelleştirin.
5. Bir bulut hizmeti (veya ayrı bir sanal ağ) hello için Web uygulaması proxy'si düğümleri oluşturun.
6. Merhaba Web uygulaması proxy'si düğümleri hello bulut hizmetinde veya sanal ağ dağıtma
   
   1. Merhaba Web uygulaması proxy'si düğümleri içeren bir dış yük dengelenmiş küme oluşturun.
   2. Merhaba dış DNS adı (FQDN) toopoint toohello bulut hizmeti ortak IP adresi (Merhaba sanal IP adresi) güncelleştirin.
   3. AD FS proxy toouse hello toohello iç yük dengeli küme hello AD FS sunucuları için karşılık gelen FQDN yapılandırın.
   4. Talep tabanlı web siteleri toouse güncelleştirmek için talep sağlayıcıları dış FQDN hello.
7. Web uygulaması proxy'si tooany makine hello AD FS sanal ağ arasında erişimi kısıtlayın.

toorestrict trafiği hello yük dengeli kümesi hello Azure iç yük dengeleyici için yalnızca trafik tooTCP için 80 ve 443 bağlantı noktalarını yapılandırılmış toobe gerekir ve tüm diğer trafik toohello iç dinamik IP adresini hello yük dengelenmiş küme bırakılır.

![ADFS ağ ACL'leri TCP 443 + 80 diyagramı izin verilir.](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

Yalnızca aşağıdaki kaynaklar hello trafiği toohello AD FS sunucuları yapabilir:

* Hello Azure iç yük dengeleyici.
* Merhaba şirket içi ağ üzerindeki bir yönetici'Hello IP adresi.

> [!WARNING]
> Merhaba tasarım Web uygulaması proxy'si düğümleri hello Azure sanal ağı içinde herhangi bir VM veya hello şirket içi ağ konumlarına ulaşmasını engellemeniz gerekir. Güvenlik duvarı kuralları hello şirket içi Gereci hızlı rota bağlantıları için veya siteden siteye VPN bağlantıları için VPN cihazı hello yapılandırarak yapılabilir.
> 
> 

Bir dezavantajı toothis iç yük dengeleyici, başlangıç AD FS sunucuları ve toohello sanal ağ eklenir başka herhangi bir sunucuya birden çok aygıtlar için hello gerek tooconfigure hello ağ ACL'leri seçeneğidir. Herhangi bir aygıt, ağ ACL'leri toorestrict trafiği tooit yapılandırmadan toohello dağıtım eklenirse, tüm dağıtım hello risk altında olabilir. Merhaba IP adreslerini hello Web uygulaması proxy'si düğümlerinin her zamankinden değiştirirseniz, hello ağ ACL'leri sıfırlamanız gerekir (Merhaba proxy'leri başka bir deyişle, yapılandırılmış toouse olmalıdır [dinamik statik IP adresleri](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)).

![ADFS ağ ACL'leri ile azure'da.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

Başka bir seçenektir toouse hello [Barracuda NG Güvenlik Duvarı'nı](https://www.barracuda.com/products/ngfirewall) AD FS proxy sunucuları ve hello AD FS sunucuları arasındaki Gereci toocontrol trafiği. Bu seçenek, güvenlik ve yüksek kullanılabilirlik için en iyi yöntemlerle uyumlu ve daha az yönetim hello ilk Kurulumdan sonra hello Barracuda NG güvenlik duvarı gerecini bir beyaz liste modu, güvenlik duvarı yönetimi sağlar ve yüklü olması gerektiğinden gerektirir doğrudan bir Azure sanal ağ üzerinde. Yeni bir sunucu toohello dağıtım eklenen her zaman hello gerek tooconfigure ağ ACL'leri ortadan kaldırır. Ancak bu seçenek ilk dağıtım karmaşıklığı ve maliyeti ekler.

Bu durumda, iki sanal ağ bir yerine dağıtılır. Bunları VNet1 ve VNet2 arayacağız. VNet1 hello proxy'leri ve hello Sts'ler ve hello ağ bağlantısı geri toohello kurumsal ağ vnet2'yi içerir. VNet1 bu nedenle özelliği fiziksel olarak (neredeyse barındırabilir) vnet2'yi ve, sırasıyla hello Kurumsal ağdan yalıtılmış. VNet1 sonra bağlı tooVNet2 kullanarak aktarım bağımsız ağ mimarisi (TINA) olarak bilinen özel bir tünel oluşturma teknolojisi. Merhaba TINA tünel olduğunda hello sanal ağların Barracuda NG Güvenlik Duvarı'nı kullanarak bağlı tooeach — her hello sanal ağların bir Barracuda.  Yüksek kullanılabilirlik için her sanal ağ üzerindeki iki Barracudas dağıtmanız önerilir; bir etkin, diğer pasif hello. Bunlar bize toomimic hello işlem içi geleneksel DMZ, Azure'da izin veren saldırısından son derece Zengin özellikleri sunar.

![Azure üzerinde güvenlik duvarı sahip ADFS.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

Daha fazla bilgi için bkz: [AD FS: Talep kullanan şirket içi ön uç uygulamasını toohello Internet genişletmek](#BKMK_CloudOnlyFed).

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>Office 365 SSO tek başına Hello hedef ise, bir alternatif tooAD FS dağıtımı
Amacınız yalnızca tooenable oturum açma Office 365 için ise başka bir alternatif toodeploying AD FS değerlerinin yoktur. Bu durumda, yalnızca DirSync Parola Eşitleme ile şirket içi dağıtabilir ve elde bu yaklaşım, AD FS veya Azure gerektirmediği için aynı sonuç ile en az dağıtım karmaşıklığını hello.

Merhaba aşağıdaki tabloda hello oturum açma işlemleri ile ve AD FS dağıtma olmadan nasıl çalıştığı karşılaştırır.

| Office 365 tek AD FS ve DirSync kullanarak oturum | Office 365 aynı oturum DirSync + Parola Eşitleme ile açma |
| --- | --- |
| 1. hello kullanıcı tooa şirket ağında günlüğe kaydeder ve kimliği doğrulanmış tooWindows Server Active Directory olduğu. |1. hello kullanıcı tooa şirket ağında günlüğe kaydeder ve kimliği doğrulanmış tooWindows Server Active Directory olduğu. |
| 2. hello kullanıcı çalıştığında tooaccess Office 365 (ben @contoso.com). |2. hello kullanıcı çalıştığında tooaccess Office 365 (ben @contoso.com). |
| 3. Office 365 hello kullanıcı tooAzure AD yönlendirir. |3. Office 365 hello kullanıcı tooAzure AD yönlendirir. |
| 4. Azure AD hello kullanıcı kimlik doğrulaması yapamaz ve AD FS şirket içi güvenle yok anlar beri hello kullanıcı tooAD FS yönlendirir. |4. Azure AD Kerberos biletleri doğrudan kabul edemez ve hello kullanıcı kimlik bilgilerini girin istekleri için bir güven ilişkisi yok. |
| 5. hello kullanıcı gönderir bir Kerberos toohello AD FS STS bilet. |5. hello kullanıcının girdiği hello aynı şirket içi parola ve Azure AD hello kullanıcı adı ve DirSync tarafından eşitlendiği parola karşı bunları doğrular. |
| 6. AD FS belirteci biçimi/talepler ve hello kullanıcı tooAzure AD yönlendiren Kerberos bileti toohello gerekli hello dönüştürür. |6. Azure AD hello kullanıcı tooOffice 365 yönlendirir. |
| 7. hello kullanıcının kimliğini doğrular, tooAzure AD (başka bir dönüşüm oluşur). |7. hello kullanıcı tooOffice 365 ve OWA hello Azure AD belirteci kullanarak oturum açabilir. |
| 8. Azure AD hello kullanıcı tooOffice 365 yönlendirir. | |
| 9. hello kullanıcı sessizce 365 tooOffice üzerinde imzalanır. | |

Parola Eşitleme senaryosu (AD FS) ile Hello DirSync ile Office 365, çoklu oturum açma "aynı burada"aynı"yalnızca kullanıcıları aynı şirket içi kimlik bilgilerini Office 365 erişirken yeniden girmeniz gerekir anlamına gelir oturum tarafından" değiştirilir. Bu veriler hello kullanıcının tarayıcı toohelp tarafından anımsanabileceğini Not sonraki komut istemlerini azaltın.

### <a name="additional-food-for-thought"></a>Ek Yemek için düşünce
* Bir Azure sanal makinesinde bir AD FS proxy'si dağıtırsanız, bağlantı toohello AD FS sunucuları gereklidir. Şirket içi olmaları durumunda hello siteden siteye VPN bağlantısı ile AD FS sunucularındaki hello sanal ağ tooallow hello Web uygulaması proxy'si düğümleri toocommunicate tarafından sağlanan yararlanan önerilir.
* Bir Azure sanal bir AD FS sunucusuna dağıtırsanız, öznitelik depoları bağlantı tooWindows Server Active Directory etki alanı denetleyicileri, makine ve yapılandırma veritabanları gereklidir ve ayrıca bir ExpressRoute veya siteden siteye VPN bağlantısı gerektirebilir Hello Azure sanal ağ ve hello şirket ağı arasında.
* Ücretler uygulanır tooall trafiği Azure sanal makinelerden (çıkış trafiği). Maliyet hello yönlendirmeli faktörü ise önerilir toodeploy hello Web uygulaması proxy'si hello AD FS sunucuları şirket içi çıkmadan Azure düğümlerine olur. Merhaba AD FS sunucuları da Azure sanal makinelerde dağıtılırsa, ek ücrete tahakkuk tooauthenticate şirket içi kullanıcıları olacaktır. Çıkış trafiği olsun veya olmasın, hello ExpressRoute veya hello VPN siteden siteye bağlantı yaptıran bakılmaksızın bir maliyet oluşturur.
* AD FS sunucuları, yüksek kullanılabilirlik için Dengeleme toouse Azure'nın yerel sunucu yükü karar verirseniz, Yük Dengeleme kullanılan toodetermine hello hello bulut hizmeti içinde hello sanal makinelerin sağlığını olan araştırmalar sağladığını unutmayın. Toohello varsayılan araştırmalar yanıt hello Aracısı Azure sanal makinelerde mevcut olmadığından Azure sanal makineleri (olarak karşılıklı tooweb veya çalışan rolleri) hello durumda özel bir araştırma kullanılması gerekir. Kolaylık olması için özel bir TCP araştırması kullanabilirsiniz; Bu yalnızca bir TCP bağlantısı (TCP Eşitlemeye kesimi gönderilen ve toowith TCP Eşitlemeye ACK kesimi yanıt) başarıyla kurulan toodetermine sanal makine sistem durumu olmasını gerektirir. Sanal makinelerinizi etkin olarak dinleyen bir TCP bağlantı noktası toowhich hello özel araştırma toouse yapılandırabilirsiniz.

> [!NOTE]
> (Örneğin, bağlantı noktası 80 ve 443) Internet toohello paylaşamaz doğrudan aynı bağlantı noktalarını ayarlayın tooexpose hello ihtiyaç makineler aynı bulut hizmetine hello. Bu nedenle, Windows Server AD FS sunucularınızın sipariş tooavoid potansiyel olarak çakışan için bir uygulama için bağlantı noktası koşulları ve Windows Server AD FS arasında bir özel bulut hizmeti oluşturmak önerilir.
> 
> 

## <a name="deployment-scenarios"></a>Dağıtım senaryoları
bölümden Merhaba, dikkate alınması gereken sıradan dağıtım senaryoları toodraw dikkat tooimportant özetlemektedir. Her senaryonun bağlantılar toomore ayrıntılarını hello kararları ve Etkenler tooconsider vardır.

1. [AD DS: Kurumsal ağ bağlantısına yönelik bir gereksinim ile AD DS algılayan bir uygulama dağıtma](#BKMK_CloudOnly)
   
    Örneğin, bir Internet'e yönelik SharePoint hizmeti bir Azure sanal makineye dağıtılır. Merhaba uygulama bağımlılık şirket ağı kaynaklarına sahiptir. Merhaba uygulama Windows Server AD DS gerektirmez, ancak gerektirmez şirket Windows Server AD DS hello.
2. [AD FS: Talep kullanan şirket içi ön uç uygulamasını toohello Internet genişletme](#BKMK_CloudOnlyFed)
   
    Örneğin, başarıyla dağıtılan şirket içi ve şirket kullanıcılar tarafından kullanılan bir talep kullanan uygulama toobecome hello Internet üzerinden erişilebilir gerekir. Merhaba uygulaması hello doğrudan Internet hem kurumsal kimlikleri kullanılarak iş ortakları ve mevcut şirket kullanıcıları tarafından erişilen toobe gerekir.
3. [AD DS: bağlantı toohello şirket ağı gerektiren Windows Server AD DS algılayan bir uygulama dağıtma](#BKMK_HybridExt)
   
    Örneğin, Windows tümleşik kimlik doğrulamasını destekler ve Windows Server AD DS yapılandırma ve kullanıcı profili verilerini depo olarak kullanan LDAP algılayan bir uygulama bir Azure sanal makineye dağıtılır. Kurumsal Windows Server AD DS varolan hello uygulama tooleverage Merhaba tercih edilir ve çoklu oturum açma sağlar. Merhaba uygulaması talep kullanan değil.

### <a name="BKMK_CloudOnly"></a>1. AD DS: Kurumsal ağ bağlantısına yönelik bir gereksinim ile AD DS algılayan bir uygulama dağıtma
![Yalnızca bulutta AD DS dağıtımı](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**Şekil 1**

#### <a name="description"></a>Açıklama
SharePoint bir Azure sanal makinesi üzerinde dağıtılır ve Merhaba uygulaması kurumsal ağ kaynaklarına üzerinde hiçbir bağımlılığı yoktur. Merhaba uygulamanın ancak Windows Server AD DS gerektiren *değil* gerektiren şirket Windows Server AD DS hello. Kullanıcılar ayrıca Azure sanal makinelerde hello bulutta barındırılan hello Windows Server AD DS etki alanına hello uygulaması aracılığıyla kendi kendine sağlanan olduğundan Kerberos ya da federasyon güvenleri gereklidir.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Senaryo konuları ve teknoloji alanları toohello senaryo nasıl Uygula
* [Ağ topolojisi](#BKMK_NetworkTopology): şirket içi bağlantılar (siteden siteye bağlantı olarak da bilinir) olmadan Azure sanal ağı oluşturun.
* [DC dağıtım yapılandırmasını](#BKMK_DeploymentConfig): yeni bir etki alanı denetleyicisi yeni, tek etki alanı, bir Windows Server Active Directory ormanına dağıtın. Bunun yanı sıra hello Windows DNS sunucusu dağıtılmalıdır.
* [Windows Server Active Directory site topolojisi](#BKMK_ADSiteTopology): kullanım hello varsayılan Windows Server Active Directory sitesi (tüm bilgisayarları Default-First-Site-Name olacaktır).
* [IP adresi ve DNS](#BKMK_IPAddressDNS):
  
  * Hello DC için bir statik IP adresi hello kümesi AzureStaticVNetIP Azure PowerShell cmdlet'ini kullanarak ayarlayın.
  * Yükleyin ve azure'da hello etki alanı denetleyicileri Windows Server DNS yapılandırın.
  * Hello adı ve IP adresini hello hello DC ve DNS sunucu rollerini barındırır VM ile Merhaba sanal ağ özelliklerini yapılandırın.
* [Genel katalog](#BKMK_GC): hello hello ormandaki ilk DC bir genel katalog sunucusu olmalıdır. Bir tek etki alanı ormanda herhangi bir ek iş hello DC gelen hello genel katalog gerektirmediğinden ek DC'leri de GC'ler yapılandırılması gerekir.
* [Merhaba Windows Server AD DS veritabanını ve SYSVOL yerleşimini](#BKMK_PlaceDB): sipariş toostore hello Windows Server Active Directory veritabanı, günlükler ve SYSVOL Azure Vm'leri olarak çalışan bir veri diski tooDCs ekleyin.
* [Yedekleme ve geri yükleme](#BKMK_BUR): toostore sistem durumu yedeklemeleri istediğiniz belirler. Gerekirse, başka bir veri diski toohello DC'yi VM toostore yedekleri ekleyin.

### <a name="BKMK_CloudOnlyFed"></a>2 AD FS: Talep kullanan şirket içi ön uç uygulamasını toohello Internet genişletme
![Şirket içi bağlantılar ile Federasyon](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**Şekil 2**

#### <a name="description"></a>Açıklama
Başarıyla dağıtılan şirket içi ve şirket kullanıcılarına gereksinimlerini toobecome doğrudan hello Internet ' erişilebilen tarafından kullanılan bir talep kullanan uygulama. Merhaba uygulama verilerini depolayan bir web ön uç tooa SQL veritabanı olarak görev yapar. Merhaba uygulama tarafından kullanılan hello SQL sunucuları hello şirket ağında da bulunur. Şirket içinde dağıtılabilir tooprovide erişim toohello şirket kullanıcıları, iki Windows Server AD FS Sts'ler ve bir yük dengeleyici silinmiş. Merhaba uygulamayı şimdi ayrıca hello doğrudan Internet hem kurumsal kimlikleri kullanılarak iş ortakları ve mevcut şirket kullanıcıları tarafından erişilen toobe gerekir.

Efor toosimplify ve bu yeni gereksinimi karşılayan hello dağıtım ve yapılandırma gereksinimlerini, iki ek web ön uçlar ve iki belirlenir Windows Server AD FS proxy sunucular, Azure sanal makinelerde yüklü olmalıdır. Tüm dört VM'ler olacaktır doğrudan toohello Internet gösterilir ve Azure sanal ağın siteden siteye VPN özelliği kullanarak bağlantı toohello şirket içi ağ sağlanacaktır.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Senaryo konuları ve teknoloji alanları toohello senaryo nasıl Uygula
* [Ağ topolojisi](#BKMK_NetworkTopology): Azure sanal ağı oluşturmak ve [şirket içi bağlantılar yapılandırmak](../vpn-gateway/vpn-gateway-site-to-site-create.md).
  
  > [!NOTE]
  > Her hello Windows Server AD FS sertifikalarının hello URL hello sertifika şablon içinde tanımlanan ve hello elde edilen sertifikaların Azure üzerinde çalışan Windows Server AD FS hello örnekler tarafından ulaşılabildiğinden emin olun. Bu şirketler arası bağlantı tooparts PKI altyapınızın gerektirebilir. Şirket içi LDAP tabanlı ve özel olarak barındırılan sonra şirket içi bağlantılar Hello CRL'nin uç nokta ise, örnek gerekli olacak için. Bu arzu değilse, bu, CRL hello Internet erişilebilen bir CA tarafından verilen gerekli toouse sertifikalar olabilir.
  > 
  > 
* [Bulut Hizmetleri Yapılandırması](#BKMK_CloudSvcConfig): iki yük dengeli sanal IP adresleri sağlayın iki bulut Hizmetleri sırada olduğundan emin olun. Merhaba ilk bulut hizmetin sanal IP adresine yönlendirilmiş toohello iki Windows Server AD FS proxy 80 ve 443 numaralı bağlantı noktalarını VM'ler olacaktır. Merhaba VM'ler olacaktır Windows Server AD FS proxy toopoint toohello IP adresi hello şirket içi yük-dengeleyicinin ön Windows Server AD FS Sts'ler hello yapılandırılır. Merhaba ikinci bulut hizmetin sanal IP adresine yönlendirilmiş toohello iki VM'ler hello web ön uç 80 ve 443 numaralı bağlantı noktalarını yeniden çalıştırmayı olacaktır. Özel bir araştırma yapılandırmanız tooensure hello yük dengeleyici yalnızca trafik toofunctioning Windows Server AD FS proxy ve web ön uç VM'ler yönlendirir.
* [Federasyon sunucusu yapılandırması](#BKMK_FedSrvConfig): yapılandırma Windows Server AD FS federasyon sunucusu (STS) toogenerate güvenlik belirteçleri hello bulutta oluşturulan hello Windows Server Active Directory ormanı için. Federasyon Talep sağlayıcı güven ilişkileri tooaccept kimliklerden istediğiniz hello farklı iş ortakları ile ayarlamak ve hello farklı uygulamalarla toogenerate belirteçleri istediğiniz bağlı olan taraf güven ilişkilerini yapılandırın.
  
    Windows Server AD FS federasyon dekiler doğrudan Internet bağlantısı yalıtılmış kalırken Çoğu senaryoda, bir Internet'e yönelik kapasite güvenlik amacıyla Windows Server AD FS proxy sunucuları dağıtılır. Dağıtım senaryonuz bağımsız olarak sanal bir IP adresiyle bir genel olarak sunulan IP adresi ve mümkün tooload Bakiye, iki Windows Server AD FS STS örnekleri ya da proxy örnekleri arasında bağlantı noktası sağlayan bulut hizmetiniz yapılandırmanız gerekir.
* [Windows Server AD FS yüksek kullanılabilirlik Yapılandırması](#BKMK_ADFSHighAvail): önerilir toodeploy yük devretme ve Yük Dengeleme için en az iki sunucu ile bir Windows Server AD FS grubunu olduğu. Windows Server AD FS yapılandırma verilerini hello Windows İç Veritabanı (WID) kullanarak tooconsider istediğiniz ve hello iç yük hello grubundaki hello sunucularda Azure toodistribute gelen istekleri yeteneğini Dengeleme kullanın.

Daha fazla bilgi için bkz: Merhaba [AD DS dağıtım kılavuzu](https://technet.microsoft.com/library/cc753963).

### <a name="BKMK_HybridExt"></a>3. AD DS: bağlantı toohello şirket ağı gerektiren Windows Server AD DS algılayan bir uygulama dağıtma
![Şirket içi AD DS dağıtımı](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**Şekil 3**

#### <a name="description"></a>Açıklama
LDAP algılayan bir uygulama, bir Azure sanal makineye dağıtılır. Windows tümleşik kimlik doğrulamasını destekler ve Windows Server AD DS yapılandırma ve kullanıcı profili verilerini depo olarak kullanır. Merhaba hedef için hello uygulama tooleverage hello şirket Windows Server AD DS var olduğundan ve çoklu oturum açma sağlar. Merhaba uygulaması talep kullanan değil. Kullanıcılar ayrıca tooaccess hello uygulamasından doğrudan hello Internet gerekir. toooptimize performans ve maliyet için hello şirket etki alanının parçası olan iki ek etki alanı denetleyicisi Azure'da hello uygulaması yanında dağıtılması belirlenir.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Senaryo konuları ve teknoloji alanları toohello senaryo nasıl Uygula
* [Ağ topolojisi](#BKMK_NetworkTopology): sahip Azure sanal ağı oluşturmak [şirketler arası bağlantı](../vpn-gateway/vpn-gateway-site-to-site-create.md).
* [Yükleme yöntemi](#BKMK_InstallMethod): hello şirket Windows Server Active Directory etki alanından çoğaltma DC'leri dağıtın. Çoğaltma için DC, hello VM üzerinde Windows Server AD DS yükleyebilir ve isteğe bağlı olarak kullan hello yüklemek gelen medya (IFM) özellik tooreduce hello toobe gereken veri miktarı çoğaltılan toohello yeni DC yükleme sırasında. Bir öğretici için bkz: [Azure üzerinde Active Directory etki alanı Denetleyicisi'nin çoğaltmasını yükleme](active-directory-install-replica-active-directory-domain-controller.md). IFM kullansanız bile, sanal DC şirket içi ve Windows Server AD DS yüklemesi sırasında çoğaltmak yerine hello tüm sanal sabit Disk (VHD) toohello bulut taşımak daha verimli toobuild hello olabilir. Güvenliğiniz için kopyalanan tooAzure silindikten sonra hello VHD hello şirket içi ağdan silmeniz önerilir.
* [Windows Server Active Directory site topolojisi](#BKMK_ADSiteTopology): yeni bir Azure site Active Directory Siteleri ve Hizmetleri oluşturun. Windows Server Active Directory alt ağ nesnesini toorepresent hello Azure sanal ağı oluşturun ve hello alt toohello site ekleyin. Windows Server Active Directory trafiğini tooand azure'dan en iyi duruma getirme ve hello yeni Azure site ve hangi hello Azure sanal ağ VPN bitiş noktası sırası toocontrol bulunur hello site içeren yeni bir site bağlantısı oluşturun.
* [IP adresi ve DNS](#BKMK_IPAddressDNS):
  
  * Hello DC için bir statik IP adresi hello kümesi AzureStaticVNetIP Azure PowerShell cmdlet'ini kullanarak ayarlayın.
  * Yükleyin ve azure'da hello etki alanı denetleyicileri Windows Server DNS yapılandırın.
  * Hello adı ve IP adresini hello hello DC ve DNS sunucu rollerini barındırır VM ile Merhaba sanal ağ özelliklerini yapılandırın.
* [Coğrafi olarak dağıtılan DC'leri](#BKMK_DistributedDCs): ek sanal ağlar gerektiği gibi yapılandırın. Active Directory site topolojisi toodifferent Azure karşılık coğrafyalara DC'leri gerektirip gerektirmediğini daha bölgeler istediğiniz toocreate Active Directory Siteleri buna göre.
* [Salt okunur DC'leri](#BKMK_RODC): dağıttığınız RODC hello Azure site içinde gerçekleştirmek için gereksinimlerinize bağlı olarak yazma işlemlerini hello DC ve hello uyumluluğu karşı uygulamaların ve hizmetlerin hello sitesinde RODC'ler sahip. Uygulama uyumluluğu hakkında daha fazla bilgi için bkz: Merhaba [salt okunur etki alanı denetleyicileri uygulama uyumluluk Kılavuzu](https://technet.microsoft.com/library/cc755190).
* [Genel katalog](#BKMK_GC): GC'ler gerekli tooservice oturum açma isteklerini çok etki alanlı ormanda olan. Bir GC hello Azure site içinde değil dağıtırsanız, kimlik doğrulama isteklerini diğer sitelerde sorguları GC'ler neden çıkış trafiği ücrete neden. trafiği toominimize, Active Directory Siteleri ve Hizmetleri Azure site hello için önbelleğe almayı evrensel grup üyeliğini etkinleştirebilirsiniz.
  
    Bir GC dağıtırsanız, site bağlantıları yapılandırmak ve site bağlantı maliyetleri hello GC hello Azure sitesi, kaynak DC olarak tooreplicate gereken diğer GC'ler tarafından tercih edilen olmaması hello aynı kısmi etki alanı bölümleri.
* [Merhaba Windows Server AD DS veritabanını ve SYSVOL yerleşimini](#BKMK_PlaceDB): sipariş toostore hello Windows Server Active Directory veritabanı, günlükler ve SYSVOL Azure Vm'leri üzerinde çalışan bir veri diski tooDCs ekleyin.
* [Yedekleme ve geri yükleme](#BKMK_BUR): toostore sistem durumu yedeklemeleri istediğiniz belirler. Gerekirse, başka bir veri diski toohello DC'yi VM toostore yedekleri ekleyin.

## <a name="deployment-decisions-and-factors"></a>Dağıtım kararlarını ve Etkenler
Bu tablo senaryolar önceki hello etkilendiğini ve bağlantıları toomore ayrıntı aşağıda ile ilgili kararları tooconsider hello hello Windows Server Active Directory teknoloji alanları özetler. Bazı teknoloji alanları geçerli tooevery dağıtım senaryosu olmayabilir ve bazı teknoloji alanları diğer teknolojisi alanlarında daha fazla kritik tooa dağıtım senaryosu olabilir.

Tüm ek çoğaltma oluşturmayacağından Örneğin, bir sanal ağ üzerinde çoğaltma DC dağıtmak ve tek bir etki alanı ormanınız varsa, toodeploy bir genel katalog sunucusu bu durumda seçme kritik toohello dağıtım senaryosu olmayacaktır. gereksinimleri. Üzerinde Hello orman birkaç etki alanı varsa, diğer yandan hello sonra hello karar toodeploy bir genel katalog bir sanal ağın kullanılabilir bant genişliğini, performans, kimlik doğrulama, dizin aramaları ve benzeri etkileyebilir.

| Windows Server Active Directory teknoloji alanı | Kararları | Etkenler |
| --- | --- | --- |
| [Ağ topolojisi](#BKMK_NetworkTopology) |Bir sanal ağ oluşturma? |<li>Gereksinimleri tooaccess Corp kaynakları</li> <li>Kimlik Doğrulaması</li> <li>Hesap yönetimi</li> |
| [DC dağıtım yapılandırması](#BKMK_DeploymentConfig) |<li>Ayrı bir ormanda herhangi bir güveni olmadan dağıtmak?</li> <li>Federasyon ile yeni bir orman dağıtabilir?</li> <li>Windows Server Active Directory orman güveni ile yeni bir orman veya Kerberos dağıtmak?</li> <li>Corp ormanı çoğaltma DC dağıtarak genişletmek?</li> <li>Yeni alt etki alanı veya etki alanı ağacı dağıtarak Corp ormanı genişletmek?</li> |<li>Güvenlik</li> <li>Uyumluluk</li> <li>Maliyet</li> <li>Esneklik ve hataya dayanıklılık</li> <li>Uygulama uyumluluğu</li> |
| [Windows Server Active Directory site topolojisi](#BKMK_ADSiteTopology) |Nasıl, alt ağlar, siteler ve site bağlantıları ile Azure sanal ağ toooptimize trafiği yapılandırmak ve maliyeti en aza indir? |<li>Alt ağ ve site tanımları</li> <li>Site bağlantı özelliklerini ve bildirim değiştirme</li> <li>Çoğaltma sıkıştırma</li> |
| [IP adresi ve DNS](#BKMK_IPAddressDNS) |Nasıl tooconfigure IP adresleri ve ad çözümleme? |<li>Hello kullan hello kümesi AzureStaticVNetIP cmdlet tooassign statik bir IP adresi kullanın</li> <li>Windows Server DNS sunucusu yüklemek ve hello adı ve IP adresini hello hello DC ve DNS sunucu rollerini barındırır VM ile Merhaba sanal ağ özelliklerini yapılandırın</li> |
| [Coğrafi olarak dağıtılan DC'leri](#BKMK_DistributedDCs) |Tooreplicate tooDCs üzerinde ayrı sanal ağlara nasıl? |Active Directory site topolojisi toodifferent Azure karşılık gelen coğrafyalara DC'leri gerektirip gerektirmediğini daha bölgeler istediğiniz toocreate Active Directory Siteleri buna göre. [Sanal ağ toovirtual ağ bağlantısı yapılandırmak](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) tooreplicate ayrı sanal ağlar üzerindeki etki alanı denetleyicileri arasında. |
| [Salt okunur DC'leri](#BKMK_RODC) |Salt okunur veya yazılabilir DC'ler kullanır? |<li>HBI/PII öznitelikleri filtre</li> <li>Filtre gizli</li> <li>Sınır giden trafik</li> |
| [Genel katalog](#BKMK_GC) |Genel katalog yüklensin mi? |<li>Tek etki alanlı orman için tüm DC'leri GC'ler olun</li> <li>Çoklu etki alanı ormanı için GC'ler kimlik doğrulaması için gereklidir</li> |
| [Yükleme yöntemi](#BKMK_InstallMethod) |Nasıl tooinstall DC azure'da? |Ya da: <li>Windows PowerShell veya Dcpromo kullanarak AD DS'yi yükleme</li> <li>VHD'yi bir şirket içi sanal DC taşıyın</li> |
| [Merhaba Windows Server AD DS veritabanını ve SYSVOL yerleşimi](#BKMK_PlaceDB) |Toostore Windows Server AD DS veritabanı günlük burada ve SYSVOL? |Dcpromo.exe varsayılan değerlerini değiştirin. Bu kritik Active Directory dosyalarını *gerekir* yazma önbelleğini uygulayan işletim sistemi disklerinde yerine yerleştirilen Azure veri disklerde. |
| [Yedekleme ve Geri Yükleme](#BKMK_BUR) |Nasıl toosafeguard ve kurtarma verilerini? |Sistem durumu yedeklemeleri oluşturma |
| [Federasyon sunucusu yapılandırma](#BKMK_FedSrvConfig) |<li>Merhaba bulutta Federasyon ile yeni bir orman dağıtabilir?</li> <li>AD FS şirket içi dağıtma ve bir proxy hello bulutta kullanıma?</li> |<li>Güvenlik</li> <li>Uyumluluk</li> <li>Maliyet</li> <li>İş ortakları tarafından erişim tooapplications</li> |
| [Bulut Hizmetleri Yapılandırması](#BKMK_CloudSvcConfig) |Bir bulut hizmeti örtük olarak dağıtılan hello ilk kez bir sanal makine oluşturun. Toodeploy ek bulut Hizmetleri gerekiyor mu? |<li>Bir VM ya da sanal makineleri doğrudan Etkilenme toohello Internet gerektiriyor mu?</li> <li> Merhaba hizmeti yük dengeleyici gerektiriyor mu?</li> |
| [Ortak ve özel IP adresi (sanal IP ve dinamik IP) için Federasyon sunucusu gereksinimleri](#BKMK_FedReqVIPDIP) |<li>Merhaba Windows Server AD FS örneği hello doğrudan Internet sınırına toobe gerekiyor mu?</li> <li>Merhaba buluta dağıtılan hello uygulama kendi Internet'e yönelik IP adresi ve bağlantı noktası gerektiriyor mu?</li> |Dağıtımınızda gerekli her sanal IP adresi için bir bulut hizmeti oluşturun |
| [Windows Server AD FS yüksek kullanılabilirlik yapılandırması](#BKMK_ADFSHighAvail) |<li>Windows Server AD FS sunucu grubumu kaç düğümler?</li> <li>Windows Server AD FS proxy grubumu kaç düğümleri toodeploy?</li> |Dayanıklılık ve hataya dayanıklılık |

### <a name="BKMK_NetworkTopology"></a>Ağ topolojisi
Sipariş toomeet başlangıç IP adresi tutarlılığını ve Windows Server AD DS, DNS gereksinimleri, gerekli toofirst oluşturma bir [Azure sanal ağı](../virtual-network/virtual-networks-overview.md) ve sanal makineleri tooit ekleyin. Kendi oluşturma sırasında Azure sanal saydam bağlayan ağ toooptionally genişletmek olup olmadığını bağlantı tooyour şirket içi Kurumsal tooon içi makineler makineleri karar vermeniz gerekir — geleneksel VPN teknolojilerini kullanarak elde edilir ve VPN bitiş noktası hello hello şirket ağı kenarında gösterilmesine gerektirir. Diğer bir deyişle, hello VPN Azure toohello Kurumsal ağdan değil tam tersini başlatılır.

Ek ücretlere bir sanal ağ tooyour şirket içi ağ tooeach VM uygulamak hello standart ücretler dışında genişletirken geçerli olduğunu unutmayın. Özellikle, CPU süresi hello Azure sanal ağ geçidi için ve hello VPN şirket içi makinelerle iletişim kurar her bir VM tarafından oluşturulan hello çıkış trafiği için ücret vardır. Ağ trafiği ücretlere hakkında daha fazla bilgi için bkz: [Azure bir bakışta fiyatlandırma](http://azure.microsoft.com/pricing/).

### <a name="BKMK_DeploymentConfig"></a>DC dağıtım yapılandırması
hello şekilde hello hizmet için DC hello gereksinimlerine bağlıdır hello yapılandırmak istediğiniz Azure üzerinde toorun. Örneğin, yeni kendi şirket ormandan yalıtılmış bir orman dağıtabileceğinizi, bir, kavram, yeni bir uygulama veya başka bir kısa vadeli projeye test etmek için Dizin Hizmetleri özgü olmayan erişim toointernal şirket kaynaklarına ancak gerektirir.

Bir avantaj olarak DC ile çoğaltmıyor ayrı bir ormanda doğrudan maliyetlerini azaltır, daha az giden ağ trafiğinin hello sistem tarafından kendisine oluşturulan kaynaklanan DC'leri şirket içi. Ağ trafiği ücretlere hakkında daha fazla bilgi için bkz: [Azure bir bakışta fiyatlandırma](http://azure.microsoft.com/pricing/).

Başka bir örnek olarak, bir hizmet için gizlilik gereksinimleri vardır, ancak hello hizmet üzerinde erişim tooyour bağlı varsayalım iç Windows Server Active Directory. Merhaba hizmeti hello bulutta toohost verileri izin verilirse, Azure ile ilgili iç ormanınız için yeni bir alt etki alanı dağıtabilirsiniz. Bu durumda, bir DC hello yeni alt etki alanının (olmadan sipariş toohelp gizlilik endişelere genel katalogda hello) dağıtabilirsiniz. Bir çoğaltma DC dağıtımı ile birlikte bu senaryo, şirket içi DC'leri bağlanabilirlik için bir sanal ağ gerektirir.

Yeni bir orman oluşturursanız, seçin olup olmadığını toouse [Active Directory güvenleri](https://technet.microsoft.com/library/cc771397) veya [federasyon güvenleri](https://technet.microsoft.com/library/dd807036). Uyumluluk, güvenlik, uyumluluk, maliyet ve dayanıklılık tarafından dikte hello gereksinimleri dengeleyin. Örneğin, tootake avantajlarından [seçime bağlı kimlik doğrulaması](https://technet.microsoft.com/library/cc755844) toodeploy Azure üzerinde yeni bir orman seçin ve bir Windows Server Active Directory güveni hello şirket içi orman hello bulut orman arasındaki oluşturmak olabilir. Ancak, Hello uygulama talep kullanan ise, Active Directory orman güvenleri yerine federasyon güvenleri dağıtabilirsiniz. Diğer bir etken Merhaba, şirket içi Windows Server Active Directory toohello bulut genişleterek daha fazla veri tooeither replicate maliyeti olması veya kimlik doğrulama ve sorgu yük sonucunda fazla giden trafik oluşturabilir.

Kullanılabilirlik ve hataya dayanıklılık için gereksinimleri da tercih ettiğiniz etkiler. Merhaba bağlantısı kesilirse, Azure üzerinde yeterli altyapı dağıttığınız sürece Örneğin, bir Kerberos güven veya bir federasyon güveni yararlanan uygulamalar tüm büyük olasılıkla tamamen ayrılır. Çoğaltma DC'leri gibi alternatif dağıtım yapılandırmaları (yazılabilir veya RODC'ler) mümkün tootolerate bağlantı kesintileri olma hello olasılığını artırmak.

### <a name="BKMK_ADSiteTopology"></a>Windows Server Active Directory site topolojisi
Toocorrectly siteler tanımlar ve sipariş toooptimize site bağlantıları trafiği ve maliyeti en aza indir. Siteleri, site bağlantıları ve alt ağları hello çoğaltma topolojisi DC'lerin ve kimlik doğrulama trafiğini hello akışını etkiler. Trafiği ücretlere aşağıdaki hello göz önünde bulundurun ve dağıtmak ve DC'leri dağıtım senaryonuz toohello gereksinimlerine göre yapılandırın:

* Merhaba ağ geçidinin kendisi için saat başına nominal bir ücret yoktur:
  
  * Başlatılan ve uygun gördüğünüz şekilde durduruldu
  * Durmuşsa, Azure Vm'leri hello şirket ağından yalıtılır
* Gelen trafik ücretsizdir
* Giden trafik ücret, çok göre[Azure bir bakışta fiyatlandırma](http://azure.microsoft.com/pricing/). Şirket içi siteler ve hello bulut siteler arasındaki site bağlantısı özellikleri gibi en iyi duruma getirebilirsiniz:
  
  * Birden çok sanal ağlar kullanıyorsanız hello site bağlantıları ve bunların maliyetleri yapılandırmanız uygun şekilde önceliğini azaltarak hello Azure'den Windows Server AD DS tooprevent site üzerinde bir hizmet ücret ödemeden aynı düzeyleri hello sağlayan. Ayrıca, tüm (varsayılan olarak etkindir) bağlantı (BASL) seçeneğinden site hello köprüsü devre dışı bırakma düşünebilirsiniz. Bu sitelere yalnızca doğrudan bağlı başka bir işlemle çoğaltmak sağlar. Geçişli bağlı sitelerdeki DC'leri artık mümkün tooreplicate birbirleriyle doğrudan olmayan, ancak ortak bir site veya siteler arasında çoğaltılması gerekir. Merhaba Ara siteler için herhangi bir nedenle kullanılamaz duruma gelirse, hello siteler arasında bağlantı kullanılabilir olsa bile arasında DC'leri geçişli bağlı sitelerdeki çoğaltmayı gerçekleşmez. Son olarak, geçişli çoğaltma davranışı bölümlerini arzu kalır burada site hello uygun site bağlantıları ve şirket içi, kurumsal ağ alanları gibi siteleri içeren bağlantı köprüleri oluşturun.
  * [Site bağlantı maliyetleri yapılandırma](https://technet.microsoft.com/library/cc794882) uygun şekilde tooavoid istenmeyen trafiği. Örneğin, varsa **deneyin sonraki en yakın siteye** ayarı etkinleştirildiğinde, hello Azure site geri toohello bağlayan hello site bağlantı nesnesinin ilişkili hello maliyet artırarak emin hello sanal ağ siteleri olan değil hello sonraki en yakın olun Kurumsal ağ.
  * Site bağlantısı yapılandırma [aralıkları](https://technet.microsoft.com/library/cc794878) ve [zamanlamaları](https://technet.microsoft.com/library/cc816906) tooconsistency gereksinimleri ve nesne değişikliklerini hızına göre. Çoğaltma zamanlamasını gecikme Toleransı ile hizalar. Yeterli nesne değişim oranı ise azalan hello çoğaltma aralığı maliyetleri kaydedebilmeniz için yalnızca en son durumunu bir değer hello DC'leri çoğaltılır.
* Maliyetleri en aza bir öncelik ise, çoğaltma zamanlanmış ve değişiklik bildirimi etkinleştirilmemiş emin olun. Siteler arasında çoğaltma yapılırken hello varsayılan yapılandırma budur. Bu hello RODC giden değişiklikler çoğaltılmaz olduğundan sanal ağ üzerinde bir RODC dağıtıyorsanız önemli değildir. Ancak yazılabilir DC dağıtırsanız, gereksiz sıklığı ile yapılandırılmış tooreplicate güncelleştirmeleri hello site bağlantısı olmadığından emin olmanız gerekir. Bir genel katalog sunucusu (GC) dağıtırsanız, DC bir sitedeki site bağlantısıyla bağlı bir kaynaktan bir GC içeren her bir site etki alanı bölümlerini çoğaltır veya Azure site içinde GC hello daha düşük maliyetli olan site bağlantıları hello emin olun.
* Olası toofurther hala hello çoğaltma sıkıştırma algoritması değiştirerek siteler arasında çoğaltma tarafından oluşturulan ağ trafiğini azaltabilir. Merhaba sıkıştırma algoritması hello REG_DWORD kayıt defteri girişi HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters\Replicator sıkıştırma algoritması tarafından denetlenir. Merhaba varsayılan değer 3, toohello Xpress sıkıştırma algoritması karşılık gelen olduğu. Hangi değişikliklerin algoritması tooMSZip hello hello değeri too2 değiştirebilirsiniz. Çoğu durumda bu hello sıkıştırma artırır, ancak bunu CPU kullanımı hello gider yapar. Daha fazla bilgi için bkz: [nasıl Active Directory çoğaltma topolojisi works](https://technet.microsoft.com/library/cc755994).

### <a name="BKMK_IPAddressDNS"></a>IP adresi ve DNS
Azure sanal makineler "adreslerini DHCP kiralık" varsayılan olarak ayrılır. Azure sanal ağı dinamik adresler sahip bir sanal makine hello sanal makine hello ömrü boyunca kalıcı hale getirmek için Windows Server AD DS hello gereksinimlerinin karşılandığından.

Sonuç olarak, Azure üzerinde bir dinamik adres kullandığınızda hello hello kira boyunca yönlendirilebilir ve hello kira hello süre eşit toohello ömrü hello bulut hizmeti olduğundan statik IP adresi kullanarak etkin olacaktır.

Ancak, Hello VM kapatma ise hello dinamik adresi serbest bırakıldı. yapabilecekleriniz ayırması Kimden tooprevent hello IP adresi, [kümesi AzureStaticVNetIP tooassign statik bir IP adresi kullanmak](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx).

Ad çözümlemesi için kendi dağıtma (veya var olan yararlanan) bir DNS sunucusu altyapısında; Azure tarafından sağlanan DNS ad çözümleme gereksinimlerine ve Windows Server AD DS Gelişmiş hello karşılamıyor. Örneğin, bunu değil dinamik SRV kayıtlarını desteklemesi ve benzeri. Ad çözümlemesi DC'leri ve etki alanına katılmış istemciler için önemli yapılandırma öğesidir. DC'lerin kaynak kayıtlarını kaydetme ve diğer DC'nin kaynak kayıtları çözme yeteneğinin olması gerekir.
Hataya dayanıklılık ve Performans nedeniyle, bu en iyi tooinstall hello Windows Server DNS hello DC'leri Azure üzerinde çalışan bir hizmettir. Ardından hello adı ve hello DNS sunucusunun IP adresi ile hello Azure sanal ağ özelliklerini yapılandırın. Merhaba sanal ağ üzerindeki diğer VM'ler başlattığınızda, DNS istemci çözümleyici ayarlarına DNS sunucusu hello dinamik IP adresi ayırma bir parçası olarak yapılandırılır.

> [!NOTE]
> Merhaba doğrudan Internet Azure üzerinde barındırılan şirket içi bilgisayarları tooa Windows Server AD DS Active Directory etki alanına katılamıyor. bağlantı noktası gereksinimleri, Active Directory ve hello etki alanına katılma işlemi pratik toodirectly sunmaya hello gerekli bağlantı noktaları oluşturmak için ve etkisi, tüm DC toohello Internet hello.
> 
> 

Sanal makineleri otomatik olarak başlangıç veya bir ad değişikliği olduğunda kendi DNS adını kaydettirin.

Bu örnek ve nasıl tooprovision ilk VM hello ve üzerinde AD DS'yi yüklemek gösteren başka bir örnek hakkında daha fazla bilgi için bkz: [Microsoft Azure üzerinde yeni bir Active Directory ormanı yüklemek](active-directory-new-forest-virtual-machine.md). Windows PowerShell'i kullanma hakkında daha fazla bilgi için bkz: [Azure PowerShell yükleme](/powershell/azureps-cmdlets-docs) ve [Azure Yönetimi cmdlet'leri](/powershell/module/azurerm.compute/#virtual_machines).

### <a name="BKMK_DistributedDCs"></a>Coğrafi olarak dağıtılan DC'leri
Azure farklı sanal ağlar üzerindeki birden çok DC'leri barındırdığında avantajları sağlar:

* Çok siteli hataya dayanıklılık
* Fiziksel olarak yakın toobranch ofisleri (daha düşük gecikme süresi)

Sanal ağlar arasında doğrudan iletişim yapılandırma hakkında daha fazla bilgi için bkz: [sanal ağ toovirtual ağ bağlantısını yapılandır](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

### <a name="BKMK_RODC"></a>Salt okunur DC'leri
Toodeploy okuma olup olmadığını toochoose gereksinim-yalnızca veya yazılabilir DC'leri. Bunları fiziksel denetime sahip olamazsınız; ancak bunların fiziksel güvenlik şube ofisleri gibi risk olduğu konumlarda dağıtılan tasarlanmış toobe RODC'ler olan olduğundan eilimli toodeploy RODC'ler olabilir.

Azure hello fiziksel güvenlik riskini bir şube ofisi mevcut olmayan, ancak sağladıkları hello özellikleri barındırabilir çok farklı nedenlerle oldukça uygun toothese ortamları olduğundan RODC'ler hala toobe daha düşük maliyetli kanıtlamak. Örneğin, giden çoğaltma RODC'ler sahip ve olan mümkün tooselectively doldurmak parolaları (Parolalar). Merhaba dezavantajı üzerinde isteğe bağlı giden trafiği toovalidate bu Sırları hello eksikliği gerektirebilir bunları bir kullanıcı veya bilgisayar kimlik doğrulaması gibi. Ancak gizli seçerek önceden doldurulmaz ve önbelleğe alınmış.

Öznitelik kümesi (SK'lar) hassas verileri toohello RODC içeren öznitelikler filtre eklemek için RODC'ler içinde ve HBI ve PII sorunları çevresinde ek bir avantaj sağlar. Merhaba SK'lar çoğaltılmış tooRODCs olmayan öznitelikleri özelleştirilebilir kümesidir. İzin verilmez veya toostore PII veya Azure üzerinde HBI istemediğiniz durumunda hello SK'lar koruyucu olarak kullanabilirsiniz. [[(Https://technet.microsoft.com/library/cc753459)] ayarlamak RODC filtrelenmiş bir öznitelik. daha fazla bilgi için bkz.

Uygulamaları RODC'ler ile uyumlu olduğundan emin olun toouse planlayın. Çoğu Windows Server Active Directory özellikli uygulamalar da RODC'ler ile çalışır, ancak bazı uygulamalar inefficiently gerçekleştirin veya erişim tooa yoksa başarısız yazılabilir DC. Daha fazla bilgi için bkz: [salt okunur DC'leri uygulama uyumluluk Kılavuzu](https://technet.microsoft.com/library/cc755190).

### <a name="BKMK_GC"></a>Genel katalog
Toochoose gerekip gerekmediği tooinstall bir genel katalog (GC). Tek etki alanlı bir ormanınız tüm DC'leri genel katalog sunucuları olarak yapılandırmanız gerekir. Hiçbir ek çoğaltma trafiğini olacağından maliyetleri artmaz.

Bir çok etki alanlı ormanda GC'ler hello kimlik doğrulama işlemi sırasında gerekli tooexpand evrensel grup üyeliklerini olur. Bir GC dağıtmayın, Azure üzerinde bir DC kimlik doğrulaması iş yükleri hello sanal ağda giden bağlantı kimlik doğrulaması trafiği tooquery GC'ler şirket içi her kimlik doğrulama girişimi sırasında dolaylı olarak oluşturur.

Her etki alanı (bölüm içinde) barındırmak için GC'ler ile ilişkili hello maliyetleri daha az tahmin edilebilir. Merhaba iş yükü Internet'e hizmeti barındıran ve Windows Server AD DS karşı kullanıcıların kimliğini doğrular, hello maliyetleri tamamen öngörülemeyen olabilir. toohelp azaltmak GC sorguları hello bulut site dışında kimlik doğrulama işlemi sırasında yapabilecekleriniz [evrensel grup üyeliğini önbelleğe'almayı etkinleştir](https://technet.microsoft.com/library/cc816928).

### <a name="BKMK_InstallMethod"></a>Yükleme yöntemi
Toochoose nasıl gereksinim hello sanal ağda tooinstall hello DC'leri:

* Yeni DC'leri yükseltin. Daha fazla bilgi için bkz: [bir Azure sanal ağ üzerinde yeni bir Active Directory ormanı yüklemek](active-directory-new-forest-virtual-machine.md).
* Merhaba şirket içi sanal DC toohello bulutunun VHD taşıyın. Bu durumda, bu hello sanal DC ","kopyalanan"ya da"kopyalanan."taşınır" şirket içi sağlamanız gerekir.

Yalnızca Azure sanal makineleri DC'ler için (karşılıklı tooAzure "web" veya "alt" rolü VM'ler) kullanın. Dayanıklı ve dayanıklılık durumunun bir DC için gereklidir. Azure sanal makineleri DC'leri gibi iş yükleri için tasarlanmıştır.

Kullanmayın SYSPREP toodeploy veya DC'leri kopyalama. Hello özelliği tooclone DC'leri yalnızca başında Windows Server 2012 ' dir. kopyalama özelliği hello desteği için VMGenerationID hello temel hiper yöneticide gerektirir. Üçüncü taraf sanallaştırma yazılım satıcıları gibi Hyper-V'de, Windows Server 2012 ve Azure sanal ağlar her ikisi de VMGenerationID, destekler.

### <a name="BKMK_PlaceDB"></a>Merhaba Windows Server AD DS veritabanını ve SYSVOL yerleşimi
Burada toolocate hello Windows Server AD DS veritabanının, günlükler ve SYSVOL'ü seçin. Azure veri disklerde dağıtılmalıdır.

> [!NOTE]
> Azure veri diskleri kısıtlanmış too1 TB içindir.
> 
> 

Veri disk sürücüleri değil önbellek yazma varsayılan yapın. Ekli tooa VM veri disk sürücülerinin yazma önbelleği kullanın. Merhaba hello VM'ın işletim sistemi perspektifinden Hello işlem tamamlanmadan önce yazma-yapar önbelleğe alma emin hello yazma taahhüt toodurable Azure depolama aracılığıyladır. Merhaba gider biraz daha yavaş yazma sırasında dayanıklılık sağlar.

Arka planda yazma disk önbelleği hello DC tarafından yapılan varsayımları geçersiz kılar çünkü bu Windows Server AD DS için önemlidir. Windows Server AD DS toodisable yazma önbelleğini çalışır ancak toohello disk GÇ sistem toohonor bu durumda. Hata toodisable yazma önbelleğini belirli koşullar altında nesneleri ve diğer sorunları kalan içinde kaynaklanan USN geri alma çıkarabilir.

Sanal DC'leri için en iyi uygulama olarak, aşağıdaki hello:

* Merhaba konak önbelleği tercihi hello Azure veri diskte hiçbiri için ayarı. Bu, AD DS işlemleri için yazma önbelleğini sorunları önler.
* Merhaba veritabanı, günlükler ve SYSVOL ya da aynı veri diski veya veri diski ayrı hello üzerinde depolar. Genellikle, ayrı bir disk hello işletim sistemi için kendisini kullanılan hello diskten budur. Merhaba anahtar takeaway bu hello Windows Server AD DS veritabanıdır ve SYSVOL'ü bir Azure işletim sistemi disk türü depolanmadığından gerekir. Varsayılan olarak, hello AD DS yükleme işlemi bu bileşenleri için Azure önerilmez % systemroot % klasörünün yükler.

### <a name="BKMK_BUR"></a>Yedekleme ve geri yükleme
Ne olduğu ve yedekleme ve geri yükleme bir DC için genel desteklenmiyor ve daha belirgin olarak bu bir VM'de çalıştıran farkında olun. Bkz: [yedekleme ve geri yükleme hakkında önemli noktalar sanallaştırılmış DC'ler için](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers).

Sistem durumu yedeklemeleri yalnızca Windows Server AD DS, Windows Server Yedekleme gibi yedekleme gereksinimleri, özellikle farkındadır yedekleme yazılımı kullanarak oluşturun.

Kopyalamayın veya VHD dosyaları DC'lerin düzenli yedeklemeler gerçekleştirmek yerine klonlayın. Bir geri yükleme şimdiye kadar Windows Server 2012 ve desteklenen bir hiper yönetici olmadan kopyalanan ya da kopyalanmış VHD'lerin USN balonları tanıtılacaktır bunları yapmak, gerekli olmalıdır.

### <a name="BKMK_FedSrvConfig"></a>Federasyon sunucusu yapılandırma
Windows Server AD FS federasyon sunucularına (Sts'ler) Hello yapılandırma kısmen olup hello Azure üzerinde toodeploy istediğiniz uygulamaları şirket içi ağınızdaki tooaccess kaynaklara gereksinimlerine göre değişir.

Merhaba uygulamalar aşağıdaki ölçütleri hello karşılıyorsa, şirket içi ağınızdan yalıtım hello uygulamaları dağıtabilirsiniz.

* SAML güvenlik belirteçleri kabul
* Exposable toohello Internet oldukları
* Şirket içi kaynaklara erişim yok

Bu durumda, Windows Server AD FS Sts'ler gibi yapılandırın:

1. Ayrı bir tek etki alanlı ormanda Azure üzerinde yapılandırın.
2. Windows Server AD FS federasyon sunucusu grubu yapılandırarak Federasyon erişimi toohello orman sağlar.
3. Windows Server AD FS (Federasyon sunucusu grubu ve Federasyon sunucusu proxy'si grubu) hello şirket içi ormanda yapılandırın.
4. Merhaba şirket içi ve Windows Server AD FS Azure örnekleri arasında bir federasyon güven ilişkisi oluşturun.

Üzerindeki diğer yandan Merhaba, hello uygulamaları tooon şirket kaynaklarına erişim gerekiyorsa, Windows Server AD FS Azure'da hello uygulaması ile aşağıdaki gibi yapılandırabilirsiniz:

1. Şirket içi ağlar ve Azure arasında bağlantı yapılandırın.
2. Windows Server AD FS federasyon sunucusu grubu hello şirket içi ormanda yapılandırın.
3. Azure üzerinde bir Windows Server AD FS federasyon sunucusu proxy'si grubu yapılandırın.

Bu yapılandırma hello şirket içi kaynakları riskini benzer tooconfiguring Windows Server AD FS uygulamalarla bir çevre ağında azaltma hello avantajına sahiptir.

İşletmeler için işbirliği gerekirse her iki durumda da, güven ilişkileri daha fazla kimlik sağlayıcıları ile kurup olduğunu unutmayın.

### <a name="BKMK_CloudSvcConfig"></a>Bulut Hizmetleri Yapılandırması
Bulut Hizmetleri toohello Internet veya tooexpose bir Internet'e yönelik Yük dengeli doğrudan tooexpose VM istiyorsanız, gerekli olan uygulama. Her bir bulut hizmeti tek bir yapılandırılabilir sanal IP adresi sağladığından, bu mümkündür.

### <a name="BKMK_FedReqVIPDIP"></a>Ortak ve özel IP adresi (sanal IP ve dinamik IP) için Federasyon sunucusu gereksinimleri
Her Azure sanal makine dinamik bir IP adresi alır. Dinamik bir IP adresi özel bir adresi yalnızca Azure içinde erişilebilir değil. Çoğu durumda, ancak bu gerekli tooconfigure, Windows Server AD FS dağıtımları için sanal bir IP adresi olacaktır. Merhaba sanal IP gerekli tooexpose Windows Server AD FS bitiş noktaları toohello Internet olduğu ve Federal iş ortakları ve istemcileri tarafından kimlik doğrulaması ve devam eden yönetimi için kullanılacaktır. Bir sanal IP adresi, bir veya daha fazla Azure sanal makineler içeren bir bulut hizmeti özelliğidir. Azure ve Windows Server AD FS dağıtılan hello talep kullanan uygulamaya Internet'e yönelik ve paylaşımı ortak bağlantı noktaları varsa, her biri kendi sanal bir IP adresi gerektirir ve bu nedenle hello uygulama için gerekli toocreate bir bulut hizmeti olacaktır ve Windows Server AD FS için ikinci.

Hello koşulları sanal IP adresini ve dinamik IP adresi tanımları için bkz: [terimleri ve tanımları](#BKMK_Glossary).

### <a name="BKMK_ADFSHighAvail"></a>Windows Server AD FS yüksek kullanılabilirlik yapılandırması
Olası toodeploy tek başına Windows Server AD FS Federasyon Hizmetleri olmakla birlikte, olan AD FS STS ve üretim ortamları için proxy'leri için en az iki düğüme sahip bir gruba toodeploy önerilir.

Bkz: [AD FS 2.0 dağıtım topolojisi hakkında önemli noktalar](https://technet.microsoft.com/library/gg982489) hello içinde [AD FS 2.0 Tasarım Kılavuzu](https://technet.microsoft.com/library/dd807036) hangi dağıtım yapılandırmasını seçenekleri en iyi toodecide, belirli gereksinimlerinize uygun şekilde ayarlayabilir.

> [!NOTE]
> Sipariş tooget Yük Dengeleme hello hello Windows Server AD FS grubunun tüm üyeleri Azure, Windows Server AD FS bitiş noktası yapılandırmak için aynı bulut hizmeti ve hello Yük Dengeleme Azure kapasitesini (varsayılan 80) HTTP ve HTTPS bağlantı noktası (varsayılan 443) için kullanın. Daha fazla bilgi için bkz: [Azure yük dengeleyici araştırmasını](https://msdn.microsoft.com/library/azure/jj151530).
> Windows Server Ağ Yükü Dengeleme (NLB), Azure üzerinde desteklenmiyor.
> 
> 

