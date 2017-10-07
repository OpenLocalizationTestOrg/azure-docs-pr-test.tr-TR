---
title: "aaaAzure veri Kataloğu genel senaryoları | Microsoft Docs"
description: "Azure veri Kataloğu hello kayıt ve yüksek değerli veri kaynaklarını bulma dahil olmak üzere, Self Servis iş zekası etkinleştirme ve veri kaynakları ve işlemleri hakkında mevcut bilgilerini yakalama için genel senaryolar genel bakış."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 60930d78-d2d4-4d5d-9651-bdda50b0da0e
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: a9bd222bcf85abc31621ce7c09264a399fbb7a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-common-scenarios"></a>Azure Veri Kataloğu genel senaryoları
Bu makalede Azure veri Kataloğu, var olan veri kaynaklarından daha fazla değer almak, kuruluşunuzun burada yardımcı olabilir yaygın senaryolar sunar.

## <a name="scenario-1-registration-of-central-data-sources"></a>Senaryo 1: Kayıt Merkezi veri kaynakları
Kuruluşlar, çok yüksek değerli veri kaynağı genellikle sahiptir. Bu veri kaynaklarının iş satır, çevrimiçi işlem işleme (OLTP) sistemleri, veri ambarlarında ve iş zekası/analytics veritabanlarını içerir. sistemleri sayısı hello ve bunlar arasında çakışma Merhaba, genellikle gelişmesi iş gereksinimleriniz ve örneğin, birleşmeler veya satın almalar sonucunda, hello iş kendisini dönüşmesi zamanla artar.

Bunu burada toolocate hello bu veri kaynaklarının içinde veri için kuruluş üyeleri tooknow zor olabilir. Merhaba aşağıdaki gibi soruları tüm çok ortaktır:

* Merhaba üç HR sistemleri ı gereken hello şirket içinde bu tür bir rapor kullanım toocreate kullanılıyor?
* Burada tooget hello satış numaraları hello mali yılın için yalnızca sona erdi sertifikalı gitmesi gereken?
* Kimin ı istemelisiniz veya tooget erişim toohello veri ambarı kullanması gereken hello işlem nedir?
* Bu değerler doğru olup olmadığını bilmek yok. Kimin ı öngörüleri için nasıl ı my ekibi ile Bu panoyu paylaşmak önce kullanılan toobe bu verileri beklenen sorabilir miyim?

toothese ve diğer sorular, Azure veri Kataloğu yanıtlar sağlar. Merhaba Merkezi, yüksek değerli, kuruluş genelinde kullanılan BT tarafından yönetilen veri kaynakları genellikle hello katalog doldurmak için hello mantıksal başlangıç noktasıdır. Herhangi bir kullanıcı bir veri kaynağı kaydedebilirsiniz rağmen büyük olasılıkla tooprovide değeri toohello en büyük sayıda kullanıcılar hello veri kaynaklarıyla kick-started hello katalog sahip benimsenmesini ve hello sistem kullanımını yardımcı olur. 

Azure veri Kataloğu ile başlıyorsanız, ilk adım toosuccess tanımlayarak ve veri tüketicileri, birçok farklı ekip tarafından kullanılan önemli veri kaynaklarını kaydederek olabilir.

Bu senaryo aynı zamanda bir fırsat tooannotate hello yüksek değerli veri kaynaklarını toomake sunar onları daha kolay toounderstand ve erişim. Bir anahtar bu çalışmaların kullanıcıların erişim toohello veri kaynağına nasıl isteyebilir tooinclude bilgi yönüdür. Azure veri Kataloğu ile Merhaba e-posta adresini hello kullanıcı veya denetleme veri kaynağı erişimi, bağlantılar tooexisting araçları veya belge sorumlu bir ekip veya hello erişim isteği işlemini açıklar serbest metin sağlayabilir. Bu bilgiler tanımlanır ve hello veri kaynağı sahipleri tarafından denetlenen hello işlemleri kullanarak veri tooeasily erişim isteği kimin kayıtlı veri kaynaklarını bulmasına ancak henüz izinleri tooaccess etkinleştirmemiş yardımcı üyeleri hello.

## <a name="scenario-2-self-service-business-intelligence"></a>Senaryo 2: Self Servis iş zekası
Geleneksel kurumsal iş zekası çözümleri toobe devam etmesine rağmen birçok kuruluş verilerin çok bir bölümü Windows'un, ayak iş kolu değiştirme hello BI Self Servis ve daha önemli yaptı. Self Servis BI kullanarak, bilgi çalışanlarının ve analistleri kendi raporları, çalışma kitaplarına ve panolar merkezi BT ekibi veya bu BT ekibin zamanlama ve kullanılabilirlik ile sınırlı kalmayarak öğesine bağlı kalmadan oluşturabilirsiniz.

