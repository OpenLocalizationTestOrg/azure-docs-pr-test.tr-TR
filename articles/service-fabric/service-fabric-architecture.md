---
title: Azure Service Fabric aaaArchitecture | Microsoft Docs
description: "Service Fabric bir dağıtılmış sistemler platform toobuild ölçeklenebilir, güvenilir ve kolay yönetilen uygulamaları hello bulut için kullanılır. Bu makalede, Service Fabric hello mimarisi gösterilmektedir."
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Service Fabric mimarisi
Service Fabric katmanlı alt sistemleri ile yerleşik olarak bulunur. Bu alt sistemleri toowrite uygulamalar etkinleştirin:

* Yüksek oranda kullanılabilir
* Ölçeklenebilir
* Yönetilebilir
* Test edilebilir

Diyagram aşağıdaki hello hello Service Fabric, ana alt sistemleri gösterir.

![Service Fabric mimarisi diyagramı](media/service-fabric-architecture/service-fabric-architecture.png)

Dağıtılmış bir sistemde hello özelliği toosecurely iletişim düğümler arasında bir küme çok önemlidir. Merhaba temel hello yığınının düğümler arasında güvenli iletişim sağlar hello aktarım alt sistemidir. Hello aktarım hello Federasyon alt sistemi, böylece Service Fabric hatalarını algılayacak, öncü seçim gerçekleştirmek ve tutarlı yönlendirme sağlayan hangi kümeleri farklı düğümler (kümeleri olarak adlandırılır) tek bir varlık hello. alt sistemi arasındadır. Merhaba Federasyon alt sistemi üzerinde katmanlanmış hello güvenilirlik alt sistemi, çoğaltma, kaynak yönetimi ve yük devretme gibi mekanizmaları Service Fabric hizmetleriyle hello güvenilirliğini sorumludur. Merhaba Federasyon alt sistemi aynı zamanda bir uygulamanın tek bir düğümde hello yaşam döngüsü yöneten hello barındırma ve etkinleştirme alt sistemi, vurgular. Merhaba yönetimi alt hello yaşam döngüsü, uygulamaların ve hizmetlerin yönetir. Merhaba Test Edilebilirlik alt sistemi hizmetlerini benzetimli hataları aracılığıyla test önce ve uygulamaları ve Hizmetleri tooproduction ortamları dağıttıktan sonra uygulama geliştiricileri yardımcı olur. Service Fabric tooresolve hizmet konumları, iletişim alt sistemi aracılığıyla hello yeteneği sağlar. gösterilen toodevelopers hello uygulama modeli tooenable araçları ile birlikte bu alt sistemleri üzerinde katmanlanmış uygulama programlama modelleri hello.

## <a name="transport-subsystem"></a>Taşıma alt sistemi
Merhaba aktarım subsystem bir noktadan noktaya veri birimi iletişim kanalı uygular. Bu kanal, service fabric kümeleri içinde iletişim ve hello service fabric kümesi ve istemciler arasında iletişim için kullanılır. Tek yönlü destekler ve yayın ve çok noktaya yayını uygulamak üzere hello temelini istek-yanıt iletişim düzenleri Federasyon katman hello. Merhaba aktarım subsystem X509 kullanarak iletişimin güvenliğini sağlar sertifikalar veya Windows Güvenliği. Bu alt sistemi Service Fabric tarafından dahili olarak kullanılır ve uygulama programlama için doğrudan erişilebilir toodevelopers değil.

