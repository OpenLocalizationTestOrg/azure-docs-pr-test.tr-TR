---
title: "aaaAzure Service Fabric en iyi güvenlik uygulamaları | Microsoft Docs"
description: "Bu makalede Azure Service Fabric güvenlik için en iyi yöntemler kümesi sağlar."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 483a21240da17d56bb4641653093ddcbad379d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-best-practices"></a>Azure Service Fabric en iyi güvenlik uygulamaları
Hızlı, kolay ve düşük maliyetli, Azure'da bir uygulamayı dağıtma. Üretim yararlı toohave bulut uygulamasında dağıtmadan önce en iyi uygulamadır uygulamanızı listesini karşı önemli ve önerilen en iyi yöntemlere hesaplama tooassist.

Azure Service Fabric kolay toopackage kolaylaştıran bir dağıtılmış sistemler platformudur, dağıtın ve ölçeklenebilir ve güvenilir mikro yönetin. Service Fabric da geliştirmeye ve bulut uygulamalarını yönetme hello önemli sorunları giderir. Geliştiriciler ve yöneticiler, karmaşık altyapı sorunlarını çözmeye çalışmak yerine görev açısından kritik, zorlu iş yüklerini uygulamaya odaklanabilir. Service Fabric, bu iş yüklerinin ölçeklenebilir, güvenilir ve yönetilebilir olmasını sağlar. 

En iyi her uygulama için biz açıklamaktadır:

-   Hangi hello en iyi uygulamadır
-   Neden bu en iyi uygulama tooenable istiyor
-   Tooenable hello en iyi yöntem başarısız olursa ne hello sonucu olabilir
-   Tooenable hello en iyi yöntem nasıl öğrenin

Şu anda aşağıdaki en iyi güvenlik uygulamaları, Azure Service Fabric hello sunuyoruz:

-   Azure Resource Manager(ARM) şablonu ve Service Fabric Azure PowerShell modülü toocreate güvenli küme kullanın
-   X.509 sertifikaları kullan
-   Güvenlik ilkelerini yapılandırma
-   Güvenilir aktörler güvenlik yapılandırması
-   Azure Service Fabric için SSL yapılandırma
-   Ağ yalıtımı/Azure Service Fabric ile güvenliği
-   Bir anahtar kasası güvenlik için ayarlama
-   Kullanıcıların tooroles atayın


## <a name="best-practices-for-securing-your-cluster"></a>Kümenizi güvenliğini sağlamak için en iyi uygulamalar

**Büyük resim**

Her zaman güvenli bir küme kullanın
-   Güvenlik küme – sertifikaları kullanma
-   İstemci erişimi (Yönetici ve salt okunur) – AAD kullanın

Otomatik dağıtımları kullanın
-   Komut dosyaları toogenerate kullanmak için dağıtmak ve diğer gizli alma
-   İçinde KV Hello gizli tutmak için diğer tüm istemci erişimi için AD kullanın
-   Hiçbir İnsan erişim toothem kimlik doğrulaması olmadan olması gerekir.

