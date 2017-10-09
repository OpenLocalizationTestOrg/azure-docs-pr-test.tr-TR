---
title: "aaaGetting başlatılan ile Microsoft Azure güvenliği | Microsoft Docs"
description: "Bu makalede, Microsoft Azure güvenlik özellikleri ve genel konular varlıklar tooa bulut sağlayıcılarına geçişini kuruluşlar için genel bakış sağlar."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>Microsoft Azure’daki güvenlik özellikleriyle çalışmaya başlama
Derleme ya da BT varlıklar tooa bulut sağlayıcısı geçirmek hello Hizmetleri ve bulut tabanlı varlıklarınızın toomanage hello güvenlik sağladıkları hello denetimleri ile veri ve uygulamaları, bir kuruluşun yeteneklerini tooprotect üzerinde bağlı.

Azure'nın altyapı hello tesis tooapplications aynı anda milyonlarca müşteri barındırmak için gelen tasarlanmıştır ve güvenlik gereksinimlerine bağlı işletmeler karşılayabilecek güvenilir bir temel sağlar. Ayrıca, Azure, çok çeşitli yapılandırılabilir güvenlik seçenekleri ve hello özelliği toocontrol sağlar bunları böylece güvenlik toomeet hello benzersiz gereksinimlerini dağıtımlarınızı özelleştirebilirsiniz.

Azure güvenliğiyle ilgili bu genel bakış makalesinde şu konuları inceleyeceğiz:

* Azure hizmetlerini ve özellikleri toohelp kullanabilirsiniz, hizmetleri ve Azure içindeki verilerinizi güvenli hale getirin.
* Microsoft güvenli hale getirdiği nasıl hello Azure altyapı toohelp verileriniz ve uygulamalarınız koruyun.

## <a name="identity-and-access-management"></a>Kimlik ve erişim yönetimi
Erişim tooIT altyapısını, veri ve uygulamaları denetleme önemlidir. Microsoft Azure, çok sayıda standartları ve API'ler için Azure Active Directory (Azure AD), Azure Storage ve destek gibi hizmetleri tarafından bu özellikleri sunar.