## <a name="federation-subsystem"></a>Federasyon alt sistemi
Dağıtılmış bir sistemde düğümler kümesi hakkında sipariş tooreason içinde toohave hello sistem tutarlı bir görünümünü gerekir. Dikiş hakkında neden tek bir birleşik kümesinde çeşitli düğümleri hello ve hello aktarım alt sistemi tarafından sağlanan hello iletişimi temelleri Hello Federasyon alt sistemi kullanır. Bu, dağıtılmış hello sistemleri temelleri tarafından diğer alt sistemleri - hata algılama, öncü seçim ve tutarlı yönlendirme hello sağlar. Merhaba Federasyon alt dağıtılmış karma tabloları 128-bit belirteci alanı ile en üstünde yerleşik olarak bulunur. Merhaba alt sistemi halka topolojisi her düğümü hello belirteç alan bir kısmı için sahiplik ayrılan hello halkası bulunan hello düğümler üzerinden oluşturur. Hata algılaması için hello katman vuruş Kalp ve yönetimini dayalı bir kiralama mekanizması kullanır. Merhaba Federasyon alt sistemi, ayrıca karmaşık birleştirme ve herhangi bir anda yalnızca tek bir sahibi belirtecin var. ayrılma protokolleri aracılığıyla garanti eder. Bu kılavuz seçim ve tutarlı yönlendirme garantileri sağlar.

## <a name="reliability-subsystem"></a>Güvenilirlik alt sistemi
Merhaba güvenilirlik subsystem sağlar hello mekanizması toomake hello hello hello kullanarak yüksek oranda kullanılabilir bir Service Fabric hizmetinin durumunu *çoğaltıcı*, *Yük Devretme Yöneticisi*, ve  *Kaynak dengeleyicisi*.

* Merhaba çoğaltıcı hello birincil hizmet çoğaltma durumu değişiklikleri otomatik olarak çoğaltılmış toosecondary çoğaltmalar, hizmet çoğaltma kümesinde hello birincil ve ikincil çoğaltmalar arasında tutarlılığı koruma olmasını sağlar. Merhaba çoğaltıcı, çekirdek Yönetimi hello yineleme kümesindeki hello çoğaltmalar arasında sorumludur. Merhaba yük devretme birimi tooget hello listesi işlemleri tooreplicate ile etkileşim kurar ve isteğe bağlı olarak hello yeniden yapılandırma aracısı hello çoğaltma kümesi hello yapılandırmayla sağlar. Bu yapılandırma, çoğaltılan toobe hangi çoğaltmaları hello işlemlere ihtiyaç gösterir. Service Fabric yüksek oranda kullanılabilir ve güvenilir model API toomake hello hizmet durumu programlama hello tarafından kullanılan Fabric çoğaltması olarak adlandırılan bir varsayılan çoğaltıcı sağlar.
* Merhaba Yük Devretme Yöneticisi düğümleri hello kümeden kaldırılmış tooor eklendiğinde hello yük otomatik olarak hello kullanılabilir düğümleri arasında dağıtılır sağlar. Merhaba kümedeki bir düğüm başarısız olursa, hello küme hello hizmet çoğaltmaları toomaintain kullanılabilirlik otomatik olarak yeniden yapılandırır.
* Hello Resource Manager hello kümedeki hata etki alanı arasında hizmet çoğaltmaları yerleştirir ve tüm yük devretme birimi işletimsel olmasını sağlar. Merhaba Resource Manager ayrıca küme düğümleri tooachieve en iyi Tekdüzen yük dağıtımı paylaşılan havuzu temel hello arasında hizmet kaynakları dengeler.

## <a name="management-subsystem"></a>Yönetim alt sistemi
Merhaba yönetimi alt uçtan uca hizmet ve uygulama yaşam döngüsü yönetimi sağlar. PowerShell cmdlet'leri ve yönetim API tooprovision etkinleştirmek, dağıtma, düzeltme eki, yükseltme ve kullanılabilirlik kaybı olmadan uygulamaları sağlanmasını. Merhaba yönetimi alt bu hizmetleri aşağıdaki hello gerçekleştirir.

