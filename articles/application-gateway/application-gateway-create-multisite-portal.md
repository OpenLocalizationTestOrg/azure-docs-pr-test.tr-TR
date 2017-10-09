---
title: "aaaHost Azure uygulama ağ geçidi ile birden çok sitesi | Microsoft Docs"
description: "Bu sayfa, hello birden çok web uygulamalarını barındırmak için mevcut bir Azure uygulama ağ geçidi yönergeleri tooconfigure sağlar hello Azure portal ile aynı ağ geçidi."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 95f892f6-fa27-47ee-b980-7abf4f2c66a9
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2172aa2c80720f6f1ab7dd91745b44654bcaee00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-existing-application-gateway-for-hosting-multiple-web-applications"></a>Birden çok web uygulamalarını barındırmak için mevcut bir uygulama ağ geçidi yapılandırma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)
> 
> 

Birden çok siteyi barındıran bir web uygulaması'birden fazla toodeploy üzerinde hello sağlar aynı uygulama ağ geçidi. Ana bilgisayar üst bilgisi hello gelen HTTP isteği, hangi dinleyicisi trafiği alacağı toodetermine kullanır. Merhaba dinleyicisi sonra hello kuralları tanımı hello ağ geçidi içinde yapılandırıldığı gibi trafik tooappropriate arka uç havuzu yönlendirir. SSL etkin web uygulamaları, uygulama ağ geçidi hello sunucu adı göstergesi (SNI) uzantısı toochoose hello doğru dinleyicisi hello web trafiği için kullanır. Tooload bakiye istekleri farklı web etki alanları toodifferent arka uç sunucu havuzu için birden çok sitesi barındırmak için ortak bir kullanılır. Benzer şekilde aynı kök etki alanı üzerinde de barındırılabilecek hello birden çok alt etki alanları aynı uygulama ağ geçidi hello.

## <a name="scenario"></a>Senaryo

Aşağıdaki örneğine hello iki arka uç sunucu havuzu ile trafiği contoso.com ve fabrikam.com için uygulama ağ geçidi hizmet: contoso sunucu havuzu ve fabrikam sunucu havuzu. Benzer Kurulum app.contoso.com ve blog.contoso.com gibi kullanılan toohost alt etki alanları olabilir.

![çok siteli senaryosu][multisite]

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo, çoklu site desteği tooan varolan uygulama ağ geçidi ekler. toocomplete toobe kullanılabilir tooconfigure bu senaryo, var olan bir uygulama ağ geçidi gerekir. Ziyaret [hello portalı kullanarak bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md) toolearn nasıl toocreate hello portal temel uygulama ağ geçidi.

Merhaba hello adımları tooupdate hello uygulama ağ geçidi gerekli şunlardır:

1. Her site için arka uç havuzları toouse oluşturun.
2. Dinleyici oluşturmak için her site, uygulama ağ geçidi destekler.
3. Kuralları toomap hello uygun arka uç ile her bir dinleyici oluşturun.

## <a name="requirements"></a>Gereksinimler

* **Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi. listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır. FQDN de kullanılabilir.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa). Çok siteli kullanan bir uygulama ağ geçitleri için ana bilgisayar adı ve SNI göstergeleri de eklenir.
* **Kural:** hello kural hello dinleyicisi, hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler. Kuralları listelendikleri hello sırada işlenir ve trafik belirginliğe bağımsız olarak eşleşen ilk kural hello aracılığıyla yönlendirilir. Temel bir dinleyici kullanan bir kural ve çok siteli dinleyicisi hem aynı bağlantı noktası, hello kuralla hello kullanarak bir kuralı varsa, örneğin, hello çok siteli dinleyicisi önce hello kural hello çok siteli kural toofunction sırayla hello temel dinleyicisiyle listelenmiş olması gerekir bekleniyordu. 
* **Sertifikalar:** her dinleyicisi benzersiz bir sertifika gerektirir, bu örnekte 2 dinleyicileri için çok siteli oluşturulur. İki .pfx sertifikaları ve bunları hello parolalarını oluşturulan toobe gerekir.

## <a name="create-back-end-pools-for-each-site"></a>Her site için arka uç havuzları oluşturma

Uygulama ağ geçidi destekler gerekirse, bu durumda 2 olması oluşturulur, contoso11.com için diğeri için fabrikam11.com her site için bir arka uç havuzu.

### <a name="step-1"></a>1. Adım

