---
title: "azure'da iş yüklerini aaaSecurity en iyi yöntemler için Iaas | Microsoft Docs"
description: " iş yükleri tooAzure Iaas Hello geçişini fırsatları tooreevaluate bizim tasarımları getirir. "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Azure Iaas iş yükleri için en iyi güvenlik uygulamaları

Hizmet (Iaas) olarak hareket eden iş yükleri tooAzure altyapı düşünmek başlatıldı gibi bazı noktalar bilginiz büyük olasılıkla gerçekleşmiş. Sanal ortamlar güvenliğini sağlama deneyimi zaten sahip olabilir. TooAzure Iaas taşıdığınızda, sanal ortamlar korumak ve uzmanlık uygulamak ve yeni seçenekler toohelp güvenli birtakım varlıklarınızı kullanın.

Biz toobring kaynakları bire tooAzure şirket içi beklemelisiniz değil, söyleyerek başlayalım. Merhaba yeni zorluklar ve hello yeni seçenekler Getir varolan bir fırsat tooreevaluate deigns, araçları ve işler.

Güvenlik için sizin sorumluluğunuzdadır bulut hizmeti başlangıç türünü temel alır. Merhaba aşağıdaki grafikte hem Microsoft hem de, sorumluluğu hello bakiyesini özetlenmektedir:


![Sorumluluk alanları](./media/azure-security-iaas/sec-cloudstack-new.png)


Biz, kuruluşunuzun güvenlik gereksinimlerine yardımcı olabilecek Azure'da hello seçenekleri bazıları ele alacağız. Güvenlik gereksinimleri, farklı türlerde iş yükleri için değişebilir aklınızda bulundurun. Bu en iyi uygulamaları bir tek başına sistemlerinizi güvenliğini sağlayabilirsiniz. Başka bir şey güvenlik gibi toochoose hello uygun seçeneğiniz vardır ve nasıl hello çözümleri birbirine boşluklar doldurarak tamamlayabilir bakın.

## <a name="use-privileged-access-workstations"></a>Ayrıcalıklı erişimli iş istasyonlarının kullanın

Kuruluşlar çoğunlukla kalan toocyberattacks yükseltilmiş haklara sahip hesaplar kullanırken Yöneticiler eylemleri gerçekleştirmek için prey. Genellikle bu amaçla yapılır değildir ancak yapılandırmayı ve işlemleri izin verdiğinden. Bu kullanıcılar çoğu kavramsal açısından bu eylemleri hello riskini anlamak ancak hala toodo seçin bunları.

E-posta denetleme ve hello Internet gözatma yetecek zararsız göründüğü gibi işlemler yapılıyor. Ancak yükseltilmiş hesapları toocompromise gözatma etkinlikleri, özel olarak hazırlanmış bir e-postaları veya diğer teknikleri toogain erişim tooyour enterprise kullanan kötü amaçlı aktör tarafından doğurabilir. Etkilenme tooaccidental güvenliğinin aşılmasına azaltma bir yolu olarak tüm Azure yönetim görevlerini gerçekleştirme için güvenli yönetim iş istasyonları hello kullanılması önerilir.

Ayrıcalıklı erişimli iş istasyonlarının (Patiler) adanmış bir işletim sistemi görevlerde hassas--Internet saldırıları ve tehdit vektörlerini korumalı bir sağlar. Bu önemli görevleri ve hesaplarından ayırma günlük kullanım iş istasyonları hello ve aygıtların kimlik avı saldırıları, uygulama ve işletim sistemi güvenlik açıkları, çeşitli kimliğe bürünme saldırılarını ve tuş vuruşu gibi kimlik bilgisi hırsızlığı saldırılara karşı güçlü koruma sağlar günlüğe kaydetme, Pass--Hash ve geçişi anahtar.

Hello PENÇE yaklaşım hello tanınmış bir uzantısıdır ve standart kullanıcı hesabından ayrı ayrı olarak atanmış bir yönetici hesabı yöntem toouse önerilir. Bir PENÇE hassas bu hesaplar için güvenilir bir iş istasyonu sağlar.

