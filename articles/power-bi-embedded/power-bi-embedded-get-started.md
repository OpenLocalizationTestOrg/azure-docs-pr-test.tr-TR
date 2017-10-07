---
title: "Microsoft Power BI Embedded ile çalışmaya aaaGet"
description: "Power BI Embedded, iş zekası uygulamanıza etkileşimli Power BI raporları ekler"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Microsoft Power BI Embedded kullanmaya başlama

**Power BI Embedded** etkileşimli Power BI raporları kendi uygulamalarınızı bu etkinleştirir uygulama geliştiricilerin tooadd bir Azure hizmetidir. **Power BI Embedded** yeniden tasarlanması gerek veya hello şekilde kullanıcıları için değiştirme olmadan mevcut uygulamalarla works oturum açın.

Kaynaklar için **Microsoft Power BI Embedded** hello sağlanan [Azure ARM API'leri](https://msdn.microsoft.com/library/mt712306.aspx). Bu durumda, sağlamanız hello kaynaktır bir **Power BI çalışma alanı koleksiyonu**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Çalışma alanı koleksiyonu oluşturma

A **çalışma alanı koleksiyonu** hello üst düzey Azure kaynağı ve uygulamanızda katıştırılmış hello içerik için bir kapsayıcıdır. **Çalışma Alanı Koleksiyonu** iki şekilde oluşturulabilir:

* Hello Azure Portal kullanarak el ile
* Hello Azure Resource Manager(ARM) API'lerini program aracılığıyla kullanma

Şimdi hello adımları toobuild yol bir **çalışma alanı koleksiyonu** hello Azure Portal kullanarak.

1. **Azure Portal**’ı açın ve oturum açın: [http://portal.azure.com](http://portal.azure.com)
2. Tıklatın **+ yeni** hello üst panelde.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. **Veri + Analiz** altında **Power BI Embedded**’a tıklayın.
4. Merhaba üzerinde **çalışma alanı koleksiyonu dikey**, hello gerekli bilgileri girin. **Fiyatlandırma** için bkz. [Power BI Embedded fiyatlandırması](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. **Oluştur**'a tıklayın.

Merhaba **çalışma alanı koleksiyonu** birkaç dakika sonra tooprovision olur. Tamamlandığında, toohello gidersiniz **çalışma alanı koleksiyonu dikey**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Merhaba **oluşturma dikey penceresi** toocall hello çalışma alanları oluşturma ve içerik toothem dağıtan API'leri ihtiyacınız hello bilgileri içerir.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Power BI API’si erişim anahtarlarını görüntüleme

Merhaba gerekli bilgileri toocall parçalarını hello Power BI API'lerini en önemli biri hello **erişim tuşları**. Kullanılan toogenerate hello bunlar **uygulama belirteçleri** kullanılan tooauthenticate olan API isteklerinizin. tooview, **erişim tuşları**, tıklatın **erişim tuşları** hello üzerinde **ayarlar dikey**. **Uygulama belirteçleri** hakkında daha fazla bilgi için bkz. [Power BI Embedded ile kimlik doğrulama ve yetkilendirme](power-bi-embedded-app-token-flow.md).

   ![](media/power-bi-embedded-get-started/access-keys.png)

İki anahtarınız olduğunu fark edeceksiniz.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Bu anahtarları kopyalayın ve uygulamanızda güvenli bir şekilde depolayın. Bir parola gibi erişim tooall hello içeriğinde sağlarız olduğundan, bu anahtarlar kabul olduğunu çok önemlidir, **çalışma alanı koleksiyonu**.

İki anahtar listelenmekle birlikte, belirli bir seferde yalnızca bir anahtar gerekir. Merhaba ikinci anahtar anahtarları erişim toohello hizmeti kesintiye uğratmadan düzenli aralıklarla yeniden oluşturabilmeniz için sağlanmıştır.

Artık uygulamanız için bir Power BI örneğine ve **Erişim Anahtarları**’na sahip olduğunuza göre, kendi uygulamanıza bir rapor aktarabilirsiniz. Önce nasıl tooimport raporu, hello sonraki bölümde bir uygulamaya oluşturma Power BI veri kümelerini ve raporları tooembed açıklar öğrenin.

## <a name="working-with-workspaces"></a>Çalışma alanları ile çalışma

Çalışma alanı koleksiyonu oluşturduktan sonra raporları ve veri kümelerini barındırmak bir çalışma alanı toocreate gerekir. toocreate bir çalışma alanı, toouse hello gerekir [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>Power BI Desktop kullanarak uygulamaya Power BI veri kümelerini ve raporları tooembed oluşturma

Artık, uygulamanız için Power BI örneğini oluşturduğunuz ve sahip **erişim tuşları**, toocreate hello Power BI veri kümeleri ve raporları tooembed istediğiniz gerekir. Veri kümeleri ve raporlar **Power BI Desktop** kullanarak oluşturulabilir. [Power BI Desktop’u ücretsiz olarak](https://go.microsoft.com/fwlink/?LinkId=521662) indirebilirsiniz. Veya, tooquickly Başlarken, hello indirebilirsiniz [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> toolearn nasıl hakkında daha fazla toouse **Power BI Desktop**, bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

İle **Power BI Desktop**, hello verilerin bir kopyasını alarak tooyour veri kaynağına bağlanmak **Power BI Desktop** veya toohello verileri doğrudan bağlanma kullanarak kaynak **DirectQuery**.

Kullanarak arasındaki farklar hello işte **alma** ve **DirectQuery**.

| İçeri Aktarma | DirectQuery |
| --- | --- |
| Tablolar, sütunlar *ve veriler* **Power BI Desktop**’a aktarılır veya kopyalanır. Görselleştirmeleri ile çalışırken **Power BI Desktop** hello verilerin bir kopyasını sorgular. toosee bu oluştu toohello temel alınan veri değişiklikleri, yenileme veya alma, bir tam, güncel veri kümesini yeniden. |Yalnızca *tablolar ve sütunlar* ve **Power BI Desktop**’a aktarılır veya kopyalanır. Görselleştirmeleri ile çalışırken **Power BI Desktop** sorguları hello her zaman görüntülemekte olduğunuz geçerli verileri anlamına gelir temel alınan veri kaynağı. |

Bağlantı tooa veri kaynağı hakkında daha fazla bilgi için bkz: [Bağlan tooa veri kaynağı](power-bi-embedded-connect-datasource.md).

Çalışmanızı **Power BI Desktop**’a kaydettikten sonra, PBIX dosyası oluşturulur. Bu dosya raporunuzu içerir. PBIX içeren veri hello içe aktarıyorsanız, ayrıca, tüm veri kümesini hello veya kullanıyorsanız **DirectQuery**, hello PBIX yalnızca veri kümesi şemasını içerir. Program aracılığıyla hello PBIX hello kullanarak çalışma alanınıza dağıttığınız [Power BI içeri aktarma API'si](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** ek API'leri toochange hello sunucu varsa ve Veri kümenizi dataset hello bir hizmet hesabı kimlik bilgisi tooand kümesi işaret ettiğinden veritabanı tooconnect tooyour veritabanı kullanır. Bkz. e [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) ve [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>API kullanarak Power BI veri kümeleri ve raporları oluşturma

### <a name="datsets"></a>Veri kümeleri

Power BI hello REST API kullanarak katıştırılmış içinde veri kümeleri oluşturabilirsiniz. Daha sonra verileri veri kümenize gönderebilirsiniz. Bu, Power BI Desktop, hello gerek kalmadan verilerle toowork sağlar. Daha fazla bilgi için bkz. [Veri Kümeleri Gönderme](https://msdn.microsoft.com/library/azure/mt778875.aspx).

### <a name="reports"></a>Reports

Bir veri kümesinden hello JavaScript API kullanarak doğrudan uygulamanıza bir rapor oluşturabilirsiniz. Daha fazla bilgi için bkz. [Power BI Embedded’de bir veri kümesinden yeni bir rapor oluşturma](power-bi-embedded-create-report-from-dataset.md).

## <a name="see-also"></a>Ayrıca Bkz.

[Bir örnek ile kullanmaya başlama](power-bi-embedded-get-started-sample.md)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[Rapor ekleme](power-bi-embedded-embed-report.md)  
[Power BI Embedded’de bir veri kümesinden yeni bir rapor oluşturma](power-bi-embedded-create-report-from-dataset.md)
[Raporları kaydetme](power-bi-embedded-save-reports.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)