Ayrıca, hello aşağıdakileri dikkate alın:
-   Ağ güvenlik gruplarını (Nsg'ler) kullanarak DMZ'ler oluşturma
-   Atlama sunucuları tooRDP küme VM'ler veya toomanage kümenizi kullanın

Kümeleri özellikle üretim iş yükleri üzerinde çalıştırılan olduğunda tooyour küme bağlanma güvenli tooprevent yetkisiz kullanıcıların olması gerekir. Olası toocreate güvenli olmayan bir küme olmasına karşın, yönetim uç noktaları toohello gösterir böylece anonim kullanıcılar tooconnect tooit verir genel Internet.

Teknolojileri tooimplement bu senaryolarda kullanılır. Merhaba [güvenlik senaryoları küme](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security) şunlardır:

-   Düğümü düğümü güvenlik bu hello VM'ler ve hello kümesindeki bilgisayarlar arasındaki iletişimin güvenliğini sağlar. Bu uygulamalar ve hizmetler hello kümedeki barındırma yetkili toojoin hello küme yalnızca bilgisayarları katılabilir sağlar.
Windows üzerinde çalışan Azure veya tek başına kümeleri üzerinde çalışan kümelerle kullanabilirsiniz [sertifika güvenliği](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security) veya [Windows Güvenliği](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-windows-security) Windows Server makinelerini için.
-   İstemcisi düğümü güvenlik-bu bir Service Fabric istemcisi ve hello kümedeki tek düğümler arasındaki iletişimin güvenliğini sağlar.
-   Rol tabanlı erişim denetimi (RBAC) - hello yönetici ve kullanıcı istemci rolleri hello küme oluşturma sırasında ayrı kimlikleri (Sertifikalar, AAD vb.) sağlayarak her biri için belirttiğiniz.
-   Güvenlik önerileri-için Azure kümeleri, düğümü düğümü güvenlik için AAD güvenlik tooauthenticate istemcileri ve sertifikalar kullanmanız önerilir.

tooconfigure hello tek başına Windows Küme bkz [tek başına windows kümesi yapılandırmak](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest).

Azure Resource Manager şablonları ve Service Fabric Azure PowerShell modülü toocreate güvenli küme kullanın.
Güvenli bir Azure Service Fabric ayarı ile küme Azure'da Azure Kaynak Yöneticisi'ni kullanarak bir adım adım kılavuzu yetenekte kullanılabilir [burada](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm).

Kümenizi Hello Azure Resource Manager şablonu toocustomize kullanın
-   VM VHD'ler için kurulum tarafından yönetilen depolama

Hello Azure Resource Manager şablonu toodrive değişiklikleri tooyour kaynak grubu kullanın
-   Kolay yapılandırma yönetimi
-   Denetim

Küme yapılandırmasını kodu olarak işle
-   Kapsamlı toodeploy seçtiğiniz hello yapılandırmaları denetleniyor
-   Örtük komutları tootweak kaynaklarınızı doğrudan kullanmaktan kaçının

Merhaba pek çok görünüşünün [Service Fabric uygulama yaşam döngüsü](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-lifecycle) otomatikleştirilebilir. [Service Fabric Azure PowerShell Modülü](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications#upload-the-application-package) dağıtma, yükseltme, kaldırma ve Azure Service Fabric uygulamaları test etmek için ortak görevleri otomatik hale getirir. Yönetilen ve HTTP API'leri uygulama yönetimi için de kullanılabilir.

## <a name="use-x509-certificates"></a>X.509 sertifikaları kullan
X.509 sertifikaları ya da Windows güvenliği kullanarak her zaman bu kümeleri korunması. Güvenlik yalnızca küme oluşturma sırasında yapılandırılır ve hello Küme oluşturulduktan sonra olası tooenable güvenlik değil.

Belirtiyorsanız bir [küme sertifika](https://docs.microsoft.com/azure/service-fabric/service-fabric-windows-cluster-x509-security), hello değeri ClusterCredentialType tooX509 olarak ayarlayın. Dış bağlantıları için sunucu sertifikası belirtiyorsanız hello ServerCredentialType tooX509 ayarlayın.

-   Üretim iş yükleri çalıştıran kümelerde kullanılan sertifikaları doğru yapılandırılmış bir Windows Server sertifika hizmeti kullanılarak oluşturulan veya bir onaylanmış sertifika yetkilisinden (CA) edinilen.
-   MakeCert.exe gibi araçları ile oluşturulmuş üretim sertifikaları test veya hiçbir zaman hiçbir geçici kullanın.
-   Kendinden imzalı bir sertifika kullanabilirsiniz, ancak yalnızca test kümeleri için alan ve üretim yapmalısınız.

Merhaba, küme güvenli değil. Herkes anonim olarak bağlanıp yönetim işlemleri gerçekleştirebileceğinden, üretim kümeleri her zaman X.509 sertifikaları veya Windows güvenliği kullanılarak güvenli hale getirilmelidir.

Daha fazla nasıl service fabric kümesi tooenable sertifikaları bakın, toolearn [service fabric kümesi için sertifikaları ekleyebilir veya kaldırabilirsiniz](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure).

## <a name="configure-security-policies"></a>Güvenlik ilkelerini yapılandırma
Service Fabric ayrıca uygulamalar tarafından hello kullanıcı hesapları altında--dağıtımının hello zamanında örneğin kullanılan güvenli hello kaynakları, dizinleri ve dosyaları sertifikaları yardımcı olur. Bu çalışan uygulamaları bile paylaşılan bir barındırılan ortamda, diğerinden daha güvenli hale getirir.

-   Bir Active Directory etki alanı grubu veya kullanıcı kullanın: Active Directory kullanıcı veya grup hesabına ait hello hizmeti hello kimlik bilgileri altında çalıştırabilirsiniz. Bu içi etki alanınızda Active Directory ve Azure Active Directory (Azure AD) değil. Bir etki alanı kullanıcısı veya grubu kullanarak (örneğin, dosya paylaşımları) hello etki alanındaki izinleri verilmiş diğer kaynaklara erişebilir.

-   HTTP ve HTTPS uç noktaları için bir güvenlik erişim ilkesi atama: RunAs İlkesi tooa hizmeti uygulamak ve hello hizmet bildirimi uç noktası kaynakları hello HTTP protokolü ile bildirir, bağlantı noktaları toothese ayrılan SecurityAccessPolicy tooensure belirtmeniz gerekir uç noktalar doğru erişim-hello hello hizmetinin altında çalıştığı RunAs kullanıcı hesabı için listelenen denetlenir. Aksi takdirde http.sys erişim toohello hizmeti yok ve hello istemciden çağrıları hatalarıyla alın.
toolearn daha service fabric bakın, güvenlik ilkelerini etkinleştirmek [uygulamanız için güvenlik ilkelerini yapılandırmak](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-runas-security).

## <a name="reliable-actors-security-configuration"></a>Güvenilir aktörler güvenlik yapılandırması
Service Fabric Reliable Actors hello aktör tasarım deseni uygulamasıdır. Tüm yazılım tasarım deseni gibi hello düzeni toouse belirli bir desene olup yapılan olsun veya olmasın bir yazılım tasarım üzerinde sorun dayalı hello karar sığar.

Genel bir yönerge olarak hello aktör düzeni toomodel sorun veya senaryoyu göz önünde bulundurun:
-   Çok sayıda sorunu alanınızı içerir (binlerce veya daha fazla) küçük, bağımsız ve yalıtılmış birim durumu ve mantığı sayısı.
-   Dış bileşenlerinden aktörler kümesi boyunca durumu sorgulama dahil olmak üzere önemli etkileşim gerektirmeyen tek iş parçacıklı nesnelerle toowork istiyor.
-   Aktör örneklerinizi g/ç işlemleri vererek beklenmeyen gecikme ile arayanlar engellemez.

Service Fabric içinde aktörler hello Reliable Actors framework uygulanır: üstünde bir aktör desen tabanlı uygulama altyapısıdır [Service Fabric Reliable Services](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction). Yazdığınız her güvenilir aktör hizmeti aslında bir bölümlenmiş, durum bilgisi olan güvenilir hizmetidir.
Her aktör aktör türünün bir örneği tanımlanır, aynı toohello .NET nesnesi .NET türünün bir örneği yoludur. Örneğin, bir hesap makinesi hello işlevselliğini uygulayan bir aktör türü olabilir ve çeşitli düğümlerde küme genelinde dağıtılan birçok aktörler türü olabilir. Her tür aktör aktör kimliği ile benzersiz olarak tanımlanır

[Çoğaltıcı güvenlik yapılandırmalarını](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-kvsactorstateprovider-configuration) çoğaltma sırasında kullanılan kullanılan toosecure hello iletişim kanalını şunlardır. Bu hizmetler yüksek oranda kullanılabilir hale getirileceğini hello verileri de güvenli olduğundan emin olmanın birbirlerinin çoğaltma trafiği, göremeyeceği anlamına gelir. Varsayılan olarak, bir boş güvenlik yapılandırması bölümü çoğaltma güvenlik engeller.
Çoğaltıcı yapılandırmaları hello aktör durumu sağlayıcısı durumu yüksek oranda güvenilir yapmaktan sorumlu hello çoğaltıcı yapılandırın.

## <a name="configure-ssl-for-azure-service-fabric"></a>Azure Service Fabric için SSL yapılandırma

Sunucu kimlik doğrulaması: [kimlik doğrular](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) hello küme yönetim uç noktaları tooa management istemcisi, böylece hello management istemcisi, toohello gerçek küme Konuşmayı bilir. Bu sertifika ayrıca sağlar bir [SSL](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) hello HTTPS yönetim API'si ve Service Fabric Explorer HTTPS üzerinden.
Özel etki alanı adı, kümeniz için edinmeniz gerekir. Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, kümeniz için kullandığınız hello özel etki alanı adı eşleşmelidir.

SSL tooconfigure bir uygulama için öncelikle tooget tarafından bir sertifika yetkilisi (CA) kullanan bu amaç için sertifikaları veren güvenilen bir üçüncü taraf imzalanmış bir SSL sertifikası gerekir. Zaten bir yoksa, SSL sertifikaları sattığı bir şirketten tooobtain gerekir.

Merhaba sertifika Azure SSL sertifikaları için gereksinimler aşağıdaki hello karşılaması gerekir:
-   Merhaba sertifika özel anahtar içermelidir.
-   anahtar değişimi için dışarı aktarılabilir tooa kişisel bilgi değişimi (.pfx) dosyasını Hello sertifika oluşturulması gerekir.
-   Merhaba sertifikanın konu adı hello kullanılan etki alanı tooaccess hello bulut hizmeti eşleşmelidir. Merhaba cloudapp.net etki alanı için bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor. Özel etki alanı adı toouse almalıdır hizmetinizi eriştiğinizde. Bir CA'dan bir sertifika isteme, hello sertifikanın konu adı, uygulamanızın hello özel etki alanı adı kullanılan tooaccess eşleşmesi gerekir. Özel etki alanı adınız contoso.com ise, örneğin, bir sertifika, için CA'dan **. contoso.com** veya **www.contoso.com.**
-   Merhaba sertifika en az 2048 bit şifreleme kullanmanız gerekir.

HTTP güvenli değil ve hello hello web tarayıcısı toohello web sunucusundan veya diğer uç noktalar arasında aktarılan verilerin iletilen olduğundan düz metin olarak konu tooeavesdropping saldırıları. Bu, saldırganların kesecek ve kredi kartı ayrıntıları ve hesabın oturum açma bilgileri gibi hassas verileri görüntüleyebilir anlamına gelir. Veri gönderilen veya HTTPS kullanarak bir tarayıcı üzerinden gönderilen, SSL gibi bilgileri şifrelenmiş ve kişiler tarafından ele güvenli olmasını sağlar.

toolearn daha bakın, [azure uygulaması için SSL yapılandırma](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate).

## <a name="network-isolationsecurity-with-azure-service-fabric"></a>Ağ yalıtımı/Azure Service Fabric ile güvenliği
Kullanım [Azure Resource Manager (ARM) şablonu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) üç nodetype ayarlamak için örnek olarak ağ güvenlik grupları kullanarak gelen ve giden ağ trafiğini güvenli küme ve toocontrol hello.

Merhaba şablonu her hello sanal makine ölçek set(VMSS) toocontrol hello trafiği hello VMSS filtrelemek için bir ağ güvenlik grubu yok. Varsayılan olarak, hello kuralları tüm gerekli trafiği hello tooallow hello şablonunda belirtilen hello sistem hizmetleri ve hello uygulama bağlantı noktaları tarafından ayarlanır. Bu kuralları gözden geçirin ve değişiklikleri toofit gereksinimlerinizi olun, sonra da dahil olmak üzere, uygulamalarınız için yeni bir tane ekleyin.

Daha fazla bilgi için bkz: [Azure Service Fabric – genel ağ senaryoları](https://docs.microsoft.com/azure/service-fabric/service-fabric-patterns-networking).

## <a name="set-up-a-key-vault-for-security"></a>Bir anahtar kasası güvenlik için ayarlama
Sertifikaları Service Fabric tooprovide kimlik doğrulama ve şifreleme toosecure içinde kullanılan bir küme ve kendi uygulamalarına çeşitli yönlerini.

Service Fabric X.509 sertifikaları toosecure bir küme kullanır ve uygulama güvenlik özellikleri sağlar. Anahtar kasası çok kullandığınız[sertifikaları yönetme](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-update-certs-azure) Azure Service Fabric kümeleri için. Bir küme Azure'da dağıtıldığında, Service Fabric kümeleri oluşturmaktan sorumlu hello Azure kaynak sağlayıcısı sertifikaları anahtar Kasası'nı çeker ve VM'ler hello kümede yükler.

Merhaba arasındaki ilişki [Azure anahtar kasası](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault), service fabric kümesi ve küme oluşturduğunda, bir anahtar kasasında depolanan sertifika kullanan hello Azure kaynak sağlayıcısı.

**Bir kaynak grubu oluşturmak** hello ilk adımdır toocreate özellikle anahtar kasanız için bir kaynak grubu. Kendi kaynak grubuna hello anahtar kasası koymak öneririz. Bu eylem, Service Fabric kümesi anahtarları ve gizli anahtarları kaybetmeden içeren hello kaynak grubunu da dahil olmak üzere hello işlem ve depolama kaynak grupları, kaldırmanıza olanak sağlar. anahtar kasanızı içeren hello kaynak grubunu hello olmalıdır tarafından kullanıldığı hello küme aynı bölgede.

**Merhaba yeni kaynak grubunda bir anahtar kasası oluşturma** dağıtım tooallow işlem kaynak sağlayıcısı tooget sertifikaları dışarı hello ve sanal makine örneklerinde yüklemek için hello anahtar Kasası'nin etkinleştirilmesi gerekir.
Daha fazla nasıl tooset Azure anahtar kasası yukarı bakın, toolearn [Azure anahtar kasası ile çalışmaya başlama](https://docs.microsoft.com/azure/key-vault/key-vault-get-started).

## <a name="assign-users-roles"></a>Kullanıcıların rollerini atama
Merhaba uygulamaları toorepresent kümenizi oluşturduktan sonra kullanıcılarınızın Service Fabric tarafından desteklenen toohello rolleri ata: salt okunur ve yönetici Merhaba Klasik Azure portalı kullanarak hello roller atayabilirsiniz.

>[!Note]
> Service Fabric rolleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-security-roles).

Azure Service Fabric bağlı tooa istemciler için iki farklı erişim denetim türlerini destekler [Service Fabric kümesi](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm): Yönetici ve kullanıcı. Erişim denetimi hello Küme Yöneticisi toolimit erişim toocertain küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için sağlar.

## <a name="next-steps"></a>Sonraki adımlar
- Hizmet dokunuz ayarı [geliştirme ortamı](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started).
- Hakkında bilgi edinin [Service Fabric destek seçenekleri](https://docs.microsoft.com/azure/service-fabric/service-fabric-support).

