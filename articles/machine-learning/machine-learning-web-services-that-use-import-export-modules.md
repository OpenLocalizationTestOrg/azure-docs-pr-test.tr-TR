---
title: "Azure Machine Learning web Hizmetleri içinde aaaUsing içeri/dışarı aktarma veri | Microsoft Docs"
description: "Nasıl toouse veri içeri aktarma ve dışarı aktarma veri modülleri toosend hello ve bir web hizmetinden veri alma öğrenin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>Veri Alma ve Veri Gönderme modüllerini kullanan Azure ML web hizmetleri dağıtma

Tahmine dayalı bir deneme oluştururken, bir web hizmeti giriş ve çıkış genellikle ekleyin. Merhaba deneme dağıttığınızda, Tüketicileri gönderebilir ve hello girişleri ve çıkışları aracılığıyla hello web hizmetinden veri alma. Bazı uygulamalar için bir tüketicinin verileri veri akışlarından kullanılabilir veya zaten Azure Blob Depolama alanı gibi bir dış veri kaynağında bulunan. Bu durumlarda, bunlar web hizmeti girişleri ve çıkışları kullanarak veri okumak veya yazmak zorunda değilsiniz. Bunlar, bunun yerine, hello toplu yürütme hizmeti (BES) tooread veri hello veri kaynağından veri içeri aktarma modülü kullanılarak kullanabilir ve sonuçları bir dışarı aktarma veri modülünü kullanarak tooa farklı veri konumu Puanlama hello yazma.

Merhaba veri içeri aktarma ve dışarı aktarma veri modüller, gelen okuyabilir ve konumlar gibi Web URL HTTP, Hive sorgusu, bir Azure SQL veritabanı, Azure Table storage, Azure Blob Depolama, veri akışı aracılığıyla sağlayan toovarious verileri veya bir şirket içi SQL veritabanına yazma.

Bu konuda hello kullanır "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi" örnek ve hello veri kümesi zaten yüklü censusdata adlı bir Azure SQL tablosuna varsayar.

## <a name="create-hello-training-experiment"></a>Merhaba eğitim denemenizi oluşturma
Merhaba açtığınızda "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi" kullandığı hello örnek yetişkin Census gelir ikili sınıflandırma dataset örnek. Ve hello tuvale hello denemesinde görüntü aşağıdaki benzer toohello arar:

