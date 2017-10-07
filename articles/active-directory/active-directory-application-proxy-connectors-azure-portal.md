---
title: "ayrı ağlar ve Azure AD uygulaması Proxy Bağlayıcısı grupları konumlardaki aaaPublishing uygulamaları | Microsoft Docs"
description: "Kapak nasıl toocreate ve Azure AD uygulama proxy'si bağlayıcılarını gruplarını yönetin."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Ayrı ağlarda ve konumları bağlayıcı gruplarını kullanarak uygulama yayımlama
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-application-proxy-connectors.md)
>

Müşteriler daha da fazla senaryoları için Azure AD uygulama proxy'si ve uygulamaları kullanın. Bu nedenle uygulama Proxy daha esnek daha fazla topolojileri etkinleştirerek yaptık. Böylece tooserve belirli uygulamaları belirli bağlayıcılar atayabilirsiniz uygulama Proxy Bağlayıcısı grupları oluşturabilirsiniz. Bu yetenek, daha fazla denetim ve yolları toooptimize sağlar, uygulama proxy'si dağıtım. 

Her uygulama ara sunucusu Bağlayıcısı tooa bağlayıcı grubu atanır. Tümü aynı bağlayıcı Grup hareket yüksek kullanılabilirlik ve Yük Dengeleme için ayrı bir birim olarak toohello ait bağlayıcılar hello. Tüm bağlayıcılar tooa bağlayıcı grubu ait. Grupları oluşturmazsanız, tüm bağlayıcılar bir varsayılan grubunda yer alan. Yöneticiniz, yeni gruplar oluşturabilir ve hello Azure Portalı'nda bağlayıcılar toothem atayın. 

Tüm uygulamaları tooa bağlayıcı grubuna atanır. Grupları oluşturmazsanız, tüm uygulamalarınızı tooa varsayılan grubuna atanır. Ancak, bağlayıcılar gruplar halinde düzenlemek, belirli bir bağlayıcının grubuyla her uygulama toowork ayarlayabilirsiniz. Bu durumda, bu gruptaki yalnızca hello bağlayıcılar hello uygulama istek üzerine hizmet. Bu özellik, uygulamalarınızı farklı konumlarda barındırılan yararlıdır. Uygulamalar her zaman fiziksel olarak Kapat toothem olan bağlayıcılar tarafından sunulan konuma göre bağlayıcı grupları oluşturabilirsiniz.

>[!TIP] 
>Büyük bir uygulama proxy'si dağıtımınız varsa, tüm uygulamaları toohello varsayılan bağlayıcı grubu atamayın. Tooan active Bağlayıcısı Grup atanıncaya kadar bu şekilde, tüm dinamik trafik yeni bağlayıcılar almadığınız. Bakım, kullanıcıları etkilemeden gerçekleştirebilmeleri için bu yapılandırma Ayrıca, boşta modda tooput bağlayıcılar geri toohello varsayılan grup taşıyarak sağlar.

## <a name="prerequisites"></a>Ön koşullar
toogroup, bağlayıcılar toomake emin olması, [birden çok bağlayıcı yüklü](active-directory-application-proxy-enable.md). Yeni bir bağlayıcı yüklediğinizde, onu otomatik olarak hello birleştirir **varsayılan** bağlayıcı grubu.

