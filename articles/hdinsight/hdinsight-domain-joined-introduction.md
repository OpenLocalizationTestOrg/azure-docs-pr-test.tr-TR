---
title: "aaaHadoop güvenliği - Hdınsight kümeleri - Azure etki alanına katılmış | Microsoft Docs"
description: "Öğrenin ...."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>Etki alanına katılmış Hdınsight kümeleri (Önizleme) ile bir giriş tooHadoop güvenliği

Azure HDInsight şimdiye kadar yalnızca tek bir kullanıcının yerel yönetici olmasını destekliyordu. Bu durum küçük çaplı uygulama ekipleri veya departmanları için idealdi. Daha fazla popülerliği hello Kurumsal kesimdeki hello kazanılan tabanlı iş yükleri için Kurumsal gerekir Hadoop olarak active directory tabanlı kimlik doğrulaması, çok kullanıcılı destek ve rol tabanlı erişim denetimi gibi düzeydeki özellikleri giderek önemli hale geldi. Etki alanına katılmış Hdınsight kümeleri kullanarak, bir Hdınsight birleştirilmiş küme tooan Active Directory etki alanı oluşturduğunuzda, Azure Active Directory toolog tooHDInsight kümede aracılığıyla doğrulanabilir çalışanlar hello Kurumsal listesi yapılandırmak. Merhaba kuruluş dışında herhangi bir kişi oturum açamıyor veya hello Hdınsight kümesine erişim. Merhaba Kurumsal Yönetici güvenlik Hive kullanarak için rol tabanlı erişim denetimi yapılandırabilirsiniz [Apache bırakabilmenizi](http://hortonworks.com/apache/ranger/), böylece kısıtlama erişim toodata tooonly gerektiği kadar. Son olarak, hello Yöneticisi çalışanlar tarafından hello veri erişimi denetleyebilirsiniz ve böylece şirket kaynaklarını İdaresi yüksek derecede elde ilkeleri, yapılan değişiklikleri tooaccess denetleyebilirsiniz.

> [!NOTE]
> Bu Önizleme'de açıklanan hello yeni özellikler yalnızca Linux tabanlı Hdınsight kümeleri Hive iş yükü için kullanılabilir. diğer iş yüklerini Merhaba, HBase, Spark, Storm ve Kafka, etkinleştirilecek gibi gelecekte serbest bırakır.

> [!IMPORTANT]
> Oozie etki alanına katılmış Hdınsight üzerinde etkin değil.

## <a name="benefits"></a>Avantajlar
Kuruluş Güvenliği dört ana katmandan oluşur: Çevre Güvenliği, Kimlik Doğrulaması, Yetkilendirme ve Şifreleme.

![Etki alanına katılmış HDInsight kümelerinin avantaj katmanları](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png).

### <a name="perimeter-security"></a>Çevre Güvenliği
HDInsight’ta çevre güvenliği sanal ağlar ve Ağ Geçidi hizmeti kullanılarak sağlanır. Bugün, bir kuruluş yöneticisi, bir sanal ağ içinde bir Hdınsight kümesi oluşturup bu ağ güvenlik grupları (gelen veya giden güvenlik duvarı kuralları) toorestrict erişim toohello sanal ağı kullanabilirsiniz. Merhaba IP adresleri hello tanımlı gelen yalnızca güvenlik duvarı kuralları hello Hdınsight kümesi, böylece çevre güvenliği sağlama ile mümkün toocommunicate olacaktır. Başka bir güvenlik katmanı da Ağ Geçidi hizmetinin kullanılmasıdır. ağ geçidi Hello ilk her gelen istek toohello Hdınsight kümesi için savunma hattı olarak davranan hello hizmetidir. Merhaba isteği kabul eder, onu doğrular ve yalnızca sonra böylece tooother adı ve veri düğümlerini hello kümedeki çevre güvenliği sağlama kümedeki diğer düğümlere hello isteği toopass toohello sağlar.

### <a name="authentication"></a>Kimlik Doğrulaması
Bu genel önizleme ile kuruluş yöneticileri etki alanına katılmış bir HDInsight kümesini [sanal ağda](https://azure.microsoft.com/services/virtual-network/) oluşturabilir. Merhaba hello Hdınsight küme düğümlerinin hello kuruluş tarafından yönetilen birleştirilmiş toohello etki alanı olacaktır. Bu sonuç [Azure Active Directory Etki Alanı Hizmetleri](../active-directory-domain-services/active-directory-ds-overview.md) kullanılarak elde edilir. Merhaba kümedeki tüm düğümlerin hello hello Kurumsal yönetir birleştirilmiş tooa etki alanı var. Bu kurulum ile Merhaba Kurumsal çalışanlar toohello küme düğümleri üzerinde etki alanı kimlik bilgilerini kullanarak oturum açabilir. Onaylanan diğer uç noktaları hello kümesi ile ton, Ambari görünümleri, ODBC, JDBC, PowerShell ve REST API'leri toointeract gibi kendi etki alanı kimlik bilgileri tooauthenticate de kullanabilir. Hello Yöneticisi bu uç noktaları aracılığıyla hello kümeyle etkileşim kullanıcı hello sayısını sınırlandırma üzerinde tam denetime sahiptir.

### <a name="authorization"></a>Yetkilendirme
Çoğu kuruluş tarafından izlenen en iyi uygulama her çalışan erişim tooall kurumsal kaynaklara sahip olur. Benzer şekilde, bu sürümle birlikte, hello Yöneticisi hello küme kaynakları için rol tabanlı erişim denetimi ilkeleri tanımlayabilirsiniz. Hello Yöneticisi yapılandırabilirsiniz Örneğin, [Apache bırakabilmenizi](http://hortonworks.com/apache/ranger/) tooset erişim denetimi ilkeleri Hive için. Bu işlev Çalışanlar yalnızca mümkün tooaccess olmasını sağlar toobe işlerinde başarılı gereksinim duyduğunuz kadar veri. SSH erişim toohello küme de sınırlı yalnızca toohello yöneticisidir.

### <a name="auditing"></a>Denetim
Hdınsight küme kaynakları yetkisiz kullanıcılara karşı ve denetim hello veri güvenliğini sağlamak için tüm toohello küme kaynaklarına erişim ve hello hello koruma yanı sıra gerekli tootrack verilerdir hello kaynakların yetkisiz olarak veya yanlışlıkla erişim. Bu önizleme ile hello Yöneticisi görüntüleyebilir ve rapor tüm erişim toohello Hdınsight küme kaynakları ve veri. uç noktaları toohello erişim denetimi ilkeleri Apache bırakabilmenizi yapılan tüm değişiklikler rapor desteklenen ve Hello Yöneticisi de görüntüleyebilirsiniz. Bir etki alanına katılmış Hdınsight kümesi hello tanıdık Apache bırakabilmenizi UI toosearch denetim günlüklerini kullanır. Merhaba arka uçta bırakabilmenizi kullanan [Apache Solr](http://hortonworks.com/apache/solr/) depolamak ve arama hello günlükleri.

### <a name="encryption"></a>Şifreleme
Toplantı Kuruluş güvenliği ve uyumluluk gereksinimleri için önemli olan verileri koruma ve erişim toodata yetkisiz çalışanlardan kısıtlama yanı sıra, bu da şifreleyerek güvenli hale getirilmelidir. Her ikisi de Hdınsight kümeleri, Azure depolama Blob veri depolarına hello ve Azure Data Lake Storage destek saydam sunucu tarafı [verilerin şifrelenmesi](../storage/common/storage-service-encryption.md) REST. Güvenli HDInsight kümeleri bekleyen verileri de kapsayan sunucu tarafı veri şifreleme özelliği ile sorunsuz bir şekilde çalışacaktır.

## <a name="next-steps"></a>Sonraki adımlar
* Etki alanına katılmış HDInsight kümesini yapılandırmak için bkz. [Etki alanına katılmış HDInsight kümelerini yapılandırma](hdinsight-domain-joined-configure.md).
* Etki alanına katılmış HDInsight kümesini yönetmek için bkz. [Etki alanına katılmış HDInsight kümelerini yönetme](hdinsight-domain-joined-manage.md).
* Hive ilkelerini yapılandırmak ve Hive sorgularını çalıştırmak için bkz. [Etki alanına katılmış HDInsight kümeleri için Hive ilkelerini yapılandırma](hdinsight-domain-joined-run-hive.md).
* Etki alanına katılmış Hdınsight kümelerinde SSH kullanarak Hive sorguları çalıştırmak için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
