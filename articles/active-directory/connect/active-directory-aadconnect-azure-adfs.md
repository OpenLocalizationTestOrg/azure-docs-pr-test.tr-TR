---
title: aaaActive Azure Directory Federasyon Hizmetleri | Microsoft Docs
description: "Bu belgede, öğreneceksiniz nasıl toodeploy AD FS azure'da yüksek kullanılabilirlik için."
keywords: "azure AD FS'de dağıtmak, azure adfs, azure adfs, azure ad fs dağıtma, adfs dağıtımı, ad fs, adfs azure'da dağıtmak, adfs azure'da dağıtmak, AD FS dağıtma azure, adfs azure, Azure, Azure, AD FS'de giriş tooAD FS, ıaas, ADFS, adfs tooazure taşıma"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Azure'da Active Directory Federasyon Hizmetlerini dağıtma
AD FS basitleştirilmiş, güvenli kimlik federasyonu ve Web’de çoklu oturum açma (SSO) özellikleri sağlar. Azure AD ile Federasyon veya O365 kullanıcıların şirket içi kullanılarak tooauthenticate kimlik bilgileri ve buluttaki tüm kaynaklara erişim sağlar. Sonuç olarak, her iki şirket içi toohave yüksek oranda kullanılabilir bir AD FS altyapısı tooensure erişim tooresources önemli olur ve hello bulutta. AD FS'nin azure'da dağıtılması en az çaba ile Merhaba yüksek kullanılabilirlik elde etmeye yardımcı olabilir.
AD FS'yi Azure’da dağıtmanın çeşitli avantajları vardır ve birkaç tanesi aşağıda listelenmiştir:

* **Yüksek kullanılabilirlik** -Azure kullanılabilirlik kümeleri hello gücüyle, yüksek oranda kullanılabilir bir altyapıya sahip olabilirsiniz.
* **Kolay tooScale** – daha fazla performans mı gerekiyor? Azure'da yalnızca birkaç tıklama ile toomore güçlü makinelere kolayca geçiş
* **Çapraz coğrafi Yedeklilik** – ile Azure coğrafi olabilirsiniz altyapınızı Merhaba Dünya çapında yüksek oranda kullanılabilir olduğunu artıklık
* **Kolay tooManage** – Azure portalındaki oldukça basit yönetim seçenekleri ile altyapınızın Yönetimi çok kolay ve zahmetsizdir 

## <a name="design-principles"></a>Tasarım ilkeleri
![Dağıtım tasarımı](./media/active-directory-aadconnect-azure-adfs/deployment.png)

Yukarıdaki Hello diyagramda AD FS altyapınızı azure'a dağıtma temel topoloji toostart hello önerilen gösterir. Merhaba ilkeleri hello arkasında hello topolojinin çeşitli bileşenlerinin aşağıda listelenmiştir:

