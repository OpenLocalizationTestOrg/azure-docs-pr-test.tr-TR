---
title: "Logic Apps bağlayıcı aaaOverview | Microsoft Docs"
description: "Bir mantıksal uygulama kullanılabilir bağlayıcılar genel bakış"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>Bir mantıksal uygulama bağlayıcıları kullanma
Bağlayıcıları hızlı erişim tooevents, verilere ve eylemlere Hizmetleri, protokolleri ve platformlar sağlar.  Merhaba, Logic Apps destekler bağlayıcıların tam listesi için [bulunabilir burada](apis-list.md).  Bağlayıcılar, tetikleyici veya bir mantıksal uygulama içinde eylem olarak kullanılabilir ve yapılandırılan bir gerektirebilir *bağlantı* toouse (örneğin: hesap tooaccess veya sonrası sizin adınıza bir Twitter yetkilendirme).

## <a name="basics"></a>Temel Bilgiler
Bağlayıcılar olan bir mantıksal uygulama toointegrate Dynamics, Azure, Salesforce gibi diğer hizmetlerle bir parçası olarak erişim barındırılan Hizmetler [ve daha fazla](apis-list.md).  Bunlar dağıtılmış ve ölçek, performans ve güvenlik hallolduğuna ile tümleştirme akışlarınızı oluşturabilmeniz Microsoft tarafından yönetilmelidir.  Bir bağlayıcı tooa mantıksal uygulama arama ve bağlayıcı eylemini seçerek eklemek veya altında tetikleyicisi **Göster Microsoft yönetilen API'ler**.

![Tetikleyici seçmek için eylem menüsü][1]

Her bağlayıcı eylem veya tetikleyici özellikleri tooconfigure kendi kümesi sahip olur.  Merhaba bilgisi düğmeleri toolearn eylem hakkında daha fazla tıklayın veya belgelerinde başvuru [toolearn daha fazla](apis-list.md).

Bir hizmet veya değil API henüz bir bağlayıcı ile toointegrate istiyorsanız, logic apps aracılığıyla da genişletebilirsiniz bir [özel bağlayıcı](../logic-apps/logic-apps-create-api-app.md) veya yalnızca doğrudan toohello hizmeti gibi HTTP protokolü üzerinden çağırın.

## <a name="triggers"></a>Tetikleyiciler
Bazı bağlayıcılar, bağlayıcı bir olay bir mantıksal uygulama yangın ve herhangi bir veri hello tetikleyici bir parçası olarak geçirin anlamına gelir bir tetikleyici vardır.  Bir tetikleyici her zaman bir mantıksal uygulama ilk adımda hello ' dir.  Popüler tetikleyiciler gibi işlemleri içerir:

* Yineleme - her saat çalıştırın
* Bir HTTP isteği alındığında
* Bir öğe tooa sıra eklendiğinde
* Bir e-posta alındığında

Bazı tetikleyiciler hello bir olay bildirim toohello mantıksal uygulama gerçekleştirilir ve başkalarının ne sıklıkta hello mantıksal uygulama hello hizmet (yukarı tooevery 15 saniye) bir olay için denetleyecektir üzerinde yapılandırılmış bir yineleme aralığı gerekir anlık ateşlenir.  

Bir olayı alındığında çalıştırmak hello mantıksal uygulama ateşlenir ve hello Eylemler hello iş akışında başlar.  Aynı zamanda tüm veriler hello tetiklemek hello akışı genelinde mümkün tooaccess olacaktır (örnek hello 'üzerinde yeni bir tweet' için tetikleyici hello tweet çalıştırmak hello geçirir).

## <a name="actions"></a>Eylemler
Çoğu bağlayıcılar hello iş akışının bir parçası yürütülen bir veya daha çok eylemler vardır.  Merhaba çalıştırdıktan sonra herhangi bir adım tetikleyiciden harekete eylemlerdir.  tooadd eylemin hello tıklatın **yeni adım** düğmesi ve arama hello toouse istediğiniz Bağlayıcı.  Bir kez seçili (ve tüm yapılandırdıktan sonra [bağlantıları](#connections) gerekli olabilecek) yapılandırabileceğiniz hello eylem kartı görürsünüz.  Herhangi bir çıkış hello belirteçleri tıklayarak veri önceki adımları seçin veya diğer bir yapılandırmada gerektiği şekilde girin.

![Bir bağlayıcı eylemi yapılandırma][2]

## <a name="connections"></a>Bağlantılar
Çoğu bağlayıcılar tooconfigure gerektiren bir *bağlantı* hello bağlayıcı kullanmadan önce.  A *bağlantı* tüm oturum veya bağlantı yapılandırması gerekli tooaccess hello bağlayıcı.  OAuth kullanın, bir bağlantı oluşturmak bağlayıcıları için (örneğin, Office 365, Salesforce veya GitHub) burada erişim belirtecinizi kullanılabilir şifrelenir ve güvenli bir Azure gizli depolama alanına depolanır hello hizmete imzalama anlamına gelir.  Diğer bağlayıcıları (örneğin, FTP ve SQL) sunucusu adresi, kullanıcı adı ve parola gibi yapılandırmasını içeren bir bağlantı gerektirir.  Bu bağlantı yapılandırma ayrıntılarını da şifrelenir ve güvenli bir şekilde depolanır.  Merhaba hizmet izin verdiği sürece bağlantıları hello hizmeti için mümkün tooaccess olacaktır.  (Örneğin, Office 365 ve Dynamics) Azure Active Directory OAuth bağlantılarında biz toorefresh hello erişim belirteci belirsiz bir süre devam edebilir.  Diğer hizmetler, ne kadar süreyle biz bir belirteç yenilenen kullanabileceği üzerinde sınırları bırakabilir.  Genel bir parola değiştirme gibi bazı eylemler tüm erişim belirteci geçersiz kılar.  

Bağlantıları görüntülenebilir ve tıklayarak Azure'da yönetilen **Gözat** ve seçerek **API bağlantıları**.  API bağlantıları kaynak Hello görüntüleme, düzenleme, güncelleştirme veya oluşturmuş olduğunuz tüm bağlantıları yeniden yetkilendirin.

## <a name="next-steps"></a>Sonraki Adımlar
* [İlk mantıksal uygulamanızı oluşturma](../logic-apps/logic-apps-create-a-logic-app.md)
* [Ortak kullanımlar ve logic apps örnekleri öğrenin](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Enterprise Integration tetikleyiciler ve Eylemler kullanmaya başlama](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