## <a name="create-connector-groups"></a>Bağlayıcı grupları oluşturma
Bu adımları toocreate istediğiniz sayıda bağlayıcı grubu kullanın. 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
1. Seçin **Azure Active Directory** > **kurumsal uygulamalar** > **uygulama proxy'si**.
2. Seçin **yeni bağlayıcı grubu**. Merhaba yeni bağlayıcı grubu dikey penceresi görünür.

   ![Yeni bir bağlayıcı grubunu seçin](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. Yeni bağlayıcı grubunuzu adlandırın, sonra Bağlayıcılar bu gruba ait hello açılır menü tooselect kullanın.
4. **Kaydet**’i seçin.

## <a name="assign-applications-tooyour-connector-groups"></a>Uygulamaları tooyour bağlayıcı grupları atama
Uygulama proxy'si ile yayımlanan her uygulama için bu adımları kullanın. İlk yayımladığınızda veya istediğinizde bu adımları toochange hello atamasını kullanabilirsiniz, uygulama tooa bağlayıcı grubu atayabilirsiniz.   

1. Merhaba yönetim panodan dizininizin seçin **kurumsal uygulamalar** > **tüm uygulamaları** > merhaba tooassign tooa bağlayıcı Grup istediğiniz uygulama >  **Uygulama proxy'si**.
2. Kullanım hello **bağlayıcı grup** istediğiniz uygulama toouse hello açılır menü tooselect hello grubu.
3. Seçin **kaydetmek** tooapply hello değiştirin.

## <a name="use-cases-for-connector-groups"></a>Bağlayıcı grupları için kullanım örnekleri 

Bağlayıcı grupları dahil olmak üzere çeşitli senaryolar için kullanışlıdır:

### <a name="sites-with-multiple-interconnected-datacenters"></a>Birden çok birbirine bağlı veri merkezleri ile siteleri

Birçok kuruluş, birbirine bağlı veri merkezleri sahiptir. Veri Merkezi çapraz bağlantıları pahalı ve yavaş olduğundan bu durumda, tookeep hello datacenter içindeki kadar trafiği mümkün olduğunca istediğiniz. Bağlayıcılar uygulamalarında hello veri merkezi içinde bulunan her veri merkezi tooserve yalnızca hello dağıtabilirsiniz. Bu yaklaşım, veri merkezi çapraz bağlantıları en aza indirir ve tooyour kullanıcılar tamamen saydam bir deneyim sağlar.

### <a name="applications-installed-on-isolated-networks"></a>Yalıtılmış ağlarda yüklü uygulamalar

Uygulamaları hello ana Kurumsal ağın parçası olmayan ağlara barındırılabilir. Yalıtılmış ağlarda tooalso yalıtmaya uygulamaları toohello ağda bağlayıcı grupları ayrılmış tooinstall bağlayıcılar kullanabilirsiniz. Bu, genellikle belirli bir uygulama, kuruluşunuz için bir üçüncü taraf satıcı tutar ortaya çıkar. 

Bağlayıcı gruplar, tooinstall bağlayıcıları kolaylaştırır, yalnızca belirli bir uygulama yayımlama bu ağlar için ayrılmış ve daha fazla toooutsource uygulama yönetimi toothird taraf satıcılar güvenliğini sağlar.

### <a name="applications-installed-on-iaas"></a>Iaas üzerinde yüklü uygulamalar 

Bulut erişimi için Iaas üzerinde yüklü uygulamalar için bağlayıcı grupları, bir ortak hizmet toosecure hello erişim tooall hello uygulamalar sağlar. Bağlayıcı gruplar şirket ağınızda ek bağımlılık oluşturun veya hello uygulama deneyimi parçalara yok. Bağlayıcılar, her bulut veri merkezinde yüklü olması ve yalnızca o ağda bulunan uygulamalar hizmet. Birkaç bağlayıcılar tooachieve yüksek kullanılabilirlik yükleyebilirsiniz.

Birden fazla sanal makine içeren bir kuruluş tootheir kendi barındırılan Iaas sanal ağa bağlı bir örnek olarak alın. tooallow çalışanların toouse Bu, bu özel ağların siteden siteye VPN kullanarak şirket ağına bağlı toohello uygulamalardır. Bu, şirket içinde olan çalışanlar için iyi bir deneyim sağlar. Ancak, çizimde hello gördüğünüz gibi şirket içinde ek altyapı tooroute erişim gerektirdiğinden, uzak çalışanlar için ideal olmayabilir:

![Azuread'i Iaas ağ](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
Azure AD uygulama ara sunucusu Bağlayıcısı gruplarıyla şirket ağınızda ek bağımlılık oluşturmadan ortak bir hizmet toosecure hello erişim tooall uygulamaları etkinleştirebilirsiniz:

![Azuread'i Iaas birden çok bulut satıcılar](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>Çoklu orman – her orman için farklı bağlayıcı grupları

Uygulama proxy'si dağıtmış olan müşterilerin çoğu, Kerberos Kısıtlı temsilci (KCD) gerçekleştirerek, çoklu oturum açma (SSO) özellikleri kullanıyor. tooachieve bu hello kullanıcılar Merhaba uygulaması doğru devredebilirsiniz hello bağlayıcı'nın makineler gerek toobe birleştirilmiş tooa etki alanı. KCD, ormanlar arası özelliklerini destekler. Ancak aralarında güven ayrı Çoklu orman ortamlarıyla olan şirketler için tek bir bağlayıcıyı tüm ormanlar için kullanılamaz. 

Bu durumda, belirli bağlayıcılar orman dağıtılabilir ve yayımlanan tooserve olan kümesi tooserve uygulamalar yalnızca bu belirli ormanda bulunan kullanıcılar ile Merhaba. Her bağlayıcı grubu farklı bir ormanda temsil eder. Merhaba Kiracı ve çoğu hello deneyimi birleşik karşın tüm ormanlar için kullanıcıların Azure AD grupları kullanarak tootheir orman uygulamaları atanabilir.
 
### <a name="disaster-recovery-sites"></a>Olağanüstü durum kurtarma sitelerinde

Sitelerinizin nasıl uygulandığını bağlı olarak bir olağanüstü durum kurtarma (DR) site ile yapabileceğiniz iki farklı yaklaşım vardır:

* DR sitenizi burada tam olarak hello ana site gibi ve sahip etkin-etkin modda oluşturulduysa aynı hello ağ ve AD ayarları, oluşturabileceğiniz hello bağlayıcılar hello hello DR sitesinde hello ana site aynı bağlayıcı grubu. Bu Azure AD toodetect yük devretme işlemlerini sizin için sağlar.
* DR sitenizi hello ana sitesinden ayrı, hello DR sitede farklı bağlayıcı grubu oluşturabilirsiniz ve ya da 1) yedekleme uygulamaları varsa veya 2) el ile gerektiği gibi hello varolan uygulama toohello DR bağlayıcı grubu yönlendir.
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>Tek bir kiracı birden çok şirket hizmet

Hizmetleri birden çok şirket için bir tek hizmet sağlayıcısı dağıtır ve Azure AD tutar modeli bir tooimplement ilgili birçok farklı yolu vardır. Bağlayıcı gruplar hello bağlayıcılar ve farklı gruplar halinde uygulamaları kurabilmeleri hello Yöneticisi yardımcı olur. Küçük şirketler için uygun olan bir şekilde tek bir toohave olduğu hello farklı şirketlerin kendi etki alanı adı ve ağlar varken Azure AD kiracısı. Bu da burada birkaç şirketler Düzenleyici ya da iş nedenleri için tek bir BT bölme hizmet M & A senaryoları ve durumlar için geçerlidir. 

## <a name="sample-configurations"></a>Örnek Yapılandırması

Uygulayabileceğiniz bazı örnekler bağlayıcı grupları aşağıdaki hello içerir.
 
### <a name="default-configuration--no-use-for-connector-groups"></a>Varsayılan yapılandırma – bağlayıcı grupları için hiçbir kullanın

Bağlayıcı grupları kullanmıyorsanız, yapılandırmanızı şöyle olabilir:

![Azuread'i bağlayıcı grup yok](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
Bu yapılandırma, küçük dağıtımları ve testleri için yeterlidir. İyi kuruluşunuzun bir düz ağ topolojisi varsa da çalışır.
 
### <a name="default-configuration-and-an-isolated-network"></a>Varsayılan yapılandırma ve yalıtılmış bir ağı

Bu yapılandırma hello varsayılan bir Iaas sanal ağ gibi yalıtılmış bir ağda çalışan belirli bir uygulamanın olduğu bir evrimi şöyledir: 

![Azuread'i bağlayıcı grup yok](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>Önerilen yapılandırması – birkaç belirli grupları için bir varsayılan grubu boşta

Önerilen yapılandırması büyük ve karmaşık kuruluşlarda hello toohave hello varsayılan bağlayıcı herhangi bir uygulama hizmet değil ve boşta veya yeni yüklenen bağlayıcıları için kullanılan bir grup olarak grubudur. Tüm uygulamalar, özelleştirilmiş bağlayıcı grupları kullanılarak sunulur. Bu, yukarıda açıklanan hello senaryoları tüm hello karmaşıklığını sağlar.

Merhaba aşağıdaki örnekte, iki veri merkezi, A ve B, her site hizmet iki bağlayıcı ile Merhaba şirket sahiptir. Her sitenin üzerinde çalışan farklı uygulamalar vardır. 

![Azuread'i bağlayıcı grup yok](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>Sonraki adımlar

* [Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)
* [Çoklu oturum açmayı etkinleştirme](application-proxy-sso-overview.md)