* **DC / ADFS Sunucuları**: 1.000’den az kullanıcınız varsa AD FS rolünü etki alanı denetleyicilerinize yükleyebilirsiniz. Merhaba etki alanı denetleyicileri üzerinde bir performans etkisi istemiyorsanız ya da 1. 000'den fazla kullanıcınız varsa AD FS'yi ayrı sunuculara dağıtın.
* **WAP sunucusu** – gerekli toodeploy Web uygulaması Proxy sunucuları, böylelikle kullanıcıların hello olmadıkları hello şirket ağında da AD FS ulaşabilirsiniz.
* **DMZ**: hello Web uygulaması Proxy sunucuları hello DMZ'ye yerleştirilir ve hello DMZ ile Merhaba iç alt ağ arasında yalnızca TCP/443 erişimine izin verilir.
* **Yük Dengeleyiciler**: AD FS ve Web uygulaması Proxy sunucularının yüksek kullanılabilirliğini tooensure, öneririz Web uygulaması Proxy sunucuları için AD FS sunucuları ve Azure yük dengeleyici için bir iç yük dengeleyici kullanarak.
* **Kullanılabilirlik kümeleri**: tooprovide artıklık tooyour AD FS dağıtımı, benzer iş yükleri için bir kullanılabilirlik kümesindeki iki veya daha fazla sanal makineyi gruplandırmanız önerilir. Bu yapılandırma planlı veya plansız bir bakım olayı sırasında en az bir sanal makinenin kullanılabilir olmasını sağlar
* **Depolama hesapları**: toohave iki depolama hesapları önerilir. Tek bir depolama hesabına sahip tek bir hata noktası toocreation açabilir ve hello dağıtım toobecome burada hello depolama hesabının arıza olası senaryoda kullanılamaz neden olabilir. İki depolama hesabı her bir hata satırı için bir depolama hesabını ilişkilendirmenize yardımcı olur.
* **Ağ ayrımı**: Web Uygulaması Proxy sunucuları ayrı bir DMZ ağına dağıtılmalıdır. Bir sanal ağı iki alt ağa bölebilir ve ardından hello Web uygulaması Proxy sunucularını yalıtılmış bir alt ağa dağıtabilirsiniz. Yalnızca, her alt ağ için hello ağ güvenlik grubu ayarlarını yapılandırmak ve yalnızca hello iki alt ağlar arasında gerekli iletişime izin verir. Aşağıda her dağıtım senaryosu için daha fazla bilgi verilmiştir

## <a name="steps-toodeploy-ad-fs-in-azure"></a>Adımları toodeploy azure'da AD FS
Bu bölümde anahat hello Kılavuzu toodeploy hello aşağıda belirtildiği hello adımları AD FS altyapısını Azure'a gösterilen.

### <a name="1-deploying-hello-network"></a>1. Merhaba ağ dağıtma
Yukarıda özetlendiği gibi tek bir sanal ağda iki alt ağ oluşturabilir veya birbirinden tamamen farklı iki sanal ağ (VNet) oluşturabilirsiniz. Bu makalede tek bir sanal ağın dağıtımına ve bu sanal ağı iki alt ağa bölmeye odaklanılacaktır. Bu şu anda iki ayrı Vnet iletişim için bir VNet tooVNet ağ geçidi gerektirecek şekilde daha kolay bir yaklaşımdır.

**1.1 Sanal ağ oluşturma**

