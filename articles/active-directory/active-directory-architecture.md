---
title: Azure Active Directory mimarisini anlama | Microsoft Docs
description: "Azure AD kiracısının ne olduğu ve Azure'ın, Azure Active Directory üzerinden nasıl yönetileceği açıklanmaktadır."
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: mtillman
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/08/2017
ms.author: markvi
ms.openlocfilehash: bf56ff167a988acd5f1163ff78beec281a654eb8
ms.sourcegitcommit: f46cbcff710f590aebe437c6dd459452ddf0af09
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/20/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Azure Active Directory mimarisini anlama
Azure Active Directory (Azure AD), kullanıcılarınız için Azure hizmet ve kaynaklarına erişimi güvenli bir şekilde yönetmenizi sağlar. Azure AD ile birlikte eksiksiz kimlik yönetimi olanakları sunulur. Azure AD özellikleri hakkında daha fazla bilgi için bkz. [Azure Active Directory nedir?](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)

Azure AD ile kullanıcı ve gruplar oluşturup bunları yönetebilir, ayrıca kurumsal kaynaklara erişim izni vermek ya da erişimi reddetmek için izinleri etkinleştirebilirsiniz. Kimlik yönetimi hakkında bilgi için bkz. [Azure kimlik yönetimi ile ilgili temel bilgiler](https://docs.microsoft.com/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Azure AD mimarisi
Azure AD’nin coğrafi olarak dağıtılmış mimarisi, müşterilerimize kurumsal düzeyde kullanılabilirlik ve performans sunmamızı sağlayan kapsamlı izleme, otomatik yeniden yönlendirme, yük devretme ve kurtarma özelliklerini bir araya getirir.

Bu makalede aşağıdaki mimari öğeler ele alınmaktadır:
 *  Hizmet mimarisi tasarımı
 *  Ölçeklenebilirlik 
 *  Sürekli kullanılabilirlik
 *  Veri merkezleri

### <a name="service-architecture-design"></a>Hizmet mimarisi tasarımı
Ölçeklenebilir, yüksek oranda kullanılabilir ve veri bakımından zengin bir sistem oluşturmanın en yaygın yolu, Azure AD veri katmanı için bağımsız yapı taşları veya *bölüm* adı verilen ölçek birimleri kullanılmasıdır. 

Veri katmanında, okuma-yazma özelliği sağlayan çok sayıda ön uç hizmeti bulunur. Aşağıdaki diyagramda, tek dizinli bir bölüme ait bileşenlerin, coğrafi olarak dağıtılmış veri merkezlerine nasıl dağıtıldığı gösterilmektedir. 

  ![Tek Dizinli Bölümler](./media/active-directory-architecture/active-directory-architecture.png)

Azure AD mimarisinin bileşenleri, birincil çoğaltma ve ikincil çoğaltma öğelerini içerir.

**Birincil çoğaltma**

*Birincil çoğaltma*, ait olduğu bölüm için *yazma* işlemlerini alır. Her yazma işlemi, çağırana başarılı sonucu döndürmeden önce hemen farklı bir veri merkezindeki ikincil çoğaltmaya çoğaltılır, böylece yazma işlemlerinin coğrafi olarak yedekli dayanıklılığı sağlanır.

**İkincil çoğaltmalar**

Tüm dizin *okumaları*, fiziksel olarak farklı coğrafi bölgelerde bulunan veri merkezlerindeki *ikincil çoğaltmalardan* sunulur. Veriler zaman uyumsuz olarak kopyalandığı için çok sayıda ikincil çoğaltma vardır. Kimlik doğrulama istekleri gibi dizin okumaları, müşterilerimize yakın veri merkezlerinden sunulur. İkincil çoğaltmalar, okuma ölçeklenebilirliğinden sorumludur.

### <a name="scalability"></a>Ölçeklenebilirlik

Ölçeklenebilirlik, bir hizmetin artan performans taleplerine göre genişleyebilme becerisidir. Yazma ölçeklenebilirliği, veri bölümlendirilerek sağlanır. Okuma ölçeklenebilirliği, bir bölümden dünyanın dört bir yanına dağıtılmış birden fazla ikincil çoğaltmaya verilerin çoğaltılması yoluyla sağlanır.

Dizin uygulamalarından gelen istekler, genellikle fiziksel olarak en yakın oldukları veri merkezine yönlendirilir. Yazma işlemleri, okuma-yazma tutarlılığı sağlamak üzere şeffaf bir şekilde birincil çoğaltmaya yönlendirilir. Dizinler çoğu zaman okuma işlemlerini sunduğundan, ikincil çoğaltmalar bölümlerin ölçeğini önemli ölçüde genişletir.

Dizin uygulamaları en yakın veri merkezlerine bağlanır. Bunun yapılması performansı artırır ve böylece ölçek genişletme mümkün olur. Bir dizin bölümünde çok sayıda ikincil çoğaltma olabileceğinden, ikincil çoğaltmalar dizin istemcilerine daha yakın yerleştirilebilir. Yalnızca yazma yoğunluklu olan iç dizin hizmeti bileşenleri, etkin birincil çoğaltmayı doğrudan hedefler.

### <a name="continuous-availability"></a>Sürekli kullanılabilirlik

Kullanılabilirlik (veya çalışma süresi) bir sistemin kesintisiz çalışma yeteneğini tanımlar. Azure AD’nin yüksek kullanılabilirliğinin anahtarı, hizmetlerimizin trafiği coğrafi olarak dağıtılmış birden fazla veri merkezinde hızla taşıyabilmesidir. Her veri merkezi birbirinden bağımsızdır ve bu özelliği sayesinde bağıntısız hata modları sağlar.

Azure AD’nin bölüm tasarımı, kurumsal AD tasarımına kıyasla basittir ve bu özellik, sistemin ölçeğini artırmak için kritik öneme sahiptir. Birincil çoğaltma yük devretme işleminin belirli şekilde gerçekleştirildiği, dikkatle düzenlenmiş tek ana konumlu bir tasarım uyguladık.

**Hataya dayanıklılık**

Bir sistem donanım, ağ ve yazılım hatalarına dayanıklı ise kullanılabilirliği daha yüksektir. Dizin üzerindeki her bölüm için yüksek oranda kullanılabilir bir ana çoğaltma mevcuttur: birincil çoğaltma. Bu çoğaltma üzerinde yalnızca bölüme yazma işlemleri gerçekleştirilir. Bu çoğaltma sürekli olarak ve yakından izlenirken, bir hata algılanması durumunda yazma işlemleri hemen başka bir çoğaltmaya kaydırılabilir (bu çoğaltma yeni birincil çoğaltma olur). Yük devretme sırasında genellikle 1-2 dakikalık yazma kullanılabilirliği kaybı olabilir. Bu süre boyunca okuma kullanılabilirliği etkilenmez.

Okuma işlemleri (yazma işlemlerinden onlarca kat fazladır) yalnızca ikincil çoğaltmalara gider. İkincil çoğaltmalar bir kez etkili olduğundan, okumalar genellikle aynı veri merkezinde bulunan başka bir çoğaltmaya yönlendirilerek belirli bir bölümdeki herhangi bir çoğaltmanın kaybı kolayca telafi edilebilir.

**Veri dayanıklılığı**

Bir yazma işlemi onaylanmadan önce en az iki veri merkezine dayanıklı şekilde işlenir. Bunu yapmak için ilk olarak yazma işlemi birincil çoğaltmaya işlenir, ardından hemen en az bir başka veri merkezine çoğaltılır. Bunun yapılması, birincil çoğaltmayı barındıran veri merkezindeki olası bir yıkıcı kaybın veri kaybıyla sonuçlanmamasını sağlar.

Azure AD, belirteç verme ile dizin okumaları için sıfır [Kurtarma Süresi Hedefi (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) ve dizin yazma işlemleri için dakika düzeyinde (~5 dakika) bir RTO sağlar. Ayrıca sıfır [Kurtarma Noktası Hedefine (RPO)](https://en.wikipedia.org/wiki/Recovery_point_objective) sahip olduğumuz için yük devretme sırasında veri kaybı yaşamayız.

### <a name="data-centers"></a>Veri merkezleri

Azure AD çoğaltmaları, dünyanın dört bir yanında bulunan veri merkezlerinde depolanır. Daha fazla bilgi edinmek için bkz. [Azure veri merkezleri](https://azure.microsoft.com/overview/datacenters).

Azure AD aşağıdaki özelliklere sahip veri merkezlerinde çalışır:

 * Kimlik Doğrulama, Graf ve diğer AD hizmetleri, Gateway hizmetinin arkasında bulunur. Gateway bu hizmetlerin yük dengelemesini yönetir. İşlemsel durum yoklamaları kullanılarak sorunlu durumda olan sunucuların algılanması halinde, otomatik olarak yük devretmesi yapar. Bu durum yoklamalarına göre Gateway, trafiği sorunsuz çalışır durumda olan veri merkezlerine dinamik olarak yönlendirir.
 * *Okumalar* için, dizin etkin-etkin bir yapılandırmada birden fazla veri merkezinde çalışan ikincil çoğaltmalara ve bunlara karşılık gelen ön uç hizmetlerine sahiptir. Tüm veri merkezinde hata oluşması durumunda, trafik otomatik olarak farklı bir veri merkezine yönlendirilir.
 *  *Yazma* işlemleri için dizin, birincil (ana) çoğaltmayı planlı (yeni birincil, eski birincil ile eşitlenir) veya acil durum yük devretme yordamları ile veri merkezlerine devreder. Veri dayanıklılığı, herhangi bir işlemenin en az iki veri merkezine çoğaltılması yoluyla elde edilir.

**Veri tutarlılığı**

Dizin modeli nihai tutarlılığa sahiptir. Zaman uyumsuz olarak çoğaltılan dağıtılmış sistemlerle ilgili genel bir sorun, “belirli” bir çoğaltmadan döndürülen verilerin güncel olmayabilmesidir. 

Azure AD, yazma işlemlerini birincil çoğaltmaya yönlendirerek ve eşzamanlı olarak ikincil çoğaltmaya geri çekerek, ikincil çoğaltmayı hedefleyen uygulamalar için okuma-yazma tutarlılığı sağlar.

Azure AD’nin Graph API’sini kullanan uygulama yazma işlemleri, okuma-yazma tutarlılığı için dizin çoğaltması ile benzeşim sağlama yönteminden yararlanır. Azure AD Graph hizmeti, okumalar için kullanılan bir ikincil çoğaltma ile benzeşimi olan mantıksal bir oturum sürdürür; benzeşim, graf hizmetinin dağıtılmış bir önbellek kullanarak önbelleğe aldığı bir “çoğaltma belirtecinde” yakalanır. Bu belirteç aynı mantıksal oturumun daha sonraki işlemleri için kullanılır. 

 >[!NOTE]
 >Yazma işlemleri, mantıksal oturumdaki okumaların verildiği ikincil çoğaltmaya hemen çoğaltılır.
 >

**Yedekleme koruması**

Dizin, bir müşterinin yanlışlıkla silmesi durumunda kolay kurtarma amacıyla kullanıcılar ve kiracılar için sabit silme yerine geçici silme gerçekleştirir. Kiracı yöneticiniz kullanıcıları yanlışlıkla silerse, bu işlemi kolayca geri alıp silinen kullanıcıları geri yükleyebilir. 

Azure AD tüm verilerin günlük yedeklemesini yapar ve bu nedenle mantıksal silme veya bozulma durumunda verileri yetkili olarak geri yükleyebilir. Veri katmanımız hata düzeltme kodları kullandığı için, hataları denetleyip disk hatalarının belirli türlerini otomatik olarak düzeltebilir.

**Ölçümler ve izleyiciler**

Yüksek oranda kullanılabilir bir hizmetin çalıştırılması için birinci sınıf ölçüm ve izleme özellikleri gerekir. Azure AD, temel hizmet durumu ölçümlerini ve her bir hizmetinin başarı ölçütlerini sürekli olarak analiz edip raporlar. Azure AD hizmeti içinde ve tüm hizmetlerde her bir senaryo için ölçüm, izleme ve uyarıları sürekli olarak geliştirip ayarlıyoruz.

Herhangi bir Azure AD hizmeti beklendiği gibi çalışmazsa, işlevselliği mümkün olan en kısa sürede yeniden sağlamak için harekete geçiyoruz. Azure AD’nin takip ettiği en önemli ölçüm, bir müşteri veya canlı site sorununu algılama ve giderme hızımızdır. Algılama süresini azaltmak (TTD Hedefi: <5 dakika) için izleme ve uyarılara, önlem alma süresini azaltmak için (TTM Hedefi: <30 dakika) operasyonel hazırlığa önemli ölçüde yatırım yapıyoruz.

**Güvenli işlemler**

Tüm işlemler için çok faktörlü kimlik doğrulaması (MFA) gibi operasyonel denetimlerin yanı sıra tüm işlemlerin denetimini yapıyoruz. Ayrıca, herhangi bir isteğe bağlı operasyonel görev için gereken geçici erişimi sürekli biçimde sağlamak üzere tam zamanında yükseltme sistemi kullanıyoruz. Daha fazla bilgi için bkz. [Güvenilir Bulut](https://azure.microsoft.com/support/trust-center).

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory geliştirici kılavuzu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)

