---
title: aaaUnderstand Azure Active Directory mimarisi | Microsoft Docs
description: "Ne açıklanır Azure AD kiracısı olan ve nasıl toomanage Azure Active Directory ile Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Azure Active Directory mimarisini anlama
Azure Active Directory (Azure AD) etkinleştirir, toosecurely erişim tooAzure Hizmetleri ve kullanıcılarınız için kaynakları yönetme. Azure AD ile birlikte eksiksiz kimlik yönetimi olanakları sunulur. Azure AD özellikleri hakkında daha fazla bilgi için bkz. [Azure Active Directory nedir?](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis)

Azure AD ile oluşturabilir ve kullanıcıları ve grupları, yönetmek ve izinleri tooallow etkinleştirmek ve tooenterprise kaynaklara erişimini. Kimlik Yönetimi hakkında daha fazla bilgi için bkz: [hello Azure Kimlik Yönetimi Temelleri](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Azure AD mimarisi
Azure AD coğrafi olarak dağıtılmış mimarisi birleştirir kapsamlı izleme, otomatik yeniden yönlendirme, yük devretme ve kurtarma özellikleri bize toodeliver Kurumsal düzeyde kullanılabilirlik ve performans tooour müşteriler etkinleştirin.

Mimari öğeleri aşağıdaki hello bu makalede ele alınmaktadır:
 *  Hizmet mimarisi tasarımı
 *  Ölçeklenebilirlik 
 *  Sürekli kullanılabilirlik
 *  Veri merkezleri

### <a name="service-architecture-design"></a>Hizmet mimarisi tasarımı
ölçeklenebilir, yüksek oranda kullanılabilir, veri bakımından zengin bir sistem olan bağımsız yapı taşları veya hello Azure AD veri katmanı için ölçek birimlerinizi aracılığıyla hello en yaygın şekilde toobuild, Ölçek birimleri çağrılır *bölümleri*. 

Merhaba veri katmanı okuma-yazma özelliği sağlamayı birkaç ön uç hizmet yok. Merhaba diyagrama hello bileşenleri tek dizini bölümünün coğrafi olarak distrubuted veri merkezleri nasıl dağıtıldığını gösterir. 

  ![Tek Dizinli Bölümler](./media/active-directory-architecture/active-directory-architecture.png)

Azure AD mimarisi Hello bileşenlerinin birincil çoğaltma ve ikincil çoğaltmaları içerir.

**Birincil çoğaltma**

Merhaba *birincil çoğaltma* tüm alan *Yazar* ait hello bölümü için. Herhangi bir işlemi hemen çoğaltılmış tooa ikincil çoğaltma farklı bir veri merkezinde başarı toohello arayan, böylece yazma coğrafi olarak yedekli dayanıklılık sağlama döndürmeden önce yazma.

**İkincil çoğaltmalar**

Tüm dizin *okumaları*, fiziksel olarak farklı coğrafi bölgelerde bulunan veri merkezlerindeki *ikincil çoğaltmalardan* sunulur. Veriler zaman uyumsuz olarak kopyalandığı için çok sayıda ikincil çoğaltma vardır. Kimlik doğrulama istekleri gibi dizin okuma Kapat tooour müşterilerdir veri merkezleri sunulur. Merhaba ikincil çoğaltmalar için okuma ölçeklenebilirlik sorumludur.

### <a name="scalability"></a>Ölçeklenebilirlik

Ölçeklenebilirlik hello artan performans taleplerini hizmet tooexpand toomeet özelliğidir. Ölçeklenebilirlik hello veri bölümlendirme tarafından elde edilen yazma. Okuma ölçeklenebilirlik bir bölüm toomultiple ikincil çoğaltmaların Merhaba dünya genelinde dağıtılan veriler yineleyerek elde edilir.

Fiziksel olarak en yakın genellikle yönlendirilmiş toohello datacenter isteklerdir dizin uygulamalardan. Yazma saydam olarak yeniden yönlendirilen toohello birincil çoğaltma tooprovide okuma-yazma tutarlılığı ' dir. Merhaba dizinleri hello zamanının çoğunu sunma okuma genellikle olduğundan ikincil çoğaltmaları hello ölçeği bölümlerinin önemli ölçüde genişletir.

Dizin uygulamaları toohello veri merkezleri en yakın bağlayın. Bunun yapılması performansı artırır ve böylece ölçek genişletme mümkün olur. Bir dizin bölümü çok sayıda ikincil çoğaltmaları olduğundan ikincil çoğaltmaları daha yakından toohello directory istemcileri yerleştirilebilir. Yazma yoğunluklu hedef hello etkin birincil çoğaltma doğrudan yalnızca iç dizin hizmetinin bileşenlerini.

### <a name="continuous-availability"></a>Sürekli kullanılabilirlik

Kullanılabilirlik (veya açık kalma süresi) kesintisiz bir sistem tooperform hello yeteneğini tanımlar. birden çok coğrafi olarak dağıtılmış veri merkezleri arasında trafiği, hizmetlerimizi hızla kaydırabilirsiniz Hello anahtar tooAzure AD'ın yüksek kullanılabilirliğe sahip. Her veri merkezi birbirinden bağımsızdır ve bu özelliği sayesinde bağıntısız hata modları sağlar.

Azure AD bölüm Basitleştirilmiş karşılaştırılan toohello Kurumsal hello sistemi ölçekleme için önemli olan AD tasarım tasarımdır. Birincil çoğaltma yük devretme işleminin belirli şekilde gerçekleştirildiği, dikkatle düzenlenmiş tek ana konumlu bir tasarım uyguladık.

**Hataya dayanıklılık**

Bir sistem daha dayanıklı toohardware, ağ ve yazılım hataları ise kullanılabilir. Merhaba dizinindeki her bölüm için yüksek oranda kullanılabilir bir ana çoğaltma var: hello birincil çoğaltma. Yalnızca yazma toohello bölüm Bu kopyada gerçekleştirilir. Bu çoğaltma sürekli ve yakından izlenmekte olan ve yazma işlemleri hemen ötelenen tooanother çoğaltma olabilir (Merhaba hale yeni birincil) bir hata algılandığında. Yük devretme sırasında genellikle 1-2 dakikalık yazma kullanılabilirliği kaybı olabilir. Bu süre boyunca okuma kullanılabilirliği etkilenmez.

(Hangi yazar tarafından birçok siparişleri büyüklük outnumber) okuma işlemleri yalnızca toosecondary çoğaltmaları gidin. İkincil çoğaltmaları ıdempotent olduğundan, herhangi bir çoğaltma belli bir bölüm kaybı kolayca hello okuma tooanother yineleme, genellikle hello yönlendirerek dengelendi aynı veri merkezinde.

**Veri dayanıklılığı**

Bir yazma işlemi taahhüt tooat en az iki veri merkezleri önceki tooit alınıyor ' dir. Bu, ilk hello birincil hello yazma yapılıyor ve hello yazma tooat en az bir diğer veri merkezine çoğaltma hemen sonra gerçekleşir. Bu, geri dönülemez kaybı hello veri merkezi barındırma hello birincil veri kaybına yol değil olası sağlar.

Azure AD tutar sıfır [kurtarma süresi hedefi (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) belirteci verme ve dizin için okur ve dakika (~ 5 dakikadır) RTO dizin hello sırasını yazar. Ayrıca sıfır [Kurtarma Noktası Hedefine (RPO)](https://en.wikipedia.org/wiki/Recovery_point_objective) sahip olduğumuz için yük devretme sırasında veri kaybı yaşamayız.

### <a name="data-centers"></a>Veri merkezleri

Azure AD çoğaltmalar Merhaba dünya genelinde bulunan veri merkezlerine depolanır. Daha fazla bilgi edinmek için bkz. [Azure veri merkezleri](https://azure.microsoft.com/en-us/overview/datacenters).

Azure AD ile Merhaba özellikleri aşağıdaki veri merkezleri arasında çalışır:

 * Kimlik doğrulama, grafik ve diğer AD Hizmetleri Ağ Geçidi Hizmeti hello bulunur. Merhaba ağ geçidi bu hizmetleri yük dengelemeyi yönetir. İşlemsel durum yoklamaları kullanılarak sorunlu durumda olan sunucuların algılanması halinde, otomatik olarak yük devretmesi yapar. Bu sistem durumu araştırmalarının bağlı olarak, ağ geçidi hello trafiği toohealthy veri merkezleri dinamik olarak yönlendirir.
 * İçin *okur*, birden çok veri merkezlerinde çalışan bir aktif-aktif yapılandırma hello dizine sahip ikincil çoğaltmaları ve karşılık gelen ön uç Hizmetleri. Bütün bir veri merkezi başarısız olması durumunda, trafiği otomatik olarak yönlendirilmiş tooa farklı datacenter olacaktır.
 *  İçin *Yazar*, hello dizin yük devretme birincil (ana) çoğaltma veri merkezleri arasında planlanmış (yeni birincil eşitlenmiş tooold birincil değil) veya Acil Durum yük devretme yordamlar. Veri dayanıklılığı herhangi yürütme tooat en az iki veri merkezleri yineleyerek elde edilir.

**Veri tutarlılığı**

Merhaba dizin modeli nihai tutarlılık biridir. Dağıtılmış zaman uyumsuz olarak çoğaltan sistemleriyle tipik sorunlardan biri, bir "özel" çoğaltmadan döndürülen hello veriler toodate olmayabilir olmasıdır. 

Azure AD yazma toohello birincil çoğaltması yönlendirerek bir ikincil çoğaltmaya hedefleyen uygulamalar için okuma-yazma tutarlılığı sağlar ve zaman uyumlu olarak hello çekme geri toohello ikincil çoğaltma yazar.

Grafik API'si, Azure AD soyutlanır benzeşim tooa dizin çoğaltma okuma-yazma tutarlılığını korumak hello kullanarak uygulama yazar. Hello Azure AD grafik hizmet benzeşimi tooa ikincil çoğaltmasının okuma için kullanılan bir mantıksal oturumu korur; benzeşim "Grafik Hizmeti önbellekleri dağıtılmış önbellek kullanarak hello bir çoğaltma belirteci" yakalanır. Bu belirteç sonra hello sonraki işlemlerde için kullanılan aynı mantıksal oturumu. 

 >[!NOTE]
 >Yazma hemen çoğaltılmış toohello ikincil çoğaltma toowhich hello mantıksal oturumunun okuma verilmiş.
 >

**Yedekleme koruması**

Merhaba directory kullanıcıları ve kiracıları için bir müşteri tarafından yanlışlıkla silmeleri durumunda kolay kurtarma için sabit siler yerine yazılım siler uygular. Kiracı yöneticinizle yanlışlıkla kullanıcılar silerse, bunlar kolayca geri ve Silinen hello kullanıcıları geri. 

Azure AD tüm verilerin günlük yedeklemesini yapar ve bu nedenle mantıksal silme veya bozulma durumunda verileri yetkili olarak geri yükleyebilir. Veri katmanımız hata düzeltme kodları kullandığı için, hataları denetleyip disk hatalarının belirli türlerini otomatik olarak düzeltebilir.

**Ölçümler ve izleyiciler**

Yüksek oranda kullanılabilir bir hizmetin çalıştırılması için birinci sınıf ölçüm ve izleme özellikleri gerekir. Azure AD, temel hizmet durumu ölçümlerini ve her bir hizmetinin başarı ölçütlerini sürekli olarak analiz edip raporlar. Azure AD hizmeti içinde ve tüm hizmetlerde her bir senaryo için ölçüm, izleme ve uyarıları sürekli olarak geliştirip ayarlıyoruz.

Herhangi bir Azure AD hizmeti beklendiği gibi çalışmıyorsa, biz hemen eylem toorestore işlevselliği mümkün olan en kısa sürede olur. Merhaba en önemli ölçüm Azure AD parçaları olan ne kadar hızlı biz algılayan ve müşteri azaltmak veya site sorunu Canlı. Biz yoğun olarak da izleme ve uyarılar toominimize zaman toodetect yatırım (TTD hedef: < 5 dakika) ve işletimsel hazırlık toominimize zaman toomitigate (TTM hedef: < 30 dakika).

**Güvenli işlemler**

Tüm işlemler için çok faktörlü kimlik doğrulaması (MFA) gibi operasyonel denetimlerin yanı sıra tüm işlemlerin denetimini yapıyoruz. Ayrıca, bir tam zamanı ayrıcalık sistem toogrant gerekli geçici erişim herhangi işletimsel görev isteğe bağlı düzenli olarak için kullanırız. Daha fazla bilgi için bkz: [güvenilir bulut hello](https://azure.microsoft.com/en-us/support/trust-center).

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory geliştirici kılavuzu](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