Daha fazla bilgi ve uygulama yönergeleri için bkz [ayrıcalıklı erişimli iş istasyonlarının](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations).

## <a name="use-multi-factor-authentication"></a>Çok faktörlü kimlik doğrulamasını kullan

Geçmiş Hello içinde ağ çevre kullanılan toocontrol erişim toocorporate verisi idi. Bir bulut ilk olarak, mobil ilk dünyada hello denetim düzlemi kimliktir: toocontrol erişim tooIaaS Hizmetleri herhangi bir CİHAZDAN kullanın. Ayrıca tooget görünürlük ve öngörü nerede ve nasıl verilerinizi kullanılıyor içine kullanırsınız. Azure kullanıcılarınızın dijital kimliğini Hello koruma aboneliklerinizi kimlik hırsızlığa ve diğer cybercrimes korumanın hello dönüm olur.

Bir hesap toosecure uygulayabileceğiniz hello en yararlı adımları tooenable iki öğeli kimlik doğrulama biridir. İki öğeli kimlik doğrulama bir şey toplama tooa parola kullanarak kimlik doğrulaması bir yoludur. Tooget yöneten bir kişi tarafından erişim hello riskini azaltmaya yardımcı olacak başka birinin parola.

[Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md) korunmasına yardımcı erişim toodata ve uygulamaları basit bir oturum açma işlemi için kullanıcı talebine buluştururken. Kolay doğrulama seçenekleri--telefon araması, SMS mesajı veya mobil uygulama bildirimi aralıklı güçlü kimlik doğrulaması sunar. Kullanıcıların tercih hello yöntemi seçin.

Merhaba en kolay yolu toouse çok faktörlü kimlik doğrulaması Windows, iOS ve Android çalıştıran mobil aygıtlarda kullanılabilir hello Microsoft Authenticator mobil uygulamasında ' dir. Merhaba en son sürümü Windows 10 ve hello tümleştirme Azure Active Directory (Azure AD) ile şirket içi Active Directory ile [iş için Windows Hello](../active-directory/active-directory-azureadjoin-passport-deployment.md) sorunsuz tek oturum açma tooAzure kaynaklar için kullanılabilir. Bu durumda, hello Windows 10 cihaz hello ikinci faktörü olarak kimlik doğrulaması için kullanılır.

Azure aboneliğinizi yönetmek hesapları ve toovirtual makinelerinizde imzalayabilirsiniz hesapları için çok faktörlü kimlik doğrulaması kullanarak, yalnızca bir parola kullanmaktan daha büyük bir düzeyde güvenlik sağlar. İki öğeli kimlik doğrulama başka biçimlerde da çalışabilir, ancak değil zaten üretimde oldukları bunların dağıtımı karmaşık olabilir.

Merhaba aşağıdaki ekran görüntüsünde bazı Azure çok faktörlü kimlik doğrulaması için hello seçenekleri gösterir:

