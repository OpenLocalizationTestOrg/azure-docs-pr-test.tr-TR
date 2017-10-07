---
title: "aaaDiscover, tanımlamak ve kişisel verileri Microsoft Azure | Microsoft Docs"
description: "Arama, Sınıflandırma, bulma ve verileri tanımlama hakkında bilgi edinin"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: af4ced1c57699dc751d55cfdf3229c7d294648a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="discover-identify-and-classify-personal-data-in-microsoft-azure"></a>Bulmak, tanımlamak ve Microsoft Azure kişisel verileri sınıflandırmak

Bu makale, nasıl toodiscover, tanımlamak ve birkaç Azure Araçları ve Hizmetleri Azure, Azure Hdınsight Hadoop kümeleri için Azure veri Kataloğu, Azure Active Directory, SQL veritabanı, Power Query kullanarak da dahil olmak üzere, kişisel verileri sınıflandırmak rehberlik sağlar. Information Protection, Azure Search ve SQL sorguları Azure Cosmos DB için.

## <a name="scenario-problem-statement-and-goal"></a>Senaryo, sorun bildirimi ve amacı

ABD tabanlı Spor şirket çok çeşitli kişisel ve diğer verileri toplar. Bu, müşterilerin ve çalışan verilerini içerir. Merhaba şirket içinde birden çok veritabanı tutar ve Azure ortamlarında birkaç farklı konumlarda depolar. Ayrıca donanım tooselling spor, da barındırmak ve kayıt hello AB dahil olmak üzere Merhaba Dünya taşıyan seçkin athletic olayları yönetmek ve bazı durumlarda hello müşteri verileri bunlar Topla sağlık bilgileri içerir.

Merhaba şirket birçok uluslararası bicycling tur her yıl barındırır ve bağlı personel Merhaba Dünya çevresinde konumlarda sahip olduğundan, birkaç hello veri kümelerini oldukça büyük. Merhaba şirket, müşteriler ve çalışanlar tarafından kullanılan Geliştirici oluşturulan uygulamalar da sahiptir.

Merhaba şirket sorunları aşağıdaki tooaddress hello ister:

- Müşteri ve çalışanın kişisel verilerini, sınıflandırılmış/ayırt hello olmalıdır diğer veri hello şirket sipariş tooensure uygun erişim ve güvenliği toplar.
- Merhaba veri yönetici gereken tooeasily hello Azure ortamı çeşitli alanlar genelindeki müşteri kişisel verilerin hello konumunu bulur.
- Görünür müşteri ve çalışanın kişisel verilerini paylaşılan belgeleri ve e-posta iletişimini etiketli toohelp olun güvenli tutulur.
- Merhaba şirketinizin uygulama geliştiricilerin kendi web ve mobil uygulamaları müşteri ve çalışan kişisel verileri için bir yol tooeasily arama gerekir.
- Geliştiriciler, kişisel veriler için kendi belge veritabanı tooquery da gerekir.

### <a name="company-goals"></a>Şirketin hedeflerine

- Kolayca bulunabilir böylece tüm müşteri ve çalışanın kişisel verilerini Azure veri Kataloğu'nda etiketli/açıklama olması gerekir. İdeal olarak müşteri ve çalışanın kişisel verilerini ayrı olarak etiketlenmiş/açıklama.
- Müşteri ve çalışan kullanıcı profilleri ve iş bilgilerini Azure Active Directory'de bulunan kişisel verileri kolayca yer alması gerekir.
- Birden çok SQL veritabanlarında bulunan kişisel verileri kolayca seçmeleri gerekir. 
- Merhaba şirketin büyük veri kümeleri bazıları Azure Hdınsight yönetilir ve Hadoop depolanan. Kişisel veriler için sorgulanabilir şekilde Excel'e aktarılmalıdır.
- Belgeleri ve e-posta iletişimini paylaşılan kişisel veriler sınıflandırılmış etiketli ve Azure Information Protection ile güvenli tutulur.
- Merhaba şirketinizin uygulama geliştiriciler mümkün toodiscover müşteri ve çalışan kişisel verilerin oluşturuncaya, Azure Search ile yapabileceklerini hello uygulamalarda olması gerekir.
- Geliştiriciler kendi belge veritabanındaki mümkün toofind kişisel verileri olması gerekir.

