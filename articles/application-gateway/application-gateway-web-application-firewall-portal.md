---
title: "aaaCreate veya web uygulaması güvenlik duvarı ile bir Azure uygulama ağ geçidi güncelleştirme | Microsoft Docs"
description: "Nasıl toocreate bir uygulama ağ geçidi kullanarak web uygulaması güvenlik duvarı ile Merhaba portal öğrenin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Merhaba portalını kullanarak bir uygulama ağ geçidi ile web uygulaması güvenlik duvarı oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

Uygulama ağ geçidi nasıl toocreate bir web uygulaması Güvenlik Duvarı etkin öğrenin.

Hello web uygulaması Güvenlik Duvarı (WAF) Azure uygulama ağ geçidi, web uygulamaları, SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini korur. Web uygulaması birçok hello OWASP üst 10 ortak web güvenlik açıklarına karşı korur.

## <a name="scenarios"></a>Senaryolar

Bu makalede iki senaryo vardır:

Merhaba ilk senaryoda, çok bilgi[web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma](#create-an-application-gateway-with-web-application-firewall)

Merhaba İkinci senaryoda, çok bilgi[web uygulaması güvenlik duvarı tooan varolan uygulama ağ geçidi eklemek](#add-web-application-firewall-to-an-existing-application-gateway).

![Senaryo örneği][scenario]

> [!NOTE]
> Merhaba uygulama ağ geçidi, özel durumu da dahil olmak üzere ek yapılandırma araştırmaları, arka uç havuzu adresleri ve ek kurallar hello uygulama ağ geçidi yapılandırıldıktan sonra ve ilk dağıtım sırasında değil yapılandırılır.

## <a name="before-you-begin"></a>Başlamadan önce

Azure uygulama ağ geçidi, kendi alt gerektirir. Bir sanal ağ oluştururken, birden çok alt ağı yeterli adres alanı toohave bıraktığınızdan emin olun. Bir uygulama ağ geçidi tooa alt dağıttığınızda, yalnızca ek uygulama ağ geçitleri eklenen mümkün toobe olan toohello alt ağ.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Web uygulaması güvenlik duvarı tooan varolan uygulama ağ geçidi Ekle

Bu örnek, bir var olan uygulama ağ geçidi toosupport web uygulaması güvenlik duvarı engelleme modunda güncelleştirir.

1. Hello Azure portal'ın **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**. Tıklatın hello hello varolan uygulama ağ geçidi **tüm kaynakları** dikey. Merhaba aboneliği zaten içinde birçok kaynak varsa hello hello ad girebilirsiniz **ada göre Filtrele...** kutusunu tooeasily erişim hello DNS bölgesi.

   ![Uygulama ağ geçidi oluşturma][1]

1. Tıklatın **Web uygulaması güvenlik duvarı** ve hello uygulama ağ geçidi ayarlarını güncelleştirin. Tıklatın tamamlandığında **Kaydet**

    Hello ayarları tooupdate bir var olan uygulama ağ geçidi toosupport web uygulaması güvenlik duvarı şunlardır:

   | **Ayar** | **Değer** | **Ayrıntılar**
   |---|---|---|
   |**Yükseltme tooWAF katmanı**| İşaretli | Merhaba katmanı hello uygulama ağ geçidi toohello WAF katmanının ayarlar.|
   |**Güvenlik Duvarı durumu**| Etkin | Bu ayar hello Güvenlik Duvarı'nı hello WAF sağlar.|
   |**Güvenlik Duvarı modu** | Önleme | Bu ayar, web uygulaması güvenlik duvarı kötü amaçlı trafiği ile nasıl ilgileneceğini değildir. **Algılama** modu yalnızca hello olayları günlüğe kaydeder, **önleme** modu hello olayları günlüğe kaydeder ve durakları hello kötü amaçlı trafiği.|
   |**Kural kümesi**|3.0|Bu ayar hello belirler [çekirdek kural kümesi](application-gateway-web-application-firewall-overview.md#core-rule-sets) diğer bir deyişle kullanılan tooprotect hello arka uç havuzu üyeleri.|
   |**Devre dışı kurallarını yapılandırma**|Değişir|tooprevent olası hatalı pozitif sonuç, bu ayarı tanır toodisable belirli [kurallar ve kural gruplarını](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Var olan bir uygulama ağ geçidi toohello WAF SKU yükseltirken hello SKU boyutunu değişiklikleri çok**orta**. Yapılandırma tamamlandıktan sonra yeniden.

    ![Dikey gösteren temel ayarları][2-1]

    > [!NOTE]
    > tooview web uygulaması güvenlik duvarı günlükler, tanılama etkinleştirilmelidir ve ApplicationGatewayFirewallLog seçtiniz. Test amacıyla örnek sayısını 1 seçilebilir. Herhangi bir örneğine altında iki örnek sayısı tooknow hello tarafından SLA kapsamında değildir ve bu nedenle önerilmez önemlidir. Web uygulaması güvenlik duvarı kullanırken küçük ağ geçidi kullanılamaz.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma

Bu senaryo aşağıdakileri yapar:

* İki örnekli bir orta web uygulaması güvenlik duvarı uygulama ağ geçidi oluşturun.
* Bir ayrılmış 10.0.0.0/16 CIDR bloğu ile AdatumAppGatewayVNET adlı bir sanal ağ oluşturun.
* Appgatewaysubnet adlı, CIDR bloğu olarak 10.0.0.0/28 kullanan bir alt ağ oluşturacaksınız.
* SSL yük boşaltımı için bir sertifika yapılandırın.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com). Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz bir aylık deneme sürümü](https://azure.microsoft.com/free)
1. Merhaba Sık Kullanılanlar hello portalı bölmesinde **yeni**
1. Merhaba, **yeni** dikey penceresinde tıklatın **ağ**. Merhaba, **ağ** dikey penceresinde tıklatın **uygulama ağ geçidi**hello görüntü aşağıdaki gösterildiği gibi:
1. Toohello Azure portalına gidin, tıklatın **yeni** > **ağ** > **uygulama ağ geçidi**

    ![Uygulama ağ geçidi oluşturma][1]

1. Merhaba, **Temelleri** görüntülenirse, dikey hello aşağıdaki değerleri girin ve ardından **Tamam**:

   | **Ayar** | **Değer** | **Ayrıntılar**
   |---|---|---|
   |**Ad**|AdatumAppGateway|Merhaba uygulama ağ geçidi Hello adı|
   |**Katmanı**|WAF|Standart ve WAF değerleri kullanılabilir. Ziyaret [web uygulaması güvenlik duvarı](application-gateway-web-application-firewall-overview.md) toolearn WAF hakkında daha fazla bilgi.|
   |**SKU boyutu**|Orta|Standart katmanı seçildiğinde küçük, Orta ve büyük seçimlerdir. WAF katmanı seçerken, Orta ve büyük yalnızca seçeneklerdir.|
   |**Örnek sayısı**|2|Merhaba uygulama ağ geçidi yüksek kullanılabilirlik için örnek sayısı. Örnek sayısı 1 yalnızca sınama amacıyla kullanılmalıdır.|
   |**Abonelik**|[Aboneliğiniz]|Bir abonelik toocreate hello uygulama ağ geçidi seçin.|
   |**Kaynak grubu**|**Yeni Oluştur:** AdatumAppGatewayRG|Bir kaynak grubu oluşturun. Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır. Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) genel bakış makalesi.|
   |**Konum**|Batı ABD||

   ![Dikey gösteren temel ayarları][2-2]

1. Merhaba, **ayarları** altında görüntülenen dikey **sanal ağ**, tıklatın **sanal ağ seçin**. Bu adımı açılır girin hello **Seç sanal ağ** dikey.  Tıklatın **Yeni Oluştur** tooopen hello **sanal ağ oluştur** dikey.

   ![sanal ağ seçin][2]

1. Merhaba üzerinde **oluşturma sanal ağ dikey** hello aşağıdaki değerleri girin ve ardından **Tamam**. Bu adım hello kapatır **sanal ağ oluştur** ve **Seç sanal ağ** dikey pencereleri. Bu hello doldurur **alt** hello alanını **ayarları** seçilen hello alt dikey.

   |**Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Ad**|AdatumAppGatewayVNET|Merhaba uygulama ağ geçidi adı|
   |**Adres alanı**|10.0.0.0/16| Bu değer hello adres alanı hello sanal ağ için kullanılabilir|
   |**Alt ağ adı**|AppGatewaySubnet|Merhaba uygulama ağ geçidi için hello alt ağ adı|
   |**Alt ağ adres aralığı**|10.0.0.0/28 | Bu alt ağ daha fazla ek alt ağlar hello sanal ağında arka uç havuzu üyeleri için izin verir|

1. Merhaba üzerinde **ayarları** altında dikey **ön uç IP yapılandırmasını**, seçin **ortak** hello olarak **IP adresi türü**

1. Merhaba üzerinde **ayarları** altında dikey **genel IP adresi**, tıklatın **genel bir IP adresi seçin**, bu adımı hello açar **genel IP adresiseçin**dikey penceresinde tıklatın **Yeni Oluştur**.

   ![genel IP seçin][3]

1. Merhaba üzerinde **ortak IP adresi oluştur** dikey penceresinde hello varsayılan değeri kabul edin ve tıklatın **Tamam**. Bu adım hello kapatır **genel IP adresi seçin** dikey penceresinde, hello **ortak IP adresi oluştur** dikey penceresinde ve doldurmak **genel IP adresi** seçilen hello ortak IP adresine sahip.

1. Merhaba üzerinde **ayarları** altında dikey **dinleyici Yapılandırması**, tıklatın **HTTP** altında **Protokolü**. toouse **https**, bir sertifika gereklidir. Böylece hello sertifika .pfx verilmesini sağlanan toobe gerekir ve hello dosyası için parolayı hello hello hello sertifikasının özel anahtarı gereklidir.

1. Merhaba yapılandırma **WAF** belirli ayarları.

   |**Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Güvenlik Duvarı durumu**| Etkin| Bu ayar WAF üzerinde veya devre dışı bırakır.|
   |**Güvenlik Duvarı modu** | Önleme| Bu ayar, kötü amaçlı trafiği WAF alır hello eylemleri belirler. Varsa **algılama** seçildiğinde trafiği yalnızca oturum.  Varsa **önleme** seçildiğinde trafiği oturum ve 403 yetkisiz yanıtta durduruldu.|


1. Merhaba Özet sayfasını gözden geçirin ve tıklatın **Tamam**.  Şimdi hello uygulama ağ geçidi sıraya ve oluşturuldu.

1. Merhaba uygulama ağ geçidi oluşturulduktan sonra hello portal toocontinue yapılandırmasındaki hello uygulama ağ geçidi tooit gidin.

    ![Uygulama ağ geçidi kaynağı görünümü][10]

Bu adımları hello dinleyicisi, arka uç havuzu, arka uç http ayarları ve kuralları için varsayılan ayarlarla temel uygulama ağ geçidi oluşturun. Merhaba sağlama başarılı olduktan sonra bu ayarları toosuit dağıtımınızı değiştirebilirsiniz

> [!NOTE]
> Merhaba temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.

## <a name="next-steps"></a>Sonraki adımlar

Ardından, öğrenebilirsiniz nasıl tooconfigure hello için bir özel etki alanı diğer adı [genel IP adresi](../dns/dns-custom-domain.md#public-ip-address) Azure DNS veya başka bir DNS sağlayıcısı kullanarak.

Bilgi nasıl tooconfigure tanılama günlük kaydını, algılanan veya web uygulaması güvenlik duvarı ile ziyaret ederek engelledi toolog hello olayları [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)

Nasıl toocreate özel durumu ziyaret ederek yoklamaları öğrenin [bir özel durum araştırması oluştur](application-gateway-create-probe-portal.md)

Nasıl tooconfigure SSL boşaltma ve Al hello maliyetli SSL şifre çözme ziyaret ederek, web sunucuları kapalı öğrenin [SSL boşaltma yapılandırın](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
