---
title: "aaaClassic portal Azure AD uygulaması Proxy bağlayıcılar | Microsoft Docs"
description: "Kapak nasıl toocreate ve Azure AD uygulama proxy'si bağlayıcılarını gruplarını yönetin."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
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
>

Bağlayıcı grupları dahil olmak üzere çeşitli senaryolar için kullanışlıdır:

* Birden çok birbirine bağlı veri merkezleri siteleriyle. Veri Merkezi çapraz bağlantıları pahalı ve yavaş olduğundan bu durumda, tookeep hello datacenter içindeki kadar trafiği mümkün olduğunca istediğiniz. Bağlayıcılar uygulamalarında hello veri merkezi içinde bulunan her veri merkezi tooserve yalnızca hello dağıtabilirsiniz. Bu yaklaşım, veri merkezi çapraz bağlantıları en aza indirir ve tooyour kullanıcılar tamamen saydam bir deneyim sağlar.
* Merhaba ana Kurumsal ağın parçası olmayan yalıtılmış ağlarda yüklü uygulamaları yönetme. Yalıtılmış ağlarda tooalso yalıtmaya uygulamaları toohello ağda bağlayıcı grupları ayrılmış tooinstall bağlayıcılar kullanabilirsiniz.
* Bulut erişimi için Iaas üzerinde yüklü uygulamalar için bağlayıcı grupları, bir ortak hizmet toosecure hello erişim tooall hello uygulamalar sağlar. Bağlayıcı gruplar şirket ağınızda ek bağımlılık oluşturun veya hello uygulama deneyimi parçalara yok. Bağlayıcılar, her bulut veri merkezinde yüklü ve bu ağda bulunan uygulamalar sunar. Birkaç bağlayıcılar tooachieve yüksek kullanılabilirlik yükleyebilirsiniz.
* İçinde belirli bağlayıcılar orman dağıtılabilir ve tooserve belirli uygulamaları birden çok orman ortamlarına desteği.
* Bağlayıcı grupları tooeither yük devretme algılamak veya yedekleme için olarak hello ana olağanüstü durum kurtarma sitede kullanılabilir site.
* Bağlayıcı grupları için de birden çok şirketler tek bir kiracı tarafından kullanılan tooserve olabilir.

## <a name="prerequisite-create-your-connectors"></a>Önkoşul: oluşturma, bağlayıcılar
toogroup, bağlayıcılar [birden çok bağlayıcı yükleme](active-directory-application-proxy-enable.md), ardından ad ve gruplandırın. Son olarak tooassign olması bunları toospecific uygulamalar.

## <a name="step-1-create-connector-groups"></a>1. adım: bağlayıcı grupları oluşturma
İstediğiniz sayıda bağlayıcı grupları oluşturabilirsiniz. Bağlayıcı grup oluşturma hello Klasik Azure portalı gerçekleştirilir.

1. Dizininizi seçin ve tıklatın **yapılandırma**.  
    ![Uygulama proxy'si, yapılandırma ekran görüntüsü - bağlayıcı gruplarının Yönet'e tıklayın](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. Uygulama proxy'si altında tıklatın **bağlayıcı grupları yönet** ve hello Grup bir ad verip bir bağlayıcı grubu oluşturun.  
    ![Uygulama Ara sunucusu Bağlayıcısı ekran görüntüsü - ad yeni grup gruplar](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>2. adım: bağlayıcıları tooyour grupları atama
Merhaba bağlayıcı grupları oluşturulduktan sonra hello bağlayıcılar toohello uygun Grup taşıyın.

1. Altında **uygulama proxy'si**, tıklatın **yönetmek Bağlayıcılar**.
2. Altında **grup**seçin her bağlayıcı için istediğiniz hello grubu. Merhaba yeni grubunda active too10 dakika toobecome hello bağlayıcılar alabilir.  
    ![Uygulama proxy'si bağlayıcılar ekran görüntüsü - açılır menüsünden grubunu seçin](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>3. adım: uygulama tooyour bağlayıcı grupları atama
Merhaba son adımı tooset sunduğu her uygulama toohello bağlayıcı grubudur.

1. Select hello dizininizde, Klasik Azure portalı içinde tooassign toohello Grup istediğiniz uygulama hello **yapılandırma**.
2. Altında **bağlayıcı grup**seçin istediğiniz uygulama toouse hello hello grubu. Bu değişikliği hemen uygulanır.  
    ![Uygulama proxy Bağlayıcısı Grup ekran görüntüsü - açılır menüsünden grubunu seçin](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Ayrıca bkz.
* [Uygulama Ara sunucusunu etkinleştirme](active-directory-application-proxy-enable.md)
* [Çoklu oturum açmayı etkinleştirme](active-directory-application-proxy-sso-using-kcd.md)
* [Koşullu erişimi etkinleştirme](active-directory-application-proxy-conditional-access.md)
* [Uygulama Ara sunucusu ile ilgili sorunları giderme](active-directory-application-proxy-troubleshoot.md)

Merhaba en son haberler ve güncelleştirmeler için hello denetleyin [uygulama ara sunucusu bloguna](http://blogs.technet.com/b/applicationproxyblog/)
