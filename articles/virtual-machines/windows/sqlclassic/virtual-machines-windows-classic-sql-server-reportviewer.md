---
title: ReportViewer Web sitesindeki aaaUse | Microsoft Docs
description: "Bu konuda nasıl toobuild bir Microsoft Azure sanal makinesinde Microsoft Azure Web sitesi ile bir rapor görüntüler hello Visual Studio ReportViewer Denetimi'ni depolanan açıklanmaktadır."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>Azure’da Barındırılan bir Web Sitesinde ReportViewer Kullanma
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Bir Microsoft Azure Web sitesi hello bir Microsoft Azure sanal makinesinde depolanan bir rapor görüntüler Visual Studio ReportViewer Denetimi'ni kullanarak oluşturabilirsiniz. Merhaba ASP.NET Web uygulaması şablonu kullanarak oluşturduğunuz bir Web uygulamasında Hello ReportViewer Denetimi'ni var.

> [!IMPORTANT]
> Merhaba ASP.NET MVC Web uygulaması şablonları hello ReportViewer Denetimi'ni desteklemez.

ReportViewer tooincorporate Microsoft Azure Web sitenizi içine görevleri aşağıdaki toocomplete hello gerekir.

* **Ekleme** derlemeleri toohello dağıtım paketi
* **Yapılandırma** kimlik doğrulama ve yetkilendirme
* **Yayımlama** ASP.NET Web uygulaması tooAzure hello