* **Küme Yöneticisi'ni**: Bu uygulamalardan güvenilirlik tooplace hello hello hizmet yerleştirme kısıtlamalarına göre hello düğümlerde hello Yük Devretme Yöneticisi ile etkileşim kuran hello birincil hizmetidir. Yük devretme alt sistemi Kaynak Yöneticisi'ni Hello hello kısıtlamaları hiçbir zaman bozuk olmasını sağlar. Merhaba Küme Yöneticisi'ni hello yaşam hello uygulamalar, sağlama toode-karşılık yönetir. Uygulama kullanılabilirliği yükseltmeler sırasında bir anlam sistem durumu açısından kaybı olmadığından emin hello sistem durumu Yöneticisi tooensure ile tümleşir.
* **Sağlık Yöneticisi**: Bu hizmet uygulamaları, hizmetleri ve küme varlık sistem durumu izleme sağlar. Küme varlıklar (örneğin, düğümleri, hizmet bölümler ve çoğaltmalar) hello Merkezi durum deposuna toplanabilecek sistem durumu bilgilerini bildirebilirsiniz. Bu sistem durumu bilgileri hello Hizmetleri ve tootake etkinleştirme hello kümedeki birden çok düğüm arasında dağıtılmış düğümleri noktası zaman genel sistem görüntüsünü gereken tüm düzeltici eylemleri sağlar. Sistem durumu sorgusu API'leri tooquery hello sistem durumu olayları etkinleştirmeniz toohello sistem durumu alt sisteminin bildirdiği. Hello sistem durumu sorgusu API'leri hello durumu depolanan hello ham sistem durumu verilerini depolamak veya hello bir araya getirilir, belirli küme varlık için sistem durumu veri yorumlanan döndür.
* **Image Store**: Bu hizmet uygulama ikili dosyaları depolama ve hello dağıtımını sağlar. Bu hizmet hello uygulamaları karşıdan yüklenen tooand olduğu bir basit dağıtılmış dosya deposu sağlar.

## <a name="hosting-subsystem"></a>Barındırma alt sistemi
Merhaba Küme Yöneticisi hizmet (her düğüm üzerinde çalışan) alt sistemi barındırma hello toomanage belirli bir düğüm için gereken bildirir. alt sistemi sonra barındırma hello hello yaşam döngüsü bu düğümde hello uygulamasının yönetir. Merhaba çoğaltmaları düzgün yerleştirilir ve iyi durumda hello güvenilirlik ve sistem durumu bileşenlerini tooensure ile etkileşim.

## <a name="communication-subsystem"></a>İletişim alt sistemi
Bu alt sistemi hello adlandırma hizmeti aracılığıyla hello küme ve hizmet bulma içinde güvenilir Mesajlaşma sağlar. Merhaba adlandırma hizmeti hello Küme hizmeti adları tooa konumunda çözümler ve kullanıcıların toomanage hizmet adları ve özellikleri sağlar. Merhaba adlandırma hizmeti kullanıldığında, istemciler güvenli bir şekilde hello küme tooresolve herhangi bir düğümün bir hizmet adı iletişim ve hizmet meta verilerini alma. Basit bir adlandırma İstemcisi API kullanarak, hizmetler ve istemcileri hello geçerli ağ konumunu düğümü yeni bir dinamizm veya hello hello kümesini yeniden boyutlandırma rağmen çözme özellikli Service Fabric kullanıcılarının geliştirebilirsiniz.

## <a name="testability-subsystem"></a>Test Edilebilirlik alt sistemi
Test Edilebilirlik Service Fabric üzerinde oluşturulmuş Hizmetleri test etmek için özellikle tasarlanmış araçlar paketidir. Merhaba araçlar sağlayan bir geliştirici kolayca anlamlı hataları anlamına ve test senaryoları tooexercise çalıştırmak ve doğrulamak çok sayıda durumları ve hizmet yaşam süresi boyunca, tüm bir denetimli ve güvenli bir şekilde yaşar geçişleri hello. Test Edilebilirlik mekanizması toorun çeşitli olası hataları kullanılabilirlik kaybetmeden yineleyebilirsiniz uzun testleri de sağlar. Bu olan bir üretim, test ortamı sağlar.

