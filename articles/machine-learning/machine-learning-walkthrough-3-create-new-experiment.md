---
title: "3. adım: yeni bir Machine Learning deneme oluşturma | Microsoft Docs"
description: "Adım 3 / hello geliştirmek Tahmine dayalı bir çözüm izlenecek yol: Azure Machine Learning Studio'da yeni bir eğitim deneme oluşturun."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a>Kılavuz Adımı 3: Yeni bir Azure Machine Learning denemesi oluşturma
Hello kılavuzun hello üçüncü adım budur [Azure Machine learning'de Tahmine dayalı analiz çözümü geliştirme](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Bir Machine Learning çalışma alanı oluşturma](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Mevcut verileri yükleme](machine-learning-walkthrough-2-upload-data.md)
3. **Yeni bir deneme oluşturma**
4. [Eğitmek ve hello modelleri değerlendir](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Merhaba Web hizmetini dağıtma](machine-learning-walkthrough-5-publish-web-service.md)
6. [Merhaba Web hizmetine erişim](machine-learning-walkthrough-6-access-web-service.md)

- - -
Bu kılavuzda Hello sonraki adım toocreate biz karşıya hello veri kümesi kullanan bir Machine Learning Studio'da bir denemeyi olacaktır.  

1. Studio'da sırasıyla **+ yeni** hello pencerenin hello altındaki.
2. Seçin **deneme**ve ardından "Boş deneme" seçin. 

    ![Yeni bir deneme oluşturma][0]

2. Select hello varsayılan hello tuvale hello başındaki ad denemeler ve toosomething anlamlı yeniden adlandırın.

    ![Denemeyi yeniden adlandırma][5]
   
   > [!TIP]
   > İyi bir uygulama toofill konusu **Özet** ve **açıklama** hello hello denemesinde için **özellikleri** bölmesi. Böylece daha sonra görünüyor herkes amaçlar ve yöntemler anlayabileceği fırsat toodocument hello deneme hello bu özellikleri sağlar.
   > 
   > ![Deneme özellikleri][6]
   > 
3. İçinde Hello modül paleti toohello sol tarafındaki hello deneme tuvalinin genişletin **kaydedilen veri kümeleri**.
4. Bul hello veri kümesi altında oluşturduğunuz **My veri kümeleri** hello tuvale sürükleyin. Hello hello adı girerek hello dataset bulabilirsiniz **arama** kutusunun hello palet üstünde.  

    ![Merhaba dataset toohello deneme ekleme][7]

## <a name="prepare-hello-data"></a>Merhaba verileri hazırlama
Görüntüleyebileceğiniz hello veri ilk 100 satırı ve bazı istatistiksel bilgileri hello tam veri kümesi için hello: hello veri kümesi (Merhaba küçük bir daire hello altındaki) hello çıkış bağlantı noktasına tıklayın ve **Görselleştir**.  

Merhaba veri dosyası sütun başlıkları ile eşleşmedi geldiğinden Studio genel başlıkları sağlamıştır (Col1, Col2, *vb.*). Temel toocreating bir model iyi başlıkları değil, ancak bunlar hello verilerle daha kolay toowork hello denemesinde olun. Ayrıca, biz sonunda bu model bir web hizmeti yayımladığınızda, hello başlıkları hello sütunları toohello kullanıcı hello hizmetinin tanımlamaya yardımcı olur.  

Sütun başlıkları hello kullanarak ekleyebiliriz [Düzenle meta veri] [ edit-metadata] modülü.
Merhaba kullandığınız [Düzenle meta veri] [ edit-metadata] modülü toochange meta veri kümesiyle ilişkilendirilmiş. Bu durumda, daha fazla kolay adlar tooprovide sütun başlıkları kullanırız. 

toouse [Düzenle meta veri][edit-metadata], hangi sütunların toomodify (Bu durumda, bunların tümünün.) ilk belirtin Ardından, bu sütunları (sütun başlıklarını değiştirme bu durumda,.) üzerinde gerçekleştirilen hello eylem toobe belirtin

1. Merhaba "meta" Merhaba modül paletindeki yazın **arama** kutusu. Merhaba [Düzenle meta veri] [ edit-metadata] hello modül listesinde görünür.

2. Merhaba sürükleyip [Düzenle meta veri] [ edit-metadata] hello modülü tuvale ve daha önce eklediğimiz hello dataset bırakın.

3. Merhaba dataset toohello bağlanmak [Düzenle meta veri][edit-metadata]: hello veri kümesi (Merhaba küçük bir daire hello dataset hello sonundaki) hello çıkış bağlantı noktasına tıklayın, toohello giriş bağlantı noktası sürükleyin [meta verileri düzenleme ] [ edit-metadata] (Merhaba küçük daire hello modülü hello üstündeki), hello fare düğmesini serbest bırakın. ya da hello tuval üzerinde hareket ettirin olsa bile hello veri kümesi ve modül bağlı kalır.
   
   Merhaba deneme bu gibi görünmelidir:  
   
   ![Düzen meta verileri ekleme][1]
   
   Merhaba kırmızı bir ünlem işareti Biz bu modül için hello özellikleri henüz ayarlamadıysanız olduğunu gösterir. Biz bu sonraki gerçekleştirirsiniz.
   
   > [!TIP]
   > Bir yorum tooa modülü bağlantısındaki hello modülü ve metin girme tarafından ekleyebilirsiniz. Bu, bir bakışta görmenize yardımcı hangi hello modülün denemenizde yapıyor. Bu durumda, hello çift [Düzenle meta veri] [ edit-metadata] modülü ve türü hello Açıklama "Ekle sütun başlıkları". Başka bir yerde hello tuvale tooclose hello metin kutusuna tıklayın. toodisplay Merhaba yorum, hello modül hello aşağı oku tıklatın.
   > 
   > ![Meta veriler modülü açıklama eklendi Düzenle][8]
   > 
4. Seçin [Düzenle meta veri][edit-metadata]ve hello **özellikleri** bölmesinde toohello hello tuvale sağına tıklayın **başlatma Sütun seçiciyi**.

5. Merhaba, **sütunları seçin** iletişim, tüm satırlarda hello select **kullanılabilir sütunlar** tıklatıp > toomove bunları çok**seçili sütun**.
   Merhaba iletişim aşağıdaki gibi görünmelidir:

   ![Seçili tüm sütunlarla Sütun Seçici][2]

6. Merhaba tıklatın **Tamam** onay işareti.

7. Merhaba edilene **özellikleri** bölmesinde, hello arayın **yeni sütun adları** parametresi. Bu alanda virgülle ve sütun sırasını ayrılmış hello kümesindeki hello 21 sütunların adlarının bir listesini girin. Merhaba dataset belgelerindeki hello UCI Web sitesinde hello sütun adları elde edebilirsiniz veya kolaylık sağlamak için kopyalama ve yapıştırma listesi aşağıdaki hello:  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   Merhaba Özellikler bölmesinde şöyle görünür:
   
   ![Özellikleri düzenleme meta veriler için][3]

> [!TIP]
> Tooverify hello sütun başlıkları istiyorsanız hello denemeyi çalıştırın (tıklatın **çalıştırmak** hello deneme tuvalinin altında). Çalışan bittiğinde (yeşil bir onay işareti görünür [Düzenle meta veri][edit-metadata]), hello hello çıkış bağlantı noktasına tıklayın [Düzenle meta veri] [ edit-metadata] Modül ' nı seçip **Görselleştir**. Herhangi bir modül hello çıktısını hello görüntüleyebilirsiniz aynı şekilde tooview hello ilerlemesini hello deneme hello verilerine.
> 
> 

## <a name="create-training-and-test-datasets"></a>Eğitim oluşturmak ve veri kümelerini test etme
Bazı veri tootrain hello modeli ve bazı tootest ihtiyacımız onu.
Merhaba sonraki adımında hello deneme biz hello dataset iki ayrı kümelerine bölünmüş şekilde: modelimizi ve test için bir tane eğitim için bir tane.

toodo bunu hello kullanırız [bölünmüş veri] [ split] modülü.  

1. Hello bulur [bölünmüş veri] [ split] modül hello tuvale sürükleyin ve toohello bağlayın [Düzenle meta veri] [ edit-metadata] modülü.

2. Varsayılan olarak, hello bölünmüş 0,5 ve hello orandır **Randomized bölünmüş** parametrenin ayarlanmış. Bu rastgele yarı hello veri çıkışı hello bir bağlantı noktası üzerinden olduğu anlamına gelir [bölünmüş veri] [ split] modülü ve yarı ile Merhaba diğer. Siz bu parametreleri ayarlamak yanı sıra hello **rastgele doldurma** parametresi, eğitim ve test verileri arasında bölme toochange hello. Bu örnekte, biz bunları olarak bırakın-değil.
   
   > [!TIP]
   > Merhaba özelliği **hello satırlar için kesir değerini ilk çıkış veri kümesi** çıkışı hello üzerinden hello verilerin ne kadar olacağını belirler *sol* çıkış bağlantı noktası. Örneğin, hello oranı too0.7 ayarlarsanız, % 70'hello veri çıkışı hello doğru bağlantı noktası üzerinden sol bağlantı noktası ve % 30 hello üzerinden olabilir.  
   > 
   > 

3. Merhaba çift [bölünmüş veri] [ split] modülü ve hello açıklama girin, "eğitim ve test veri Böl % 50". 

Merhaba hello çıkışları kullanırız [bölünmüş veri] [ split] ancak biz gibi çalışır, ancak şimdi toouse seçin hello eğitim verisi olarak sol çıkış ve sağa hello modülü çıkış olarak test verileri.  

Hello belirtildiği gibi [önceki adımı](machine-learning-walkthrough-2-upload-data.md), düşük olarak yüksek kredi riski misclassifying hello maliyetidir beş kez yüksek olarak düşük kredi riski misclassifying hello maliyeti daha yüksek. Bu tooaccount, bu maliyet işlevi yansıtır yeni bir veri kümesi oluşturur. Her düşük riskli örnek çoğaltılmaz sırada hello yeni kümesindeki her yüksek riskli örnek beş kez çoğaltılır.   

Bu çoğaltma yapabiliriz R kodu kullanarak:  

1. Bulma ve hello sürükleyin [R betiği yürütün] [ execute-r-script] hello deneme tuvale modülü. 

2. Merhaba çıkış bağlantı noktasına sol hello bağlanmak [bölünmüş veri] [ split] modülü toohello Merhaba ilk bağlantı noktası ("Dataset1") giriş [R betiği yürütün] [ execute-r-script] Modül.

3. Merhaba çift [R betiği yürütün] [ execute-r-script] modülü ve hello yorum girin "maliyet ayarlaması Ayarla".

4. Merhaba, **özellikleri** bölmesinde, delete hello varsayılan hello metinde **R betiği** parametre ve bu komut dosyasını girin:
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![R betiği hello R betiği yürütün Modülü][9]

Bu aynı çoğaltma işlemi için her çıktı Merhaba, toodo ihtiyacımız [bölünmüş veri] [ split] sahip eğitim ve test verileri bu hello hello şekilde aynı modülü maliyet ayarlama. Merhaba çoğaltarak budur en kolay yolu toodo hello [R betiği yürütün] [ execute-r-script] modülü biz yalnızca yapılan ve toohello bağlanan diğer çıkış başlangıç bağlantı noktası [bölünmüş veri] [ split] modülü.

1. Sağ hello [R betiği yürütün] [ execute-r-script] modülü ve select **kopya**.

2. Merhaba deneme tuvalinin sağ tıklatıp **Yapıştır**.

3. Merhaba yeni modül konumu sürükleyin ve hello hello sağ çıkış bağlantı noktasına bağlanmak [bölünmüş veri] [ split] modülü toohello ilk giriş bağlantı noktası bu yeni [R betiği yürütün] [ execute-r-script] modülü. 

4. Merhaba tuvale Hello altındaki tıklatın **çalıştırmak**. 

> [!TIP]
> Merhaba R betiği yürütün modülü Hello kopyasını hello aynı hello özgün modülü olarak komut dosyası içerir. Merhaba tuvalde bir modül kopyalayıp, hello kopyalama hello özgün tüm hello özelliklerini korur.  
> 
> 

Bizim denemeyi şimdi şuna benzer:

![Bölünmüş modülü ve R betiklerini ekleme][4]

Denemelerinizi içinde R betiklerini kullanma hakkında daha fazla bilgi için bkz: [denemenizi R ile genişletme](machine-learning-extend-your-experiment-with-r.md).

**Sonraki: [eğitimi ve hello modelleri değerlendir](machine-learning-walkthrough-4-train-and-evaluate-models.md)**

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