## <a name="azure-active-directory-data-discovery"></a>Azure Active Directory: Veri bulma

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) Microsoft'un bulut tabanlı, çok kiracılı dizin ve kimlik yönetimi hizmetidir. Müşteri ve çalışan kullanıcı profilleri ve kişisel veriler içeren kullanıcı iş bilgilerini bulun, [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) hello kullanarak (AAD) ortam [Azure portal](https://portal.azure.com/).

Toofind istediğiniz veya belirli bir kullanıcı için kişisel verileri değiştirirseniz, bu seçenek özellikle yararlıdır. Ayrıca ekleyin ya da kullanıcı profilini değiştirmek ve iş. Merhaba dizin için genel yönetici olan bir hesapla oturum gerekir.

### <a name="how-do-i-locate-or-view-user-profile-and-work-information"></a>Nasıl bulun veya kullanıcı profilini görüntülemek ve iş bilgileri?

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.

2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

   ![nasıl kullanıcı profilini bulun ve iş](media/how-to-discover-classify-personal-data-azure/user-profile.png)

3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **kullanıcılar**.

  ![Açılış kullanıcı ve Grup](media/how-to-discover-classify-personal-data-azure/users-groups.png)

4. Hello üzerinde **kullanıcılar ve gruplar - kullanıcıların** dikey penceresinde hello listeden bir kullanıcı seçin ve ardından, hello dikey penceresinde hello seçilen kullanıcı, **profili** kişisel verileri içerebilir tooview kullanıcı profili bilgileri .

  ![Kullanıcı Seç](media/how-to-discover-classify-personal-data-azure/select-user.png)

5. Tooadd gerekir veya kullanıcı profili bilgilerini değiştirmek, bunu yapmak ve ardından, hello komut çubuğunda **kaydedin.**
6. Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **iş bilgisi** kişisel verileri içerebilir tooview kullanıcı iş bilgileri.

 ![iş bilgileri görüntüleme](media/how-to-discover-classify-personal-data-azure/work-info.png)

7. Tooadd gerekir ya da kullanıcı iş bilgilerini değiştirmek, bunu yapmak ve ardından, hello komut çubuğunda **kaydedin.**

## <a name="azure-sql-database-data-discovery"></a>Azure SQL Database: Veri bulma

[Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) yapı ve uygulamalarını geliştiriciler yardımcı olan bir bulut veritabanıdır. Kişisel veriler bulunabilir [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50) standart SQL sorgularını kullanarak. Azure SQL esnek sorgu (Önizleme) kullanıcıların tooperform arası veritabanı sorguları sağlar.

Bir ayrıntılı [SQL veritabanı](../sql-database/sql-database-technical-overview.md) öğretici bir SQL veritabanı kullanarak birçok yönleri açıklanmaktadır nasıl dahil toobuild biri ve nasıl toorun verileri sorgular. Merhaba, bağlantılar toospecific bölümleri ile Merhaba öğreticideki kullanılabilir hello bilgilerinin özeti aşağıdadır.

### <a name="how-do-i-build-a-sql-database"></a>Bir SQL veritabanı nasıl oluşturulacağına?

Üç yolu toodo vardır:

