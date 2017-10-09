---
title: "birden çok Hdınsight kümeleri bir Azure Data Lake Store hesabı - Azure ile aaaUse | Microsoft Docs"
description: "Bir Hdınsight birden çok toouse tek bir Data Lake Store hesabı ile nasıl küme öğrenin"
keywords: "hdınsight depolama, hdfs, yapılandırılmış veri, yapılandırılmamış verileri, veri gölü deposu"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>Birden çok Hdınsight kümeleri ile bir Azure Data Lake Store hesabınız

Hdınsight sürüm 3.5 ile başlayarak, hello varsayılan dosya sistemi Azure Data Lake Store hesapları ile Hdınsight kümeleri oluşturabilirsiniz.
Data Lake Store, büyük miktarlarda verinin yalnızca barındırmak için ideal hale getirir sınırsız depolama destekler; ancak da barındırmak için birden çok Hdınsight tek bir Data Lake deposu hesap paylaşan kümeleri. Nasıl toocreate bir Hdınsight kümesini Data Lake Store hello depolama ile instructionson için bkz: [Hdınsight kümeleri oluşturma Data Lake Store ile](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Bu makale, bir tek ve paylaşılan veri Gölü depolamak birden çok kullanılan hesabı ayarlama önerileri toohello Data Lake Deposu Yöneticisi sağlar **etkin** Hdınsight kümeleri. Bu öneriler, paylaşılan bir Data Lake store hesabında birden çok güvenli yanı sıra güvenli olmayan Hadoop kümeleri toohosting uygulayın.


## <a name="data-lake-store-file-and-folder-level-acls"></a>Data Lake Store dosya ve klasör düzeyinde ACL'leri

Merhaba, bu makalenin kalanında yakından açıklanan Azure Data Lake Store içinde dosya ve klasör düzeyinde ACL'ler iyi bir bilgiye sahip olduğunu varsayar [erişim denetimi Azure Data Lake Store'da](../data-lake-store/data-lake-store-access-control.md).

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>Birden çok Hdınsight kümeleri için Data Lake Store Kurulumu
Bize iki düzeyli klasör hiyerarşisi birden çok Hdınsight kümeleri ile bir Data Lake Store hesabı kullanarak tooexplain hello ilgili öneriler alın. Bir Data Lake Store hesabı hello klasör yapısı ile sahip göz önünde bulundurun **/kümeleri/Finans**. Bu yapı ile Merhaba Finans kuruluş tarafından gerekli tüm hello kümeleri /clusters/finance hello depolama konumu olarak kullanabilirsiniz. Başka bir kuruluş, pazarlama söyleyin, istediği toocreate Hdınsight kümeleri kullanarak aynı Data Lake Store hesabı Merhaba, /clusters/marketing oluşturabilirsiniz gelecekteki hello içinde. Şu an için yalnızca kullanalım **/kümeleri/Finans**.

Bu klasör yapısı toobe etkili bir şekilde Hdınsight kümeleri tarafından kullanılan tooenable Merhaba Data Lake Store yönetici uygun izinleri hello tabloda açıklandığı gibi atamanız gerekir. Merhaba tabloda gösterilen hello izinleri tooAccess ACL'ler ve değil varsayılan ACL'leri karşılık gelir. 


|Klasör  |İzinler  |Sahip olan kullanıcı  |Sahip olan grup  | Adlı kullanıcı | Adlı kullanıcı izinleri | Adlandırılmış Grup | Adlandırılmış grup izinleri |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x--x  |Yönetici |Yönetici  |Hizmet sorumlusu |--x  |FINGRP   |r-x         |
|/Clusters | rwxr-x--x |Yönetici |Yönetici |Hizmet sorumlusu |--x  |FINGRP |r-x         |
|/ kümeleri/Finans | rwxr-x--t |Yönetici |FINGRP  |Hizmet sorumlusu |rwx  |-  |-     |

Merhaba tabloda

- **Yönetici** hello oluşturan ve Data Lake Store hesabı hello Yöneticisi.
- **Hizmet sorumlusu** hello hesabıyla ilişkilendirilmiş hello Azure Active Directory (AAD) hizmet asıl.
- **FINGRP** hello Finans kuruluş kullanıcılardan içeren aad'de oluşturduğunuz bir kullanıcı grubu.

Yönergeler için nasıl toocreate (oluşturan ayrıca bir hizmet sorumlusu) bir AAD uygulaması bkz [bir AAD uygulaması oluşturabilir](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application). Yönergeler için nasıl toocreate AAD, bir kullanıcı grubunda bkz [Azure Active Directory içinde grupları yönetme](../active-directory/active-directory-accessmanagement-manage-groups.md).

Bazı önemli noktaları tooconsider.

