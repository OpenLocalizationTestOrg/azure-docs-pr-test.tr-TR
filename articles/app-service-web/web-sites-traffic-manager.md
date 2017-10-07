---
title: "aaaControlling Azure web uygulaması trafiği ile Azure trafik Yöneticisi"
description: "TooAzure web uygulamaları ilgili olarak bu makalede Azure trafik Yöneticisi için Özet bilgiler sağlanır."
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Azure Traffic Manager ile Azure web uygulaması trafiğini denetleme
> [!NOTE]
> Bu makale, tooAzure App Service Web Apps ilgili olarak Microsoft Azure trafik Yöneticisi için Özet bilgiler sağlar. Daha fazla bilgi hakkında Azure Traffic Manager kendisini hello bu makalenin sonunda hello bağlantıları ziyaret ederek bulunabilir.
> 
> 

## <a name="introduction"></a>Giriş
Azure Traffic Manager toocontrol kullanabileceğiniz nasıl web istemcilerinden gelen istekleri dağıtılmış tooweb Azure App Service'te uygulamalardır. Web uygulama uç noktaları tooa Azure Traffic Manager profilini eklendiğinde, Azure trafik Yöneticisi (çalıştığından, durdurulduğundan veya silinmiş), web uygulamalarınızı hello durumunu böylece bu uç hangisinin trafik alması gereken karar verebilirsiniz izler.

## <a name="load-balancing-methods"></a>Yük Dengeleme yöntemleri
Azure Traffic Manager üç farklı bir Yük Dengeleme yöntemi kullanır. Bu liste tooAzure web uygulamaları ilgili olarak aşağıdaki hello açıklanmaktadır.

* **Yük devretme**: web uygulaması kopyalar farklı bölgelerde varsa, bu yöntem tooconfigure bir web uygulaması tooservice tüm web istemci trafiğini kullanın ve başka bir web uygulaması örneği hello ilk web uygulamanızı trafiği farklı bir bölgeye tooservice yapılandırın kullanılamaz duruma gelir.
* **Hepsini bir kez**: web uygulaması kopyalar farklı bölgelerde varsa, bu yöntem toodistribute trafiği eşit hello web uygulamalarında de farklı bölgelerdeki kullanabilirsiniz.
* **Performans**: hello performans yöntemi hello kısa gidiş dönüş süresi tooclients üzerinde göre trafiği dağıtır. Merhaba performans yöntemi hello içindeki web uygulamaları için kullanılabilir aynı bölgede ya da farklı bölgelerde.

## <a name="web-apps-and-traffic-manager-profiles"></a>Web uygulamaları ve trafik Yöneticisi profilleri
tooconfigure hello denetim web uygulaması trafik, Azure trafik Yöneticisi'nde hello üç yük dengeleyici daha önce açıklanan yöntemlerinden birini kullanan bir profil oluşturmak ve toocontrol trafiği toohello istediğiniz hello uç noktaları (Bu durumda, web uygulamaları) Ekle profili. (Çalıştığından, durdurulduğundan veya silinmiş), web uygulaması durumu olan düzenli olarak iletildiğinden toohello profil böylece Azure Traffic Manager trafik uygun şekilde yönlendirebilirsiniz.

Azure Traffic Manager ile Azure kullanırken aşağıdaki noktaları göz önünde hello bulundurun:

* Merhaba içindeki web uygulama yalnızca dağıtımları için aynı bölgede, Web uygulamaları zaten şekilde tooweb uygulama modu olmadan yük devretme ve hepsini işlevsellik sağlar.
* İçin dağıtımlarda Merhaba Web uygulamaları başka bir Azure bulut hizmeti ile birlikte kullanın aynı bölgede, iki uç noktaları tooenable karma senaryo türlerini birleştirebilirsiniz.
* Bu gibi durumlarda, her bölge bir web uygulaması uç noktası yalnızca bir profil belirtebilirsiniz. Bir bölge için bir uç nokta olarak bir web uygulaması seçtiğinizde, bu profil için seçilmek kullanılamaz hale bu bölgedeki diğer web uygulamaları hello.
* bir Azure Traffic Manager profili belirtmeniz hello web uygulama uç noktaları hello altında görünür **etki alanı adları** bölümünde hello Yapılandır sayfasında hello profil hello web uygulaması, ancak orada yapılandırılabilir olmaz.
* Bir web uygulaması tooa profili ekledikten sonra hello **Site URL'si** bir ayarlamış olduğunuz hello Pano hello Web üzerinde uygulamanızın portal sayfası hello web uygulamasının hello özel etki alanı URL'sini görüntüler. Aksi takdirde hello trafik Yöneticisi profili URL'si gösterilir (örneğin, `contoso.trafficmgr.com`). Her ikisi de hello web uygulamasının doğrudan etki alanı adı hello ve hello trafik Yöneticisi URL hello web uygulamanızın yapılandırma sayfasında hello altında görünür olacaktır **etki alanı adları** bölümü.
* Özel etki alanı beklenen şekilde, ancak ek tooadding bunları tooyour web uygulamaları çalışır, DNS harita toopoint toohello trafik Yöneticisi URL yapılandırmanız gerekir. Hakkında bilgi için bir Azure web uygulaması için özel bir etki alanı tooset bkz [bir Azure web sitesi için bir özel etki alanı adı yapılandırma](app-service-web-tutorial-custom-domain.md).
* Yalnızca standart veya premium modunda tooa Azure Traffic Manager profilini web uygulamaları da ekleyebilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar
Bir kavramsal ve teknik genel bakış Azure trafik Yöneticisi'nin için bkz: [trafik Yöneticisi'ne genel bakış](../traffic-manager/traffic-manager-overview.md).

Trafik Yöneticisi Web uygulamaları ile kullanma hakkında daha fazla bilgi için bkz: hello blog gönderileri [kullanarak Azure Traffic Manager ile Azure Web siteleri](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) ve [Azure Traffic Manager artık Azure Web siteleri ile tümleştirmek](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