- Bir Azure SQL veritabanı hello oluşturulabilir [Azure portal](https://portal.azure.com/). Merhaba öğreticide, işlem ve depolama kaynakları bir kaynak grubu ve mantıksal sunucu içinde belirli bir dizi kullanacaksınız. AdventureWorks adlı kurgusal bir şirkette örnek verileri kullanacaksınız. Ayrıca, bir sunucu düzeyinde güvenlik duvarı kuralı oluşturacaksınız. toolearn nasıl toodo Bu, ziyaret hello [hello Azure portalında bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-portal.md) Öğreticisi.

  ![Azure SQL veritabanı oluşturma](media/how-to-discover-classify-personal-data-azure/create-database.png)
- Bir SQL veritabanı hello de oluşturulabilir [Azure bulut Kabuk](https://azure.microsoft.com/features/cloud-shell/) CLI, tarayıcı tabanlı bir komut satırı aracıdır. Merhaba aracı hello Azure portalında kullanılabilir ve doğrudan buradan çalıştırabilirsiniz. Bu öğreticide hello aracını başlatmak, komut dosyası değişkenleri tanımlayın, bir kaynak grubu ve mantıksal sunucu oluşturmak ve bir sunucu güvenlik duvarı kuralı yapılandırın. Ardından örnek verilerle bir veritabanı oluşturun. toolearn toocreate veritabanınızı bu şekilde nasıl ziyaret hello [hello Azure CLI kullanarak tek bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-cli.md) Öğreticisi.

  ![CLIT Öğreticisi](media/how-to-discover-classify-personal-data-azure/cli-tutorial.png)

>[!NOTE]
Azure CLI Linux Yöneticiler ve geliştiriciler tarafından yaygın olarak kullanılır. Bazı kullanıcılar, daha kolay ve PowerShell, daha sezgisel, üçüncü seçenek olan bulun.

- Son olarak, bir komut satırı/komut dosyası kullanılan araç toocreate olduğu PowerShell kullanarak bir SQL veritabanı oluşturun ve Azure ve diğer kaynakları yönetin. Bu öğreticide hello aracını başlatmak, komut dosyası değişkenleri tanımlayın, bir kaynak grubu ve mantıksal sunucu oluşturmak ve bir sunucu güvenlik duvarı kuralı yapılandırın. Ardından örnek verilerle bir veritabanı oluşturacaksınız.

Başlangıç Öğreticisi hello Azure PowerShell modülü sürüm 4.0 veya üstünü gerektirir. Get-Module - listavailable birlikte AzureRM toofind sürümünüzü çalıştırın. Tooinstall veya yükseltme gerekiyorsa, yükleme Azure PowerShell modülü bakın.

```PowerShell
New-AzureRmSQLDatabase -ResourceGroupName $resourcegroupname `
-ServerName $servername `
-DatabaseName $databasename `
-RequestedServiceObjectiveName "s0"
```

toolearn toocreate veritabanınızı bu şekilde nasıl ziyaret hello [Powershell kullanarak tek bir Azure SQL veritabanı oluşturma](../sql-database/sql-database-get-started-powershell.md) Öğreticisi.

>[!Note]
Windows yöneticileri toouse PowerShell eğilimi gösterir, ancak bazı Azure CLI tercih.

### <a name="how-do-i-search-for-personal-data-in-sql-database-in-hello-azure-portal"></a>Ne arama hello Azure portal SQL veritabanındaki kişisel veriler için? **

Kişisel veriler için hello yerleşik sorgu Düzenleyicisi aracı hello Azure portal toosearch içinde kullanabilirsiniz. SQL server yönetici oturum açma ve parola kullanarak toohello aracında oturum ve bir sorgu girin.

  ![Merhaba portal kullanarak sql arama](media/how-to-discover-classify-personal-data-azure/search-sql-portal.png)

Adım 5 hello öğreticinin örnek bir sorgu hello sorgu Düzenleyicisi bölmesinde gösterir, ancak (Ayrıca iki tablolardaki verileri birleştiren ve döndürülen hello veri kümesi içindeki hello kaynak sütunu için diğer adlar oluşturur) kişisel ya da hassas bilgi odaklanmak değil. Merhaba aşağıdaki ekran görüntüsünde hello sorgu döndürülen hello sonuçlar bölmesinde yanı sıra adım 5 ' gösterir:

  ![sorgu düzenleyicisi](media/how-to-discover-classify-personal-data-azure/query-editor.png)

Veritabanınızı MyTable çağırdıysanız, kişisel bilgi için bir örnek sorgu adı, sosyal güvenlik numarası ve kimlik numarasını içerebilir ve şuna benzer:

"Adı, SSN, kimlik numarası gelen MyTable Seç"

Merhaba sorgusunu çalıştırın ve hello hello sonuçlarında görmek **sonuçları** bölmesi.

Merhaba nasıl tooquery bir SQL veritabanı hello Azure portal ile ilgili daha fazla bilgi için ziyaret [hello SQL veritabanını sorgula](../sql-database/sql-database-get-started-portal.md) hello öğreticinin bölümü.

### <a name="how-do-i-search-for-data-across-multiple-databases"></a>Birden çok veritabanı arasında nasıl verileri için arama?

SQL esnek sorgu (Önizleme), tooperform veritabanları arası ve birden çok veritabanı sorguları sağlar ve tek bir sonuç döndürür. Merhaba [öğreticiye genel bakış](../sql-database/sql-database-elastic-query-overview.md) senaryoları için ayrıntılı bir açıklama içerir ve veritabanı dikey ve yatay bölümleme arasındaki farkı hello açıklar. Yatay bölümleme "parçalama." olarak adlandırılır

  ![Dikey bölümleme](media/how-to-discover-classify-personal-data-azure/vertical-partition.png)

  ![Yatay bölümleme](media/how-to-discover-classify-personal-data-azure/horizontal.png)

başlatıldı, tooget ziyaret hello [Azure SQL Database esnek sorgu genel bakış (Önizleme)](../sql-database/sql-database-elastic-query-overview.md) sayfası.

#### <a name="power-query-for-importing-azure-hdinsight-hadoop-clusters-data-discovery-for-large-data-sets"></a>Power Query (Azure Hdınsight Hadoop kümeleri almak için): büyük veri kümeleri için veri bulma

Hadoop, Apache depolama ve işleme hizmeti için Hadoop kümeleri içinde depolanan ve analiz büyük veri kümeleri, açık bir kaynaktır. [Azure Hdınsight](https://azure.microsoft.com/services/hdinsight/) kullanıcılar toowork Hadoop ile Azure'da kümeleri sağlar. Power Query bir Excel eklemek, başka şeylerin Bul farklı kaynaklardan veri kullanıcılarına yardımcı olur bileşenidir.

Azure hdınsight'ta Hadoop kümeleri ile ilişkili kişisel veriler Power Query ile alınan tooExcel olabilir. Merhaba veri Excel'de olduğunda bir sorgu tooidentify kullanabilirsiniz.

#### <a name="how-do-i-use-excel-power-query-tooimport-hadoop-clusters-in-azure-hdinsight-into-excel"></a>Nasıl Excel Power Query tooimport Hadoop kümeleri Azure Hdınsight'ta Excel'e kullanabilirim?

Bir Hdınsight Öğreticisi tüm bu işlemde size yol gösterir. Önkoşulları açıklar ve bir bağlantı tooa içerir [Azure Hdınsight kullanmaya başlama](../hdinsight/hdinsight-hadoop-linux-tutorial-get-started.md) Öğreticisi. Yönergeleri kapsar Excel 2016 yanı sıra 2013 ve 2010 (adımları hello daha eski sürümleri Excel için biraz farklı). Merhaba Excel Power Query Eklentisi yoksa, hello öğretici şunların nasıl yapıldığını gösterir tooget onu. Başlangıç Öğreticisi Excel'de başlayacaksınız ve bir Azure Blob Depolama hesabı kümenizle ilişkilendirilmiş toohave gerekir.

  ![Excel sorgusu](media/how-to-discover-classify-personal-data-azure/excel.png)

toolearn nasıl toodo Bu, ziyaret hello [Power Query kullanarak bağlanmak Excel tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md) Öğreticisi.

Kaynak: [Power Query kullanarak bağlan Excel tooHadoop](../hdinsight/hdinsight-connect-excel-power-query.md)

## <a name="azure-information-protection-personal-data-classification-for-documents-and-email"></a>Azure Information Protection: belgeler ve e-posta kişisel veri sınıflandırması

[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) etiketleri tooclassify uygulamak ve dahili olarak veya harici olarak paylaşılan belgeleri korumak ve iletişim e-posta Azure müşterilere yardımcı olabilir. Bu öğelerin bazıları, müşteri veya çalışanın kişisel bilgiler içerebilir. Kural ve koşulları Yöneticiler veya kullanıcılar tarafından otomatik olarak veya el ile tanımlanabilir. Örneğin, bir kullanıcı, kredi kartı bilgilerini içeren bir belge kaydetme, isterse hello yönetici tarafından yapılandırılan etiket öneride görür.

### <a name="how-do-i-try-it"></a>Bunu nasıl deneyin?

Kuruluşunuz için uygun olabilir, toogive Azure Information Protection try toosee istiyorsanız hello ziyaret [hızlı başlangıç Öğreticisi](https://docs.microsoft.com/information-protection/get-started/infoprotect-quick-start-tutorial). Beş temel adımlarda size yol gösterir — etiketleme ve eylemde paylaşımı yükleme tooconfiguring İlkesi tooseeing sınıflandırma gelen — ve az yarım saat sürer.

### <a name="how-do-i-deploy-it"></a>Nasıl dağıtırım?

Kuruluşunuz için Azure Information Protection toodeploy kullanmak isterseniz, hello ziyaret [Sınıflandırma, etiketleme ve koruma için dağıtım yol haritasını](https://docs.microsoft.com/information-protection/plan-design/deployment-roadmap).

### <a name="is-there-anything-else-i-should-know"></a>Bilmeniz gereken başka bir şey var mı?

Tooset bunun nasıl ziyaret aracılığıyla düşündüğünüz yardımcı olacak tamamlayıcı bilgiler için hello [hazır, ayarlayın, koruma!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
blog postası. Ve onay hello Azure Information Protection hakkında daha fazla bilgi için aşağıda listelenen daha fazla bağlantılar öğrenin.

## <a name="azure-search-data-discovery-for-developer-apps"></a>Azure arama: Geliştirici uygulamaları veri bulma

[Azure arama](https://azure.microsoft.com/services/search/) uygulamalarınız için zengin veri arama deneyimi sağlar ve geliştiriciler için bulut arama çözümüdür. Azure Search'te Azure Cosmo DB, Azure SQL Database, Azure Blob Storage, Azure Table depolama veya özel müşteri JSON verilerini kaynaklanan, kullanıcı tanımlı dizinler arasında toolocate veri sağlar. Ayrıca, kişisel veri türleri veya belirli kişilerin hello kişisel veriler için hello Azure Search REST API'sini toosearch kullanarak Lucene sorguları yapısı. Tam metin araması, Basit Sorgu söz dizimi ve Lucene sorgu söz dizimi özellikleri içerir. 

## <a name="how-do-i-use-sql-tooquery-data"></a>SQL tooquery verileri nasıl kullanabilirim?

Merhaba temelleri ile toobegin ziyaret hello [Azure CosmosD DB: nasıl SQL kullanarak tooquery](../cosmos-db/tutorial-query-documentdb.md) Öğreticisi. Başlangıç Öğreticisi, örnek bir belge ve iki örnek SQL sorguları ve sonuçları sağlar.

SQL sorguları oluşturma konusunda daha fazla ayrıntılı yönergeler için ziyaret [SQL sorgularını Azure Cosmos DB belge DB API için.](../cosmos-db/documentdb-sql-query.md)

Yeni tooAzure Cosmos DB iseniz ve nasıl toocreate bir veritabanı bir koleksiyonu ekleyin ve veri ekleme toolearn gibi hello ziyaret [Azure Cosmos DB: DocumentDB API web uygulaması oluşturma](../cosmos-db/create-documentdb-dotnet.md) hızlı başlangıç Öğreticisi. Toodo isterseniz bunu .NET, Java veya Python gibi dışındaki bir dilde yalnızca seçin tercih ettiğiniz dili toohello site aldıktan sonra.

## <a name="next-steps"></a>Sonraki adımlar

[Azure SQL Veritabanı](https://azure.microsoft.com/services/sql-database/?v=16.50)

[SQL Veritabanı nedir?](../sql-database/sql-database-technical-overview.md)

[SQL veritabanı sorgu düzenleyici Azure portalında kullanılabilir] (https://azure.microsoft.com/blog/t-sql-query-editor-in-browser-azure-portal/)

[Azure Information Protection nedir?](https://docs.microsoft.com/information-protection/understand-explore/what-is-information-protection)

[Azure Rights Management nedir?](https://docs.microsoft.com/information-protection/understand-explore/what-is-azure-rms)

[Azure Information Protection: Hazır, ayarlayın, koruyun!](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/21/azure-information-protection-ready-set-protect/)
