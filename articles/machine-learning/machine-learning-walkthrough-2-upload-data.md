---
title: "2. adım: Verileri bir Machine Learning deneme yükleme | Microsoft Docs"
description: "Adım 2 / hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: karşıya yükleme Azure Machine Learning Studio'ya genel verilere depolanır."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>Kılavuz Adımı 2: Mevcut verileri bir Azure Machine Learning denemesine yükleme
Merhaba kılavuzun hello ikinci adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Bir Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **Mevcut verileri yükleme**
3. [Yeni bir deneme oluşturma](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eğitmek ve hello modelleri değerlendir](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Merhaba Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)
6. [Merhaba Web hizmetine erişim](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop kredi riski için Tahmine dayalı bir model, biz tootrain kullanın ve böylelikle hello modeli test veri gerekir. Bu kılavuzda hello UC Irvine Machine Learning depodan hello "UCI Statlog (Almanca kredi veri) veri kümesi" kullanacağız. Burada bulabilirsiniz:  
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ML/DataSets/Statlog+(German+Credit+Data)</a>

Adlı hello dosya kullanacağız **german.data**. Bu dosya tooyour yerel sabit diske yükleyin.  

Merhaba **german.data** dataset kredi için son 1000 başvuran 20 değişkenlerin satırları içerir. Bu 20 değişkenleri hello veri kümesi'nin özellikler kümesini temsil eden (Merhaba *özelliği vektör*), her kredi başvuran için tanımlayıcı özellikleri sağlar. Her satırda ek bir sütun düşük kredi riski ve 300 yüksek riskli olarak tanımlanan 700 başvuran ile Merhaba Başvuranın hesaplanan kredi riski temsil eder.

Merhaba UCI hello özelliği vektör bu veriler için başlangıç özniteliklerini açıklamasını sağlar. Bu, finansal bilgileri, kredi geçmişi, çalışma durumu ve kişisel bilgileri içerir. Her başvuran için ikili bir derecelendirme belirli bir düşük olup olmadığını gösteren veya yüksek olmuştur kredi riski. 

Bu veri tootrain bir Tahmine dayalı bir analiz modeli kullanacağız. Biz bittiğinde modelimizi mümkün tooaccept yeni bir tek bir özellik vektörünü olması ve çözemiyorsa düşük veya yüksek kredi riski olup olmadığını tahmin etmek.  

Burada, ilginç geçiş verilmiştir. Merhaba UCI Web sitesi belirtilenlerden hello veri kümesine açıklaması biz bir kişinin kredi riski misclassify varsa ne maliyetleri hello.
Bir yüksek kredi riski gerçekten düşük kredi riski yapılandırabilecek için Hello modeli tahmin, hello modeli bir misclassification yaptı.
Ancak hello ters misclassification beş kez daha pahalı toohello finansal kuruluştan: hello modeli düşük kredi riski gerçekte bir yüksek kredi riski yapılandırabilecek için tahmin durumunda.

Bu türdeki misclassification Hello maliyetini beş kez hello başka bir yolla misclassifying daha yüksek olmasını sağlamak, tootrain modelimizi istiyoruz.
Bir basit yol toodo bu bizim deneme hello modelinde eğitim olduğunda yüksek kredi riski birisiyle temsil eden (beş kez) girişler çoğaltarak. Gerçekte yüksek riskli olduğunuzda hello modeli birisi düşük kredi riski olarak misclassifies, daha sonra hello model, aynı misclassification beş kez kez için her yinelenen yapar. Bu, bu hata hello eğitim sonuçlarında hello maliyetini artırır.


## <a name="convert-hello-dataset-format"></a>Merhaba dataset biçimine dönüştürün
Merhaba özgün veri kümesi boş ayrılmış bir biçim kullanır. Virgül ile alanları değiştirerek hello dataset biz dönüştürme machine Learning Studio'da bir virgülle ayrılmış değer (CSV) dosyası ile daha iyi çalışır.  

Bu veriler birçok yolu tooconvert vardır. Tek yönlü hello aşağıdaki Windows PowerShell komutunu kullanmaktır:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

Merhaba UNIX azaltılabilir komutunu kullanarak başka bir yöntemdir:  

    sed 's/ /,/g' german.data > german.csv  

Her iki durumda da adlı bir dosya hello verileri virgülle ayrılmış bir sürümünü oluşturduk **german.csv** , bizim deneme kullanırız.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Merhaba dataset tooMachine Learning Studio karşıya yükle
Dönüştürülen tooCSV biçiminde Hello verileri silindikten sonra tooupload ihtiyacımız Machine Learning Studio içine. 

1. Açık hello Machine Learning Studio giriş sayfası ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Merhaba menüsünü ![menü][1] hello sol üst köşesinde hello penceresi tıklatın **Azure Machine Learning**seçin **Studio**ve oturum açın.

3. Tıklatın **+ yeni** hello pencerenin hello altındaki.

4. Seçin **DATASET**.

5. Seçin **yerel DOSYADAN**.

    ![Yerel bir dosyadan bir veri kümesi ekleyin][2]

6. Merhaba, **yeni bir veri kümesi karşıya** iletişim kutusunda, tıklatın **Gözat** ve hello bulur **german.csv** , oluşturduğunuz dosya.

7. Merhaba veri kümesi için bir ad girin. Bu kılavuzda "UCI Almanca kredi kartı verileri" çağrısı.

8. Veri türü için **üst bilgi içeren genel CSV dosyası (. nh.csv)**.

9. İsterseniz bir açıklama ekleyin.

10. Merhaba tıklatın **Tamam** onay işareti.  

    ![Merhaba dataset karşıya yükle][3]

Bir deneme kullandığımız bir veri kümesi modüle hello veri yükler.

Merhaba tıklayarak tooStudio yüklediğiniz veri kümeleri yönetebilir **veri KÜMELERİ** sekmesini toohello hello Studio penceresinin sol.

![Veri kümelerini yönetme][4]

Bir deneme diğer veri türleri alma hakkında daha fazla bilgi için bkz: [eğitim verilerinizi Azure Machine Learning Studio'ya içeri](machine-learning-data-science-import-data.md).

**Sonraki: [yeni bir deneme oluşturma](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
