---
title: "Oluşturma ve bir expressroute bağlantı hattı değiştirme: PowerShell: Azure Klasik | Microsoft Docs"
description: "Bu makalede, oluşturma ve bir expressroute bağlantı hattı sağlama hello adım adım anlatılmaktadır. Bu makalede ayrıca, nasıl toocheck hello durumu, güncelleştirme veya silme ve hattınız yetkisini kaldırma gösterir."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>Oluşturma ve PowerShell (Klasik) kullanarak bir expressroute bağlantı hattı değiştirme
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-circuit-classic.md)
>

Bu makalede PowerShell cmdlet'leri ve hello Klasik dağıtım modeli kullanarak bir Azure expressroute bağlantı hattı hello adımları toocreate anlatılmaktadır. Bu makalede ayrıca, nasıl toocheck hello durumu, güncelleştirme veya silme ve bir expressroute bağlantı hattı yetkisini kaldırma gösterir.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**Azure dağıtım modelleri hakkında**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Başlamadan önce
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>1. Adım Merhaba önkoşulları ve iş akışı makaleleri gözden geçirin
Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>2. Adım Merhaba hello Azure Hizmet Yönetimi (SM) PowerShell modülleri en son sürümlerini yükleyin
Merhaba yönergeleri izleyin [Azure PowerShell cmdlet'leri ile çalışmaya başlama](/powershell/azure/overview) nasıl hakkında adım adım yönergeler için tooconfigure bilgisayar toouse hello Azure PowerShell modüllerinizi.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>3. Adım Tooyour Azure hesabı oturum ve bir abonelik seçin
1. Yükseltilmiş haklarla PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

        Login-AzureRmAccount

2. Merhaba hesabının Hello abonelikleri kontrol edin.

        Get-AzureRmSubscription

3. Birden fazla aboneliğiniz varsa, toouse istediğiniz hello aboneliği seçin.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Ardından, aşağıdaki cmdlet'i tooadd hello Azure aboneliği tooPowerShell hello Klasik dağıtım modeli için kullanın.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Oluşturma ve bir expressroute bağlantı hattı sağlama
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>1. Adım ExpressRoute için Hello PowerShell modülleri alın
 Zaten yapmadıysanız, sipariş toostart hello ExpressRoute cmdlet'lerini kullanmaya hello PowerShell oturumunda hello Azure ve ExpressRoute modülleri almanız gerekir. Merhaba modülleri içe hello oldukları konumu tooon yerel bilgisayarınızda yüklü. Tooinstall hello modülleri kullanılan Hello yöntemine bağlı olarak, başlangıç konumu aşağıdaki örnekte gösterildiği hello farklı olabilir. Merhaba örneği gerekiyorsa değiştirin.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Adım Desteklenen sağlayıcılar, konumları ve bant genişlikleri Hello listesini alma
Bir expressroute bağlantı hattı oluşturmadan önce desteklenen bağlantı sağlayıcıları, konumları ve bant genişliği seçenekleri hello listesi gerekir.

PowerShell cmdlet hello `Get-AzureDedicatedCircuitServiceProvider` , sonraki adımlarda kullanacağınız bu bilgiler verir:

    Get-AzureDedicatedCircuitServiceProvider

Bağlantı sağlayıcınız listelenip toosee kontrol edin. Bir bağlantı hattı oluşturduğunuzda, daha sonra gerekir çünkü aşağıdaki bilgilerle hello not edin:

* Ad
* PeeringLocations
* BandwidthsOffered

Şimdi hazır toocreate bir expressroute bağlantı hattı olduğunuz.         

### <a name="step-3-create-an-expressroute-circuit"></a>3. Adım ExpressRoute bağlantı hattı oluşturma
Aşağıdaki örnek hello nasıl toocreate 200 MB/sn expressroute bağlantı hattı Silikon vadisi Equinix aracılığıyla gösterir. Farklı bir sağlayıcı ve farklı ayarlar kullanıyorsanız, bu bilgileri isteğiniz yaptığınızda değiştirin.

> [!IMPORTANT]
> ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren Fatura edilecek. Merhaba bağlantı sağlayıcı hazır tooprovision hello hattı olduğunda bu işlemi gerçekleştirmek emin olun.
> 
> 

Merhaba, yeni bir hizmet anahtarı için bir örnek isteği aşağıdadır:

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

Ya da toocreate hello premium eklentisi ile bir expressroute bağlantı hattı istiyorsanız, aşağıdaki kullanım hello örneğine. Toohello başvuran [ExpressRoute SSS](expressroute-faqs.md) hello premium eklentisi hakkında daha fazla ayrıntı için.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


Merhaba yanıt hello hizmet anahtarı içerir. Merhaba aşağıdakini çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>4. Adım. Tüm hello ExpressRoute bağlantı hatları listesi
Merhaba çalıştırabilirsiniz `Get-AzureDedicatedCircuit` tooget tüm listesini hello oluşturduğunuz ExpressRoute bağlantı hatları komutu:

    Get-AzureDedicatedCircuit

Merhaba yanıt aşağıdaki örneğine benzeri toohello olacaktır:

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Hello kullanarak herhangi bir zamanda bu bilgiler alabilirsiniz `Get-AzureDedicatedCircuit` cmdlet'i. Hiçbir parametre olmadan çağrı hello yapmadan tüm hello devreleri listeler. Hizmet anahtarınız hello listelenmez *ServiceKey* alan.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Merhaba aşağıdakini çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Adım. Merhaba hizmet anahtar tooyour bağlantı sağlayıcı sağlamak için Gönder
*ServiceProviderProvisioningState* hello hizmet sağlayıcı tarafında sağlama hello geçerli durumu hakkında bilgi sağlar. *Durum* Microsoft yan hello üzerinde hello durumunu sağlar. Merhaba hattı durumları sağlama hakkında daha fazla bilgi için bkz: [iş akışları](expressroute-workflows.md#expressroute-circuit-provisioning-states) makalesi.

Yeni bir expressroute bağlantı hattı oluşturduğunuzda, hello hattı durumu aşağıdaki hello olacaktır:

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Merhaba hattı hello bağlantı sağlayıcı için etkinleştirme işleminin hello olduğunda durumu aşağıdaki toohello geçer:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Bir expressroute bağlantı hattı, toobe mümkün toouse durumunu izleyen hello onu olması gerekir:

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Adım. Merhaba durumunu ve hello hattı anahtar hello durumunu düzenli aralıklarla denetleyin
Bu, sağlayıcınız hattınız etkin olduğunda bilmenizi sağlar. Merhaba hattı yapılandırıldıktan sonra *ServiceProviderProvisioningState* olarak görüntülenir *hazırlandı* hello aşağıdaki örnekte gösterildiği gibi:

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>7. Adım. Yönlendirme yapılandırması oluşturma
Toohello başvuran [expressroute bağlantı hattı yönlendirme yapılandırması (oluşturma ve hattı eşlemeler değiştirme)](expressroute-howto-routing-classic.md) makale adım adım yönergeler için.

> [!IMPORTANT]
> Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir. Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. adım. Sanal ağ tooan expressroute bağlantı hattı bağlantı
Ardından, sanal ağ tooyour expressroute bağlantı hattı bağlayın. Çok başvuran[bağlama ExpressRoute bağlantı hattına toovirtual ağlar](expressroute-howto-linkvnet-classic.md) adım adım yönergeler için. ExpressRoute için hello Klasik dağıtım modeli kullanarak bir sanal ağ toocreate gerekirse bkz [ExpressRoute için bir sanal ağ oluşturma](expressroute-howto-vnet-portal-classic.md).

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı Hello durumunu alma
Hello kullanarak herhangi bir zamanda bu bilgiler alabilirsiniz `Get-AzureCircuit` cmdlet'i. Hiçbir parametre olmadan çağrı hello yapmadan tüm hello devreleri listeler.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Bir parametre toohello araması olarak hello hizmet anahtarını geçirerek belirli bir expressroute bağlantı hattı hakkında bilgi alabilirsiniz.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


Aşağıdaki örnek hello çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı değiştirme
Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.

Yapabileceğiniz kapalı kalma süresi ile aşağıdaki hello:

* Etkinleştirmek veya devre dışı bir expressroute bağlantı hattı için ExpressRoute premium eklentisi.
* Artış hello bant genişliği, expressroute bağlantı hattı var. kapasite kullanılabilir hello bağlantı noktasında sağlanır. Önceki sürüme indirme bir bağlantı hattının bant genişliği hello Not desteklenmiyor. 
* Ölçülen veri tooUnlimited veri planından ölçümü hello değiştirin. Bu değişen hello ölçüm planından veri desteklenmiyor sınırsız veri tooMetered unutmayın.
* Etkinleştirme ve devre dışı *izin Klasik işlemleri*.

Toohello başvuran [ExpressRoute SSS](expressroute-faqs.md) sınırlar ve sınırlamalar hakkında daha fazla bilgi için.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium eklentisi
Merhaba aşağıdaki PowerShell cmdlet'ini kullanarak, varolan bağlantı hattınız için hello ExpressRoute premium eklentisi etkinleştirebilirsiniz:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

Bağlantı hattınız şimdi hello ExpressRoute premium eklentisi özellikleri etkin olacaktır. Biz hello komutu başarıyla çalıştırıldı hemen için hello premium eklenti özelliğini faturalama başlayacak unutmayın.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium eklentisi
> [!IMPORTANT]
> Merhaba standart bağlantı hattı için izin daha büyük olan kaynaklar kullanıyorsanız, bu işlemi başarısız olabilir.
> 
> 

#### <a name="considerations"></a>Dikkat edilmesi gerekenler

* Premium toostandard düşürmek önce sanal ağlar bağlantılı toohello hattı hello sayısı 10'dan az olduğundan emin olmalısınız. Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve Faturalanan hello premium oranları olması.
* Tüm sanal ağları diğer coğrafi bölgelerde bağlantısını gerekir. Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve Faturalanan hello premium oranları olması.
* Yol tablosu özel eşleme için 4. 000'den az yolları olmalıdır. Rota tablosu boyutunuz 4.000 yolları büyükse, hello BGP oturumu bırakacaktır ve 4.000 tanıtılan önekler hello sayısı gider kadar yeniden iler hale olmaz.

#### <a name="disable-hello-premium-add-on"></a>Merhaba premium eklentisi devre dışı bırak
Merhaba aşağıdaki PowerShell cmdlet'ini kullanarak var olan bağlantı hattınız için hello ExpressRoute premium eklentisi devre dışı bırakabilirsiniz:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute devresi bant genişliği
Merhaba denetleyin [ExpressRoute SSS](expressroute-faqs.md) desteklenen sağlayıcınız için bant seçenekleri. (Hattınız oluşturulduğu) hello fiziksel bağlantı noktası izin verdiği sürece, varolan bağlantı hattınız hello boyutundan büyük olan herhangi bir boyutta seçebilirsiniz.

> [!IMPORTANT]
> Merhaba varolan bağlantı noktasında yetersiz kapasite ise toorecreate hello expressroute bağlantı hattı olabilir. Varsa hiçbir ek kapasite kullanılabilir o konumda hello hattı yükseltemezsiniz.
>
> Bir expressroute bağlantı hattı kesintiye uğratmadan hello bant genişliği azaltma olamaz. Bant genişliği eski sürüme düşürmeyi toodeprovision hello expressroute bağlantı hattı gerektirir ve yeni bir expressroute bağlantı hattı yeniden sağlayın.
> 
> 

#### <a name="resize-a-circuit"></a>Bir bağlantı hattı yeniden boyutlandırma

Gereksinim boyutu karar verdikten sonra komutu tooresize aşağıdaki hello hattınız kullanabilirsiniz:

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Bağlantı hattınız hello Microsoft tarafında boyutlandırılmış. Bu değişiklik, bağlantı sağlayıcısı tooupdate yapılandırmalarını kendi yan toomatch başvurmanız gerekir. Biz Merhaba faturalama başlayacak Not bant genişliği seçeneği bu noktasından güncelleştirdi.

Merhaba hello hattı bant genişliğini artırma olduğunda aşağıdaki hata görürseniz, bu var. Varolan hattınız oluşturulduğu hello fiziksel bağlantı noktası hiçbir yeterli bant genişliği sol anlamına gelir. Bu hattı toodelete sahip ve yeni bir hattı ihtiyacınız hello boyutunun oluşturma. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme

### <a name="considerations"></a>Dikkat edilmesi gerekenler

* Tüm sanal ağlardan hello expressroute bağlantı hattı için bu işlemi toosucceed bağlantısını gerekir. Denetleme olan tüm sanal ağlarınız varsa toosee, bu işlem başarısız olursa toohello hattı bağlı.
* Merhaba ExpressRoute bağlantı hattı Hizmet Sağlayıcısı sağlama durumu ise **sağlama** veya **hazırlandı** kendi tarafında hizmet sağlayıcısı toodeprovision hello hattınız ile çalışmanız gerekir. Biz tooreserve kaynakları devam edecek ve hello hizmet sağlayıcısı sağlamayı hello hattı tamamlandıktan ve bize bildiren kadar sizi faturalandırmak.
* Merhaba hizmet sağlayıcısı hello hattı sağlaması kaldırılıyor. sağlaması değilse (Merhaba Hizmet Sağlayıcısı sağlama durumu çok ayarlamak**sağlanmadı**) hello hattı sonra silebilirsiniz. Bu hello hattı için fatura durdurur.

#### <a name="delete-a-circuit"></a>Bir bağlantı hattı Sil

Hello aşağıdaki komutu çalıştırarak, expressroute bağlantı hattı silebilirsiniz:

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>Sonraki adımlar
Bağlantı hattınız oluşturduktan sonra aşağıdaki hello emin olun:

* [Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme](expressroute-howto-routing-classic.md)
* [Sanal ağ tooyour expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md)

