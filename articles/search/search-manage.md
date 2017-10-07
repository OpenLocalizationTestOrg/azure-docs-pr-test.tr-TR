---
title: "aaaService yönetiminde Azure arama için hello Azure portalı"
description: "Azure Search, hello Azure portalını kullanarak Microsoft Azure üzerinde barındırılan bulut arama hizmeti yönetin."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Azure arama için Hizmet Yönetimi hello Azure portal'nde
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

Azure Search zengin arama deneyimi özel uygulamalara oluşturmak için kullanılan tam olarak yönetilen, bulut tabanlı arama hizmetidir. Bu makalede hello kapsayan *Hizmet Yönetim* hello gerçekleştirebileceğiniz görevler [Azure portal](https://portal.azure.com) zaten sağlanmış bir arama hizmeti için. *Hizmet Yönetim* tasarım gereği, kısıtlı toohello görevleri aşağıdaki basit olan:

* Yönetme ve güvenliğini erişim toohello *api anahtarlarından* okuma veya yazma erişimi tooyour hizmeti için kullanılır.
* Hizmet kapasite, bölümler ve çoğaltmalar Merhaba ayırma değiştirerek ayarlayın.
* Kaynak kullanımı, hizmet katmanının göreli toomaximum sınırları izleyin.

**Kapsamda değil** 

*İçerik Yönetimi* (veya dizin yönetimi) toooperations başvuruyor arama trafiği toounderstand sorgu toplu analiz etme gibi kişiler arayın ve nasıl başarılı arama sonuçları müşteriler toospecific yönlendirmede koşulları Bul belgeleri dizininize. Bu alanda daha fazla yardım için bkz: [Azure arama için arama trafiği analiz](search-traffic-analytics.md).

*Sorgu performansı* Ayrıca bu makalede hello kapsamında değildir. Daha fazla bilgi için bkz: [izlemek kullanım ve sorgu ölçümleri](search-monitor-usage.md) ve [performans ve en iyi duruma getirme](search-performance-optimization.md).

*Yükseltme* bir yönetim görevi değildir. Merhaba hizmet sağlandığında kaynakların ayrıldığından taşıma tooa farklı katmanı yeni bir hizmet gerektirir. Ayrıntılar için bkz [bir Azure Search hizmeti oluşturma](search-create-service-portal.md).

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>Yönetici hakları
Sağlama veya hello hizmetin kendisini yetkisini bir Azure Abonelik Yöneticisi veya ortak yönetici tarafından yapılabilir.

Bir hizmet içinde erişim toohello hizmeti URL'si kimseyle ve yönetici api anahtarı okuma-yazma erişimi toohello hizmeti vardır. Okuma-yazma erişimi sağlayan hello özelliği tooadd, silmek veya API anahtarları, dizinler, dizin oluşturucular, veri kaynakları, zamanlamaları ve rol atamalarını aracılığıyla uygulanan dahil olmak üzere sunucu nesneleri değiştirmek [RBAC tanımlı rolleri](#rbac).

Azure Search tüm kullanıcı etkileşimi bu modlarından birini içinde döner: okuma-yazma erişimi toohello hizmeti (yönetici hakları) veya salt okunur erişim toohello hizmeti (sorgu hakları). Daha fazla bilgi için bkz: [hello api anahtarlarından yönetmek](#manage-keys).

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>Yönetici erişimi için RBAC rolleri Ayarla
Azure sağlayan bir [genel rol tabanlı yetkilendirme modelini](../active-directory/role-based-access-control-configure.md) hello portal ya da Resource Manager API'leri yönetilen tüm hizmetler için. Sahibi, katkıda bulunan ve okuyucu rollerinin Active Directory Kullanıcıları, grupları ve güvenlik sorumlularının atanan tooeach rolü Hizmet Yönetimi hello düzeyini belirler. 

Azure arama için yönetim görevleri aşağıdaki hello RBAC izinleri belirler:

| Rol | Görev |
| --- | --- |
| Sahip |Oluşturun veya hello hizmet veya hello hizmetinde, API anahtarları, dizinler, dizin oluşturucular, Dizin Oluşturucu veri kaynakları ve dizin oluşturucu zamanlamaları gibi herhangi bir nesnede silin.<p>Sayıları ve depolama boyutu da dahil olmak üzere hizmetin durumunu görüntüleyin.<p>Ekleyin veya rol üyeliğini (yalnızca bir sahibi rol üyeliğini yönetebilir) silin.<p>Abonelik yöneticileri ve hizmet sahiplerini otomatik üyelik hello sahipleri rolünde sahiptir. |
| Katılımcı |Aynı düzeyde erişim sahibi, RBAC rol yönetimi eksi. Örneğin, katılımcı yeniden ve görüntüleyebilirsiniz `api-key`, rol üyeliklerini değiştiremez ancak. |
| Okuyucu |Hizmet durumu ve sorgu anahtarları görüntüleyin. Bu rolün üyeleri hizmet yapılandırmasında değişiklik yapamaz veya yönetici anahtarları görüntüleyebilirsiniz. |

Roller, erişim hakları toohello Hizmeti uç noktası vermeyin. Arama hizmeti işlemleri, dizin yönetimi, dizin oluşturma ve sorgular gibi arama verileri api anahtarlarından, değil rolleri denetlenir. Daha fazla bilgi için bkz: "Yetkilendirmesi Yönetimi karşılık veri işlemleri için" [rol tabanlı erişim denetimi nedir](../active-directory/role-based-access-control-what-is.md).

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>Günlüğe kaydetme ve sistem bilgileri
Azure arama günlük dosyaları için bir bireysel hizmet hello portalı veya programlama arabirimleri ile kullanıma sunmuyor. Merhaba temel katmanı ve üstünde, Microsoft Azure Search hizmetler için hizmet düzeyi sözleşmelerine (SLA) göre % 99,9 kullanılabilirliğini izler. Merhaba hizmeti yavaş veya istek işleme SLA eşiklerin altına düştüğünde, destek ekiplerini hello günlük dosyaları kullanılabilir toothem ve adres hello sorunu gözden geçirin.

Hizmet hakkında genel bilgiler açısından hello yolları aşağıdaki bilgileri elde edebilirsiniz:

* Merhaba Portalı'nda, bildirimler, özellikler ve durum iletileri aracılığıyla hello hizmeti panosundaki.
* Kullanarak [PowerShell](search-manage-powershell.md) veya hello [Yönetimi REST API](https://docs.microsoft.com/rest/api/searchmanagement/) çok[hizmeti özelliklerini alma](https://docs.microsoft.com/rest/api/searchmanagement/services), veya dizin kaynak kullanımına durumu.
* Aracılığıyla [trafiği analytics arama](search-traffic-analytics.md), daha önce belirtildiği gibi.

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>API anahtarları Yönet
Tüm istekleri tooa arama hizmeti özellikle hizmetinizin api oluşturulan anahtarı gerekir. Bu API anahtarı erişim tooyour Arama Hizmeti uç noktası kimlik doğrulaması için hello tek mekanizmadır. 

Bir API anahtarı rastgele oluşturulmuş sayılar ve harflerden oluşan bir dizedir. Aracılığıyla [RBAC izinleri](#rbac), silebilir veya hello anahtarları okumak, ancak kullanıcı tanımlı bir parola ile bir anahtar değiştirilemiyor. 

İki tür anahtarları kullanılan tooaccess arama hizmetinizi şunlardır:

* Yönetici (Merhaba Hizmeti'ne yönelik bir okuma-yazma işlemi için geçerli)
* Sorgu (geçerli bir dizin sorgular gibi salt okunur işlemler için)

Merhaba hizmeti sağladığında yönetici api anahtarı oluşturulur. Olarak belirtilen iki yönetici anahtarları vardır *birincil* ve *ikincil* tookeep bunları doğrudan, ancak gerçekte oldukları değiştirilebilir. Böylece, bir erişim tooyour hizmeti kaybetmeden dönebilirsiniz her hizmetin iki yönetici anahtarları vardır. Her iki yönetici anahtarını yeniden oluşturmak, ancak toohello toplam yönetici anahtar sayısı ekleyemezsiniz. En fazla arama hizmeti başına iki yönetici anahtarları yoktur.

Sorgu anahtarları arama doğrudan çağıran istemci uygulamalar için tasarlanmıştır. Too50 sorgu anahtarları oluşturabilirsiniz. Uygulama kodunda hello arama URL'si ve bir sorgu api anahtarını tooallow salt okunur erişim toohello hizmeti belirtin. Uygulama kodunuz, ayrıca, uygulamanız tarafından kullanılan hello dizini belirtir. Birlikte, hello uç noktası, salt okunur erişimi ve bir hedef dizin için bir API anahtarı hello bağlantı istemci uygulamanızdan hello kapsam ve erişim düzeyi tanımlayın.

tooget veya yeniden api anahtarlarından, açık hello hizmet panosunu. Tıklatın **ANAHTARLARI** tooslide hello Anahtar Yönetimi sayfasını açın. Yeniden veya anahtarlar oluşturmak için hello hello sayfanın başında komutlardır. Varsayılan olarak, yalnızca yönetici anahtarları oluşturulur. Sorgu api anahtarlarından el ile oluşturulması gerekir.

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>Güvenli API anahtarları
Anahtar güvenlik hello portal ya da Resource Manager arabirimleri (PowerShell veya komut satırı arabirimi) aracılığıyla erişimi kısıtlayarak sağlamış. Belirtildiği gibi abonelik yöneticileri görüntülemek ve tüm API anahtarlarını yeniden oluştur. Önlem olarak erişim toohello yönetici anahtarlarına sahip rol atamalarını toounderstand gözden geçirin.

1. Merhaba hizmet panosunda, hello erişim simgesi tooslide açık hello kullanıcılar dikey tıklayın.
   ![][7]
2. Kullanıcılar, var olan rol atamalarını gözden geçirin. Beklendiği gibi abonelik yöneticileri hello sahip rolü aracılığıyla tam erişim toohello hizmeti zaten sahip.
3. Ayrıca, toodrill tıklatın **abonelik yöneticileri** ve ardından arama hizmetinizde ortak yönetim haklarına sahip hello rol ataması listesi toosee genişletin.

Başka bir şekilde tooview erişim izinleri olan tooclick **rolleri** hello kullanıcılar dikey. Bunun yapılması, kullanılabilir roller ve kullanıcılar veya gruplar atanan tooeach rol hello sayısını görüntüler.

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>Kaynak kullanımını izleme
Merhaba panosunda kaynak izleme hello hizmet panosunu ve hello hizmetini sorgulayarak edinebilirsiniz birkaç ölçümleri gösterilen sınırlı toohello bilgilerdir. Hello kullanım bölümdeki hello hizmeti panosundaki hızlı bir şekilde bölüm kaynak düzeyleri, uygulamanız için yeterli olup olmadığını belirleyebilirsiniz.

Merhaba arama hizmeti API'si kullanılarak, belgeler ve dizin sayısına elde edebilirsiniz. Fiyatlandırma katmanı hello üzerinde göre bu sayıları ile ilişkili sabit sınırları vardır. Daha fazla bilgi için bkz: [Search hizmet limitleri](search-limits-quotas-capacity.md). 

* [Dizin istatistikleri Al](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [Count belgeleri](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> Davranışları önbelleğe alma, geçici olarak bir sınırı overstate. Örneğin, paylaşılan hello hizmetini kullanırken, bir belge görebilirsiniz hello sabit 10.000 belge limiti üzerinden sayısı. Merhaba overstatement geçicidir ve sonraki sınırı zorlaması denetimi hello algılandı. 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>Olağanüstü durum kurtarma ve hizmet kesintilerine karşı

Biz verilerinizi hurda rağmen hello küme veya veri merkezi düzeyinde bir kesinti ise Azure Search hello hizmetinin anlık yük devretme sağlamaz. Merhaba veri merkezinde bir küme başarısız olursa, hello işletim ekibi algılayabilir ve toorestore hizmeti çalışacak. Hizmet geri yükleme sırasında kapalı kalma yaşayacaktır. Hizmet iadeleri toocompensate hello başına hizmet olarak kullanım dışı kalması için istek [hizmet düzeyi sözleşmesi (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/). 

Microsoft'un denetimi dışında yıkıcı hatalar hello olay sürekli hizmet gerekirse, verebilir [ek bir hizmet sağlamak](search-create-service-portal.md) farklı bir bölgeye ve uygulama coğrafi çoğaltma stratejisi tooensure dizinler Tüm hizmetler arasında tam olarak gereksizdir.

Kullanan müşteriler [dizin oluşturucular](search-indexer-overview.md) toopopulate ve yenileme dizinleri, olağanüstü durum kurtarma hello yararlanarak coğrafi özgü dizin oluşturucular aracılığıyla işleyebilir aynı veri kaynağı. Farklı bölgelerde, her bir dizin oluşturucu çalıştıran iki hizmet hello dizin aynı veri kaynağı tooachieve coğrafi yedeklilik. Ayrıca coğrafi olarak yedekli veri kaynaklarından sıralıyorsanız, artımlı birincil çoğaltmalardan dizin oluşturma, Azure Search'te dizin oluşturucular yalnızca gerçekleştirebilir unutmayın. Bir yük devretme olayından emin toore noktası hello dizin oluşturucu toohello yeni birincil çoğaltma olabilir. 

Dizin oluşturucular kullanmazsanız, uygulama kodu toopush nesneleri ve veri toodifferent arama hizmetleri paralel olarak kullanırsınız. Daha fazla bilgi için bkz: [performans ve Azure Search'te iyileştirme](search-performance-optimization.md).

## <a name="backup-and-restore"></a>Yedekleme ve geri yükleme

Azure Search birincil veri depolama çözümü olduğundan, biz Self Servis yedekleme ve geri yükleme için resmi bir mekanizma sağlamaz. Bir dizin yanlışlıkla silerseniz oluşturmak ve bir dizinini doldurmak için kullanılan uygulama kodunuz hello gerçek geri yükleme seçeneğidir. 

Dizin, bir toorebuild (var olduğu varsayılarak) silin, hello hizmetindeki hello dizini yeniden oluşturun ve birincil veri deposundan verileri alarak yeniden yükleyin. Alternatif olarak, çok ulaşmak[müşteri desteği]() toosalvage dizinler bölgesel bir kesintinin ise.


<a id="scale"></a>

## <a name="scale-up-or-down"></a>Ölçek büyütme veya küçültme
Her arama hizmeti en az bir çoğaltma ve bir bölüm ile başlar. İçin kaydolduysanız bir [özel kaynakları sağlar katmanı](search-limits-quotas-capacity.md), hello tıklatın **ölçek** döşeme hello hizmet Pano tooadjust kaynak kullanımı.

Merhaba hizmeti ya da kaynak aracılığıyla kapasite eklediğinizde, bunları otomatik olarak kullanır. Başka bir eylem yapmanız gereken, ancak hello etkisini hello yeni kaynak gerçekleştirilmiş önce kısa bir gecikme olduğunu. Ek kaynaklar 15 dakika veya daha fazla tooprovision alabilir.

 ![][10]

### <a name="add-replicas"></a>Çoğaltmaları ekleme
Sorgular (QPS) saniyede artırmayı veya yüksek kullanılabilirlik elde çoğaltmaları ekleyerek yapılır. Her çoğaltma bir kopyasını bir dizin daha fazla dizin hizmeti sorgu isteği işlemek için kullanılabilen sahiptir, böylece bir daha fazla çoğaltma ekleme tooone çevirir. Yüksek kullanılabilirlik için en az 3 çoğaltmaları gereklidir (bkz [kapasite planlaması](search-capacity-planning.md) Ayrıntılar için).

Daha fazla çoğaltmaları sahip bir arama hizmeti çok sayıda dizinleri Yük Dengeleme sorgu isteklerini yükleyebilirsiniz. Daha fazla kopyasını hello dizin kullanılabilir tooservice hello istek olduğunda sorgu toplu düzeyini verildiğinde, sorgu işleme toobe daha hızlı olacaktır. Sorgu gecikmesi karşılaşıyorsanız hello Ek çoğaltmalar çevrimiçi olduktan sonra performansını olumlu bir etki bekleyebilirsiniz.

Çoğaltmaları ekledikçe sorgu işleme artar rağmen onu değil tam olarak çift veya çoğaltmaları tooyour hizmet ekledikçe Üçlü. Tüm arama uygulamaları sorgu performansına impinge konu tooexternal faktörlerdir. Karmaşık sorgular ve ağ gecikmesini toovariations sorgusu yanıt sürelerini katkıda bulunan iki faktörlerdir.

### <a name="add-partitions"></a>Bölüm Ekle
Çoğu hizmet uygulamaları bölümleri yerine daha fazla çoğaltmaları yerleşik ihtiyacı vardır. Artan belge sayısı gerekli olduğu durumlarda, standart hizmet için kaydolduysanız bölümleri ekleyebilirsiniz. Temel katman, ek bölümler için sağlamaz.

Merhaba standart katmanı, bölümler 12'ün katları eklenir (özellikle, 1, 2, 3, 4, 6 veya 12). Bu bir parçalama yapıdır. Tüm yüklenebilir 1 bölüme depolanan veya 2, 3, 4, 6 ve 12 bölümleri (bölüm başına tek parça) eşit olarak bölünmüş 12 parça bir dizin oluşturulur.

### <a name="remove-replicas"></a>Çoğaltmaları Kaldır
Sonra nokta yüksek sorgu birimlerin (örneğin, tatil satış üzerinden sonra) arama sorgu yüklerinin normalleştirilmiş sonra çoğaltmaları azaltabilir.

toodo Bu, taşıma hello çoğaltma kaydırıcı geri tooa düşük sayı. Yapmanız gereken başka bir adım vardır. Merhaba çoğaltma sayısı azaltmayı hello veri merkezindeki sanal makineleri siler. Sorgu ve veri alımı işlemlerinizin artık vm'lerinde daha az önce çalışır. Merhaba alt sınırı bir çoğaltmadır.

### <a name="remove-partitions"></a>Bölümlerini Kaldır
Çoğaltmalar, hiçbir ek çaba çaba gerektiren kaldırma kullanılmasının aksine, azaltılabilir olandan daha fazla depolama alanı kullanıyorsanız, bazı iş toodo olabilir. Çözümünüzü üç bölüm kullanıyorsanız, hello yeni depolama alanı gerekenden daha az ise, örneğin, downsizing tooone veya iki bölüm bir hata oluşturur. Beklediğiniz gibi seçimlerinizi toodelete dizinleri ya da belgeler ilişkili dizini toofree alanı içinde veya hello geçerli yapılandırmayı korumak.

Hangi dizin parça belirli bölümlerinde depolanan belirten algılama yöntemi yoktur. Sahip olduğunuz bölümleri hello sayısına göre paylaşabiliyor olmasını tooreduce depolama tooa boyutunu gerekir her bölüm yaklaşık 25 GB depolama sağlar. Toorevert tooone bölüm istiyorsanız, tüm 12 parça toofit gerekir.

Gelecekteki planlamayla toohelp toocheck depolama isteyebileceğiniz (kullanarak [dizin istatistikleri almak](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) ne kadar gerçekten kullandığınız toosee. 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>Ölçek ve dağıtım üzerinde en iyi yöntemler
Bu 30 dakikalık videoda, coğrafi olarak dağıtılan iş yükleri de dahil olmak üzere gelişmiş dağıtım senaryoları için en iyi uygulamaları gözden geçirir. Ayrıca bkz [performans ve Azure Search'te iyileştirme](search-performance-optimization.md) Yardım konusu kapak hello sayfalar için aynı işaret eder.

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>Sonraki adımlar
Hizmet Yönetimi hello kavramları anladığınızda, kullanmayı [PowerShell](search-manage-powershell.md) tooautomate görevler.

Ayrıca hello gözden geçirme öneririz [performans ve en iyi duruma getirme makale](search-performance-optimization.md).

Video toowatch hello hello önceki bölümünde belirtildiği başka bir önerilir. Bu bölümde belirtilen hello teknikleri daha ayrıntılı bilgi sağlar.

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