[Azure AD](../active-directory/active-directory-whatis.md) bir kimlik deposu ve kimlik doğrulama, yetkilendirme ve erişim denetimi kuruluşun kullanıcıları, grupları sağlayan ve nesneleri altyapısı. Azure AD, geliştiricilerin kendi uygulamalarında etkili şekilde toointegrate Kimlik Yönetimi de sunar. Endüstri standardı protokoller gibi [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0), [WS-Federasyon](https://msdn.microsoft.com/library/bb498017.aspx), ve [Openıd Connect](http://openid.net/connect/) .NET, Java, Node.js ve PHP gibi platformlarda oturum açma olası olun.

Merhaba REST tabanlı grafik API'si geliştiriciler dizininden tooread ve yazma toohello herhangi bir platform sağlar. Desteği aracılığıyla [OAuth 2.0](http://oauth.net/2/), geliştiricilerin mobil oluşturabilir ve Microsoft ve üçüncü taraf tümleştirme web uygulamaları API'leri web ve kendi güvenli web API oluşturma. .Net, Windows Mağazası, iOS ve Android’e yönelik mevcut açık kaynak istemci kitaplıklarına ek olarak yeni kitaplıklar da geliştirilmektedir.

### <a name="how-azure-enables-identity-and-access-management"></a>Azure’da kimlik ve erişim yönetimini etkinleştirme
Azure AD kuruluşunuz için tek başına bulut dizini olarak veya mevcut şirket içi Active Directory ortamınızla tümleşik bir çözüm olarak kullanılabilir. Tümleştirme özelliklerinden bazıları dizin eşitleme ve çoklu oturum açma (SSO) hizmetleridir. Bunlar, mevcut şirket içi kimliklerinizi hello ulaşabileceği hello buluta genişletmek ve hello yönetici ve kullanıcı deneyimini geliştirmek.

Diğer kimlik ve erişim yönetimi özelliklerinden bazıları şunlardır:

* Azure AD etkinleştirir [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) tooSaaS uygulamaları burada barındırılır. Bazı uygulamalar Azure AD federasyonu kullanırken diğerleri parola SSO hizmetinden yararlanır. Federasyon uygulamaları kullanıcı hazırlama ve parola kasası desteği de sunabilir.
* Erişim toodata [Azure Storage](https://azure.microsoft.com/services/storage/) kimlik doğrulaması denetlenir. Her Depolama hesabı bir birincil anahtara sahip ([depolama hesabı anahtarı](https://msdn.microsoft.com/library/azure/ee460785.aspx), veya SAK) ve ikincil bir gizli anahtar (Merhaba paylaşılan erişim imzası veya SAS).
* Azure AD kimlik Federasyon üzerinden bir hizmet olarak kullanarak sağlar [Active Directory Federasyon Hizmetleri](../active-directory/fundamentals-identity.md), eşitleme ve çoğaltma ile şirket içi dizinleri.
* [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md) bir mobil uygulama, telefon araması veya kısa mesaj kullanarak kullanıcıların tooverify oturum açma işlemleri gerektiren hello çok faktörlü kimlik doğrulama hizmetidir. Hello Azure multi-Factor Authentication sunucusu ile ve özel uygulamalar ve dizinler hello SDK kullanarak Azure AD toohelp güvenli şirket içi kaynaklar ile kullanılabilir.
* [Azure AD etki alanı Hizmetleri](https://azure.microsoft.com/services/active-directory-ds/) , etki alanı denetleyicilerini dağıtmaya olmadan Azure sanal makineleri tooa etki alanına olanak tanır. Toothese sanal makinelerinizde Kurumsal Active Directory kimlik bilgilerinizle oturum açın ve etki alanına katılmış sanal makineler, Azure virtual machines tüm Grup İlkesi tooenforce güvenlik temelleri kullanarak yönetebilirsiniz.
* [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) toohundreds kimlikleri milyonlarca ölçeklendirilebilen bir yüksek oranda kullanılabilir kimlik genel yönetim hizmeti tüketiciye yönelik uygulamalar için sağlar. Bu hizmet mobil platformlar ve web platformlarıyla tümleştirilebilir. Tüketicileriniz, var olan sosyal hesaplarını kullanarak veya yeni kimlik bilgileri oluşturma uygulamalarınızı özelleştirilebilir deneyimler aracılığıyla tooall içinde imzalayabilirsiniz.

## <a name="data-access-control-and-encryption"></a>Veri erişim denetimi ve şifreleme
Microsoft, görevlerin ayrılmasını ayrımı hello ilkeleri uygular ve [en az ayrıcalık](https://en.wikipedia.org/wiki/Principle_of_least_privilege) Azure işlemleri boyunca. Erişim toodata Azure destek personeli tarafından denetlenen ve günlüğe kaydedilen bir "tam zamanında" temelinde hello katılım tamamlandıktan sonra sonra verilen iptal ve açık izninizi gerektirir.

Azure aktarımda veya durağan verilerin korunması için birden çok yetenekleri de sağlar. Bu veri, dosyaları, uygulamaları, hizmetleri, iletişim ve sürücüler için şifreleme içerir. Azure'da yerleştirme önce bilgilerini şifrelemek ve ayrıca anahtarları, şirket içi veri merkezleri içinde depolar.

![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Azure şifreleme teknolojileri
Kullanarak yönetim erişimi tooyour abonelik ortamda ayrıntıları toplayabilirsiniz [Azure AD raporlama](../active-directory/active-directory-reporting-audit-events.md). Yapılandırabileceğiniz [BitLocker Sürücü Şifrelemesi](https://technet.microsoft.com/library/cc732774.aspx) Azure gizli bilgileri içeren VHD'lerde.

Verilerinizin güvenliğini tookeep yardımcı olacak Azure diğer özellikleri içerir:

* Uygulama geliştiriciler kullanabilir, Azure'da hello Windows kullanarak dağıtın hello uygulamalara şifreleme [CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx) ve .NET Framework.
* Tamamen Azure Blob Depolama için istemci tarafı şifreleme ile Merhaba anahtarları denetler. Merhaba depolama hizmeti hiçbir zaman hello anahtarları görür ve hello verilerin şifresini çözmek yetersiz.
* [Azure Rights Management (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (Merhaba ile [RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) dosya ve veri düzeyi şifreleme ve veri sızıntısı önleme ilke tabanlı erişim yönetimi üzerinden sağlar.
* Azure destekler [tablo ve sütun düzeyi şifreleme (TDE/Temizle)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx) SQL Server sanal makineleri ve onu destekleyen üçüncü taraf Anahtar Yönetimi sunucuları veri merkezlerinde şirket.
* Depolama hesabı anahtarları, paylaşılan erişim imzaları, yönetim sertifikaları ve diğer anahtarlar benzersiz tooeach Azure Kiracı verilebilir.
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx) karma depolama tooAzure depolama karşıya yüklemeden önce bir 128-bit ortak/özel anahtar çifti aracılığıyla verileri şifreler.
* Azure destekler ve SSL/TLS, IPSec ve AES, hello veri türleri, kapsayıcıları ve taşımaları bağlı olarak dahil olmak üzere çok sayıda şifreleme mekanizmaları kullanır.

## <a name="virtualization"></a>Sanallaştırma
Hello Azure platformu, sanallaştırılmış bir ortam kullanır. Kullanıcı örnekleri çalıştırmak tek başına sanal makineler erişim tooa fiziksel ana bilgisayar sunucunuz yoksa ve fiziksel kullanarak bu yalıtım zorlanan [işlemci (halka-0/halkası-3) ayrıcalık düzeylerini](https://en.wikipedia.org/wiki/Protection_ring).

Halka 0 hello en ayrıcalıklı ve 3 hello az olmasıdır. daha düşük ayrıcalıklı halkası 1'de Hello konuk işletim sistemi çalışır ve en az ayrıcalıklı Halka 3 çalışan uygulamaların hello. Bu sanallaştırma fiziksel kaynakların, konuk işletim sistemi ve hiper yönetici, ek güvenlik ayrımı hello iki arasında sonuçta arasında tooa açıkça birbirinden yol açar.

Hello Azure hiper yönetici mikro çekirdek gibi davranır ve tüm donanım erişim isteklerini işlemek için konuk sanal makineleri toohello ana bilgisayardan VMBus adında bir paylaşılan bellek arabirimi kullanarak geçirir. Bu, kullanıcıların ham okuma/yazma/yürütme erişim toohello sistem elde etmesini engeller ve sistem kaynaklarını paylaşımı hello riskini azaltır.

![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>Azure’da sanallaştırma uygulamaları
Azure hello hiper yöneticide uygulanabilir ve bir yapı denetleyicisi aracısı tarafından yapılandırılan bir hiper yönetici Güvenlik Duvarı (paket filtresi) kullanır. Bu bileşen, kiracıların yetkisiz erişimden korunmasına yardımcı olur. Varsayılan olarak, tüm trafiği, bir sanal makine oluşturulduğunda ve ardından hello doku Denetleyicisi aracı hello paket filtre tooadd yapılandırır engellenir *kuralları ve özel durumları* tooallow yetkili trafiği.

Burada programlanan iki kural kategorisi vardır:

* **Makine yapılandırma veya altyapı kuralları**: varsayılan olarak, tüm iletişimin engellenir. Var. özel durumları tooallow olan bir sanal makine toosend ve DHCP ve DNS trafiği alabilir. Sanal makineler, aynı zamanda toohello "Genel" Internet ve gönderme trafiği tooother içindeki sanal makineleri hello küme ve hello işletim sistemi Etkinleştirme sunucusu trafik gönderebilir. izin verilen giden hedefleri Hello sanal makineler listesi Azure yönlendirici alt ağlar içermez, Azure yönetim uç ve diğer Microsoft özellikleri yedekleyin.
* **Rol yapılandırma dosyası**: Bu gelen erişim denetim listeleri (ACL'ler) tabanlı hello kiracının hizmet modelinde hello tanımlar. Bir kiracı Web ön uç bağlantı noktası 80 üzerinde belirli bir sanal makine varsa bir uç nokta hello yapılandırıyorsanız Örneğin, ardından Azure TCP bağlantı noktası 80 tooall IP'leri açar [Azure Klasik dağıtım modeli](../azure-resource-manager/resource-manager-deployment-model.md). Merhaba çalışan rolü yalnızca toohello sanal makine içinde hello açar çalıştıran, arka uç veya çalışan rolü hello sanal makine varsa, aynı Kiracı.

## <a name="isolation"></a>Yalıtım
Ayırma tooprevent başka bir önemli bulut güvenlik gereksinimidir bilgileri yetkisiz ve istemeyerek aktarımını paylaşılan çok kiracılı mimarisinde dağıtımlar arasında.

Azure uygulayan [ağ erişim denetimi](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/) ve VLAN yalıtımı, ACL'leri, ile arasında ayrım yapma yük dengeleyicileri ve IP filtreleri. Dış trafiğini sınırlayan gelen tooports ve protokolleri, sanal makinelerde tanımlarsınız. Azure Implements ağ filtreleme sahte tooprevent trafiği ve gelen ve giden trafiği tootrusted platform bileşenleri kısıtlayın. Sınır koruma cihazlarına uygulanan trafik akış ilkeleri, trafiği varsayılan olarak reddeder.

![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-getting-started/sec-azgsfig3.PNG)

Ağ adresi çevirisi (NAT) kullanılan dış trafiğinden iç ağ trafiğini tooseparate. İç trafik dışarıdan yönlendirilemez. Dışarıdan yönlendirilebilen [sanal IP adresleri](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx), yalnızca Azure içinde yönlendirilebilen [iç Dinamik IP](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) adreslerine çevrilir.

Dış trafiğin tooAzure sanal makineleri güvenlik duvarı ACL'ler yönlendiriciler, yük Dengeleyiciler ve Katman 3 anahtarları. Yalnızca bilinen belirli protokollere izin verilir. ACL'ler Konuk sanal makinelerden yönetimi için kullanılan tooother VLAN'ları yer toolimit trafiği alır. Ayrıca, IP filtreleri hello ana bilgisayar işletim sistemi başka sınırları hello trafiği her iki veri bağlantı ve ağ katmanlardaki üzerinden trafik filtre.

### <a name="how-azure-implements-isolation"></a>Azure’da yalıtım uygulamaları
Hello Azure yapı denetleyicisi altyapı kaynaklarını tootenant iş yükleri için ayırma sorumludur ve tek yönlü iletişim hello konak toovirtual makinelerden yönetir. Hello Azure hiper yönetici bellek zorunlu kılan ve ağ trafiğini tooguest OS kiracılar işlem ayırma ve sanal makineler arasında güvenli bir şekilde yönlendirir. Azure ayrıca kiracılar, depolama ve sanal ağlar için yalıtım uygular.

* Her Azure AD kiracısı güvenlik sınırları kullanarak mantıksal olarak yalıtılmış.
* Azure depolama hesaplarıdır benzersiz tooeach abonelik ve bir depolama hesabı anahtarı kullanarak kimlik doğrulamalı erişimi gerekir.
* Sanal ağlar birleşimi benzersiz özel IP adresleri, güvenlik duvarları ve IP ACL'ler mantıksal olarak yalıtılmış. Yük Dengeleyici trafiği toohello uygun kiracılar uç nokta tanımları tabanlı rota.

## <a name="virtual-networks-and-firewalls"></a>Sanal ağlar ve güvenlik duvarları
Merhaba [dağıtılmış ve sanal ağlar](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) Azure Yardımı'nda özel ağ trafiğinizi diğer Azure sanal ağ trafiğinden mantıksal olarak yalıtılmış olduğundan emin olun.

![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-getting-started/sec-azgsfig4.PNG)

Aboneliğiniz birden çok yalıtılmış özel ağlar (ve içermelidir güvenlik duvarı, Yük Dengeleme ve ağ adresi çevirisi).

Azure ağ arasında ayrım yapma her Azure üç birincil düzeyde toologically segregate trafiği küme sağlar. [Sanal yerel ağlar](https://azure.microsoft.com/services/virtual-network/) (VLAN) kullanılan hello Azure ağ hello kalan tooseparate müşteri trafiğinden. Erişim toohello dış hello kümeden Azure Ağ Yük Dengeleyici ile sınırlıdır.

Sanal makinelerden ağ trafiğini tooand hello hiper yönetici sanal anahtar aracılığıyla geçmesi gerekir. Merhaba IP Filtresi bileşeni hello kök işletim sistemi hello kök sanal makineden hello Konuk sanal makineleri ve hello Konuk sanal makineleri birbirinden ayırır. Bir kiracının düğümleri ve hello arasında trafiği toorestrict iletişimin filtreleme gerçekleştiren diğer kiracılardan ayırmanın (Merhaba Müşteri'nin hizmet yapılandırmasını temel alarak) genel Internet.

Merhaba IP Filtresi Konuk sanal makinelerden önlemeye yardımcı olur:

* Sahte trafiği oluşturuluyor.
* Trafik almıyor toothem ele.
* Trafik tooprotected altyapı uç noktaları yönlendirerek.
* Gönderme veya uygunsuz alma yayın trafiği.

Sanal makinelerinizi üzerine yerleştirebilirsiniz [Azure sanal ağlar](https://azure.microsoft.com/documentation/services/virtual-network/). Bu sanal ağlar şirket ortamlarında, yapılandırdığınız benzer toohello ağlardır oldukları genellikle bir sanal anahtar ile ilişkili. Sanal makineler aynı sanal ağ iletişim kurabilir toohello birbiriyle ek yapılandırmaya gerek olmadan bağlı. Sanal ağ içindeki farklı alt ağlar da yapılandırabilirsiniz.

Azure sanal ağ teknolojileri toohelp güvenli iletişim sanal ağınızda aşağıdaki hello kullanabilirsiniz:

* [**Ağ güvenlik grupları (Nsg'ler)**](../virtual-network/virtual-networks-nsg.md). Bir NSG toocontrol trafiği tooone veya daha fazla sanal makine örnekleri, sanal ağınızda bulunan kullanabilirsiniz. NSG’de trafik yönüne, protokole, kaynak adresle bağlantı noktasına ve hedef adresle bağlantı noktasına göre trafiğe izin veren ya da reddeden erişim denetim kuralları yer alır.
* [**Kullanıcı tanımlı yönlendirme**](../virtual-network/virtual-networks-udr-overview.md). Merhaba, tooa belirli alt toogo tooa sanal ağ güvenlik Gereci akan paketlerde için sonraki atlama hello belirtin, kullanıcı tanımlı yollar oluşturarak bir sanal gereç yoluyla paketlerin yönlendirilmesini kontrol edebilirsiniz.
* [**IP iletimi**](../virtual-network/virtual-networks-udr-overview.md). Bir sanal ağ güvenlik Gereci adresli tooitself olmayan gelen trafiği mümkün tooreceive olması gerekir. bir sanal makine tooreceive trafiği tooallow tooother hedefleri ele, hello sanal makine için IP iletimini etkinleştirme.
* [**Zorlamalı tünel oluşturma**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md). Zorlamalı tünel, yeniden yönlendirme veya "denetleme ve denetim için siteden siteye VPN tüneli aracılığıyla bir sanal ağ geri tooyour şirket içi konumunda sanal makineleriniz tarafından oluşturulan tüm Internet'e bağlı trafik zorla" sağlar
* [**Uç nokta ACL'lerini**](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Hangi makinelerin uç nokta ACL'lerini tanımlayarak hello Internet tooa sanal makineden gelen bağlantılara sanal ağınızda izin kontrol edebilirsiniz.
* [**İş ortağı ağ güvenliği çözümleri**](https://azure.microsoft.com/marketplace/). Azure Market hello erişebilirsiniz ortak ağ güvenlik çözümlerini mevcuttur.

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Azure sanal ağlar ve güvenlik duvarları nasıl uygular
Azure güvenlik duvarları paket filtreleme varsayılan olarak tüm konak ile Konuk sanal makineleri uygular. Hello Azure Marketi Windows işletim sistemi görüntüleri Windows Güvenlik Duvarı varsayılan olarak etkin de vardır. Yük Dengeleyici Azure genel kullanıma yönelik ağları denetim iletişimin hello çevre dayalı IP müşteri yöneticiler tarafından yönetilen ACL'lere.

Azure’un normal çalışma süreçleri veya olağanüstü durum sırasında bir müşterinin verilerini taşıması halinde ilgili işlemler özel ve şifreli iletişim kanallarından gerçekleştirilir. Sanal ağlar ve güvenlik duvarları tarafından Azure toouse işe diğer özellikleri şunlardır:

* **Yerel ana bilgisayar güvenlik duvarı**: Azure Service Fabric ve Azure Storage yok hiper yönetici sahip yerel bir işletim sisteminde çalışır. Bu nedenle hello windows güvenlik duvarı hello önceki iki kural kümesini ile yapılandırılır. Depolama yerel toooptimize performans çalışır.
* **Ana bilgisayar güvenlik duvarı**: hello ana bilgisayar güvenlik duvarı hello hiper yönetici çalışan tooprotect hello ana bilgisayar işletim sistemi değil. Merhaba kuralları programlanmış tooallow yalnızca hello Service Fabric denetleyicisini ve belirli bir bağlantı noktasında kutuları tootalk toohello ana bilgisayar işletim sistemi geçin. Merhaba diğer tooallow DHCP yanıt ve DNS yanıtları durumlardır. Azure hello şablonu hello ana bilgisayar işletim sistemi için güvenlik duvarı kuralları sahip bir makine yapılandırma dosyasını kullanır. Merhaba konağının dış saldırıdan bir Windows Güvenlik duvarı yapılandırılmış toopermit iletişimi yalnızca kaynaklardan bilinen, kimlik doğrulamalı korunur.
* **Konuk Güvenlik Duvarı'nı**: hello sanal makine anahtarı paket filtresi (örneğin, Windows Güvenlik Duvarı parçası hello konuk işletim sistemi hello) farklı yazılım programlanmış ancak hello kurallarında çoğaltır. Merhaba iletişimi yapılandırmaları hello ana bilgisayarında IP Filtresi tarafından izin verilen olsa bile hello Konuk sanal makine güvenlik duvarı yapılandırılmış toorestrict iletişimleri tooor hello Konuk sanal makineden olabilir. Örneğin, iki olmuştur, sanal ağlar arasında toouse hello Konuk sanal makine güvenlik duvarı toorestrict iletişim yapılandırılmış tooconnect tooone seçebilirsiniz başka bir.
* **Depolama Güvenlik Duvarı'nı (FW)**: hello depolama ön uç güvenlik duvarını hello yalnızca 80/443 ve diğer gerekli yardımcı programı bağlantı noktaları üzerinde trafiği toobe filtreler. Merhaba Güvenlik Duvarı'nı hello depolama arka uç depolama ön uç sunuculardan yalnızca iletişimleri toocome kısıtlar.
* **Sanal ağ geçidi**: Merhaba [Azure sanal ağ geçidi](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) , iş yüklerini Azure Virtual Network tooyour bağlanma hello şirket içi ağ geçidi şirket içi sitelere olarak görev yapar. Gerekli tooconnect tooon içi siteleri aracılığıyla olan [IPSec siteden siteye VPN tünelleri](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md), aracılığıyla veya [ExpressRoute](../expressroute/expressroute-introduction.md) devreler. IPSec/IKE VPN tünelleri hello ağ geçitleri IKE el sıkışmaları gerçekleştirmek ve hello IPSec S2S VPN tünelleri hello sanal ağlar ve şirket içi siteler arasında oluşturabilir. Sanal ağ geçitleri de sonlandırmak [noktadan siteye VPN'lerde](../vpn-gateway/vpn-gateway-point-to-site-create.md).

## <a name="secure-remote-access"></a>Güvenli uzaktan erişim
Merhaba bulutta depolanan veriler yeterli etkin korumaları tooprevent açığından yararlanma girişimi ve gizliliği ve bütünlük aktarım sırasında hatayla korumak gerekir. Buna bir kuruluşun ilke tabanlı, denetlenebilir kimlik ve erişim yönetim sistemleri ile bağlantılı ağ denetimleri dahildir.

Yerleşik şifreleme teknolojisi içinde ve dağıtımlar, Azure bölgeleri arasında ve Azure tooon içi veri merkezleri arasında tooencrypt iletişim sağlar. Yönetici erişim toovirtual makineleri aracılığıyla [uzak masaüstü oturumları](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), [uzaktan Windows PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx), ve hello Azure portalında her zaman şifrelenir.

toosecurely şirket içi veri merkezi toohello bulut genişletmek, Azure hem de sağlar [siteden siteye VPN](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) ve [noktadan siteye VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md), ayrılmış bağlantılarıyla artı [ExpressRoute](../expressroute/expressroute-introduction.md)(sanal ağlar VPN üzerinden şifrelenir bağlantıları tooAzure).

### <a name="how-azure-implements-secure-remote-access"></a>Azure’da güvenli uzaktan erişim uygulamaları
Her zaman bağlantıları toohello Azure portal kimlik doğrulaması ve SSL/TLS gerektirir. Yönetim sertifikaları tooenable güvenli yönetim yapılandırabilirsiniz. Endüstri standardı güvenlik protokolleri gibi [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) ve [IPSec](https://en.wikipedia.org/wiki/IPsec) tam olarak desteklenir.

[Azure ExpressRoute](../expressroute/expressroute-introduction.md), Azure veri merkezleri ile şirketinizde veya bir birlikte bulundurma ortamında bulunan altyapı arasında özel bağlantılar oluşturmanızı sağlar. ExpressRoute bağlantıları hello Git değil genel Internet. Bunlar, daha fazla güvenilirlik, yüksek hız, düşük gecikme ve normal Internet tabanlı bağlantılar daha yüksek güvenlik sağlar. Bazı durumlarda, arasında veri aktarma şirket içi konumlara ve ExpressRoute bağlantıları kullanarak Azure önemli maliyet avantajları da sağlar.

## <a name="logging-and-monitoring"></a>Günlüğe kaydetme ve izleme
Kimliği doğrulanmış olayların günlüğe kaydedilmesini bir denetim izi'ni üreten güvenlikle ilişkili Azure sağlar ve tasarlanan toobe dirençli tootampering durumda. Bu, güvenlik olay günlüklerini Azure altyapı sanal makineler ve Azure AD gibi sistem bilgilerini içerir. Güvenlik olay izleme DHCP veya DNS sunucusu IP adresi değişiklikleri gibi Olay toplama içerir; erişim tooports, protokolleri veya tasarım gereği engellenmiş durumda olan IP adresleri; Güvenlik İlkesi veya Güvenlik Duvarı ayarlarında değişiklikler; hesabı veya grup oluşturma; ve beklenmeyen veya işlemler sürücü yükleme.

![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-getting-started/sec-azgsfig5.PNG)

Ayrıcalıklı kullanıcı erişimini ve etkinliklerini, yetkilendirilmiş ve yetkilendirilmemiş erişim girişimlerini, sistem özel durumlarını ve bilgi güvenliği olaylarını kaydeden denetim günlükleri belirli bir süre boyunca saklanır. günlük toplama ve saklama tooyour kendi gereksinimlerini yapılandırmak için günlüklerinizi hello bekletme kümeleri ' dir.

### <a name="how-azure-implements-logging-and-monitoring"></a>Azure’da günlüğe kaydetme ve izleme uygulamaları
Yerel veya sanal olup azure yönetim Aracısı (MA) ve Azure Güvenlik İzleyicisi (ASM) aracıları tooeach işlem, depolama ya da Yönetim altındaki doku düğümü dağıtır. Her yönetim Aracısı hello Azure sertifika deposundan alınabilir ve İleri Tanılama'ı önceden yapılandırılmış bir sertifika ile yapılandırılmış tooauthenticate tooa hizmet takım depolama hesabı ve olay veri toohello depolama hesabı ' dir. Bu aracıları dağıtılan toocustomers sanal makineleri olup olmadığı.

Azure yöneticileri günlükleri kimliği doğrulanmış ve denetlenen erişim toohello günlükleri için bir web Portalı aracılığıyla erişin. Yöneticiler günlükleri ayrıştırabilir, filtreleyebilir, bağıntı kurabilir ve çözümleyebilir. Günlükleri doğrudan yönetici erişimi toohelp korumalı hello Azure hizmet takım depolama hesapları günlük kurcalanmaya karşı engeller.

Microsoft, hello Syslog protokolünü kullanarak ağ aygıtlarının ve Microsoft Denetim toplama Hizmetleri (ACS) kullanarak ana bilgisayar sunucularına günlükleri toplar. Bu günlükler, şüpheli olayları için uyarılar oluşturulduğunda günlük veritabanına yerleştirilir. Hello Yöneticisi erişmek ve bu günlüklerini analiz edin.

[Azure tanılama](https://msdn.microsoft.com/library/azure/gg433048.aspx) toocollect Azure'da çalışan bir uygulama Tanılama verileri sağlayan Azure özelliğidir. Hata ayıklama ve sorun giderme performansını ölçmek, kaynak kullanımı, trafik analizi, kapasite planlaması izleme ve denetim için tanılama veri budur. Merhaba tanılama veriler toplandıktan sonra aktarılan tooan kalıcılığı için Azure depolama hesabı olabilir. Aktarımları da zamanlanabilir veya isteğe bağlı.

## <a name="threat-mitigation"></a>Tehdit azaltma
Ayrıca tooisolation, şifreleme ve filtreleme, Azure bir dizi tehdit azaltma mekanizmalar ve işlemler tooprotect altyapı ve Hizmetleri kullanır. Bu dahili denetimler ve kullanılan teknolojiler toodetect içerir ve DDoS, ayrıcalık yükseltme ve hello gibi gelişmiş tehditleri düzeltmek [OWASP üst-10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

Merhaba güvenlik denetimleri ve risk yönetimi işlemleri Microsoft bulut altyapısı azaltmak yer toosecure içinde hello güvenlik olayları riskini. Olay bir olay tarafından oluşur Hello hello güvenlik olay Yönetimi (SIM) hello Microsoft çevrimiçi güvenlik hizmetleri ve uyumluluk (OSSC) ekip içinde hazır toorespond herhangi bir zamanda Ekiptir.

### <a name="how-azure-implements-threat-mitigation"></a>Azure’da tehdit azaltma uygulamaları
Azure güvenlik denetimleri yer tooimplement tehdit azaltma sahiptir ve ayrıca toohelp müşteriler kendi ortamlarında olası tehditlerin azaltılmasına. Merhaba aşağıdaki listede Azure tarafından sunulan hello tehdit azaltma özellikleri özetlenmektedir:

* [Azure kötü amaçlı yazılımdan koruma](azure-security-antimalware.md) tüm altyapı sunucuları üzerinde varsayılan olarak etkindir. İsteğe bağlı olarak, kendi sanal makinelerde etkinleştirebilirsiniz.
* Microsoft sunucuları, ağları ve uygulamaları toodetect tehditleri izleme sürekli tutar ve davranışları önleyebilir. Otomatik uyarılar anormal davranışları, iç ve dış tehditlerinin tootake düzeltme eylemi vermeden yöneticileri bildirir.
* Web uygulaması güvenlik duvarı gibi aboneliklerinizi içinde üçüncü taraf güvenlik çözümlerini dağıtmak [Barracuda](https://techlib.barracuda.com/ng54/deployonazure).
* Microsoft'un yaklaşımı toopenetration test içeren "[kırmızı gruplama](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf)," Microsoft Güvenlik uzmanları Azure tootest savunma gerçek hayattaki karşı (müşteri olmayan) dinamik üretim sistemlerinde saldırmak içerir Gelişmiş , kalıcı tehditler.
* Tümleşik dağıtım sistemleri hello dağıtım ve güvenlik düzeltme eklerini yüklemesini hello Azure platformu yönetin.

## <a name="next-steps"></a>Sonraki adımlar
[Azure Güven Merkezi](https://azure.microsoft.com/support/trust-center/)

[Azure Güvenlik Ekibi Blogu](http://blogs.msdn.com/b/azuresecurity/)

[Microsoft Güvenlik Yanıt Merkezi](https://technet.microsoft.com/library/dn440717.aspx)

[Active Directory Blogu](http://blogs.technet.com/b/ad/)