![Çok faktörlü kimlik doğrulama seçenekleri](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>Sınırlayabilir ve yönetici erişimini kısıtlamak

Azure aboneliğinizi yönetmek hello hesaplarını güvenli hale getirme son derece önemlidir. Merhaba güvenliğinin bu hesapların tüm hello hello değerini tooensure hello gizliliği ve veri bütünlüğü sürebilir diğer adımlar üzerindeki geçersiz kılar. Son olarak hello tarafından gösterilen [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden) sızıntısı sınıflandırılmış bilgilerinin iç saldırıların büyük tehdit toohello neden her kuruluşun genel güvenlik.

Kişiler için yönetici hakları tarafından aşağıdaki ölçütleri benzer toothese değerlendirin:

- Bunlar, yönetici ayrıcalıkları gerektiren görevler gerçekleştiriyorsunuz?
- Ne sıklıkta hello görevler gerçekleştirilir?
- Şirket adına başka bir yönetici tarafından hello görev neden yapılamaz belirli bir nedenle var mı?

Belge diğer tüm bilinen alternatif yaklaşımlar toogranting hello ayrıcalık ve neden her kabul edilebilir değil.

tam zamanında yönetim Hello kullanımını hello gereksiz hesaplarının varlığı yükseltilmiş haklara sahip olduğunda bu hakları gerekmeyen dönemlerde engeller. Yöneticiler işlerini yapabilmesi için hesapları sınırlı bir süre için hakları yükseltilmiş. Ardından, bu hakları hello sonunda bir kaydırma veya bir görev tamamlandığında kaldırılır.

Kullanabileceğiniz [Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage, izleme ve Denetim erişimi kuruluşunuzdaki. Kuruluşunuzdaki kişiler uygulamanız hello eylemlerin farkında kalır yardımcı olur. Ayrıca, tam zamanında yönetim tooAzure AD'in uygun admins hello kavramı sunarak getirir. Bunlar kimin hello olası toobe hesaplarıyla yönetici haklarına olan bireylerdir. Kullanıcıların bu tür bir etkinleştirme işlemi boyunca gidebilir ve sınırlı bir süre için yönetici hakları verilmesi.


## <a name="use-devtest-labs"></a>DevTest Labs kullanın

Labs ve geliştirme ortamları için Azure kullanarak test ve geliştirme kuruluşlar toogain çeviklik donanım tedarik tanıtan alma koyma hello gecikmelerinden sağlar. Ne yazık ki, Azure veya desire toohelp ile benzerlik eksikliği hızlandırmak kendi benimseme hello yönetici toobe aşırı izin veren hakları atama ile neden olabilir. Bu riski istemeden hello kuruluş toointernal saldırıları doğurabilir. Bazı kullanıcılar sahip olması gereken daha çok daha fazla erişim izni.

Merhaba [Azure DevTest Labs](../devtest-lab/devtest-lab-overview.md) hizmet kullanır [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) (RBAC). RBAC kullanarak, yalnızca hello erişim düzeyini kullanıcılar toodo için gerekli izni veren işlerini rollere ekibiniz içinde görevleri ayırabilirsiniz. RBAC önceden tanımlı rollerle (sahibi, Laboratuvar kullanıcı ve katkıda bulunan) gelir. İşbirliği büyük ölçüde kolaylaştırma ve bu rolleri tooassign hakları tooexternal ortakları bile kullanın.

DevTest Labs RBAC kullandığından, ek, olası toocreate olan [özel roller](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md). DevTest Labs yalnızca izinleri hello yönetimini basitleştirir, sağlanan ortamları alma hello işlemini basitleştirir. Ayrıca, geliştirme ve test ortamları üzerinde çalıştığınız takım tipik diğer zorluklar uğraşmanız yardımcı olur. Bazı hazırlık gerektirir, ancak hello uzun vadede şeyler ekibiniz için kolaylaştırır.

Azure DevTest Labs özellikleri içerir:

- Merhaba üzerinde yönetici denetime kullanılabilir toousers seçenekleri. Hello Yöneticisi izin verilen VM boyutlarını, VM'lerin ve VM'ler başlatıldığında en fazla ve kapatma gibi merkezi olarak yönetebilir.
- Otomasyon laboratuvar ortamı oluşturma.
- Maliyet İzlemesi.
- Geçici birlikte çalışma için basitleştirilmiş dağıtım VM'lerin.
- Self Servis kullanıcıları tooprovision kendi labs şablonları kullanarak sağlayan.
- Yönetme ve tüketimini sınırlamak.

![DevTest Labs toocreate bir laboratuvar kullanma](./media/azure-security-iaas/devtestlabs.png)

Ek ücret ödemeden DevTest Labs hello kullanımı ile ilişkilidir. Merhaba oluşturulmasını labs, ilkeleri, şablonları ve yapıları ücretsizdir. Sanal makineler, depolama hesapları ve sanal ağlar gibi labs kullanılan Azure kaynaklarını yalnızca hello için ücret ödersiniz.



## <a name="control-and-limit-endpoint-access"></a>Uç noktası erişim denetimi ve sınırı

Barındırma Labs veya Azure üretim sistemlerinde sistemlerinizi toobe hello Internet üzerinden erişilebilir gerektiği anlamına gelir. Varsayılan olarak, yeni bir Windows sanal makine hello RDP bağlantı noktası Internet hello erişilebilir olan ve hello SSH bağlantı noktası açmak Linux sanal makine içeriyor. Adımları gösterilen toolimit uç noktalarını alma yetkisiz erişim gerekli toominimize hello sorununa neden olur.

Azure teknolojileri hello erişim toothose yönetim uç noktaları kısıtlamanıza yardımcı olabilir. Azure'da, kullandığınız [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) (Nsg'ler). Azure Resource Manager dağıtım için kullandığınızda Nsg'ler tüm ağları toojust hello yönetim uç noktaları (RDP veya SSH) hello erişimi sınırlayın. Nsg'ler düşünürken, yönlendirici ACL'ler düşünün. Bunları Azure ağlarınızı çeşitli kesimleri arasındaki tootightly denetim hello ağ iletişimi kullanabilirsiniz. Çevre ağı ya da diğer yalıtılmış ağlarda benzer toocreating ağlarda budur. Merhaba trafiği inceleyebilir değil, ancak ağ kesimleri ile yardımcı olurlar.


Azure'da, yapılandırdığınız bir [siteden siteye VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) şirket içi ağınızdan. Siteden siteye VPN, şirket içi ağ toohello bulut genişletir. Bu, başka bir fırsat toouse Nsg'ler sunar, hello Nsg'ler toonot de değiştirebilirsiniz çünkü yerden erişim'den hello yerel ağ diğer imkan tanır. Ardından, yönetim ilk bağlantı toohello VPN aracılığıyla Azure ağı tarafından yapılır gerektirebilir.

Merhaba siteden siteye VPN seçeneğini burada şirket içi kaynaklarınızı Azure ile yakından tümleşik üretim sistemlerine barındırma durumlarda en cazip olabilir.

Alternatif olarak, hello kullanabilirsiniz [noktası site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) seçeneği yok toomanage sistemleri istediğiniz durumlarda tooon şirket kaynaklarına erişim. Bu sistemlere kendi Azure sanal ağındaki yalıtılmış. Hello Azure içine Administrators can VPN yönetimsel iş istasyonunda ortamından barındırılan.

>[!NOTE]
>Merhaba Nsg'ler toonot ACL'lerin hello Internet erişimi toomanagement uç noktalarının izin ya da VPN seçeneği tooreconfigure hello kullanabilirsiniz.

Başka bir seçenek dikkate değer bir [Uzak Masaüstü Ağ Geçidi](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md) dağıtım. Bu dağıtım kullanabileceğiniz toosecurely daha ayrıntılı uygulama toothose bağlantıları denetlerken bu tooRemote Masaüstü sunucuları HTTPS üzerinden bağlanma.

Olurdu özellikleri tooinclude erişebilirsiniz:

- Yönetici toolimit bağlantıları toorequests belirli sistemlerden seçenekleri.
- Akıllı kart kimlik doğrulaması veya Azure çok faktörlü kimlik doğrulaması.
- Hangi sistemleri birisi toovia hello ağ geçidi bağlanabileceği denetler.
- Diski ve aygıt yeniden yönlendirme denetler.

## <a name="use-a-key-management-solution"></a>Anahtar yönetimi çözümü kullanın

Güvenli anahtar yönetimi, hello bulutta temel tooprotecting verilerdir. İle [Azure anahtar kasası](../key-vault/key-vault-whatis.md)küçük parolaları gibi ve güvenli bir şekilde şifreleme anahtarlarını saklamak parolalar donanım güvenlik modülleri (HSM'ler). Ek güvenlik için HSM'lerde anahtarları içeri aktarabilir veya oluşturabilirsiniz.

Microsoft işlemleri anahtarlarınızı FIPS 140-2, Düzey 2 doğrulanmış HSM'ler (donanım ve bellenim). Azure günlük ile izleme ve denetim anahtar kullanımı: Azure veya güvenlik bilgileri ve Olay yönetimi (SIEM) sistemine ek analiz ve tehdit algılama için günlükleri kanal.

Bir Azure aboneliği olan herhangi bir kişi oluşturabilir ve anahtar kasalarını kullanabilirsiniz. Anahtar kasası geliştiricilere ve güvenlik yöneticilerine avantaj sağlasa da, uygulanabilir ve bir kuruluştaki Azure hizmetleri yönetmek için sorumlu bir yönetici tarafından yönetiliyor.


## <a name="encrypt-virtual-disks-and-disk-storage"></a>Sanal diskleri ve disk depolamayı şifrelemek

[Azure Disk şifrelemesi](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0) adresleri Merhaba, veri hırsızlığı veya bir disk taşıyarak elde yetkisiz erişimden Etkilenme tehdit. Merhaba disk ekli tooanother sistem diğer güvenlik denetimlerini atlayarak bir yolu olarak oluşturulabilir. Disk şifrelemesi kullanır [BitLocker](https://technet.microsoft.com/library/hh831713) Windows ve Linux tooencrypt işletim sistemi ve veri sürücüleri DM-Crypt. Azure Disk şifrelemesi anahtar kasası toocontrol ile tümleşir ve hello şifreleme anahtarları yönetin. Premium depolama ile standart VM'ler ve VM'ler için kullanılabilir.

Daha fazla bilgi için bkz: [Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler](azure-security-disk-encryption.md).

[Azure depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md) REST, verilerinizi korumaya yardımcı olur. Merhaba depolama hesabı düzeyinde etkinleştirilir. Bizim veri merkezlerinde yazılır ve siz eriştiğinizde otomatik olarak çözülür gibi verileri şifreler. Hello aşağıdaki senaryoları destekler:

- Şifreleme blok blobları, ekleme blobları ve sayfa BLOB'ları
- Arşivlenen VHD'leri ve şablonları şifrelenmesini tooAzure şirket içi getirildi.
- Temel işletim sistemi ve veri diskleri şifreleme Vhd'lerinizi kullanılarak oluşturulan Iaas VM'ler için

Azure depolama şifrelemesi ile devam etmeden önce iki sınırlamaları dikkat edin:

- Klasik depolama hesaplarında kullanılamaz.
- Yalnızca şifreleme etkinleştirildikten sonra yazılan verileri şifreler.

## <a name="use-a-centralized-security-management-system"></a>Bir Merkezi güvenlik yönetimi sistemi kullanın

Sunucularınızın düzeltme eki uygulama, yapılandırma, olayları ve güvenlik sorunlarının düşünülebilir etkinlikler için izlenen toobe gerekir. kullanabileceğiniz olanlar işlemiyle ilgili tooaddress [Güvenlik Merkezi](https://azure.microsoft.com/services/security-center/) ve [Operations Management Suite güvenlik ve Uyumluluk](https://azure.microsoft.com/services/security-center/). Bu seçeneklerin ikisi de hello işletim sisteminde hello yapılandırmasının ötesinde gidin. Ayrıca altyapı, ağ yapılandırması ve sanal gereç kullanımı gibi temel hello hello yapılandırmasını izlenmesini sağlar.

## <a name="manage-operating-systems"></a>İşletim sistemlerini yönetme

Bir Iaas dağıtımında, hala hello yönetimi gibi başka bir sunucuya veya iş istasyonu, ortamınızda dağıtmak hello sistemlerinin sorumludur. Düzeltme eki uygulama sağlamlaştırma, hakları ataması ve herhangi bir etkinlik toohello bakım sisteminizin yine sizin sorumluluğunuzdadır ilişkilidir. Şirket içi kaynaklarınıza ile sıkı bir şekilde tümleşik sistemler için bunu istemeyebilirsiniz toouse hello aynı araçları ve virüsten koruma ve kötü amaçlı yazılımdan koruma, düzeltme eki uygulama ve yedekleme gibi şeyler için şirket içi kullanmakta olduğunuz yordamlar.

### <a name="harden-systems"></a>Sistemleri sağlamlaştırmak
Böylece yüklenen hello uygulamalar için gerekli olan hizmet uç kullanıma Azure Iaas tüm sanal makinelerin sıkı. Windows sanal makineler için Microsoft hello için taban çizgisi olarak yayımlar hello önerilere uyun [güvenlik uyumluluk Yöneticisi](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) çözümü.

Güvenlik uyumluluk Yöneticisi ücretsiz bir araçtır. Tooquickly kullanmak yapılandırabilir ve masaüstü bilgisayarlar, geleneksel veri merkezi ve özel ve genel bulut Grup İlkesi ve System Center Configuration Manager kullanarak yönetebilirsiniz.

Güvenlik uyumluluk Yöneticisi ilkeleri Dağıt hazır ve test edilmiş Desired Configuration Management yapılandırma paketleri sağlar. Bu taban çizgileri dayalı [Microsoft Güvenlik Kılavuzu](https://technet.microsoft.com/en-us/library/cc184906.aspx) öneriler ve endüstri en iyi uygulamalar. Yapılandırma değişikliklerini, adres uyumluluk gereksinimleri, yönetme ve güvenlik tehditlerini azaltılmasına yardımcı olur.

İki farklı yöntemler kullanarak güvenlik uyumluluk Yöneticisi tooimport hello geçerli yapılandırmasını bilgisayarlarınızı kullanabilirsiniz. İlk olarak, Active Directory tabanlı Grup İlkeleri aktarabilirsiniz. İkinci olarak, bir "altın ana" Merhaba yapılandırmasını içeri aktarabilirsiniz hello kullanarak başvuru makinesini [LocalGPO aracı](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) tooback hello yerel Grup İlkesi. Bu gibi durumlarda, hello yerel Grup İlkesi sonra güvenlik uyumluluk Yöneticisi içine aktarabilirsiniz.

Standartlar tooindustry en iyi yöntemler karşılaştırın, özelleştirin ve yeni ilkeler ve Desired Configuration Management yapılandırma paketleri oluşturun. Tüm desteklenen Windows 10 Anniversary Update ve Windows Server 2016 içeren işletim sistemi için taban çizgilerini yayımlandı.


### <a name="install-and-manage-antimalware"></a>Yükleme ve kötü amaçlı yazılımdan koruma yönetme

Üretim ortamınızdan ayrı olarak barındırılan ortamlar için bir kötü amaçlı yazılımdan koruma uzantısı toohelp kullanabilirsiniz, sanal makinelerin korunmasına ve bulut hizmetlerini. İle tümleştirilir [Azure Güvenlik Merkezi](../security-center/security-center-intro.md).


[Microsoft Antimalware](azure-security-antimalware.md) gerçek zamanlı koruma, zamanlanmış tarama, kötü amaçlı yazılım düzeltme, imza güncelleştirmeleri, altyapı güncelleştirmeleri, örnekleri, dışlama olay toplama, raporlama gibi özellikler içerir ve [PowerShell desteği](https://msdn.microsoft.com/library/dn771715.aspx).

![Azure kötü amaçlı yazılımdan koruma](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>Merhaba en son güvenlik güncelleştirmelerini yükleyin
Müşteriler tooAzure taşırken hello ilk iş yüklerinin labs ve dışa dönük sistemleri bazılarıdır. Azure barındırılan sanal makinelerinizi uygulamalar veya toobe erişilebilir toohello Internet gereken hizmetler barındırıyorsanız, düzeltme eki uygulama hakkında temkinli olabilir. Merhaba işletim sisteminin ötesine geçen düzeltme eki. Üçüncü taraf uygulamalar yüklenmemiş güvenlik açıklarından de iyi düzeltme eki yönetimi yerinde olduğunda önlenebilir tooproblems yol açabilir.

### <a name="deploy-and-test-a-backup-solution"></a>Dağıtma ve bir yedekleme çözümüne sınama

Güvenlik güncelleştirmeleri olduğu gibi bir yedekleme ele toobe hello gereken başka bir işlem işleyecek şekilde. Bu, üretim ortamınızın toohello bulut genişletme parçası olan sistemlerinin geçerlidir. Test ve geliştirme sistemleri benzer toowhat kullanıcılar geri yükleme özellikleri dayalı olarak, şirket içi ortamlarla deneyimlerini alışık sağlayın yedekleme stratejilerini izlemeniz gerekir.

Üretim iş yükleri tooAzure varolan yedekleme çözümleri ile mümkün olduğunda tümleştirmeniz taşındı. Veya, kullanabileceğiniz [Azure yedekleme](../backup/backup-azure-arm-vms.md) toohelp, yedekleme gereksinimlerinize adres.


## <a name="monitor"></a>İzleme

[Güvenlik Merkezi](../security-center/security-center-intro.md) tooidentify olası güvenlik açıklarını hello Azure kaynaklarınızın güvenlik durumunu devam eden değerlendirilmesini sağlar. Öneriler listesi gerekli denetimlerin yapılandırılması hello işleminde size rehberlik eder.

Örneklere şunlar dahildir:

- Kötü amaçlı yazılımdan koruma sağlama toohelp tanımlamak ve kötü amaçlı yazılımı kaldırın.
- Ağ güvenlik gruplarını ve kurallarını toocontrol trafiği toovirtual makineleri yapılandırma.
- Web uygulaması güvenlik duvarı toohelp, web uygulamalarınızı hedefleyen saldırılara karşı korumaya sağlama.
- Eksik sistem güncelleştirmelerini dağıtma.
- Merhaba eşleşmeyen işletim sistemi yapılandırmalarını ele alma temelleri önerilir.

Merhaba aşağıdaki görüntüde bazılarını Güvenlik Merkezi'nde etkinleştirebilirsiniz hello seçeneklerini gösterir.

![Azure Güvenlik Merkezi ilkeleri](./media/azure-security-iaas/security-center-policies.png)

[Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md) , yönetmek ve şirket içi korumak ve bulut altyapısı yardımcı olan bir Microsoft bulut tabanlı BT yönetimi çözümüdür. Operations Management Suite bulut tabanlı bir hizmet olarak uygulandığı için hızlı ve en düşük yatırım altyapı kaynaklar ile dağıtılabilir.

Yeni özellikler otomatik olarak devam eden bakım kaydetme teslim edilir ve maliyetleri yükseltin. Operations Management Suite ayrıca System Center Operations Manager ile tümleştirilir. Farklı bileşenler toohelp dahil olmak üzere yüklerinizi Azure daha iyi yönetebilmek sahip bir [güvenlik ve Uyumluluk](../operations-management-suite/oms-security-getting-started.md) modülü.

Operations Management Suite tooview bilgilerinde kaynaklarınızı hakkında hello güvenlik ve uyumluluk özellikleri kullanabilirsiniz. dört ana kategoriye düzenlenmiş Hello bilgiler:

- **Güvenlik etki alanları**: daha fazla güvenlik kayıtları zamanla keşfedin. Kötü amaçlı yazılım değerlendirmesi erişim, değerlendirme, ağ güvenlik bilgileri, kimlik ve erişim bilgileri ve bilgisayarlar güvenlik olayları ile güncelleştirin. Hızlı erişim toohello Azure Güvenlik Merkezi panosunu yararlanın.
- **Önem düzeyindeki sorunlar**: hızlı etkin sorunlar hello sayısını tanımlamak ve hello bu sorunların önem derecesi.
- **Algılama (Önizleme)**: saldırı tanımlamak, kaynaklarına karşı durum gibi güvenlik uyarıları görselleştirme tarafından desenleri.
- **Tehdit Intelligence**: saldırı tanımlamak hello sayısı toplam giden kötü amaçlı IP trafiği, sunucularıyla görselleştirme tarafından desenleri hello kötü amaçlı tehdit türü ve burada bu IP'leri geliyor gelen gösteren bir harita.
- **Ortak Güvenlik sorguları**: hello en yaygın güvenlik listesini sorgular ortamınızı toomonitor kullanabilirsiniz bkz. Bu sorguları birine tıkladığınızda hello **arama** dikey penceresi açılır ve bu sorgu için hello sonuçları gösterir.

Merhaba aşağıdaki ekran görüntüsünde Operations Management Suite görüntüleyebilirsiniz hello bilgi örneği gösterilmektedir.

![Operations Management Suite güvenlik temelleri](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>Sonraki adımlar


* [Azure Güvenlik Ekibi Blogu](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Microsoft Güvenlik Yanıt Merkezi](https://technet.microsoft.com/library/dn440717.aspx)
* [Azure güvenlik en iyi uygulamaları ve desenleri](security-best-practices-and-patterns.md)