Tooan varolan uygulama ağ geçidi hello Azure portal (https://portal.azure.com) gidin. Seçin **arka uç havuzları** tıklatıp **Ekle**

![arka uç havuzları ekleme][7]

### <a name="step-2"></a>2. Adım

Merhaba arka uç havuzu hello bilgileri doldurun **pool1**, başlangıç IP adresi veya FQDN hello arka uç sunucuları için ekleme ve tıklatın **Tamam**

![arka uç havuzu pool1 ayarları][8]

### <a name="step-3"></a>3. Adım

Merhaba arka uç havuzları dikey penceresinde tıklatın **Ekle** tooadd ek bir arka uç havuzu **pool2**, başlangıç IP adresi veya FQDN hello arka uç sunucuları için ekleme ve tıklatın **Tamam**

![arka uç havuzu pool2 ayarları][9]

## <a name="create-listeners-for-each-back-end"></a>Her arka uç için dinleyicileri oluşturma

Uygulama ağ geçidi HTTP 1.1 dayanır bir Web sitesinde birden çok konak üstbilgileri toohost hello aynı genel IP adresi ve bağlantı noktası. Merhaba portalında oluşturulan hello temel dinleyicisi, bu özelliği içermiyor.

### <a name="step-1"></a>1. Adım

Tıklatın **dinleyicileri** varolan uygulama ağ geçidi hello ve tıklatın **çok siteli** tooadd hello ilk dinleyicisi.

![dinleyicileri genel bakış dikey penceresi][1]

### <a name="step-2"></a>2. Adım

Merhaba dinleyicisinin hello bilgileri doldurun. Bu örnekte SSL sonlandırma yapılandırılır, yeni bir ön uç bağlantı noktası oluşturun. SSL sonlandırma için kullanılan hello .pfx sertifika toobe karşıya yükleyin. Merhaba yalnızca bu karşılaştırıldığında dikey toohello standart temel dinleyicisi dikey penceresinde hello hostname farktır.

![Dinleyici özellikleri dikey penceresi][2]

### <a name="step-3"></a>3. Adım

Tıklatın **çok siteli** ve hello ikinci site için hello önceki adımda açıklandığı gibi başka bir dinleyici oluşturun. Merhaba ikinci dinleyici için farklı bir sertifika toouse emin olun. Merhaba yalnızca bu karşılaştırıldığında dikey toohello standart temel dinleyicisi dikey penceresinde hello hostname farktır. Merhaba dinleyicisinin hello bilgileri doldurun ve tıklayın **Tamam**.

![Dinleyici özellikleri dikey penceresi][3]

> [!NOTE]
> Hello uygulama ağ geçidi için Azure portalı dinleyicileri oluşturulmasını uzun süre çalışan bir görevdir, işlem biraz zaman toocreate hello Bu senaryoda iki dinleyicileri sürebilir. Ne zaman tam hello dinleyicileri görüntü aşağıdaki hello görüldüğü gibi hello Portalı'nda göster:

![Dinleyici genel bakış][4]

## <a name="create-rules-toomap-listeners-toobackend-pools"></a>Kuralları toomap dinleyicileri toobackend havuzları oluşturma

### <a name="step-1"></a>1. Adım

Tooan varolan uygulama ağ geçidi hello Azure portal (https://portal.azure.com) gidin. Seçin **kuralları** ve hello mevcut varsayılan kuralı seçme **kuralı 1** tıklatıp **Düzenle**.

### <a name="step-2"></a>2. Adım

Merhaba kuralları dikey görüntü aşağıdaki hello görüldüğü gibi doldurun. Merhaba ilk dinleyici ve ilk havuzu seçme ve tıklayarak **kaydetmek** tamamlandığında.

![Mevcut kuralı düzenleyin][6]

### <a name="step-3"></a>3. Adım

Tıklatın **temel kural** toocreate hello ikinci kuralı. Merhaba ikinci dinleyici ve ikinci arka uç havuzu ile Merhaba formu doldurun ve tıklayın **Tamam** toosave.

![temel kural dikey ekleme][10]

Bu senaryo, var olan bir uygulama ağ geçidi hello Azure portal aracılığıyla çok siteli desteğiyle yapılandırma tamamlar.

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooprotect ile Web siteleri [uygulama ağ geçidi - Web uygulaması güvenlik duvarı](application-gateway-webapplicationfirewall-overview.md)

<!--Image references-->
[1]: ./media/application-gateway-create-multisite-portal/figure1.png
[2]: ./media/application-gateway-create-multisite-portal/figure2.png
[3]: ./media/application-gateway-create-multisite-portal/figure3.png
[4]: ./media/application-gateway-create-multisite-portal/figure4.png
[5]: ./media/application-gateway-create-multisite-portal/figure5.png
[6]: ./media/application-gateway-create-multisite-portal/figure6.png
[7]: ./media/application-gateway-create-multisite-portal/figure7.png
[8]: ./media/application-gateway-create-multisite-portal/figure8.png
[9]: ./media/application-gateway-create-multisite-portal/figure9.png
[10]: ./media/application-gateway-create-multisite-portal/figure10.png
[multisite]: ./media/application-gateway-create-multisite-portal/multisite.png