![Sanal ağ oluşturma](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

Hello Azure portal, sanal ağ seçin ve hello sanal ağ ve bir alt ağı tek tıklamayla hemen dağıtabilirsiniz. Int alt ağı da tanımlanır ve eklenen VM'ler toobe için hazırdır.
Merhaba sonraki adıma tooadd başka bir alt ağ toohello, yani hello DMZ alt ağıdır. toocreate hello DMZ alt yeterlidir

* Yeni oluşturulan hello ağı seçin
* Merhaba özelliklerinde alt ağ seçin
* Ekle düğmesi hello üzerinde hello alt ağ panelini tıklatın
* Hello alt ağ adı ve adres alanı bilgilerini toocreate hello alt ağı belirtin

![Alt ağ](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![Alt ağ DMZ](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2. Merhaba ağ güvenlik grupları oluşturma**

Bir ağ güvenlik grubu (NSG) izin veren veya bir sanal ağ tooyour VM örnekleri ağ trafiği reddeden erişim denetimi listesi (ACL) kurallarının bir listesini içerir. NSG'ler alt ağlarla veya bu alt ağların içindeki tekil VM örnekleriyle ilişkili olabilir. Bir NSG'yi bir alt ağ ile ilişkili olduğunda hello ACL kuralları bu alt ağdaki tooall hello VM örnekleri uygulayın.
Bu kılavuz Hello amaçla iki Nsg'ler oluşturacağız: bir iç ağ ve DMZ için birer tane olmak. Bunlar sırasıyla NSG_INT ve NSG_DMZ olarak etiketlenecektir.

![NSG oluşturma](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

NSG oluşturulduktan hello sonra 0 gelen ve 0 giden kural olacaktır. Merhaba ilgili sunucularda Hello roller yüklenip çalışır olduktan sonra ardından hello gelen ve giden kuralları according istenen toohello düzeyde güvenlik yapılabilir.

![NSG başlatma](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

Merhaba Nsg'ler oluşturulduktan sonra nsg_ınt alt ağı ile ilişkilendirin INT ve alt ağ DMZ ile NSG_DMZ. Örnek bir ekran görüntüsü aşağıda verilmiştir:

![NSG yapılandırma](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* Alt ağlar tooopen hello paneli alt ağlar için tıklayın
* Merhaba NSG ile Merhaba alt tooassociate seçin 

Yapılandırmadan sonra alt ağlar hello paneli aşağıdaki gibi görünmelidir:

![NSG’den sonra alt ağlar](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3. Bağlantı tooon içi oluşturma**

Bir bağlantı tooon içi Azure sipariş toodeploy hello etki alanı denetleyicisi (DC) ihtiyacımız. Azure, şirket içi altyapı tooyour Azure altyapı çeşitli bağlantı seçenekleri tooconnect sunar.

* Noktadan siteye
* Sanal Ağ Sitesinden siteye
* ExpressRoute

Toouse ExpressRoute önerilir. ExpressRoute, Azure veri merkezleri ile şirketinizde veya bir birlikte bulundurma ortamında bulunan altyapı arasında özel bağlantılar oluşturmanızı sağlar. ExpressRoute bağlantıları hello Git değil genel Internet. Bunlar, hello Internet daha fazla güvenilirlik, yüksek hız, düşük gecikme ve normal bağlantıları daha yüksek güvenlik sağlar.
Toouse ExpressRoute önerilse de kuruluşunuz için en uygun olan bağlantı yöntemini seçebilirsiniz. ExpressRoute kullanan çeşitli bağlantı seçenekleri toolearn ExpressRoute ve hello hakkında daha fazla okuma [ExpressRoute teknik genel bakış](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Depolama hesabı oluşturma
Sipariş toomaintain yüksek kullanılabilirlik ve tek bir depolama hesabına bağımlılığı önlemek, iki depolama hesabı oluşturabilirsiniz. Merhaba makineler her kullanılabilirlik kümesinde iki gruba ayırın ve ardından her grubu ayrı bir depolama hesabına atayın.

![Depolama hesabı oluşturma](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Kullanılabilirlik kümeleri oluşturma
Her rol için (DC/AD FS ve WAP), 2 makineleri her hello minimum içeren kullanılabilirlik kümeleri oluşturun. Bunun yapılması her rol için daha yüksek kullanılabilirlik elde edilmesine yardımcı olur. Oluşturma hello kullanılabilirlik kümeleri oluşturulurken hello aşağıdaki üzerinde temel toodecide şöyledir:

* **Hata etki alanları**: sanal makinelerin aynı hata etki alanı paylaşımına hello hello aynı güç kaynağı ve fiziksel ağ anahtarı. En az 2 hata etki alanı önerilir. Bu dağıtım hello amaç için olduğu gibi bırakabilirsiniz ve 3 Hello varsayılan değeri.
* **Güncelleme etki alanları**: aynı güncelleme etki alanına birlikte güncelleştirme sırasında yeniden toohello ait makineler. Toohave en az 2 güncelleme etki alanına istiyor. Merhaba varsayılan değer 5'tir ve bu dağıtım hello amaç için olduğu gibi bırakılabilir

![Kullanılabilirlik kümeleri](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

Kullanılabilirlik kümeleri aşağıdaki hello oluşturma

| Kullanılabilirlik Kümesi | Rol | Hata etki alanları | Güncelleme etki alanları |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Sanal makineleri dağıtma
Merhaba sonraki adım altyapınızdaki farklı rolleri hello barındıracak toodeploy sanal makineleri olacaktır. Her kullanılabilirlik kümesinde en az iki makine olması önerilir. Merhaba temel dağıtımı için dört sanal makineler oluşturun.

| Makine | Rol | Alt ağ | Kullanılabilirlik kümesi | Depolama hesabı | IP Adresi |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |Statik |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |Statik |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |Statik |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |Statik |

Fark etmiş olabileceğiniz gibi hiçbir NSG belirtilmemiştir. Azure hello alt ağ düzeyinde NSG kullanmanıza olanak sağlayan olmasıdır. Daha sonra da hello alt ağ veya başka ile Merhaba NIC nesnesi tek NSG'yi ilişkili hello kullanarak makine ağ trafiği kontrol edebilirsiniz. [Ağ Güvenlik Grubu (NSG) nedir?](https://aka.ms/Azure/NSG) makalesinde daha fazla bilgi bulabilirsiniz.
Merhaba DNS yönetiyorsanız statik IP adresi önerilir. Azure DNS kullanabilir ve bunun yerine toohello yeni makinelere Azure Fqdn'lerine göre hello DNS kayıtlarını etki alanınız için bkz.
Merhaba dağıtım tamamlandıktan sonra sanal makine bölmeniz aşağıdaki gibi görünmelidir:

![Dağıtılmış Sanal Makineler](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5. Yapılandırma hello etki alanı denetleyicisi / AD FS sunucuları
 Sipariş tooauthenticate gelen bir isteğin, AD FS toocontact hello etki alanı denetleyicisi gerekir. toosave hello gelen kimlik doğrulaması için Azure tooon içi DC'ye maliyetli seyahat önerilir toodeploy azure'da hello etki alanı denetleyicisinin çoğaltma. Sipariş tooattain yüksek kullanılabilirlik, en az 2 etki alanı denetleyicilerini kullanılabilirlik kümesi toocreate önerilir.

| Etki alanı denetleyicisi | Rol | Depolama hesabı |
|:---:|:---:|:---:|
| contosodc1 |Çoğaltma |contososac1 |
| contosodc2 |Çoğaltma |contososac2 |

* Hello iki sunucuyu DNS ile çoğaltma etki alanı denetleyicisi olarak Yükselt
* Merhaba Sunucu Yöneticisi'ni kullanarak hello AD FS rolünü yükleyerek Hello AD FS sunucularını yapılandırın.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. İç Yük Dengeleyici’yi (ILB) Dağıtma
**6.1. Merhaba ILB oluşturma**

bir ILB toodeploy, yük Dengeleyiciler'i seçin hello Azure portal ve tıklayın (+) ekleyin.

> [!NOTE]
> görmüyorsanız, **yük Dengeleyiciler** menünüzde tıklatın **Gözat** hello hello portalının sol alt ve görene kadar kaydırın **yük dengeleyici**.  Merhaba sarı yıldız tooadd ardından onu tooyour menüsü. Şimdi hello Yeni Yük Dengeleyici simgesini tooopen hello paneli toobegin yapılandırması hello yük dengeleyicinin seçin.
> 
> 

![Yük dengeleyiciye göz atma](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **Ad**: tüm uygun bir ad toohello yük dengeleyici verin
* **Düzeni**: Bu yük dengeleyici hello AD FS sunucularının önüne yerleştirilir ve iç ağ bağlantıları yalnızca "Dahili" seçmek için tasarlanmıştır
* **Sanal ağ**: AD FS dağıttığınız hello sanal ağ seçin
* **Alt ağ**: hello burada dahili alt ağı seçin
* **IP Adresi ataması**: Statik

![İç yük dengeleyici](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

' İ tıklattıktan sonra oluşturmak ve hello ILB dağıtılan hello yük Dengeleyiciler listesinde görmeniz gerekir:

![ILB’den sonra yük dengeleyiciler](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

Sonraki adımdır tooconfigure hello arka uç havuzu ve hello arka uç araştırmasının.

**6.2. ILB arka uç havuzunu yapılandırma**

Select hello ILB hello yük Dengeleyiciler panelinde yeni oluşturulan. Merhaba ayarlar paneli açılır. 

1. Merhaba ayarlar panelinden arka uç havuzlarını seçin
2. Arka uç havuzu paneli Hello eklemek için sanal makine Ekle'ye tıklayın
3. Kullanılabilirlik kümesi seçebileceğiniz bir panel açılır
4. Merhaba AD FS kullanılabilirlik kümesi seçin

![ILB arka uç havuzunu yapılandırma](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3. Araştırmayı yapılandırma**

Merhaba ILB Ayarları panelinde araştırmalar'ı seçin.

1. Ekle'ye tıklayın
2. Araştırmanın ayrıntılarını belirtin a. **Ad**: Araştırmanın adı b. **Protokol**: TCP c. **Bağlantı noktası**: 443 (HTTPS) d. **Aralığı**: 5 (varsayılan değer) – bu ise, ILB araştırma hello arka uç havuzu e hello makinelerinizde hello aralığı. **Sağlıksız eşik sınırı**: (varsayılan val ue) 2 – geçmesi ILB bildirme bir makine hello arka uç havuzu duyuracağı ve Dur gönderen trafiği tooit içinde ardışık araştırma hataları hello eşiğinin budur.

![ILB araştırmasını yapılandırma](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4. Yük dengeleme kuralları oluşturma**

Sipariş tooeffectively Bakiye hello trafiği, hello ILB'nin Yük Dengeleme kuralları ile yapılandırılması gerekir. Sipariş toocreate Yük Dengeleme kuralı, 

1. Yük Dengeleme kuralı hello ILB, hello ayarlar panelinden seçin
2. Hello Yük Dengeleme kuralı panelinde Ekle'ye tıklayın
3. Merhaba Ekle Yük Dengeleme kuralı panelinde bir. **Ad**: hello kuralı b için bir ad sağlayın. **Protokol**: TCP seçin c. **Bağlantı noktası**: 443 d. **Arka uç bağlantı noktası**: 443 e. **Arka uç havuzu**: hello AD FS kümesi önceki f için oluşturduğunuz hello havuzunu seçin. **Araştırma**: AD FS sunucuları için daha önce oluşturduğunuz Select hello araştırma

![ILB dengeleme kurallarını yapılandırma](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5. ILB ile DNS güncelleme**

Tooyour DNS sunucusu gidin ve hello ILB için bir CNAME oluşturun. Merhaba CNAME hello Federasyon Hizmeti için hello ILB toohello IP adresini işaret eden hello IP adresi olmalıdır. Merhaba ILB DIP adresi 10.3.0.8 ve yüklü hello Federasyon Hizmeti örneğin fs.contoso.com için too10.3.0.8 işaret eden fs.contoso.com için bir CNAME oluşturun.
Bu, tüm fs.contoso.com sonunda hello ILB ilişkin iletişim ve olan uygun şekilde yönlendirilmesini güvence altına alır.

### <a name="7-configuring-hello-web-application-proxy-server"></a>7. Merhaba Web Uygulama Proxy sunucusunu yapılandırma
**7.1. Merhaba Web uygulaması Proxy sunucuları tooreach AD FS sunucularını yapılandırma**

Web uygulaması Proxy sunucuları hello ILB'nin arkasındaki mümkün tooreach hello AD FS sunucuları olduğunu sipariş tooensure içinde hello %systemroot%\system32\drivers\etc\hosts hello ILB için bir kayıt oluşturun. Ayırt edici ad (DN) hello Not hello Federasyon Hizmeti adı, örneğin fs.contoso.com olmalıdır. Ve hello IP girişi, hello ILB'nin IP adresi (Merhaba örnekte olduğu gibi 10.3.0.8) olmalıdır.

**7.2. Merhaba Web uygulaması Proxy rolünü yükleme**

Web uygulaması Proxy sunucularının ILB'nin arkasındaki mümkün tooreach hello AD FS sunucularının olduğundan emin olduktan sonra sonraki hello Web uygulaması Proxy sunucularını yükleyebilirsiniz. Web uygulaması Proxy sunucuları birleştirilmiş toohello etki alanı olması. Merhaba Web uygulaması Proxy rollerini hello uzaktan erişim rolünü seçerek hello iki Web uygulaması Proxy sunucusuna yükleyin. Merhaba Sunucu Yöneticisi'ni toocomplete hello WAP yüklemesini yol gösterecektir.
Hakkında daha fazla bilgi için toodeploy WAP, okuma [yükleme ve başlangıç Web uygulaması Ara sunucusu yapılandırma](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.  Merhaba Internet'e yönelik (Genel) yük dengeleyici dağıtımı
**8.1.  İnternet’e Yönelik (Genel) Yük Dengeleyici oluşturma**

Hello Azure portal, yük Dengeleyiciler seçin ve ardından Ekle'ye tıklayın. Merhaba oluşturma yük dengeleyici Masası'nda aşağıdaki bilgilerle hello girin

1. **Ad**: hello yük dengeleyicinin adı
2. **Düzen**: Genel – Bu seçenek Azure’a bu yük dengeleyicinin genel erişime açık olması gerektiğini söyler.
3. **IP Adresi**: Yeni bir IP adresi (dinamik) oluşturun

![İnternet'e yönelik yük dengeleyici](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

Dağıtımdan sonra hello yük dengeleyici hello yük Dengeleyiciler listesinde görünür.

![Yük dengeleyici listesi](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2. Bir DNS etiketi toohello genel IP atayın**

Merhaba yük Dengeleyiciler panelinde toobring hello paneli yapılandırma yukarı hello yeni oluşturulan yük dengeleyici girişine tıklayın. Altındaki adımları tooconfigure hello DNS etiketini genel IP için hello izleyin:

1. Merhaba ortak IP adresine tıklayın. Bu hello hello genel IP paneli ve ayarları açılır
2. Yapılandırma’ya tıklayın
3. Bir DNS etiketi belirtin. Bu, her yerden, contosofs.westus.cloudapp.azure.com erişebileceği hello Genel DNS etiketi olur. Bir giriş ekleyebilirsiniz hello dış DNS hello dış toohello DNS etiketi çözümler hello Federasyon Hizmeti (like fs.contoso.com) için yük dengeleyici (contosofs.westus.cloudapp.azure.com).

![İnternet'e yönelik yük dengeleyiciyi yapılandırma](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![İnternet'e yönelik yük dengeleyiciyi yapılandırma (DNS)](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3. İnternet’e Yönelik (Genel) Yük Dengeleyici için arka uç havuzunu yapılandırma** 

Aynı adımlar hello iç yük dengeleyici oluşturma olduğu gibi izleme hello tooconfigure hello arka uç havuzu için Internet'e yönelik (Genel) yük dengeleyici hello kullanılabilirlik olarak hello WAP sunucularının ayarlayın. Örneğin, contosowapset.

![İnternet’e Yönelik Yük Dengeleyicinin arka uç havuzunu yapılandırma](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4. Araştırmayı yapılandırma**

Merhaba hello iç yük dengeleyici tooconfigure hello araştırması hello arka uç havuzunu WAP sunucularının için yapılandırma olduğu gibi aynı adımları izleyin.

![İnternet'e Yönelik Yük Dengeleyici araştırmasını yapılandırma](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5. Yük dengeleme kuralları oluşturma**

ILB tooconfigure hello Yük Dengeleme olduğu gibi aynı adımları TCP 443 kural hello izleyin.

![İnternet’e Yönelik Yük Dengeleyicinin dengeleme kurallarını yapılandırma](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9. Merhaba ağ güvenliğini sağlama
**9.1. Merhaba iç alt ağ güvenliğini sağlama**

Genel olarak, tooefficiently (sırayla aşağıda listelenen hello) dahili alt ağınızın güvenliğini kuralları aşağıdaki hello gerekir

| Kural | Açıklama | Akış |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Merhaba HTTPS iletişimi çevre ağından izin ver |Gelen |
| DenyInternetOutbound |Hiçbir erişim toointernet |Giden |

![INT access rules (inbound)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[comment]: <> (![INT access rules (inbound)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [comment]: <> (![INT access rules (outbound)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2. Merhaba DMZ alt ağ güvenliğini sağlama**

| Kural | Açıklama | Akış |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |Internet toohello DMZ HTTPS izin ver |Gelen |
| DenyInternetOutbound |HTTPS toointernet dışında herhangi bir şey engellenir |Giden |

![EXT access rules (inbound)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[comment]: <> (![EXT access rules (inbound)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [comment]: <> (![EXT access rules (outbound)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> İstemci kullanıcı sertifikası kimlik doğrulaması (X509 kullanıcı sertifikaları kullanan clientTLS kimlik doğrulaması) gerekliyse AD FS, gelen erişim için TCP bağlantı noktası 49443’ün etkinleştirilmesini gerektirir.
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10. Merhaba AD FS oturum açmayı test etme
Merhaba kolay AD FS hello Idpınitiatedsignon.aspx sayfasının kullanmaktır tootest yoludur. Gerekli tooenable olduğundan, sipariş toobe mümkün toodo içinde IdpInitiatedSignOn hello AD FS özellikleri hello. AD FS kurulumunuzu tooverify Hello adımları izleyin

1. Çalışma hello aşağıdaki cmdlet'i hello AD FS sunucusunda PowerShell, tooset kullanarak, onu tooenabled.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. Herhangi bir dış makineden https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx sayfasına erişin  
3. Merhaba AD FS sayfasını görmelisiniz aşağıdaki gibi:

![Oturum açma sayfasını test etme](./media/active-directory-aadconnect-azure-adfs/test1.png)

Oturum açma başarılı olduğunda aşağıdaki gibi bir başarı iletisi gösterilir:

![Test başarılı](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Azure'da AD FS dağıtma şablonu
Merhaba şablon 6 makine Kurulum, 2 her etki alanı denetleyicileri, AD FS ve WAP dağıtır.

[Azure Dağıtım Şablonu'nda AD FS](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Bu şablonu dağıtırken var olan bir sanal ağı kullanabilir veya yeni bir sanal ağ oluşturabilirsiniz. Merhaba hello dağıtımı özelleştirmek için kullanılabilen çeşitli parametreleri hello dağıtım işlemindeki hello parametresinin kullanımının hello açıklamasıyla aşağıda listelenmiştir. 

| Parametre | Açıklama |
|:--- |:--- |
| Konum |Merhaba bölge toodeploy hello kaynakları, örneğin Doğu ABD. |
| StorageAccountType |Merhaba depolama hesabı oluşturuldu Hello türü |
| VirtualNetworkUsage |Var olan sanal ağın kullanılıp kullanılmayacağını veya yeni bir sanal ağın oluşturulup oluşturulmayacağını belirtir |
| VirtualNetworkName |Merhaba sanal ağ tooCreate, mevcut veya yeni sanal ağ kullanımını zorunlu Hello adı |
| VirtualNetworkResourceGroupName |Merhaba hello varolan sanal ağ bulunduğu hello kaynak grubunun adını belirtir. Merhaba dağıtım hello varolan sanal ağ hello Kimliğini bulabilmek için var olan bir sanal ağ kullanırken, bu zorunlu bir parametre olur. |
| VirtualNetworkAddressRange |Merhaba hello adres aralığı yeni VNET, yeni bir sanal ağ oluşturuyorsanız zorunlu |
| InternalSubnetName |Merhaba iç alt ağ, her iki sanal ağ kullanım seçenekleri (yeni veya varolan) zorunlu Hello adı |
| InternalSubnetAddressRange |Yeni bir sanal ağ oluşturma hello etki alanı denetleyicileri ve ADFS sunucuları, zorunlu varsa hello iç alt Hello adres aralığı. |
| DMZSubnetAddressRange |Merhaba Windows uygulaması proxy sunucuları, yeni bir sanal ağ oluşturuyorsanız zorunlu içeren hello dmz alt Hello adres aralığı. |
| DMZSubnetName |Merhaba iç alt ağ, her iki sanal ağ kullanım seçenekleri (yeni veya varolan) zorunlu Hello adı. |
| ADDC01NICIPAddress |Merhaba iç IP adresi Merhaba ilk etki alanı denetleyicisi, bu IP adresi toohello DC statik olarak atanmış olması ve hello iç alt ağ içindeki geçerli IP adresi olmalıdır |
| ADDC02NICIPAddress |Merhaba iç IP adresi Merhaba ikinci etki alanı denetleyicisi, bu IP adresi toohello DC statik olarak atanmış olması ve hello iç alt ağ içindeki geçerli IP adresi olmalıdır |
| ADFS01NICIPAddress |Merhaba iç IP adresi hello ilk ADFS sunucusunun bu IP adresi statik olarak toohello ADFS sunucusuna atanır ve hello iç alt ağ içindeki geçerli IP adresi olmalıdır |
| ADFS02NICIPAddress |Hello iç IP adresi hello ikinci ADFS sunucusu, bu IP adresi statik olarak toohello ADFS sunucusuna atanır ve hello iç alt ağ içindeki geçerli IP adresi olmalıdır |
| WAP01NICIPAddress |Merhaba iç IP adresi hello ilk WAP sunucusunun, bu IP adresi toohello WAP sunucusu statik olarak atanır ve hello DMZ alt ağ içindeki geçerli IP adresi olmalıdır |
| WAP02NICIPAddress |Merhaba iç IP adresi hello ikinci WAP sunucusunun, bu IP adresi toohello WAP sunucusu statik olarak atanır ve hello DMZ alt ağ içindeki geçerli IP adresi olmalıdır |
| ADFSLoadBalancerPrivateIPAddress |Merhaba ADFS Hello iç IP adresini yük dengeleyici, bu IP adresi toohello yük dengeleyicisi statik olarak atanmış olması ve hello iç alt ağ içindeki geçerli IP adresi olmalıdır |
| ADDCVMNamePrefix |Etki Alanı Denetleyicileri için Sanal Makine adı ön eki |
| ADFSVMNamePrefix |AD FS sunucuları için Sanal Makine adı ön eki |
| WAPVMNamePrefix |WAP sunucuları için Sanal Makine adı ön eki |
| ADDCVMSize |Merhaba etki alanı denetleyicileri Hello vm boyutu |
| ADFSVMSize |Merhaba ADFS sunucuları Hello vm boyutu |
| WAPVMSize |Merhaba WAP sunucularının Hello vm boyutu |
| AdminUserName |Merhaba adını hello hello sanal makinelerin yerel yönetici |
| AdminPassword |Merhaba hello hello sanal makinelerde yerel yönetici hesabı parolasını |

## <a name="additional-resources"></a>Ek kaynaklar
* [Kullanılabilirlik Kümeleri](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [İç yük dengeleyici](https://aka.ms/Azure/ILB/Internal)
* [İnternet'e Yönelik Yük Dengeleyici](https://aka.ms/Azure/ILB/Internet)
* [Depolama hesapları](https://aka.ms/Azure/Storage)
* [Azure Sanal Ağları](https://aka.ms/Azure/VNet)
* [AD FS ve Web Uygulaması Proxy Bağlantıları](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Sonraki adımlar
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
* [Azure AD Connect kullanarak AD FS’yi yapılandırma ve yönetme](active-directory-aadconnectfed-whatis.md)
* [Azure Traffic Manager ile Azure’da yüksek kullanılabilirliğe sahip çapraz coğrafi AD FS dağıtımı](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

