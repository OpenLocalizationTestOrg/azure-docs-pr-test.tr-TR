---
title: "aaaCreate dış Azure uygulama hizmeti ortamı"
description: "Açıklar toocreate çalışırken bir uygulama hizmeti ortamını nasıl oluşturacağınızı bir uygulama ya da tek başına"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>Bir dış uygulama hizmeti ortamı oluşturun #

Azure uygulama hizmeti ortamı bir Azure uygulama hizmeti dağıtımı bir Azure sanal ağındaki (VNet) bir alt ağ ile değil. Uygulama hizmeti ortamı (ana) iki yolu toodeploy vardır:

- Dış IP adresi üzerinde bir VIP ile genellikle bir dış ana çağrılır.
- Hello dahili uç noktayı bir iç yük dengeleyici (ILB) olduğundan hello ile VIP iç IP adresi üzerinde genellikle bir ILB ana olarak adlandırılır.

Bu makale size nasıl gösterir toocreate bir dış ana. Merhaba ana genel bakış için bkz: [giriş toohello uygulama hizmeti ortamı][Intro]. Nasıl toocreate bir ILB ana, bkz. bilgi [oluşturma ve kullanma bir ILB ana][MakeILBASE].

## <a name="before-you-create-your-ase"></a>Ana oluşturmadan önce ##

Ana oluşturduktan sonra hello aşağıdaki değiştiremezsiniz:

- Konum
- Abonelik
- Kaynak grubu
- Kullanılan sanal ağ
- Kullanılan alt ağ
- Alt ağ boyutu

> [!NOTE]
> Bir sanal ağı seçin ve bir alt ağ belirttiğinizde, büyüklükte tooaccommodate Gelecekteki büyümeyi olduğundan emin olun. Dosya boyutu öneririz `/25` 128 adreslerine sahip.
>

## <a name="three-ways-toocreate-an-ase"></a>Üç şekilde toocreate bir ana ##

Üç şekilde toocreate bir ana vardır:

- **Bir uygulama hizmeti planı oluşturma sırasında**. Bu yöntem, tek bir adımda hello ana ve hello uygulama hizmeti planı oluşturur.
- **Bir tek başına eylem olarak**. Bu yöntem boş bir ana olduğu tek başına ana, oluşturur. Bu yöntem daha gelişmiş bir işlem toocreate bir ana kullanılır. Bir ana toocreate bir ILB ile kullanırsınız.
- **Bir Azure Resource Manager şablondan**. Bu yöntem İleri düzey kullanıcılar için kullanılır. Daha fazla bilgi için bkz: [bir ana şablondan oluşturma][MakeASEfromTemplate].

Bir dış ana hello ana tüm HTTP/HTTPS trafiğini toohello uygulamaları internet'ten erişilebilen bir IP adresi isabetler anlamına gelen genel bir VIP sahiptir. Bir ILB ile bir ana ana hello tarafından kullanılan hello alt ağdan bir IP adresi vardır. Merhaba ILB ASE'de barındırılan uygulamalar kullanıma sunulan olmayan doğrudan toohello Internet.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>Bir ana ve bir uygulama hizmeti planı birlikte oluşturma ##

Merhaba uygulama hizmeti planı, uygulamaların bir kapsayıcıdır. App Service içinde bir uygulama oluşturduğunuzda, seçin veya bir uygulama hizmeti planı oluşturun. Uygulama hizmeti planları Hello kapsayıcı modeli ortamları tutun ve uygulama hizmeti planları uygulamaları basılı tutun.

bir uygulama hizmeti planı oluştururken bir ana toocreate:

