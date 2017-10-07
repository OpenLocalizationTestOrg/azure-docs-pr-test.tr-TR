---
title: "aaaPublish Hdınsight uygulamalarını - Azure | Microsoft Docs"
description: "Bilgi nasıl toocreate ve Hdınsight uygulamalarını yayımlama."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>Hello Azure Marketi içine Hdınsight uygulamalarını yayımlama
HDInsight uygulaması kullanıcıların Linux tabanlı HDInsight kümesine yükleyebileceği bir uygulamadır. Bu uygulamalar Microsoft veya bağımsız yazılım satıcıları (ISV) tarafından ya da sizin tarafınızdan geliştirilebilir. Bu makalede, bilgi nasıl toopublish hello Azure Marketi Hdınsight uygulamasına.  Yayımlama hello Azure Marketi içine hakkında genel bilgi için bkz: [bir teklif toohello Azure Marketi'nde yayımlama](../marketplace-publishing/marketplace-publishing-getting-started.md).

Hdınsight uygulamalarını kullanmak hello *Getir bilgisayarınızı kendi lisans (KLG)* burada uygulama sağlayıcısı hello uygulama tooend-kullanıcıları lisansı sağlamaktan sorumlu ve son kullanıcılar yalnızca ücretli Azure tarafından hello kaynaklar için bunlar modeli , hello Hdınsight kümesi ve VM/düğümleri gibi oluşturun. Şu anda hello uygulamanın kendisi için fatura Azure üzerinden yapılmamaktadır.

Uygulama ile ilgili diğer Hdınsight makale:

* [Hdınsight uygulamaları yükleme](hdinsight-apps-install-applications.md): tooinstall bir Hdınsight uygulaması tooyour nasıl kümeleri öğrenin.
* [Özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md): öğrenin nasıl tooinstall ve test özel Hdınsight uygulamaları.

## <a name="prerequisites"></a>Ön koşullar
toosubmit, özel uygulama toohello Market oluşturduktan ve özel uygulamanızı test gerekir. Aşağıdaki makaleleri hello bakın:

* [Özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md): öğrenin nasıl tooinstall ve test özel Hdınsight uygulamaları.

Ayrıca Geliştirici hesabınızı kayıtlı gerekir. Bkz: [bir teklif toohello Azure Marketi'nde yayımlama](../marketplace-publishing/marketplace-publishing-getting-started.md) ve [Microsoft Developer hesabı oluşturma](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Uygulama tanımlama
Uygulamaları toohello Azure Marketi yayımlamak için söz konusu iki adımı vardır.  İlk tanımladığınız bir **createUiDef.json** uygulamanızın dosya tooindicate; ile uyumludur ve sonra hello Azure portal hello şablondan yayımlayın. hello bölümü aşağıdaki örnek bir createUiDef.json dosyası değil.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| Alan | Açıklama | Olası değerler |
| --- | --- | --- |
| types |Merhaba uygulamanın uyumlu olduğu küme türleri hello. |Hadoop, HBase, Storm, Spark, (veya bunların herhangi bir birleşimi) |
| tiers |Merhaba uygulamanın uyumlu olduğu küme katmanları hello. |Standart, Premium (veya her ikisi) |
| versions |Merhaba uygulamanın uyumlu olduğu Hdınsight küme türleri hello. |3.4 |

## <a name="application-install-script"></a>Uygulama yükleme betiği
Bir uygulama yüklendiğinde bir kümede (var olan bir ya da yeni bir tane), bir kenar düğümüne oluşturulduğundan ve hello uygulama yükleme komut dosyası üzerinde çalıştırın.
  > [!IMPORTANT]
  > Merhaba uygulama yükleme betik adları Hello adı biçimi aşağıdaki hello ile belirli bir küme için benzersiz olması gerekir.
  > 
  > name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > Üç bölümleri toohello komut dosyası adı olduğunu unutmayın:
  > 
  > 1. Merhaba uygulama adı veya ad ilgili toohello uygulama içermesi gereken bir betik adı ön eki.
  > 2. Okunabilirlik için bir "-" işareti.
  > 3. Parametre hello gibi hello uygulama adı ile benzersiz bir dize işlevi.
  > 
  > Yukarıdaki hello sona eriyor olma bir örnektir: betik eylemi listesinde hue-Install-v0-4wkahss55hlas hello içinde kalıcı. Örnek bir JSON yükü için bkz. [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).
  > 
Hello yükleme komut dosyası hello aşağıdaki özelliklere sahip olması gerekir:
1. Merhaba betik ıdempotent olduğundan emin olun. Birden fazla çağrı toohello komut dosyası üretmek hello aynı sonucu.
2. Merhaba betik düzgün sürümlü olmalıdır. Yükseltme veya değişiklikleri tooinstall Merhaba uygulaması çalıştığınız müşterileri etkilenmez böylece test hello komut dosyası için farklı bir konum kullanın. 
3. Yeterli günlük toohello betikleri her noktada ekleyin. Genellikle, komut dosyası günlükleri hello hello tek yolu toodebug uygulama yükleme sorunlardır.
4. Böylece Hello yükleme geçici ağ sorunları etkilenmez çağrıları tooexternal Hizmetleri veya kaynakları yeterli yeniden deneme olduğundan emin olun.
5. Kodunuzu hello düğümlerinde Hizmetleri başlıyorsanız hello Hizmetleri izlenir ve toostart düğümü yeniden başlatma durumunda otomatik olarak yapılandırılmış emin olun.

## <a name="package-application"></a>Uygulama paketleme
HDInsight uygulamalarınızı yüklemek için tüm gerekli dosyaları içeren bir zip dosyası oluşturun. Zip dosyasında hello [uygulama yayımlama](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. [Özel HDInsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md) konusunda örneğe bakın.
* Gerekli tüm betikler.

> [!NOTE]
> Uygulama dosyaları (varsa web uygulama dosyaları dahil) hello üzerinde genel olarak erişilebilir olan herhangi bir uç nokta bulunabilir.
> 

## <a name="publish-application"></a>Uygulama yayımlama
Aşağıdaki adımları toopublish Hdınsight uygulaması hello izleyin:

1. Toohello üzerinde oturum [Azure yayımlama portalında](https://publish.windowsazure.com/).
2. Tıklatın **çözüm şablonları** hello sol toocreate yeni bir çözüm şablonu gelen.
3. Bir ad girin ve ardından **Yeni çözüm şablonu oluştur**’a tıklayın.
4. Tıklatın **Geliştirme Merkezi hesabı oluşturun ve birleştirme hello Azure program** tooregister bunu yapmadıysanız şirket.  Bkz. [Microsoft Developer hesabı oluşturma](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Tıklatın **bazı topolojiler tooget başlatıldı tanımlamak**. Bir çözüm şablonu topolojileri "üst" tooall değil. Bir teklif/çözüm şablonunda birden fazla topoloji tanımlayabilirsiniz. Bir teklif toostaging gönderildiğinde tüm topolojileri ile gönderilir. 
6. Bir topoloji adı girin ve hello artı işaretini tıklatın.
7. Yeni bir sürüm girin ve sonra hello artı işaretine tıklayın.
8. Karşıya yükleme hello zip dosyası içinde hazırlanmış [Uygulama paketleme](#package-application).  
9. **Sertifika İste**’ye tıklayın. Merhaba Microsoft Sertifika ekibi hello dosyalarını gözden geçirin ve hello topolojiyi onaylar.

## <a name="next-steps"></a>Sonraki adımlar
* [Hdınsight uygulamaları yükleme](hdinsight-apps-install-applications.md): tooinstall bir Hdınsight uygulaması tooyour nasıl kümeleri öğrenin.
* [Özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md): öğrenin nasıl toodeploy yayımlanmamış bir Hdınsight uygulaması tooHDInsight.
* [Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme](hdinsight-hadoop-customize-cluster-linux.md): öğrenin nasıl toouse betik eylemi tooinstall ek uygulamalar.
* [Azure Resource Manager şablonları kullanarak Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-arm-templates.md): nasıl toocall Resource Manager şablonları toocreate Hdınsight kümeleri öğrenin.
* [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md): nasıl toouse boş bir kenar düğümü Hdınsight kümesine erişmek, Hdınsight uygulamalarını test etme ve barındırma öğrenin Hdınsight uygulamaları.