![Merhaba deneme'nin ilk yapılandırması.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

hello Azure SQL tablosuna tooread hello veri:

1. Merhaba dataset modülü silin.
2. Merhaba bileşenleri arama kutusunda, içeri aktarma yazın.
3. Merhaba sonuçları listesinden bir *veri içeri aktarma* modülü toohello deneme tuvaline.
4. Merhaba çıkışına bağlayın *veri içeri aktarma* hello modülü hello girişi *Clean Missing Data* modülü.
5. Özellikler bölmesinde seçin **Azure SQL veritabanı** hello içinde **veri kaynağı** açılır.
6. Merhaba, **veritabanı sunucusu adı**, **veritabanı adı**, **kullanıcı adı**, ve **parola** alanlar için uygun bilgileri hello girin Veritabanınızı.
7. Merhaba veritabanı sorgu alanına sorgu aşağıdaki hello girin.
   
     [yaş] seçin
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     dbo.censusdata;
8. Merhaba deneme tuvalinin Hello altındaki tıklatın **çalıştırmak**.

## <a name="create-hello-predictive-experiment"></a>Merhaba tahmini deneme oluşturma
Sonraki hello Tahmine dayalı denemeye, web hizmetini dağıtma ayarlayın.

1. Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı** seçip **Tahmine dayalı Web hizmeti [önerilen]**.
2. Merhaba kaldırmak *Web hizmeti girişi* ve *Web hizmeti çıkış modülleri* hello Tahmine dayalı denemeye gelen. 
3. Dışarı aktarma Hello bileşenleri arama kutusuna yazın.
4. Merhaba sonuçları listesinden bir *verileri dışa aktar* modülü toohello deneme tuvaline.
5. Merhaba çıkışına bağlayın *Score Model* hello modülü hello girişi *verileri dışa aktar* modülü. 
6. Özellikler bölmesinde seçin **Azure SQL veritabanı** hello veri hedef açılır içinde.
7. Merhaba, **veritabanı sunucusu adı**, **veritabanı adı**, **Server kullanıcı hesabı adı**, ve **Server kullanıcı hesabı parolasını** alanları girin Merhaba veritabanınız için uygun bilgileri.
8. Merhaba, **virgülle ayrılmış kaydedilmiş sütunları toobe listesi** alan, skoru etiketleri yazın.
9. Merhaba, **veri tablo adı alanı**, dbo yazın. ScoredLabels. Merhaba tablo mevcut değilse hello deneme çalıştırdığınızda veya hello web hizmeti adlı oluşturulur.
10. Merhaba, **virgülle ayrılmış datatable sütunlar listesi** alan, ScoredLabels yazın.

Bir uygulama çağrıları son web hizmeti hello yazdığınızda, çalışma zamanında farklı bir giriş sorgu veya hedef tablo toospecify isteyebilirsiniz. tooconfigure bu girişleri ve çıkışları, kullanın hello Web hizmeti parametreleri özellik tooset hello *veri içeri aktarma* Modülü *veri kaynağı* özelliği ve hello *verileri dışa aktar* modu veri hedef özelliği.  Merhaba Web hizmeti parametreleri hakkında daha fazla bilgi için bkz: [AzureML Web hizmeti parametreleri girişi](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) hello Cortana Intelligence ve makine öğrenme blogu.

Merhaba alma sorgu ve hello hedef tablo için tooconfigure hello Web hizmeti parametreleri:

1. Hello için hello Özellikler bölmesinde *veri içeri aktarma* modülü, hello hello simgesini tıklatın top hello sağındaki **veritabanı sorgusu** alan ve seçin **web hizmeti parametresi ayarlamak**.
2. Hello için hello Özellikler bölmesinde *verileri dışa aktar* modülü, hello hello simgesini tıklatın top hello sağındaki **veri tablo adı** alan ve seçin **web hizmeti parametresi ayarlanmış**.
3. Hello hello sonundaki *verileri dışa aktar* hello de modülü Özellikler bölmesinde **Web hizmeti parametreleri** bölümünde veritabanı sorgusu tıklayın ve sorguyu yeniden adlandırın.
4. Tıklatın **veri tablo adı** ve yeniden adlandırmak **tablo**.

İşiniz bittiğinde, denemenizi benzer toohello görüntü aşağıdaki gibi görünmelidir:

![Deneme son görünümünü.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

Artık hello deneme bir web hizmeti olarak dağıtabilirsiniz.

## <a name="deploy-hello-web-service"></a>Merhaba web hizmetini dağıtma
Klasik veya yeni bir web hizmeti tooeither dağıtabilirsiniz.

### <a name="deploy-a-classic-web-service"></a>Klasik Web hizmetini dağıtma
Klasik Web hizmeti olarak toodeploy ve bir uygulama tooconsume oluşturun bunu:

1. Merhaba deneme tuvalinin Hello altındaki Çalıştır'ı tıklatın.
2. Çalıştırma hello tamamlandığında tıklayın **Web hizmeti Dağıt** seçip **Web hizmeti Dağıt [Klasik]**.
3. Merhaba web hizmeti panosunda API anahtarınızı bulun. Kopyalayın ve daha sonra toouse kaydedin.
4. Merhaba, **varsayılan uç nokta** tablo, hello tıklatın **toplu iş yürütme** bağlantı tooopen hello API Yardım sayfası.
5. Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.
6. Merhaba Hello API Yardım sayfası, bulma **örnek kod** hello sayfanın hello kısmına.
7. Kopyalama ve hello C# örnek kodu, Program.cs dosyasına yapıştırın ve tüm başvuruları toohello blob depolama kaldırın.
8. Merhaba Hello değerini güncelleştirmek *apikey ile yapılan* daha önce kaydedilmiş hello API anahtarıyla değişken.
9. Merhaba istek bildirim ve güncelleştirme hello parametrelerinin değerleri Web hizmeti toohello geçirilen bulun *veri içeri aktarma* ve *verileri dışa aktar* modüller. Bu durumda, hello özgün sorgu kullanır, ancak yeni bir tablo adı tanımlayın.
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. Merhaba uygulamayı çalıştırın. 

Çalıştırma hello tamamlama sonrasında yeni bir tablo sonuçları Puanlama hello içeren toohello veritabanına eklenir.

### <a name="deploy-a-new-web-service"></a>Yeni bir Web hizmetini dağıtma

> [!NOTE] 
> toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir. Daha fazla bilgi için bkz: [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md). 

Yeni bir Web hizmeti olarak toodeploy ve bir uygulama tooconsume oluşturun bunu:

1. Merhaba deneme tuvalinin Hello altındaki tıklatın **çalıştırmak**.
2. Çalıştırma hello tamamlandığında tıklayın **Web hizmeti Dağıt** seçip **Web hizmeti dağıtma [Yeni]**.
3. Merhaba dağıtmak deneme sayfasında, web hizmetiniz için bir ad girin ve bir fiyatlandırma planı seçin ve ardından **dağıtma**.
4. Merhaba üzerinde **Hızlı Başlangıç** sayfasında, **Tüket**.
5. Merhaba, **örnek kod** 'yi tıklatın **toplu**.
6. Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.
7. Merhaba C# örnek kodu kopyalayıp Program.cs dosyanıza yapıştırın.
8. Merhaba Hello değerini güncelleştirmek *apikey ile yapılan* hello ile değişken **birincil anahtar** hello bulunan **temel tüketim bilgileri** bölümü.
9. Merhaba bulun *scoreRequest* bildirim ve güncelleştirme hello parametrelerinin değerleri Web hizmeti toohello geçirilen *veri içeri aktarma* ve *verileri dışa aktar* modüller. Bu durumda, hello özgün sorgu kullanır, ancak yeni bir tablo adı tanımlayın.
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. Merhaba uygulamayı çalıştırın. 

