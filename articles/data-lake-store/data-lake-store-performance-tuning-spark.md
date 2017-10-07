---
title: "Data Lake Store Spark performans ayarlama yönergeleri aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store Spark performans kuralları ayarlama"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Performans yönergeler Spark Hdınsight ve Azure Data Lake Store için ayarlama

Spark üzerinde performans ayarlaması için küme üzerinde çalışan uygulama tooconsider hello sayısı gerekir.  Varsayılan olarak 4 çalıştırabilirsiniz, HDI kümesi üzerinde aynı anda uygulamaları (Not: hello varsayılan ayardır konu toochange).  Merhaba varsayılan ayarları geçersiz kılar ve hello kümesinin daha fazla bilgi için bu uygulamaları kullanmak için daha az uygulamaları toouse karar verebilirsiniz.  

## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).
* **Bir Azure Data Lake Store hesabı**. Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)
* **Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile. Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md). Merhaba küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.
* **Azure Data Lake Store üzerinde Spark kümesinde çalışan**.  Daha fazla bilgi için bkz: [kullanım Hdınsight Spark küme tooanalyze verileri Data Lake Store'da](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **Performans ayarlama yönergeleri ADLS**.  Genel performans için bkz [Data Lake deposu performans rehberi ayarlama](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>Parametreler

Spark işlerinin çalıştırırken, ADLS bizi tooincrease performansına olabilir hello en önemli ayarları şunlardır:

* **NUM yürütücüler** -hello yürütülebilir eşzamanlı görev sayısı.

* **Bellek içi Yürütücü** -hello tooeach Yürütücü ayrılmış bellek miktarı.

* **Yürütücü çekirdek** -çekirdek hello sayısı tooeach Yürütücü ayrılmış.                     

**NUM yürütücüler** Num yürütücüler hello Maksimum sayıda paralel olarak çalıştırılabilir görev ayarlayacak.  paralel olarak çalıştırılabilir görevleri gerçek sayısını Hello hello bellek ve CPU kaynaklarını kümenizdeki kullanılabilir sınırlıdır.

**Bellek içi Yürütücü** bu hello tooeach Yürütücü ayrılan bellek miktarıdır.  Her Yürütücü için ihtiyaç duyulan hello bellek hello işinde bağlıdır.  Karmaşık işlemleri için daha yüksek toobe hello bellek gerekir.  Okuma ve yazma gibi basit işlemleri için bellek gereksinimlerini daha düşük olacaktır.  Hello için bellek miktarı her Yürütücü Ambari içinde görüntülenebilir.  Ambari, tooSpark gidin ve hello yapılandırmalar sekmesini görüntüleyin.  

**Yürütücü çekirdek** bu hello Yürütücü çalıştırılabilir paralel iş parçacıklarının sayısını belirler Yürütücü başına kullanılan çekirdek hello miktarını belirler.  Örneğin, varsa Yürütücü çekirdek = 2, her Yürütücü hello Yürütücü 2 Paralel Görevler çalıştırabilirsiniz.  Merhaba Yürütücü-çekirdek hello işinde bağımlı olur.  Daha fazla Paralel Görevler her Yürütücü işleyebilmesi için g/ç yoğun iş büyük miktarda bellek görev başına gerektirmez.

Varsayılan olarak, Hdınsight'ta Spark çalıştırıldığında, her fiziksel çekirdek için iki sanal YARN çekirdek tanımlanır.  Bu bağlam birden çok iş parçacığından değiştirme miktarına ve concurrecy iyi bir denge sağlar.  

## <a name="guidance"></a>Rehber

Spark analitik iş yükleri toowork Data Lake Store'da verilerin ile çalışırken, Data Lake Store ile Merhaba en son Hdınsight sürüm tooget hello en iyi performansı kullanmanızı öneririz. İşinizi daha fazla g/ç yoğun olduğunda, belirli parametreleri yapılandırılmış tooimprove performans olabilir.  Azure Data Lake Store yüksek verimlilik işleyebilecek bir yüksek oranda ölçeklenebilir depolama platformudur.  Merhaba işi okuma veya yazma çoğunlukla oluşuyorsa, Azure Data Lake Store gelen g/ç tooand eşzamanlılık artırma performansı arttırabilir.

G/ç yoğun işleri için birkaç genel yolları tooincrease eşzamanlılık vardır.

**1. adım: kümenizde çalışan kaç uygulamalar belirlemek** – hello geçerli dahil olmak üzere hello kümede çalışan kaç uygulamalar bilmeniz gerekir.  4 olduğunu hello için varsayılan değerleri ayarı varsayar her Spark eş zamanlı olarak çalıştırılan uygulamalar.  Bu nedenle, yalnızca % 25'hello kümenin her uygulama için kullanılabilir olacaktır.  tooget daha iyi performans, yürütücüler hello sayısını değiştirerek hello varsayılanlarını geçersiz kılabilirsiniz.  

**2. adım: Bellek içi Yürütücü ayarlama** – hello ilk şey tooset hello Yürütücü-bellektir.  Merhaba bellek hello işi devam eden toorun olduğunuz bağımlı olur.  Yürütücü başına daha az bellek ayırarak eşzamanlılık artırabilir.  İşinizi çalıştırdığınızda yetersiz bellek özel durumları görürseniz, bu parametrenin hello değerini artırmanız gerekir.  Bir tooget daha fazla bellek daha yüksek miktarlarda bellek sahip bir küme kullanarak veya kümenizin hello boyutunu artırmayı alternatiftir.  Daha fazla bellek daha fazla eşzamanlılık anlamı kullanıldığında, daha fazla yürütücüler toobe olanak sağlar.

**3. adım: Ayarlama Yürütücü çekirdek** – isteğe bağlı olarak karmaşık işlemleri olmayan g/ç yoğun iş yükleri için çok sayıda Yürütücü çekirdek tooincrease hello Yürütücü başına Paralel Görevler sayısı ile iyi toostart değil.  Yürütücü çekirdek too4 ayarı iyi bir başlangıç noktasıdır.   

    executor-cores = 4
Yürütücü çekirdek hello sayısını artırmayı farklı Yürütücü çekirdeğiyle deneyebilirsiniz şekilde daha fazla paralellik verecektir.  Daha karmaşık işlemleri sahip işleri hello Yürütücü başına çekirdek sayısı azaltmanız gerekir.  Yürütücü çekirdek ise 4'ten yüksek ayarlanmış sonra atık toplama verimsiz hale ve performansı düşebilir.

**Adım 4: küme YARN bellek miktarını belirlemek** – bu bilgiler Ambari içinde kullanılabilir.  TooYARN gidin ve hello yapılandırmalar sekmesini görüntüleyin.  Merhaba YARN bellek Bu pencerede görüntülenir.  
Not: hello penceresinde olmakla birlikte, aynı zamanda hello varsayılan YARN kapsayıcı boyutu görebilirsiniz.  Merhaba YARN kapsayıcı boyutu olan hello Yürütücü parametresi başına bellek ile aynı.

    Total YARN memory = nodes * YARN memory per node
**5. adım: num yürütücüler Hesapla**

**Bellek kısıtlama hesaplamak** -hello num yürütücüler parametre bellek veya CPU göre kısıtlı.  Merhaba bellek kısıtlama hello uygulamanız için kullanılabilir YARN bellek miktarı tarafından belirlenir.  Toplam YARN bellek alın ve yürütücü bellekle bölün.  Merhaba kısıtlaması biz uygulamaları hello sayısına göre Böl şekilde uygulamaları hello sayısı için XML'deki ölçeklendirilmiş toobe gerekir.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**CPU kısıtlaması hesaplamak** -hello CPU kısıtlaması bölü hello Yürütücü başına çekirdek sayısı toplam sanal çekirdek hello olarak hesaplanır.  Her fiziksel çekirdek için 2 sanal çekirdek vardır.  Benzer toohello bellek kısıtlama, uygulamaları hello sayısına göre Böl sahibiz.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Ayarlama num yürütücüler** – hello num yürütücüler parametre belirlenir gerçekleştirerek hello hello bellek kısıtlaması ile Merhaba CPU en düşük. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
Daha yüksek bir sayı yürütücüler sayısı ayarlanması, performans mutlaka artırmaz.  Daha fazla yürütücüler ekleme ekleyeceksiniz dikkate almanız gereken potansiyel olarak performansı düşürebilir her ek Yürütücü için fazladan genel gider.  NUM yürütücüler tarafından hello küme kaynağı ilişkisindeki.    

## <a name="example-calculation"></a>Örnek hesaplama

Şu anda çalışan 2 uygulamaları hello dahil olmak üzere bir bulacağınızı toorun 8 D4v2 düğümden oluşan bir küme sahip varsayalım.  

**1. adım: kümenizde çalışan kaç uygulamalar belirlemek** – 2 olduğunu bildiğiniz bir toorun bulacağınızı hello dahil olmak üzere kümenizde uygulamaları.  

**2. adım: Bellek içi Yürütücü ayarlama** – Bu örnekte, 6 GB bellek Yürütücü g/ç yoğun iş için yeterli olacaktır olan belirleriz.  

    executor-memory = 6GB
**3. adım: Ayarlama Yürütücü çekirdek** – bir g/ç yoğun iş olacağından, biz her Yürütücü too4 çekirdeği hello sayısını ayarlayabilirsiniz.  4 çöp toplama sorunlara neden olabilirsiniz daha Yürütücü toolarger başına çekirdek ayarlama.  

    executor-cores = 4
**Adım 4: küme YARN bellek miktarını belirlemek** – biz her D4v2 25 GB YARN bellek olduğunu tooAmbari toofind dışarı gidin.  8 düğüm olduğundan, hello bellek YARN 8 ile çarpılır.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**5. adım: num yürütücüler hesaplamak** – hello num yürütücüler parametre belirlenir gerçekleştirerek hello en az hello bellek kısıtlaması ile Merhaba tarafından bölünmüş hello CPU sayısı Spark üzerinde çalıştırılan uygulamalar.    

**Bellek kısıtlama hesaplamak** – hello bellek kısıtlama Yürütücü başına hello bellek bölü hello toplam YARN bellek olarak hesaplanır.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**CPU kısıtlaması hesaplamak** -hello CPU kısıtlaması bölü hello Yürütücü başına çekirdek sayısı toplam yarn çekirdek hello olarak hesaplanır.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Set num-yürütücüler**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