1. Merhaba, [Azure portal](https://portal.azure.com/)seçin **yeni** > **Web + mobil** > **Web uygulaması**.

    ![Web uygulaması oluşturma][1]

2. Aboneliğinizi seçin. Merhaba uygulama hello ana oluşturulur hello aynı abonelik.

3. Kaynak grubunu seçin veya oluşturun. Kaynak gruplarıyla ilgili Azure kaynaklarını bir birim olarak yönetebilirsiniz. Kaynak grupları, aynı zamanda, uygulamalarınız için rol tabanlı erişim denetimi kuralları oluşturmak olduğunda yararlıdır. Daha fazla bilgi için bkz: Merhaba [Azure Resource Manager'a genel bakış][ARMOverview].

4. Merhaba uygulama hizmeti planı seçin ve ardından **Yeni Oluştur**.

    ![Yeni uygulama hizmeti planı][2]

5. Merhaba, **konumu** aşağı açılan listesinden, toocreate hello ana select hello bölgesini. Varolan bir ana seçerseniz, yeni bir ana oluşturulmaz. Uygulama hizmeti planı Hello hello Seçtiğiniz ana oluşturulur. 

6. Seçin **fiyatlandırma katmanı**ve hello birini **Isolated** SKU'ları fiyatlandırması. İsterseniz bir **Isolated** SKU kartı ve bir ana değil bir konum, yeni bir ana oluşturuldu. konumda. toostart hello işlem toocreate bir ana seçin **seçin**. Merhaba **Isolated** SKU yalnızca bir ana ile birlikte kullanılabilir. Ayrıca diğer fiyatlandırma SKU ASE'de dışında kullanamazsınız **Isolated**.

    ![Fiyatlandırma katmanı seçimi][3]

7. Merhaba, ana için ad girin. Bu ad, hello adreslenebilir ad uygulamalarınız için kullanılır. Merhaba ana Hello adı ise _appsvcenvdemo_, hello etki alanı adı *. appsvcenvdemo.p.azurewebsites.net*. Adlı bir uygulama oluşturursanız, *mytestapp*, mytestapp.appsvcenvdemo.p.azurewebsites.net adreslenebilir. Merhaba adında boşluk kullanamazsınız. Büyük harf karakterler kullanırsanız, hello etki alanı adı hello toplam küçük, bu adı sürümüdür.

    ![Yeni uygulama hizmeti planının adı][4]

8. Azure, sanal ağ ayrıntıları belirtin. Şunlardan birini seçin **Yeni Oluştur** veya **Varolanı seç**. Merhaba seçeneği tooselect olan bir VNet hello seçili bölgede bir VNet varsa kullanılabilir. Seçerseniz **Yeni Oluştur**, hello VNet için bir ad girin. Bu ada sahip yeni bir Resource Manager Vnet'i oluşturulur. Merhaba adres alanı kullanan `192.168.250.0/23` hello seçili bölgede. Seçerseniz **var olanı Seç**, gerekir:

    a. Birden fazla varsa hello VNet adres bloğu, seçin.

    b. Yeni bir alt ağ adı girin.

    c. Merhaba hello alt ağ boyutunu seçin. *Bir boyut büyüklükte tooaccommodate gelecekteki büyümesini, ana tooselect unutmayın.* Öneririz `/25`, 128 adresi olduğunu ve en büyük ölçekli bir ana işleyebilir. Öneririz yok `/28`, örneğin, çünkü yalnızca 16 adresleri kullanılabilir durumdadır. Altyapı en az beş adreslerini kullanır. İçinde bir `/28` alt sol en fazla bir ölçeklendirme 11 örnekleri.

    d. Merhaba alt ağ IP aralığını seçin.

9. Seçin **oluşturma** toocreate hello ana. Bu işlem ayrıca hello uygulama hizmeti planı ve hello uygulama oluşturur. Merhaba ana, uygulama hizmeti planı ve uygulama olan tüm altında hello aynı abonelik ve ayrıca, aynı hello kaynak grubu. Farklı bir kaynak grubu, ana alması gerekiyorsa ya da bir ILB ana gerekiyorsa hello adımları toocreate bir ana tek başına izleyin.

## <a name="create-an-ase-by-itself"></a>Tek başına bir ana oluşturma ##

Bir ana tek başına oluşturursanız, hiçbir şey var. Boş bir ana hala hello altyapısı için aylık bir ücret doğurur. Bu adımları toocreate bir ILB ile bir ana ya da kendi kaynak grubundaki bir ana toocreate izleyin. Ana oluşturduktan sonra uygulama içinde hello normal işlemi kullanarak oluşturabilirsiniz. Yeni ana hello konumu olarak seçin.

1. Arama için Azure Marketi hello **uygulama hizmeti ortamı**, ya da seçin **yeni** > **Web mobil** > **uygulama hizmeti Ortam**. 

2. Merhaba, ana adını girin. Bu ad, hello ana oluşturulan hello uygulamalar için kullanılır. Merhaba adı ise *mynewdemoase*, hello alt etki alanı adı *. mynewdemoase.p.azurewebsites.net*. Adlı bir uygulama oluşturursanız, *mytestapp*, mytestapp.mynewdemoase.p.azurewebsites.net adreslenebilir. Merhaba adında boşluk kullanamazsınız. Büyük harf karakterler kullanırsanız, hello etki alanı adı hello toplam küçük hello adı sürümüdür. Bir ILB kullanırsanız, ana adınızı alt etki alanı içinde kullanılmaz, ancak bunun yerine ana oluşturma sırasında açıkça belirtilmiştir.

    ![Ana adlandırma][5]

3. Aboneliğinizi seçin. Bu abonelik ayrıca hello hello ana tüm uygulamaları kullanan bir yerdir. Başka bir abonelikte bir VNet, ana koymak olamaz.

4. Seçin veya yeni bir kaynak grubu belirtin. Merhaba kaynak grubu için ana kullanılan hello ağınız için kullanılan aynı olması gerekir. Varolan bir sanal ağ seçerseniz, hello kaynak grubu, ana için güncelleştirilmiş tooreflect seçimdir, sanal ağınızı. *Resource Manager şablonunu kullanırsanız, hello VNet kaynak grubundan farklı bir kaynak grubu ile bir ana oluşturabilirsiniz.* bir şablondan bir ana toocreate bkz [bir şablondan bir uygulama hizmeti ortamı oluşturma][MakeASEfromTemplate].

    ![Kaynak grubu seçimi][6]

5. VNet ve konumunu seçin. Yeni bir VNet oluşturun veya varolan bir sanal ağ seçin: 

    * Yeni bir VNet seçerseniz, bir ad ve konum belirtebilirsiniz. Merhaba yeni VNet hello adres aralığı 192.168.250.0/23 ve varsayılan adlı bir alt ağ vardır. Merhaba alt 192.168.250.0/24 tanımlanır. Yalnızca Resource Manager Vnet'i seçebilirsiniz. Merhaba **VIP türü** seçim belirler, ana doğrudan erişilebilir değilse hello Internet (harici) veya bir ILB kullanıyorsa. Bu seçenekler hakkında daha fazla toolearn bkz [oluşturma ve kullanma uygulama hizmeti ortamı olan bir iç yük dengeleyici][MakeILBASE]. 

      * Seçerseniz **dış** hello için **VIP türü**, kaç tane dış IP adresleri hello sistem IP tabanlı SSL amacıyla oluşturulur seçebilirsiniz. 
    
      * Seçerseniz **dahili** hello için **VIP türü**, ana kullanan hello etki alanına belirtmeniz gerekir. Bir ana ortak veya özel adres aralıkları kullanan bir sanal ağ dağıtabilirsiniz. bir ortak adres aralığına sahip bir VNet toouse, önceden toocreate hello VNet gerekir. 
    
    * Varolan bir sanal ağ seçerseniz, hello ana oluşturulduğunda, yeni bir alt ağ oluşturulur. *Merhaba Portalı'nda önceden oluşturulmuş bir alt ağ kullanılamıyor. Resource Manager şablonunu kullanırsanız, var olan bir alt ağ ile bir ana oluşturabilirsiniz.* bir şablondan bir ana toocreate bkz [bir şablondan bir uygulama hizmeti ortamı oluşturma][MakeASEfromTemplate].

## <a name="app-service-environment-v1"></a>App Service Ortamı v1 ##

Uygulama hizmeti ortamı'nı (ASEv1) ilk sürümü hello örneklerini oluşturabilirsiniz. işlem, arama hello Market toostart için **uygulama hizmeti ortamı v1**. Hello hello ana oluşturduğunuz aynı şekilde hello tek başına ana oluşturun. Sona erdiğinde, ASEv1 iki ön uçlar ve iki çalışanları vardır. ASEv1 ile Merhaba ön uçlar ve çalışanları yönetmeniz gerekir. Uygulama hizmeti planları oluşturduğunuzda otomatik olarak eklenir. Merhaba ön uçlar hello HTTP/HTTPS uç noktalar olarak davranmasına ve trafik toohello çalışanları gönderin. Merhaba, uygulamalarınızı barındırmak hello rolleri çalışanlardır. Ana oluşturduktan sonra ön uç ve çalışanları hello miktarını ayarlayabilirsiniz. 

toolearn ASEv1, hakkında daha fazla bilgi görmek [giriş toohello uygulama hizmeti ortamı v1][ASEv1Intro]. Ölçeklendirme ile ilgili daha fazla bilgi için bkz: yönetme ve ASEv1, izleme [nasıl tooconfigure bir uygulama hizmeti ortamı][ConfigureASEv1].

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
