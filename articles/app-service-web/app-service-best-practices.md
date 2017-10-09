---
title: "Azure App Service için aaaBest yöntemler"
description: "En iyi yöntemler ve Azure App Service için sorun giderme öğrenin."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Azure Uygulama Hizmeti için En İyi Uygulamalar
Bu makalede kullanmak için en iyi uygulamalar özetlenmektedir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). 

## <a name="colocation"></a>Birlikte bulundurma
Bir web uygulaması ve bir veritabanı gibi bir çözüm oluşturma Azure kaynaklarını farklı bölgelerde hello efektleri zaman bulunan hello aşağıdakileri içerebilir:

* Kaynaklar arasındaki iletişimde daha yüksek gecikme süresi
* Para ücretleri için giden veri aktarımı üzerinde hello belirtildiği gibi bölgeler arası [Azure fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/data-transfers).

Birlikte bulundurma hello aynı bölgede bir web uygulaması gibi bir çözüm oluşturma Azure kaynakları için en iyisidir ve toohold içeriği veya veri bir veritabanı veya depolama hesabı kullanılır. Ne zaman belirli iş ya da bunları değil toobe nedeni tasarım sürece bulundukları emin olmalısınız Oluşturma kaynakları aynı Azure bölgesinde hello. Bir uygulama hizmeti uygulaması toohello taşıyabilirsiniz hello yararlanarak veritabanınızla aynı bölgede [uygulama kopyalama özelliği hizmeti](app-service-web-app-cloning-portal.md) Premium App Service planı uygulamalar için kullanılabilir.   

## <a name="memoryresources"></a>Ne zaman beklenenden daha fazla bellek uygulamaları kullanma
Ne zaman fark uygulama izleme aracılığıyla belirtildiği gibi beklenenden daha fazla bellek kullanır veya hizmet önerileri göz önünde bulundurun hello [uygulama hizmeti otomatik düzeltme özelliği](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites). Merhaba otomatik düzeltme özelliği için hello seçeneklerden birini bir bellek eşiğine dayalı özel eylemler sürüyor. Gelen e-posta bildirimleri tooinvestigation hello çalışan işlem geri dönüştürme tarafından bellek dökümü tooon-nokta azaltma aracılığıyla Eylemler aralık hello spektrumun. Otomatik Düzeltme yapılandırılabilir web.config aracılığıyla ve kolay bir kullanıcı arabirimi aracılığıyla hello için bu Web günlüğü gönderisinde bölümünde anlatıldığı gibi [App Service destek Site uzantısı](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps).   

## <a name="CPUresources"></a>Ne zaman uygulamaları beklenenden daha fazla CPU kullanır
Ne zaman bir uygulama beklenen veya karşılaştığında olandan daha fazla CPU kullanan fark CPU ani izleme aracılığıyla belirtildiği şekilde yinelenen veya ölçeklendirmeyi veya uygulama hizmeti planı hello ölçeklendirme hizmet önerileri göz önünde bulundurun. Uygulamanızı statefull uygulamanız ise durum bilgisiz, ölçekleme çıkış size daha fazla esneklik ve daha yüksek ölçek olası verecektir sırada ölçeklendirmeyi hello tek seçenek ise. 

"Statefull" vs "durum bilgisiz" uygulamalar hakkında daha fazla bilgi için bu videoyu izleyebilirsiniz: [ölçeklenebilir baştan sona çok katmanlı bir uygulama Microsoft Azure Web uygulaması üzerinde planlama](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid). Uygulama hizmeti ölçekleme ve otomatik ölçeklendirme seçenekleri hakkında daha fazla bilgi için okumaya devam edin: [bir Web uygulamasını Azure App Service'te ölçeklendirme](web-sites-scale.md).  

## <a name="socketresources"></a>Ne zaman yuva kaynakları tükendi
Tükettiğini giden TCP bağlantıları için ortak bir nedeni hello uygulanan tooreuse TCP bağlantısı olmayan istemci kitaplıklarından birini ya da daha yüksek bir düzeyinde Protokolü HTTP - değil işlevden tutma gibi hello durumda kullanılır. Lütfen yapılandırılmış veya kodunuz verimli kullanılmasını giden bağlantılar için erişilebilir, App Service planı tooensure hello uygulamalarında başvurduğu hello kitaplıkların her hello belgelerini gözden geçirin. Ayrıca uygun oluşturma ve bağlantıları sızmasını sürümü veya temizleme tooavoid hello kitaplığı belgeleri yönergeleri izleyin. Bu tür istemci kitaplıkları araştırmalar işlenirken ilerleme etkisi toomultiple örnekleri ölçeklendirme tarafından azaltıldığından.  

## <a name="appbackup"></a>Ne zaman uygulamanızı yedekleme başarısız başlatır
Uygulama yedekleme başarısız neden olan iki en yaygın nedenleri hello: Geçersiz depolama ayarları ve geçersiz veritabanı yapılandırması. Değişiklikleri toostorage veya veritabanı kaynakları veya nasıl değişiklikler olduğunda bu hatalar genellikle durum tooaccess bu kaynakları (örneğin hello yedekleme ayarlarında seçili hello veritabanı için güncelleştirilmiş kimlik). Yedeklemeleri genellikle bir zamanlamaya göre çalışmasını ve (için kopyalama ve hello yedeklemeye dahil edilen içeriği toobe okuma) (için dosyalar yedeklendi hello çıktısı) erişim toostorage ve veritabanları gerektirir. Merhaba ya da bu kaynakları olacaktır tooaccess başarısız sonucu tutarlı yedekleme hatası. 

Lütfen yedekleme hatası oluştuğunda, hangi tür hatanın gerçekleştiği en son sonuçları toounderstand gözden geçirin. Depolama erişim hataları hello durumda, lütfen gözden geçirin ve hello yedekleme yapılandırmada kullanılan hello depolama ayarlarını güncelleştirin. Veritabanı erişim hataları hello durumda, lütfen gözden geçirin ve uygulama ayarlarının bir parçası, bağlantı dizelerini güncelleştirmek; tooupdate devam yedekleme yapılandırması tooproperly gerekli hello veritabanlarını içerir. Uygulama yedekleme hakkında daha fazla bilgi için lütfen hello bakın [Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md) belgeleri.

## <a name="nodejs"></a>Yeni Node.js uygulamalarını dağıtılan tooAzure uygulama hizmeti olduğunda
Azure uygulama hizmeti varsayılan Node.js uygulamaları için hedeflenen toobest seri hello en yaygın uygulamaları ihtiyaçlarını yapılandırmadır. Node.js uygulamanız için yapılandırma veya kişiselleştirilmiş ayarlama tooimprove performansı fayda CPU/bellek/ağ kaynakları için kaynak kullanımı en iyi duruma getirme, bizim en iyi yöntemler ve sorun giderme adımlarını gözden. Bu belge makalede ihtiyacınız olabilecek hello iisnode ayarları açıklanır Node.js uygulamanız için tooconfigure açıklar çeşitli senaryolar veya uygulamanızın karşılaştığı sorunları ve gösterir nasıl hello tooaddress bu sorunları: [en iyi uygulamalar ve Azure App Service'te düğümü uygulamalar için sorun giderme kılavuzu](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md).   