- Merhaba iki düzey klasör yapısı (**/ / Finans/kümeleri**) oluşturulur ve uygun izinlere sahip hello Data Lake Store yönetici tarafından sağlanan **önce** hello depolama hesabıyla kümeleri için. Bu yapı kümeleri oluşturulurken otomatik olarak oluşturulmaz.
- Yukarıdaki Hello örnek önerir grubunun sahibi olan hello ayarı **/kümeleri/Finans** olarak **FINGRP** ve sorgulamasına **r-x** erişim tooFINGRP toohello tüm klasör hiyerarşisi Merhaba kökünden başlatılıyor. Bu FINGRP hello üyeleri kökünden başlayarak hello klasör yapısı gidebilirsiniz sağlar.
- Farklı AAD hizmet asıl adı altında kümeleri oluşturabilir, hello durumda **/kümeleri/Finans**, hello Yapışkan-bit (Merhaba üzerinde ayarlandığında **Finans** klasörü) klasörleri bir hizmeti tarafından oluşturulan sağlar Asıl hello tarafından diğer silinemiyor.
- Merhaba klasör yapısı ve izinleri yerinde olduktan sonra Hdınsight küme oluşturma işlemi kümeye özgü depolama loaction altında oluşturur **/ / Finans/kümeleri**. Örneğin, hello adı fincluster01 sahip bir küme için hello depolama olabilir **/clusters/finance/fincluster01**. Merhaba sahipliği ve Hdınsight kümesi tarafından oluşturulan hello klasörler için izinleri gösterildiğini burada hello tablosunda.

    |Klasör  |İzinler  |Sahip olan kullanıcı  |Sahip olan grup  | Adlı kullanıcı | Adlı kullanıcı izinleri | Adlandırılmış Grup | Adlandırılmış grup izinleri |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/Clusters/finanace/fincluster01 | rwxr-x---  |Hizmet sorumlusu |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>Önerileri için girdi ve çıktı verilerini işi

Biz giriş verileri tooa işi ve bir iş çıkışlarından hello öneri dışında bir klasörde depolanır **/kümeleri**. Bu, silinen tooreclaim hello küme özgü bir klasörde olsa bile, bazı depolama alanı, hello iş girişleri ve çıkışları gelecekte kullanılmak üzere hala kullanılabilir olmasını sağlar. Böyle bir durumda hello klasör hiyerarşisi hello iş girişleri ve çıkışları depolamak için uygun düzeyde bir erişim hello için hizmet sorumlusu verdiğinden emin olun.

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>Tek bir depolama hesabına paylaşımı kümelerinde sınırla

Bu kümelerinde çalıştırılmayı hello iş yükü Hello sınırı tek bir Data Lake Store hesabı paylaşabilirsiniz kümeleri hello sayısına bağlıdır. Çok fazla sayıda küme veya çok yoğun iş yükleri bir depolama hesabını paylaşmak hello kümelerinde sahip hello depolama hesabı giriş/çıkış tooget kısıtlanan neden olabilir.

## <a name="support-for-default-acls"></a>Varsayılan ACL desteği

Adlı kullanıcı erişimi (yukarıdaki hello tablosundaki gösterildiği gibi) bir hizmet sorumlusu oluştururken, öneririz **değil** hello adlı kullanıcı varsayılan ACL ile ekleme. Sahibi olan kullanıcı, sahibi olan Grup ve diğerleri için varsayılan ACL'leri sonuçları 770 izinleri hello atamasını kullanarak adlı kullanıcının erişimi sağlama. Bu varsayılan değeri 770 sahibi olan kullanıcı (7) veya sahibi olan Grup (7) izinlerinin hemen almaz, ancak hemen başkalarının (0) tüm izinleri alır. Bu bilinen bir sorun bir belirli kullanım ayrıntılı hello olarak ele alınan örneği ile sonuçlanır [bilinen sorunlar ve geçici çözümler](#known-issues-and-workarounds) bölümü.

## <a name="known-issues-and-workarounds"></a>Bilinen sorunlar ve geçici çözümler

Bu bölümde, bilinen sorunlar Hdınsight kullanarak Data Lake Store ve bunların geçici çözümleri için hello listelenir.

### <a name="publicly-visible-localized-yarn-resources"></a>Herkese görünür yerelleştirilmiş YARN kaynaklar

Yeni bir Azure Data Lake store hesabı oluşturulduğunda, hello kök dizini otomatik olarak erişim ACL izni BITS kümesi too770 ile sağlanır. Merhaba kök klasörün sahibi olan kullanıcı hello hesap (Merhaba Data Lake Store Yöneticisi) oluşturulan toohello kullanıcı ayarı ve hello sahibi olan Grup hello hesabı oluşturuldu hello kullanıcının birincil grup toohello ayarlanır. Erişim yok "başkaları için" sağlanır.

Bu ayarları tooaffect bir özel Hdınsight kullanım, yakalanan örneği bilinen [YARN 247](https://hwxmonarch.atlassian.net/browse/YARN-247). İş gönderimlerini bir hata iletisi benzer toothis ile başarısız olabilir:

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

Ortak kaynakları hello yerelleştirilirken YARN JIRA daha önce bağlı hello içinde tüm hello yerelleştiriciye doğrular belirtildiği gibi istenen hello uzak dosya sistemi izinlerini denetleyerek gerçekten ortak kaynaklardır. Bu koşul sığmayan LocalResource yerelleştirme için reddedilir. izinler için onay Merhaba, "başkaları için" okuma erişim toohello dosyası içerir. Bu senaryo Giden kutusu Azure Data Lake çok tüm erişimini engellediği beri Azure Data Lake, Hdınsight kümelerinde barındırdığında çalışmaz kök klasör düzeyinde "diğer".

#### <a name="workaround"></a>Geçici çözüm
Kümesini yürütmek Okuma izinlerini **başkalarının** hello hiyerarşisi aracılığıyla örneğin  **/** , **/kümeleri** ve   **/kümeleri/Finans**  hello yukarıdaki tabloda gösterildiği gibi.

## <a name="see-also"></a>Ayrıca bkz.

* [Hdınsight kümesi Data Lake Store ile depolama alanı olarak oluşturun.](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


