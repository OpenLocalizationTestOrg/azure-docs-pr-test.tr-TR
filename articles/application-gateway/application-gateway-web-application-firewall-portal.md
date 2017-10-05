---
title: "Azure uygulama ağ geçidi ile web uygulaması güvenlik duvarı güncelle | Microsoft Docs"
description: "Portalı kullanarak bir uygulama ağ geçidi ile web uygulaması güvenlik duvarı oluşturma hakkında bilgi edinin"
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
ms.openlocfilehash: 650f26d19615d27a94f3947aad7b7904b6c1fabc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-the-portal"></a>Portalı kullanarak bir uygulama ağ geçidi ile web uygulaması güvenlik duvarı oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

Bir web uygulaması Güvenlik Duvarı etkin uygulama ağ geçidi oluşturmayı öğrenin.

Azure uygulama ağ geçidi, web uygulaması Güvenlik Duvarı (WAF), SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini web uygulamaları korur. Web uygulaması birçok OWASP üst 10 ortak web güvenlik açıklarına karşı korur.

## <a name="scenarios"></a>Senaryolar

Bu makalede iki senaryo vardır:

İlk senaryoda, öğrenin [web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma](#create-an-application-gateway-with-web-application-firewall)

İkinci senaryoda, öğrenin [var olan bir uygulama ağ geçidi için web uygulaması güvenlik duvarı ekleme](#add-web-application-firewall-to-an-existing-application-gateway).

![Senaryo örneği][scenario]

> [!NOTE]
> Özel durumu da dahil olmak üzere uygulama ağ geçidinin ek yapılandırma araştırmaları, arka uç havuzu adresleri ve ek kurallar uygulama ağ geçidi yapılandırıldıktan sonra ve ilk dağıtım sırasında değil yapılandırılır.

## <a name="before-you-begin"></a>Başlamadan önce

Azure uygulama ağ geçidi, kendi alt gerektirir. Bir sanal ağ oluştururken, birden çok alt ağa sahip için yeterli adres alanı bıraktığınızdan emin olun. Bir alt ağ için bir uygulama ağ geçidi dağıttığınızda, yalnızca ek uygulama ağ geçidi alt ağına eklemek kullanabilirsiniz.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Web uygulaması güvenlik duvarı için var olan bir uygulama ağ geçidi Ekle

Bu örnek web uygulaması güvenlik duvarı engelleme modunda desteklemek için varolan uygulama ağ geçidi güncelleştirir.

1. Azure Portal **Sık Kullanılanlar** bölmesinde, **Tüm kaynaklar**’a tıklayın. Mevcut uygulama ağ geçidi tıklatın **tüm kaynakları** dikey. Zaten seçili abonelik çeşitli kaynaklar varsa, ad girebilirsiniz **ada göre Filtrele...** girebilirsiniz.

   ![Uygulama ağ geçidi oluşturma][1]

1. Tıklatın **Web uygulaması güvenlik duvarı** ve uygulama ağ geçidi ayarlarını güncelleştirin. Tıklatın tamamlandığında **Kaydet**

    Web uygulaması güvenlik duvarı desteklemek için varolan uygulama ağ geçidi güncelleştirmek için ayarlar şunlardır:

   | **Ayar** | **Değer** | **Ayrıntılar**
   |---|---|---|
   |**WAF katmanına yükseltme**| İşaretli | Bu uygulama ağ geçidi WAF katmanına katmanı ayarlar.|
   |**Güvenlik Duvarı durumu**| Etkin | Bu ayar, Güvenlik Duvarı'nı WAF sağlar.|
   |**Güvenlik Duvarı modu** | Önleme | Bu ayar, web uygulaması güvenlik duvarı kötü amaçlı trafiği ile nasıl ilgileneceğini değildir. **Algılama** modu yalnızca, olayları günlüğe kaydeder, **önleme** modu olayları günlüğe kaydeder ve kötü amaçlı trafiği durdurur.|
   |**Kural kümesi**|3.0|Bu ayar belirler [çekirdek kural kümesi](application-gateway-web-application-firewall-overview.md#core-rule-sets) arka uç havuzu üyelerini korumak için kullanılır.|
   |**Devre dışı kurallarını yapılandırma**|Değişir|Olası hatalı pozitif sonuç önlemek için bu ayarı belirli devre dışı bırakmanızı sağlar [kurallar ve kural gruplarını](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > WAF SKU için var olan bir uygulama ağ geçidi yükseltme yaparken, SKU boyutunu değişikliklerini **orta**. Yapılandırma tamamlandıktan sonra yeniden.

    ![Dikey gösteren temel ayarları][2-1]

    > [!NOTE]
    > Web uygulaması güvenlik duvarı günlüklerini görüntülemek için tanılama etkinleştirilmelidir ve ApplicationGatewayFirewallLog seçtiniz. Test amacıyla örnek sayısını 1 seçilebilir. Tüm örnek sayısı iki örneği altında SLA kapsamında değildir ve bu nedenle önerilmez bilmeniz önemlidir. Web uygulaması güvenlik duvarı kullanırken küçük ağ geçidi kullanılamaz.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma

Bu senaryo aşağıdakileri yapar:

* İki örnekli bir orta web uygulaması güvenlik duvarı uygulama ağ geçidi oluşturun.
* Bir ayrılmış 10.0.0.0/16 CIDR bloğu ile AdatumAppGatewayVNET adlı bir sanal ağ oluşturun.
* Appgatewaysubnet adlı, CIDR bloğu olarak 10.0.0.0/28 kullanan bir alt ağ oluşturacaksınız.
* SSL yük boşaltımı için bir sertifika yapılandırın.

1. [Azure Portal](https://portal.azure.com)’da oturum açın. Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz bir aylık deneme sürümü](https://azure.microsoft.com/free)
1. Sık Kullanılanlar portalı bölmesinde **yeni**
1. **Yeni** dikey penceresinde, **Ağ** öğesine tıklayın. İçinde **ağ** dikey penceresinde tıklatın **uygulama ağ geçidi**aşağıdaki görüntüde gösterildiği gibi:
1. Azure Portalı'na gidin, tıklatın **yeni** > **ağ** > **uygulama ağ geçidi**

    ![Uygulama ağ geçidi oluşturma][1]

1. İçinde **Temelleri** görünür, dikey penceresinde aşağıdaki değerleri girin ve ardından **Tamam**:

   | **Ayar** | **Değer** | **Ayrıntılar**
   |---|---|---|
   |**Ad**|AdatumAppGateway|Uygulama ağ geçidi adı|
   |**Katmanı**|WAF|Standart ve WAF değerleri kullanılabilir. Ziyaret [web uygulaması güvenlik duvarı](application-gateway-web-application-firewall-overview.md) WAF hakkında daha fazla bilgi edinmek için.|
   |**SKU boyutu**|Orta|Standart katmanı seçildiğinde küçük, Orta ve büyük seçimlerdir. WAF katmanı seçerken, Orta ve büyük yalnızca seçeneklerdir.|
   |**Örnek sayısı**|2|Uygulama ağ geçidi yüksek kullanılabilirlik için örnek sayısı. Örnek sayısı 1 yalnızca sınama amacıyla kullanılmalıdır.|
   |**Abonelik**|[Aboneliğiniz]|Uygulama ağ geçidinin oluşturulacağı bir abonelik seçin.|
   |**Kaynak grubu**|**Yeni Oluştur:** AdatumAppGatewayRG|Bir kaynak grubu oluşturun. Kaynak grubu adı, seçili abonelik içinde benzersiz olmalıdır. Kaynak grupları hakkında daha fazla bilgi için, [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups)’a genel bakış makalesini okuyun.|
   |**Konum**|Batı ABD||

   ![Dikey gösteren temel ayarları][2-2]

1. İçinde **ayarları** altında görüntülenen dikey **sanal ağ**, tıklatın **sanal ağ seçin**. Bu adımı açılır girin **Seç sanal ağ** dikey.  Tıklatın **Yeni Oluştur** açmak için **sanal ağ oluştur** dikey.

   ![sanal ağ seçin][2]

1. Üzerinde **oluşturma sanal ağ dikey** aşağıdaki değerleri girin ve ardından **Tamam**. Bu adım kapatır **sanal ağ oluştur** ve **Seç sanal ağ** dikey pencereleri. Bu doldurur **alt** alanını **ayarları** dikey penceresinde seçilen alt ağ ile.

   |**Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Ad**|AdatumAppGatewayVNET|Uygulama ağ geçidi adı|
   |**Adres alanı**|10.0.0.0/16| Bu değer sanal ağ adres alanı|
   |**Alt ağ adı**|AppGatewaySubnet|Uygulama ağ geçidi için alt ağ adı|
   |**Alt ağ adres aralığı**|10.0.0.0/28 | Bu alt ağ daha fazla ek alt ağlar sanal ağında arka uç havuzu üyeleri için izin verir|

1. Üzerinde **ayarları** altında dikey **ön uç IP yapılandırmasını**, seçin **ortak** olarak **IP adresi türü**

1. Üzerinde **ayarları** altında dikey **genel IP adresi**, tıklatın **genel bir IP adresi seçin**, bu adımı açılır **genel IP adresi seçin** Dikey penceresinde tıklatın **Yeni Oluştur**.

   ![genel IP seçin][3]

1. Üzerinde **ortak IP adresi oluştur** dikey penceresinde, varsayılan değeri kabul edin ve tıklatın **Tamam**. Bu adım kapatır **genel IP adresi seçin** dikey penceresinde **ortak IP adresi oluştur** dikey penceresinde ve doldurmak **genel IP adresi** seçilen genel IP adresine sahip.

1. Üzerinde **ayarları** altında dikey **dinleyici Yapılandırması**, tıklatın **HTTP** altında **Protokolü**. Kullanılacak **https**, bir sertifika gereklidir. Bir .pfx verme sağlanacak sertifika gereksinimlerini ve dosyanın parolası, böylece sertifikanın özel anahtarı gereklidir.

1. Yapılandırma **WAF** belirli ayarları.

   |**Ayar** | **Değer** | **Ayrıntılar** |
   |---|---|---|
   |**Güvenlik Duvarı durumu**| Etkin| Bu ayar WAF üzerinde veya devre dışı bırakır.|
   |**Güvenlik Duvarı modu** | Önleme| Bu ayar, kötü amaçlı trafiği Eylemler WAF alır belirler. Varsa **algılama** seçildiğinde trafiği yalnızca oturum.  Varsa **önleme** seçildiğinde trafiği oturum ve 403 yetkisiz yanıtta durduruldu.|


1. Özet sayfasını gözden geçirin ve tıklatın **Tamam**.  Artık uygulama ağ geçidi sıraya ve oluşturuldu.

1. Uygulama ağ geçidi oluşturulduktan sonra kendisine uygulama ağ geçidi yapılandırmasının devam edebilmesi için portalında gidin.

    ![Uygulama ağ geçidi kaynağı görünümü][10]

Bu adımları dinleyicisi, arka uç havuzu, arka uç http ayarları ve kuralları için varsayılan ayarlarla temel uygulama ağ geçidi oluşturun. Sağlama başarılı olduktan sonra dağıtımınızı uyacak şekilde bu ayarları değiştirebilirsiniz

> [!NOTE]
> Temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.

## <a name="next-steps"></a>Sonraki adımlar

Ardından, bir özel etki alanı diğer adı için yapılandırma hakkında bilgi edinebilirsiniz [genel IP adresi](../dns/dns-custom-domain.md#public-ip-address) Azure DNS veya başka bir DNS sağlayıcısı kullanarak.

Algılanan ya da engelledi ile web uygulaması güvenlik duvarı adresini ziyaret ederek günlük olaylarıyla tanılama günlük yapılandırmayı öğrenin [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)

Özel sistem durumu araştırmalarının ziyaret ederek oluşturmayı öğrenin [bir özel durum araştırması oluştur](application-gateway-create-probe-portal.md)

SSL boşaltma yapılandırmak ve web sunucularınızın kapalı maliyetli SSL şifre çözme ziyaret ederek ele öğrenin [SSL boşaltma yapılandırın](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