## <a name="prerequisites"></a>Ön koşullar
Gözden hello "genel öneri ve en iyi uygulamalar" bölümünde [SQL Server Business Intelligence Azure Virtual Machines'de](../classic/ps-sql-bi.md).

> [!NOTE]
> ReportViewer denetimleri, Visual Studio, Standard Edition veya üzeri aktarılır. Merhaba Web Developer Express Edition kullanıyorsanız, hello yüklemelisiniz [MICROSOFT Rapor Görüntüleyicisi 2012 çalışma zamanı](https://www.microsoft.com/download/details.aspx?id=35747) toouse hello ReportViewer çalışma zamanı özellikleri.
> 
> Yapılandırılan yerel işleme modunda ReportViewer Microsoft Azure'da desteklenmiyor.

## <a name="adding-assemblies-toohello-deployment-package"></a>Derlemeleri toohello dağıtım paketi ekleme
ASP.NET uygulama şirket içi barındırdığınızda hello ReportViewer derlemeler genellikle doğrudan hello genel derleme önbelleğinde hello IIS sunucusunun (GAC) Visual Studio yükleme sırasında yüklenir ve doğrudan hello uygulama tarafından erişilebilir. ASP.NET uygulamanızı hello bulutta Microsoft Azure içine toobe yüklü herhangi bir şey izin verme konak hello GAC, emin olmanız gerekir böylece ancak hello ReportViewer derlemeleri uygulamanızı yerel olarak kullanılabilir. Projenizde başvuruları toothem ekleyerek bunu ve bunları yapılandırma toobe yerel olarak kopyalanır.

Uzaktan işleme modunda ReportViewer Denetimi'ni hello derlemeleri aşağıdaki hello kullanır:

* **Microsoft.ReportViewer.WebForms.dll**: ihtiyacınız hello ReportViewer kodunu içerir toouse ReportViewer sayfanıza. Projenizde ASP.NET sayfaya ReportViewer Denetimi'ni bıraktığınızda tooyour projesi bu derleme için bir başvuru eklenir.
* **Microsoft.ReportViewer.Common.dll**: çalışma zamanında hello ReportViewer denetimi tarafından kullanılan sınıfları içerir. Tooyour proje otomatik olarak eklenmez.

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd başvuru tooMicrosoft.ReportViewer.Common
* Projenizin sağ **başvuruları** düğümü ve Seç **Başvuru Ekle**hello derleme hello .NET sekmesini seçin ve'ı tıklatın **Tamam**.

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>ASP.NET uygulaması tarafından yerel olarak erişilebilir toomake hello derlemeler
1. Merhaba, **başvuruları** klasör özelliklerini hello Özellikler bölmesinde görünmesini sağlayacak şekilde hello Microsoft.ReportViewer.Common derleme'yi tıklayın.
2. Merhaba Özellikler bölmesinde ayarlayın **kopya yerel** tooTrue.
3. Adım 1 ve 2 Microsoft.ReportViewer.WebForms için yineleyin.

### <a name="tooget-reportviewer-language-pack"></a>tooget ReportViewer dil paketi
1. Merhaba uygun Microsoft Rapor Görüntüleyicisi 2012 çalışma zamanı yeniden dağıtılabilir paketi yükleme [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386).
2. Select hello dilden hello açılır liste ve hello sayfa yeniden yönlendirilen toohello karşılık gelen İndirme Merkezi sayfayı alır.
3. Tıklatın **karşıdan** ReportViewerLP.exe toostart hello indirilmesi.
4. ReportViewerLP.exe indirdikten sonra tıklatın **çalıştırmak** tooinstall hemen veya tıklatın **kaydetmek** toosave, tooyour bilgisayar. Tıklatırsanız **kaydetmek**, hello dosyasını kaydettiğiniz hello klasörünün hello adı unutmayın.
5. Merhaba dosyasını kaydettiğiniz hello klasörünü bulun. ReportViewerLP.exe sağ tıklayın, **yönetici olarak çalıştır**ve ardından **Evet**.
6. ReportViewerLP.exe çalıştırdıktan sonra hello c:\windows\assembly sahip hello kaynak dosyaları görürsünüz **Microsoft.ReportViewer.Webforms.Resources** ve **Microsoft.ReportViewer.Common.Resources** .

### <a name="tooconfigure-for-localized-reportviewer-control"></a>yerelleştirilmiş ReportViewer denetimin tooconfigure
1. Karşıdan yükle ve yukarıda belirtilen yönergeleri aşağıdaki hello tarafından hello Microsoft Rapor Görüntüleyicisi 2012 çalışma zamanı yeniden dağıtılabilir paketini yükleyin.
2. Oluşturma <language> hello proje ve kopyalama hello klasöründe ilişkili kaynak derleme dosyaları. Merhaba kopyalanan kaynak assembly dosyaları toobe şunlardır: **Microsoft.ReportViewer.Webforms.Resources.dll** ve **Microsoft.ReportViewer.Common.Resources.dll**. Merhaba kaynak assembly dosyaları seçin ve hello Özellikler bölmesinde ayarlayın **tooOutput dizin kopyalama** çok "**her zaman Kopyala**".
3. Ayarlama kültür & UICulture hello web projesi için hello. Tooset hello kültür ve bir ASP.NET Web sayfası için UI kültürü nasıl görürüm hakkında daha fazla bilgi için [nasıl yapılır: kümesi için ASP.NET Web sayfası Genelleştirme kültür ve UI kültürü hello](http://go.microsoft.com/fwlink/?LinkId=237461).

## <a name="configuring-authentication-and-authorization"></a>Kimlik doğrulama ve yetkilendirme yapılandırma
Merhaba ReportViewer toouse uygun kimlik bilgilerine tooauthenticate hello rapor sunucusu ile gerektiriyor ve hello kimlik bilgilerini istediğiniz hello report server tooaccess hello raporları tarafından yetkilendirilmelidir. Kimlik doğrulama hakkında daha fazla bilgi için hello teknik incelemesine bakın [Reporting Services Rapor Görüntüleyicisi denetimi ve Microsoft Azure sanal makine tabanlı rapor sunucuları](https://msdn.microsoft.com/library/azure/dn753698.aspx).

## <a name="publish-hello-aspnet-web-application-tooazure"></a>Yayımlama Hello ASP.NET Web uygulaması tooAzure
Bir ASP.NET Web uygulaması tooAzure yayımlama ile ilgili yönergeler için bkz: [nasıl yapılır: geçirmek ve bir Web uygulaması tooAzure Visual Studio'dan yayımlamak](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md) ve [Web uygulamaları ve ASP.NET kullanmaya başlama](../../../app-service-web/app-service-web-get-started-dotnet.md).

> [!IMPORTANT]
> Çözüm Gezgini'nde hello kısayol menüsünde Hello Azure dağıtım projesi eklemek veya Azure bulut hizmeti projesi Ekle komutu görünmüyorsa, hello proje too.NET Framework 4 toochange hello hedef Framework'ü gerekebilir.
> 
> Merhaba iki komutları sağlayan temelde hello aynı işlevselliği. Bir ya da hello diğer komutu hello Microsoft Azure SDK'sı sürümüne bağlı olarak yüklediğiniz hello kısayol menüsünde görüntülenir.
> 
> 

## <a name="resources"></a>Kaynaklar
[Microsoft raporları](http://go.microsoft.com/fwlink/?LinkId=205399)

[Azure Sanal Makinelerde SQL Server İş Zekası](../classic/ps-sql-bi.md)

[Bir Azure VM ile bir yerel moddaki bir rapor sunucusunda PowerShell tooCreate kullanın](../classic/ps-sql-report.md)

