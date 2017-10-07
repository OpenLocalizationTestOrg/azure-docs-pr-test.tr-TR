---
title: "aaaAccess Hadoop YARN uygulama günlüklerini program aracılığıyla - Azure | Microsoft Docs"
description: "Access uygulaması Hdınsight Hadoop kümesinde programlı olarak günlüğe kaydeder."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Windows tabanlı Hdınsight üzerinde erişim YARN uygulama günlükleri
Bu konuda, nasıl Azure hdınsight'ta Hadoop Windows tabanlı kümede bitirdikten YARN (henüz başka bir kaynak Uzlaştırıcı) uygulamaları için günlükleri tooaccess hello açıklanmaktadır.

> [!IMPORTANT]
> Bu belgedeki Hello bilgiler yalnızca tooWindows tabanlı Hdınsight kümeleri geçerlidir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement). Linux tabanlı Hdınsight kümelerinde YARN erişme hakkında bilgi günlükleri için bkz: [erişim YARN uygulama günlüklerini hdınsight'ta Linux tabanlı Hadoop üzerinde](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>Ön koşullar
* Bir Windows tabanlı Hdınsight kümesi.  Bkz: [Hdınsight oluşturma Windows tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>YARN zaman çizelgesi sunucu
Merhaba <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN zaman çizelgesi sunucu</a> de framework özgü olarak uygulama bilgilerini iki farklı arabirimleri aracılığıyla tamamlanmış uygulamaları genel bilgiler sağlar. Bu avantajlar şunlardır:

* 3.1.1.374 sürümüyle etkin ya da daha yüksek depolama ve alma Hdınsight kümelerinde genel uygulama bilgilerinin açıldı.
* Hdınsight kümelerinde Hello çerçeveye özel uygulama bilgileri hello zaman çizelgesi sunucu bileşeninin şu anda kullanılamıyor.

Uygulamalar hakkında genel bilgiler aşağıdaki veriler, her türlü hello içerir:

* Merhaba uygulama kimliği, uygulamanın benzersiz tanıtıcısı
* Merhaba uygulaması başlatan hello kullanıcı
* Toocomplete Merhaba uygulaması denemeleri hakkında bilgi yapılan
* Belirtilen uygulama girişimleri tarafından kullanılan Merhaba kapsayıcılara

Bu bilgileri, Hdınsight kümelerinde Azure Resource Manager tooa geçmişi hello varsayılan kapsayıcı varsayılan Azure depolama hesabınızın deposundaki tarafından depolanır. Bu genel veriler tamamlanmış uygulamalar üzerinde bir REST API'si alınabilir:

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>YARN uygulamalar ve günlükleri
YARN kaynak Yönetimi'nden uygulama zamanlama/izleme ayrıştırarak birden fazla programlama modeli (bunlardan biri olan MapReduce) destekler. Bu genel yapılır *ResourceManager* (RM) çalışan-düğüm başına *NodeManagers* (NMs) ve uygulama başına *ApplicationMasters* (AMs). Merhaba uygulama başına AM kaynakları (CPU, bellek, disk, ağ) hello RM ile uygulamanızı çalıştırmak için anlaşır Merhaba RM olarak verilen bu kaynakları NMs toogrant ile çalışır *kapsayıcıları*. Merhaba AM hello RM tarafından Merhaba kapsayıcılara atanan tooit hello ilerlemesini izlemek için sorumludur Bir uygulama Merhaba uygulaması hello doğasına bağlı olarak çok sayıda kapsayıcı gerektirebilir.

Ayrıca, her uygulama katları oluşabilir *uygulama denemeleri* hello varlığı çökme (Crash) veya bir AM arasındaki iletişimi toohello kaybı nedeniyle, sipariş toofinish içinde ve bir RM Bu nedenle, kapsayıcı bir uygulamanın tooa belirli girişimi verilir. Bir fikir hello bağlam YARN uygulama tarafından gerçekleştirilen çalışmanın temel birim için bir kapsayıcı sağlar ve bir kapsayıcı hello bağlamında yapılır tüm iş üzerinde hangi hello kapsayıcı ayrılan hello tek çalışan düğümünde gerçekleştirilir. Bkz: [YARN kavramları] [ YARN-concepts] daha ayrıntılı başvuru.

Uygulama (ve ilişkili hello kapsayıcı günlükleri) sorunlu Hadoop uygulamalarında hata ayıklama de önemlidir. YARN toplama, toplama ve hello ile uygulama günlükleri depolamak için iyi bir çerçeve sağlar [günlük toplama] [ log-aggregation] özelliği. bir alt düğüm üzerindeki tüm kapsayıcıları arasında günlükleri toplar ve bir uygulama bittikten sonra toplanmış başına bir günlük dosyası çalışan düğümüne hello varsayılan dosya sistemi olarak saklar gibi hello günlük toplama özellik erişen uygulama günlüklerini daha belirleyici kolaylaştırır. Uygulamanızın yüzlerce veya binlerce kapsayıcıların kullanabilir, ancak günlükleri tek alt düğüm üzerinde çalışan tüm kapsayıcıları için her zaman toplanmış tooa tek bir dosya, uygulamanız tarafından kullanılan çalışan düğümü başına bir günlük dosyasında kaynaklanan görüntülenir. Günlük toplama Hdınsight kümelerinde varsayılan olarak etkinleştirilmiştir (sürüm 3.0 ve üstü), ve toplanan günlükleri hello varsayılan kapsayıcı kümenizin hello konumu şu anda bulunabilir:

    wasb:///app-logs/<user>/logs/<applicationId>

Bu konumda bulunan *kullanıcı* Merhaba uygulaması başlatan hello kullanıcı hello adıdır ve *ApplicationId* hello YARN RM tarafından atanan bir uygulamanın hello benzersiz tanımlayıcıdır.

Bunlar yazıldığı şekilde hello toplanmış günlükleri doğrudan okunabilir olmayan bir [TFile][T-file], [ikili biçimi] [ binary-format] kapsayıcı dizini. YARN CLI araçlarını toodump, bu günlükler uygulamalar veya ilgi kapsayıcıları için düz metin olarak sağlar. YARN komutları (tooit RDP bağlandıktan sonra) doğrudan hello küme düğümleri üzerinde aşağıdaki hello birini çalıştırarak düz metin olarak bu günlükleri görüntüleyebilirsiniz:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>YARN ResourceManager kullanıcı Arabirimi
Merhaba YARN ResourceManager UI hello küme headnode üzerinde çalışır ve Azure portalı panosunun hello erişilebilir:

1. Çok oturum[Azure portal](https://portal.azure.com/).
2. Merhaba sol menüsünde **Gözat**, tıklatın **Hdınsight kümeleri**, tooaccess hello YARN uygulama günlüklerini istediğiniz Windows tabanlı bir kümesine tıklayın.
3. Merhaba üst menüsünde **Pano**. Yeni bir tarayıcıda açılan bir sayfa görürsünüz adlı sekmesini **Hdınsight sorgu konsol**.
4. Gelen **Hdınsight sorgu konsol**, tıklatın **Yarn kullanıcı Arabiriminde**.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
