---
title: "Azure uygulama hizmeti ile ClearDB MySql veritabanları için aaaFAQ | Microsoft Docs"
description: "Azure uygulama hizmeti ile ClearDB MySQL veritabanları kullanma toocommon sorular yanıtlanmaktadır."
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>Azure Uygulama Hizmeti ile ClearDB MySQL veritabanları hakkında SSS
Bu SSS ClearDB MySQL veritabanları Azure Web uygulamaları için satın alma ve kullanma hakkında sık sorulan soruları yanıtlar.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>Azure üzerinde MySQL için hangi seçenekleri var mı?
Birkaç seçeneğiniz vardır:

* [Paylaşılan ClearDB MySQL veritabanı](/marketplace/partners/cleardb/databases/)
* [ClearDB MySQL Premium kümeleri](/marketplace/partners/cleardb-clusters/cluster/)
* [Bir Azure VM çalıştıran MySQL kümesi](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Tek bir Azure VM'de çalışan MySQL örneği](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB hizmeti barındırma MySQL olan ve hello MySQL altyapısı tarafından yönetilir. Bir Azure sanal makinesinde kendi MySQL kümesi veya veritabanı çalıştırdığınızda tooset hello MySQL sunucusu varsa ve düzeltme ekleri ile güncel tutun.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>Bir kredi kartı ihtiyacım hello Web uygulaması + hello Azure Marketi MySQL şablonunda var?
Bu, kullanmakta olduğunuz abonelik hello türüne bağlıdır. Bazı yaygın olarak kullanılan abonelik türleri şunlardır:

* [Kullandıkça Öde](/offers/ms-azr-0003p/): bir kredi kartı ve kredi kartınızdan ücret Ücretli bir MySQL veritabanı satın aldığınızda gerektirir.
* [Ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/): Microsoft Azure ile kullanmak üzere Hizmetleri ancak üçüncü taraf kaynakları satın izin vermeyen krediler içerir. toopurchase üçüncü taraf hizmetleri veya toouse bir kredi kartı gerekir Ücretli bir MySQL veritabanı abonelik etkin. Web uygulamaları için ücretsiz ClearDB MySQL veritabanı oluşturabilirsiniz.
* [MSDN aboneliği](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) ve **MSDN Geliştirme Test Kullandıkça Öde**: benzer tooFree deneme bir MSDN aboneliği toohave bir kredi kartı toopurchase bir Ücretli ClearDB MySQL çözümü gerektirir.
* [Kurumsal Anlaşma (Kurumsal Sözleşme)](https://azure.microsoft.com/pricing/enterprise-agreement/): EA müşteriler kendi EA karşı her üç aylık tüm Azure Marketi (üçüncü taraf) aldıklarını ayrı, birleştirilmiş bir fatura için faturalandırılır. Tüm Market satın alımları için parasal taahhüt hello dışında faturalandırılır. Şu anda Azure deposu kullanılabilir toocustomers Azerbaycan, Hırvatistan, Norveç ve Porto Riko kayıtlı değil, lütfen unutmayın. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): Web uygulamaları için yalnızca ücretsiz ClearDB veritabanları oluşturabilirsiniz. Ücretsiz ClearDB MySQL veritabanları oluşturabilirsiniz hello sayısına bir sınır yoktur. Bu hizmet yalnızca deneme için tasarlandığı gibi ücretsiz veritabanlarından üretim web uygulamaları için kullanılan toobe olmadığına dikkat edin.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>$3.50 bir Web uygulaması + MySQL için hello Azure Marketi gelen ücret neden?
$3.50 olduğu Titan Hello varsayılan veritabanı seçeneğidir. Merhaba maliyet veritabanı oluşturma sırasında gösterme ve yanlışlıkla düşündüğünüz kaydetmedi bir veritabanı satın alabilirsiniz. Numaralı toofind bir şekilde tooimprove hello deneyimi çalışıyoruz ancak o zamana kadar tıklatmadan önce tüm, seçilen fiyatlandırma katmanlarına web uygulaması ve veritabanı için denetlemelisiniz **oluşturma** ve hello kaynakları hello dağıtımı başlatılıyor.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>MySQL kendi Azure sanal makinede çalışan. Azure web uygulaması toomy Veritabanım bağlayabilir miyim?
Evet. Uzaktan erişim tooyour web uygulaması, Azure VM verdiği sürece, web uygulaması tooyour veritabanınızı bağlanabilir. Daha fazla bilgi için bkz: [bir sanal makinede yüklemek MySQL](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>Hangi ülkelerde desteklenen ClearDB Premium MySQL kümeleri misiniz?
[ClearDB Premium MySQL kümeleri](/marketplace/partners/cleardb-clusters/cluster/) tüm Azure bölgeleri Hindistan, Avustralya, Brezilya Güney ve Çin hello özel durumla dünya çapında kullanılabilir.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>ClearDB premium küme çözümü ile yeni bir küme önceki toocreating bir veritabanı oluşturabilirim?
Hayır, boş ClearDB kümeleri oluşturma desteklenmiyor. Hello Azure portalı toocreate veritabanları hello yeni bir küme oluşturabilir bir kümede tanır aynı anda.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>I t toodelete kullanıldığı bir ClearDB MySQL veritabanı uygulamalarım biri tarafından çalışırsanız uyarılırsınız?
Hayır, Azure, uygulamanızın bağımlı bir Market satın alma silerseniz uyarmaz.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>Hangi bölgeleri ClearDB veritabanlarında oluşturabilirim?
Azure Market kullanılabilir toocustomers Azerbaycan, Hırvatistan, Norveç veya Porto Riko kayıtlı değil. ClearDB bu bölgede kullanılamıyor.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>Bir üretim web uygulaması ve veritabanı için hangi fiyatlandırma katmanı seçmeliyim?
Temel veya daha yüksek bir fiyatlandırma katmanı Web uygulamaları için kullanın. ClearDB için Satürn veya Jüpiter planı öneririz. Hello özellikler ve her ikisi de her fiyatlandırma katmanının sınırlamalarını gözden [Web Apps](https://azure.microsoft.com/pricing/details/app-service/) ve [ClearDB MySQL veritabanları](/marketplace/partners/cleardb/databases/) toochoose hello gereksinimlerinize uyan bir.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>Bir plan tooanother nasıl ClearDB veritabanı yükseltme?
Merhaba, [Azure portal](https://portal.azure.com), ClearDB bir paylaşılan barındırma veritabanı ölçeklendirebilirsiniz. Bu okuma [makale](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn daha fazla. Şu anda yükseltme hello Azure portal ClearDB Premium kümeleri için desteklemiyoruz.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>Azure portalında my ClearDB veritabanı göremiyorum?
Biz Azure Kaynak Yöneticisi'ni kullanarak ClearDB veritabanı oluşturursanız veya [yeni Azure Portal](https://portal.azure.com), hello görünür olmaz [eski Azure Portal](https://manage.windowsazure.com). toowork-bu sorunu toolink veritabanınız el ile ise toohello web uygulaması. Benzer şekilde, hello ClearDB veritabanı oluşturma [eski portalı](https://manage.windowsazure.com) yapmamayı hello veritabanınızda mümkün toosee olması [yeni Azure Portal](https://portal.azure.com). Yoktur hiçbir iş-geçici hello ikinci senaryo için.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>Veritabanı bağlantısı kesilse kimin destek için ile iletişim?
Kişi [ClearDB Destek](https://www.cleardb.com/developers/help/support) herhangi ilgili sorunlar veritabanı için. Tooprovide hazır, Azure abonelik bilgilerinizi ile bunları.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>ClearDB MySQL veritabanı küme çözümüme için ek kullanıcılar oluşturabilir miyim?
Hayır. Ek kullanıcılar oluşturamaz ancak ClearDB veritabanı kümenizde ek veritabanları oluşturabilirsiniz.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>Basic/Pro serisi veritabanları yükseltilmiş yerinde benzer tooPlanetary planlarında bugün ClearDB portal olabilir mi?
Evet, veritabanları olabilir temel serisi yerinde (temel 500 aracılığıyla temel 60) yükseltilmiştir. Pro serisi olabilir yerinde (Pro 1000 aracılığıyla Pro 125) Pro 60 dışında yükseltildi. Pro 60 veritabanı şu anda yükseltiliyor desteklemez. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>Bir abonelik tooanother Kaynaklarım geçirdiğinizde, my ClearDB MySQL veritabanı de geçirilen mu?
Gerçekleştirdiğinizde kaynak geçişi abonelikler arasında bazı [sınırlamalar](app-service-web/app-service-move-resources.md) uygulayın. ClearDB MySQL veritabanı bir üçüncü taraf hizmeti ve bu nedenle Azure abonelik geçişi sırasında geçirilmedi. Merhaba, MySQL geçişini yönetiyorsanız değil, önceki toomigrating Azure veritabanı kaynakları, ClearDB MySQL veritabanları devre dışı bırakılabilir. Web uygulamanız için Azure aboneliği geçiş işlemini gerçekleştirmek ve el ile veritabanlarınızı ilk geçirin. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>I my abonelikte harcama sınırı hello ulaştı. Merhaba sınırı kaldırıldı ve hello veritabanı erişilebilir değil ancak uygulama Hizmetim çevrimiçidir. Merhaba ClearDB veritabanı yeniden nasıl etkinleştirebilirim?
Kişi [ClearDB Destek](https://www.cleardb.com/developers/help/support) hello veritabanını toore etkinleştir. Bunları Azure abonelik bilgilerini ve veritabanı adı ile sağlayın.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>Bir kredi kartı abonelik tooan EA abonelikten bir ClearDB veritabanı aktarabilir miyim?
ClearDB veritabanlarında hello mevcut abonelikleri ile ilişkilendirilmiş hello kredi kartı kullanın. toouse bir EA abonelik verileri tooa yeni veritabanı toomigrate gerekir:

* Yeni bir ClearDB veritabanı EA aboneliğinizle satın alın.
* Veri tooyour yeni veritabanınızı geçirin.
* Uygulama toouse hello yeni veritabanınız güncelleştirin.
* Eski ClearDB veritabanını silin.

MySQL (ClearDB) ile yeni bir web uygulaması oluşturduğunuzda veya MySQL veritabanı (ClearDB) oluşturma seçtiğiniz hello abonelik hello hizmet için nasıl ödeme belirler. Bir EA abonelikle biz hello tedarik hello Azure portal'ın ClearDB gibi hello üçüncü taraf hizmetleri engellemez. EA abonelikleri dışında parasal taahhüt faturalandırılır ve üç aylık ve arrears faturalandırılır. Merhaba EA müşteri herhangi bir üçüncü taraf Market Hizmetleri için bir kredi kartı toopay gibi bir ödeme yöntemi yukarı tooset gerekir.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>Merhaba ücretleri EA aboneliğindeki ClearDB kaynaklar için burada görüyor musunuz?
Doğrudan EA müşteriler için Azure Marketi ücretleri hello Enterprise Portal üzerinde görülebilir. Tüm Market satın alımları ve tüketim dışında parasal taahhüt faturalandırılır ve üç aylık ve arrears faturalandırılır unutmayın. Toohello üçüncü taraf hizmet sağlayıcıları ve can şekilde kendi EA bir kredi kartı gibi bir ödeme yöntemi etkinleştirerek hesabı doğrudan EA müşterilerin toopay sahip.

Dolaylı EA müşteriler kendi Azure Marketi abonelikleri üzerinde hello bulabilir **Aboneliklerini Yönet** hello Enterprise Portal ancak Fiyatlandırma sayfasında gizlenir. Müşteriler, Market ücretleri hakkında bilgi için kendi LSP başvurmalıdır.

Üçüncü taraf hizmetleri için erişim tooAzure Market EA Azure kayıt yöneticiler tarafından yönetilebilir. Devre dışı veya erişim too3rd taraf satın alma işlemleri hello hesaplarını yönetme ve abonelikleri deposunda hello hesapları bölümünde bulunan hello Enterprise Portal'ndan yeniden etkinleştirin.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>Kimin ı sorular için faturamı ClearDB hizmetleri hakkında EA Aboneliğimi iletişim?
Kişi [Kurumsal Müşteri Destek](http://aka.ms/AzureEntSupport) bakımından toobilling EA kayıt altında ile. Merhaba EA Portal destek ekibi sorunuza yanıt veya sorununuzu Yardım.

## <a name="more-information"></a>Daha fazla bilgi
[Azure Market SSS](/marketplace/faq/)

