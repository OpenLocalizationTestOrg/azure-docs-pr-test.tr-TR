---
title: "aaaCreate Service Fabric kümesi hello Azure portalı | Microsoft Docs"
description: "Bu makalede, Azure kullanarak güvenli bir Service Fabric kümesi tooset nasıl hello Azure portalı ve Azure anahtar kasası açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Azure'da hello Azure portal kullanarak bir Service Fabric kümesi oluştur
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Azure portal](service-fabric-cluster-creation-via-portal.md)
> 
> 

Hello Azure portal kullanarak azure'da güvenli bir Service Fabric kümesi ayarlama hello adımlarını anlatan bir adım adım kılavuz budur. Bu kılavuz, aşağıdaki adımları hello açıklanmaktadır:

* Anahtar kasası toomanage anahtarlarını küme güvenlik ayarlayın.
* Güvenli bir küme Azure'da hello Azure portal oluşturun.
* Yöneticiler sertifikaları kullanarak kimlik doğrulaması.

> [!NOTE]
> Azure Active Directory ile kullanıcı kimlik doğrulaması ve uygulama güvenliği için sertifikalar ayarlama gibi daha gelişmiş güvenlik seçenekleri için [Azure Kaynak Yöneticisi'ni kullanarak kümenizi oluşturduktan][create-cluster-arm].
> 
> 

Güvenli bir küme dağıtma, yükseltme ve uygulamaları, hizmetleri ve içerdikleri hello veri silme içeren yetkisiz erişim toomanagement işlemleri engelleyen bir kümedir. Güvenli olmayan bir küme herkes tooat dilediğiniz zaman bağlanmak ve böylelikle yönetim işlemlerini gerçekleştirmek bir kümedir. Olası toocreate güvenli olmayan bir küme olmasına rağmen olan **güvenli küme toocreate tavsiye**. Güvenli olmayan bir küme **daha sonra korunamıyor** -yeni bir küme oluşturulması gerekir.

Merhaba kavramları olan hello güvenli küme hello kümeleri Linux kümeleri veya Windows kümeleri oluşturmak için aynı. Güvenli Linux kümeleri oluşturmak için daha fazla bilgi ve yardımcı komut dosyaları için lütfen bkz. [Linux'ta güvenli küme oluşturma](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Merhaba hello Yardımcısı betiği tarafından sağlanan elde parametreleri hello Portalı'na doğrudan hello bölümde açıklandığı gibi girilebilir [hello Azure portal bir küme oluşturmak](#create-cluster-portal).

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum
Bu kılavuzu kullanır [Azure PowerShell][azure-powershell]. Yeni bir PowerShell oturumu başlatılırken tooyour içinde Azure hesabınızı ve oturum Azure komutları çalıştırmadan önce aboneliğinizi seçin.

Tooyour azure hesabında oturum:

```powershell
Login-AzureRmAccount
```

Aboneliğinizi seçin:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Anahtar Kasası ayarlama
Başlangıç Kılavuzu'nun bu bölümü Service Fabric uygulamaları ve Azure Service Fabric kümesi için bir anahtar kasası oluşturmada size yol gösterir. Anahtar kasası üzerinde tam bir kılavuz için bkz: Merhaba [anahtar kasası kullanmaya başlama Kılavuzu][key-vault-get-started].

Service Fabric X.509 sertifikaları toosecure bir küme kullanır. Azure anahtar kasası Azure Service Fabric kümeleri için kullanılan toomanage sertifikaları olur. Bir küme Azure'da dağıtıldığında hello Azure kaynak sağlayıcısı Service Fabric kümeleri oluşturmak için sorumlu sertifikaları anahtar Kasası'nı çeker ve VM'ler hello kümede yükler.

Merhaba Aşağıdaki diyagramda hello anahtar kasası, Service Fabric kümesi ve küme oluşturduğunda, anahtar kasasında depolanan sertifika kullanan hello Azure kaynak sağlayıcısı arasındaki ilişki gösterilmektedir:

![Sertifika Yükleme][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Kaynak Grubu oluşturma
Merhaba ilk adımı toocreate özellikle anahtar kasası için yeni bir kaynak grubu oluşturur. İşlem ve depolama kaynak grupları - gibi Service Fabric kümesi olan hello kaynak grubuna - kaldırabilmeniz anahtar kasası, kendi kaynak grubuna koyma anahtarları ve gizli anahtarları kaybetmeden önerilir. Anahtar kasası olan hello kaynak grubuna hello olmalıdır tarafından kullanıldığı hello küme aynı bölgede.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Anahtar kasası oluşturma
Bir anahtar kasası hello yeni kaynak grubu oluşturun. Merhaba anahtar kasası **dağıtımı için etkinleştirilmelidir** tooallow Service Fabric kaynak sağlayıcısı tooget sertifikaları dışarı hello ve küme düğümlerine yükleyin:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

Var olan bir anahtar kasası varsa Azure CLI kullanarak dağıtım için etkinleştirebilirsiniz:

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Sertifikaları tooKey kasası ekleme
Sertifikaları Service Fabric tooprovide kimlik doğrulama ve şifreleme toosecure içinde kullanılan bir küme ve kendi uygulamalarına çeşitli yönlerini. Service Fabric sertifikaların nasıl kullanıldığını daha fazla bilgi için bkz: [Service Fabric kümesi güvenlik senaryoları][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Küme ve sunucu sertifikası (gerekli)
Bu sertifika, gerekli toosecure bir kümedir ve yetkisiz erişim tooit engelleyebilirsiniz. Birkaç yolla küme güvenlik sağlar:

* **Küme kimlik doğrulaması:** düğümü düğümü iletişimin küme Federasyon kimlik doğrulamasını yapar. Yalnızca bu sertifikayla kimliğini kanıtlamak düğümleri hello kümeye katılabilir.
* **Sunucu kimlik doğrulaması:** hello management istemcisi, toohello gerçek küme Konuşmayı bilir böylece hello küme yönetim uç noktaları tooa yönetim istemci kimliğini doğrular. Bu sertifika de SSL hello HTTPS yönetim API'si ve Service Fabric Explorer için HTTPS üzerinden sağlar.

tooserve bu amacıyla, hello sertifika hello aşağıdaki gereksinimleri karşılamalıdır:

* Merhaba sertifika özel anahtar içermelidir.
* anahtar değişimi için dışarı aktarılabilir tooa kişisel bilgi değişimi (.pfx) dosyasını Hello sertifika oluşturulması gerekir.
* Merhaba sertifikanın konu adı hello kullanılan etki alanı tooaccess hello Service Fabric kümesi eşleşmelidir. Merhaba kümenin HTTPS yönetim uç noktaları ve Service Fabric Explorer için gerekli tooprovide SSL budur. Hello için bir sertifika yetkilisinden (CA) bir SSL sertifikası elde edemiyor `.cloudapp.azure.com` etki alanı. Kümeniz için özel etki alanı adı satın alır. İstediğinde bir CA hello sertifikanın konu adındaki bir sertifika, kümeniz için kullanılan hello özel etki alanı adı eşleşmelidir.

### <a name="client-authentication-certificates"></a>İstemci kimlik doğrulama sertifikaları
Ek istemci sertifikalarını Yöneticiler küme yönetim görevleri için kimlik doğrulaması. Service Fabric sahip iki erişim düzeyleri: **yönetici** ve **salt okunur kullanıcı**. En azından, yönetici erişimi için tek bir sertifika kullanılması gerekir. Ek kullanıcı düzeyinde erişim için ayrı bir sertifika sağlanmalıdır. Erişim rolleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi][service-fabric-cluster-security-roles].

Service Fabric ile tooupload istemci kimlik doğrulama sertifikaları tooKey kasa toowork gerekmez. Bu sertifikalar yalnızca yetkili toousers küme yönetimi için sağlanan toobe gerekir. 

> [!NOTE]
> Azure Active Directory hello yolu tooauthenticate istemciler için küme yönetimi işlemleri önerilen ' dir. Azure Active Directory toouse, şunları yapmalısınız [Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturmak][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Uygulama sertifikaları (isteğe bağlı)
Ek sertifikaların herhangi bir sayıda uygulama güvenlik amacıyla bir kümede yüklenebilir. Kümenizi oluşturmadan önce hello düğümlerinde gibi yüklü bir sertifika toobe gerektiren hello güvenlik senaryolarını göz önünde bulundurun:

* Şifreleme ve şifre çözme uygulama yapılandırma değerleri
* Çoğaltma sırasında düğümler arasında veri şifreleme 

Uygulama sertifikaları hello Azure portal aracılığıyla bir küme oluştururken yapılandırılamaz. Küme kurulumu zaman tooconfigure uygulama sertifikalar, şunları yapmalısınız [Azure Kaynak Yöneticisi'ni kullanarak bir küme oluşturmak][create-cluster-arm]. Oluşturulduktan sonra uygulama sertifikaları toohello küme de ekleyebilirsiniz.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Azure kaynak sağlayıcısı kullanmak için sertifikaları biçimlendirme
Özel anahtar dosyaları (.pfx) eklenir ve doğrudan anahtar kasası kullanılır. Ancak, bir base-64 kodlanmış dize ve hello özel anahtar parolası olarak hello .pfx içeren özel bir JSON biçiminde depolanan anahtarları toobe hello Azure kaynak sağlayıcısı gerektirir. Bu gereksinimler, anahtarları bir JSON dizesinde yerleştirilir ve olarak depolanan tooaccommodate *gizli* anahtar Kasası'nda.

Bu işlem daha kolay toomake PowerShell modülüdür [github'da][service-fabric-rp-helpers]. Bu adımları toouse hello modülü izleyin:

1. Merhaba depodaki tüm içeriğini Hello bir yerel dizine indirin. 
2. PowerShell penceresinde Hello modülünü içeri aktarın:

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Merhaba `Invoke-AddCertToKeyVault` bu PowerShell modülünü komutu otomatik olarak bir sertifika özel anahtarı bir JSON dizeye biçimlendirir ve tooKey kasası yükler. Tooadd hello küme sertifika ve tüm ek uygulama sertifikaları tooKey kasası kullanın. Kümenizdeki tooinstall istediğiniz ek sertifika için bu adımı yineleyin.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Bunlar düğümü kimlik doğrulaması, yönetim uç noktası güvenlik ve kimlik doğrulama ve tüm ek uygulama güvenliği için sertifikaları yükler bir Service Fabric kümesi Resource Manager şablonu yapılandırmak için tüm hello anahtar kasası önkoşulları X.509 sertifikaları kullanan özellikler. Bu noktada, Azure kurulumunda aşağıdaki hello şimdi olmalıdır:

* Anahtar kasası kaynak grubu
  * Anahtar Kasası
    * Küme sunucu kimlik doğrulama sertifikası

< /a "oluşturma-küme-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Hello Azure portal kümesi oluşturma
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Service Fabric küme kaynağı Hello için arama
![Service Fabric kümesi hello Azure portal şablona arayın.][SearchforServiceFabricClusterTemplate]

1. İçinde toohello oturum [Azure portal][azure-portal].
2. Tıklatın **yeni** tooadd yeni bir kaynak şablonu. Arama hello hello Service Fabric kümesi şablonunun **Market** altında **her şeyi**.
3. Seçin **Service Fabric kümesi** hello listeden.
4. Toohello gidin **Service Fabric kümesi** dikey penceresinde tıklatın **oluşturma**,
5. Merhaba **oluşturma Service Fabric kümesi** dikey penceresinde hello aşağıdaki dört adımları vardır.

#### <a name="1-basics"></a>1. Temel Bilgiler
![Yeni bir kaynak grubu oluşturma ekran görüntüsü.][CreateRG]

Merhaba temel bilgileri dikey penceresinde, kümeniz için tooprovide hello temel ayrıntıları gerekir.

1. Merhaba, kümenin adını girin.
2. Girin bir **kullanıcı adı** ve **parola** hello VM'ler için Uzak Masaüstü.
3. Tooselect hello emin olun **abonelik** özellikle birden çok aboneliğiniz varsa, dağıtılmış, küme toobe istiyor.
4. Oluşturma bir **yeni kaynak grubu**. Bunu hello hello küme adıyla aynı özellikle toomake değişiklikleri tooyour dağıtım çalıştığınız veya kümenizi sildiğinizden bunları daha sonra bulma yardımcı olan bu yana en iyi toogive olur.
   
   > [!NOTE]
   > Varolan bir kaynak grubu toouse karar verebilirsiniz rağmen iyi bir uygulama toocreate yeni bir kaynak grubu var. Bu işlem, ihtiyacınız olmayan kolay toodelete kümeleri kolaylaştırır.
   > 
   > 
5. Select hello **bölge** toocreate hello küme istiyor. Anahtarınızı kasa aynı bölgede yer hello kullanmanız gerekir.

#### <a name="2-cluster-configuration"></a>2. Küme yapılandırması
![Düğüm türü oluşturma][CreateNodeType]

Küme düğümlerinizi yapılandırın. Düğüm türleri hello VM boyutları, VM'ler hello sayısını ve bunların özelliklerini tanımlar. Kümenizi birden fazla olabilir düğüm türü, ancak hello birincil düğüm türü (Merhaba hello portalında tanımlayan birinci) olması gerekir en az beş VM'ler, bu Service Fabric Sistem Hizmetleri yerleştirildiği hello düğüm türü olduğu gibi. Yapılandırmayın **yerleşim özellikleri** çünkü "nodetypename"adlı bir varsayılan yerleştirme özelliği otomatik olarak eklenir.

> [!NOTE]
> Yaygın bir senaryo birden çok düğüm türü için bir ön uç hizmeti ve arka uç hizmeti içeren bir uygulamadır. Tooput hello ön uç hizmeti bağlantı noktalarını açık toohello Internet küçük sanal makineleri (örneğin, D2 VM boyutları) üzerinde istediğiniz, ancak isterseniz tooput hello arka uç hizmetine (ile VM boyutları D4, D6, D15 vb. gibi) daha büyük sanal makineleri üzerinde hiçbir İnternete bağlantı açık.
> 
> 

1. Düğüm türünüz (1 too12 karakterler yalnızca harfler ve sayılar içeren) için bir ad seçin.
2. Hello minimum **boyutu** VM'lerin hello birincil düğüm türü hello tarafından yönetilir **dayanıklılık** katmanı hello küme için seçin. Merhaba hello dayanıklılık katmanı için Bronz varsayılandır. Dayanıklılık hakkında daha fazla bilgi için bkz: [nasıl toochoose hello Service Fabric kümesi güvenilirlik ve dayanıklılık][service-fabric-cluster-capacity].
3. Merhaba VM boyutu ve fiyatlandırma katmanı seçin. D-serisi VM'ler SSD sürücülerine sahip ve durum bilgisi olan uygulamalar için tavsiye edilir. Kısmi çekirdeğe sahip tüm VM SKU kullanın veya değil 7 GB kullanılabilir disk kapasiteleri daha az sahip. 
4. Merhaba minimum **numarası** VM'lerin hello birincil düğüm türü hello tarafından yönetilir **güvenilirlik** seçtiğiniz katmanı. Merhaba hello güvenilirlik katmanı için Gümüş varsayılandır. Güvenilirliği hakkında daha fazla bilgi için bkz: [nasıl toochoose hello Service Fabric kümesi güvenilirlik ve dayanıklılık][service-fabric-cluster-capacity].
5. Merhaba hello düğüm türü için VM sayısını seçin. Yukarı veya aşağı hello sayısında VM'ler düğüm türü daha sonra ölçeklendirebilirsiniz ancak hello birincil düğüm türüne hello minimum seçmiş olduğunuz hello güvenilirlik düzeyi tarafından yönetilir. Diğer düğüm türleri, en az 1 VM olabilir.
6. Özel uç noktaları yapılandırın. Bu alan tooenter tooexpose hello Azure yük dengeleyici toohello aracılığıyla istediğiniz bağlantı noktalarının virgülle ayrılmış bir liste sağlar, uygulamalarınız için genel Internet. Bir web uygulaması tooyour küme toodeploy düşünüyorsanız, örneğin, "80" Buraya girdiğiniz bağlantı noktası 80, kümesine tooallow trafiğine. Uç noktalar hakkında daha fazla bilgi için bkz: [uygulamaları ile iletişim][service-fabric-connect-and-communicate-with-services]
7. Küme yapılandırma **tanılama**. Varsayılan olarak, tanılama sorunlarını giderme ile küme tooassist üzerinde etkindir. Toodisable tanılama hello değiştirmek istiyorsanız **durum** çok geçiş**devre dışı**. Tanılama kapatma olan **değil** önerilir.
8. Hello doku yükseltme kümesi istediğiniz modu seçin. Seçin **otomatik**, hello sistem tooautomatically çekme hello en son sürüme yedeklemek istiyorsanız ve küme tooit tooupgrade deneyin. Başlangıç modu çok ayarlamak**el ile**toochoose desteklenen bir sürüm istiyorsanız.

> [!NOTE]
> Service Fabric desteklenen sürümlerini çalıştıran kümeler destekliyoruz. Merhaba seçerek **el ile** modu yapmakta hello sorumluluk tooupgrade üzerinde Küme desteklenen tooa sürümü. Merhaba hello doku yükseltme modu hakkında daha fazla ayrıntı görmek için [service fabric Küme yükseltme belge.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Güvenlik
![Azure Portal'da güvenlik yapılandırmalarını ekran görüntüsü.][SecurityConfigs]

Merhaba son adım hello anahtar kasası ve bilgileri daha önce oluşturduğunuz sertifika kullanarak tooprovide sertifika bilgileri toosecure hello kümedir.

* Merhaba karşıya elde hello çıktıyla Hello birincil sertifikası alanları doldurmak **küme sertifika** tooKey kasası kullanılarak hello `Invoke-AddCertToKeyVault` PowerShell komutu.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Merhaba denetleyin **Gelişmiş ayarları Yapılandır** tooenter istemci sertifikalarını kutusunda **yönetici istemci** ve **salt okunur istemci**. Bu alanlarda yönetici istemci sertifikanızın parmak izi hello ve salt okunur kullanıcının istemci sertifikanızın hello parmak izi varsa girin. Yöneticiler tooconnect toohello küme denediğinizde, yalnızca hello parmak izi değerleri eşleşen bir parmak izine sahip bir sertifika varsa erişim buraya girilen verilir.  

#### <a name="4-summary"></a>4. Özet
!["Dağıtma Service Fabric kümesi" görüntüleme hello başlangıç panosunun ekran görüntüsü ][Notifications]

toocomplete hello küme oluşturma, tıklatın **Özet** sağlamış ya da indirme toosee hello yapılandırmaları Merhaba, kümenizi toodeploy kullanılan Azure Resource Manager şablonu. Merhaba zorunlu ayarları girdikten sonra hello **Tamam** düğmesi yeşil olur ve tıklayarak hello küme oluşturma işlemi başlatabilirsiniz.

Merhaba oluşturma ilerlemesi hello Bildirimlerde görebilirsiniz. (Hello durum çubuğu, ekranınızın sağ üst hello en yakın hello "zil" simgesine tıklayın.) Tıkladıysanız **PIN tooStartboard** göreceğiniz hello küme oluştururken **Service Fabric kümesi dağıtma** toohello sabitlenmiş **Başlat** Panosu.

### <a name="view-your-cluster-status"></a>Küme durumunu görüntüleme
![Küme ayrıntıları hello panosunda ekran görüntüsü.][ClusterDashboard]

Kümenizi oluşturduktan sonra kümenizi hello portalında inceleyebilirsiniz:

1. Çok Git**Gözat** tıklatıp **Service Fabric kümeleri**.
2. Kümenizi bulun ve tıklatın.
3. Şimdi kümenizi hello kümenin ortak uç noktası ve bağlantı tooService Fabric Explorer dahil olmak üzere hello panosundaki hello ayrıntılarını görebilirsiniz.

Merhaba **düğümü İzleyici** hello kümenin Pano dikey bölümde sağlıklı ve iyi olan VM'ler hello sayısını belirtir. Hello kümenin durumu hakkında daha fazla ayrıntı bulabilirsiniz [Service Fabric sistem durumu modeli giriş][service-fabric-health-introduction].

> [!NOTE]
> Service Fabric kümeleri durumunu - "çekirdek Bakımı" başvurulan tooas korumak ve belirli bir sayıda düğüm toobe her zaman toomaintain kullanılabilirliği gerektirir. Therfore, değil genellikle hello kümedeki tüm makineler aşağı güvenli tooshut ilk yapmadığınız sürece bir [tam yedekleme, durumu][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Uzaktan bağlantı tooa sanal makine ölçek kümesi örneği veya bir küme düğümü
Her hello NodeTypes, küme sonuçlarınızda ayarı alınırken bir sanal makine ölçek kümesi belirtin. Bkz: [uzaktan bağlanma tooa sanal makine ölçek kümesi örnek] [ remote-connect-to-a-vm-scale-set] Ayrıntılar için.

## <a name="next-steps"></a>Sonraki adımlar
Bu noktada, yönetim kimlik doğrulaması için sertifikaları kullanarak güvenli bir küme var. Ardından, [tooyour kümesine bağlanın](service-fabric-connect-to-secure-cluster.md) ve nasıl çok öğrenin[uygulama parolaları yönetme](service-fabric-application-secret-management.md).  Ayrıca, öğrenin [Service Fabric destek seçenekleri](service-fabric-support.md).

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