Self Servis BI senaryolarda, kullanıcıların yaygın olarak birçok önceden BI ve analiz için kullanılmamış birden fazla kaynaktan veri birleştirin. Bu veri kaynaklarının bazıları zaten biliniyor olabilir ancak bunu hangi toodo toolocate zor toodiscover olması ve olası veri kaynakları için belirli bir görevi değerlendirin.

Geleneksel olarak, bu bulma işlemi el ile bir bilgisayardır: analistleri diğer kişilerin Aranan hello verilerle çalışmak kendi eş ağ bağlantıları tooidentify kullanın. Bir veri kaynağı bulundu ve kullanılan sonra hello işlem yeniden her sonraki Self Servis BI çabayla, birden çok kullanıcı bulma yedekli el ile işlemi gerçekleştirmek için yinelenir.

Azure veri Kataloğu ile kuruluşunuz bu döngüsü çaba bozulabilir. Bir veri kaynağı geleneksel araçlarla öğrendiğinizde bir analist bunu toomake kaydedebilirsiniz, gelecekteki hello diğer kullanıcılar tarafından daha kolay bulunabilir. Merhaba analist hello kayıtlı veri varlıklarına açıklama tarafından daha fazla değer ekleyebilirsiniz, ancak bu ek açıklama tootake yer gerekmez hello aynı saat kayıt. Kullanıcılar kendi zamanlamaları izin olarak zaman içinde kademeli olarak hello kataloğa kayıtlı değer toohello veri kaynakları ekleme katkıda bulunabilir.

Bu organik büyüme hello katalog içeriğinin doğal tamamlama bir toohello eylemli kayıt merkezi veri kaynaklarının değil. Çok sayıda kullanıcı gerekir verilerle önceden doldurma hello katalog motivator ilk kullanım ve bulma olabilir. Etkinleştirme kullanıcıları tooregister ve açıklama ek kaynakları, bunları ve diğer kuruluş üyeleri bağlı bir şekilde tookeep olabilir.

Bu, özellikle Self Servis BI bu senaryo odaklanıyor olsa da, hello aynı desenleri ve zorluklar toolarge ölçekli şirket BI projeleri de uygulanacağını dikkate değerdir. Veri Kataloğu'nu kullanarak, kuruluşunuz veri kaynağı bulma işlemini elle içerir çaba artırabilir.

## <a name="scenario-3-capturing-tribal-knowledge"></a>Senaryo 3: Yakalama grupsal bilgilere
Nasıl hangi verilerin bildiğiniz, işinizin toodo gerekir ve nerede toofind verileri?

Bir süredir işinizde bırakıldı, büyük olasılıkla yalnızca bildiğiniz. İşlem öğrenme gradual gitti ve zaman içinde anahtar tooyour günlük çalışma hello veri kaynakları hakkında öğrendiniz.

Yeni bir çalışan ekibinizin katıldığında, o kişiyi mu nasıl hangi verilerin hello iş için gerekli olduğunu biliyor ve nerede toofind onu?

Büyük olasılıkla olan hello yeni bir kişiye tooyou soruları ile gelir.

Devam eden bu grupsal bilgilere aktarımını hello veri kaynağı bulma işlemi küçük ve büyük kuruluşlarda bir parçasıdır. Daha üst düzey ve deneyimli takım üyeleri bilgi hello yıllar içinde yerleşik sahiptir ve daha yeni ekip üyelerinin tooask öğrenilen bunları sorularınız varsa. Hello genellikle en önemli bilgiler yalnızca birkaç anahtar kişinin hello kafa içinde var ve bu kişilere tatile olan veya hello takım bırakın, hello kuruluş yükselmesine.

Onların bilgileri normalde olun çaba toodocument e-posta yoluyla veya takım SharePoint sitesinde Word belgelerinde paylaşımı veri uzmanları. Bu yaklaşım değerli olabilse de, yeni bir bulma sorun sunar: kişilerin nasıl yapılacağı hangi belge var, bilmeniz ve nerede toofind onu?

Azure veri Kataloğu ile tek, merkezi konumda depolamak ve bu grupsal bilgilere paylaşımı ve kolayca bulunabilir yapmak için kuruluşunuzun yok. Veri Kataloğu'nda, veri uzmanlar doğrudan veri varlıklarına açıklama ve tooexisting belgelere bağlantılar sağlar. Kuruluş üyeleri hello katalog toodiscover bir veri kaynağı kullandığınızda, bunlar yalnızca hello kaynak kendisi, aynı zamanda daha önceden varolan hello bilgi yalnızca kuruluşunuzun uzmanlar, hello minds içinde bulabilirsiniz.
