---
title: "aaaConnect tooSQL C ve C++ kullanarak veritabanı | Microsoft Docs"
description: "Kullanım hello örnek modern uygulama C++ ile bu hızlı başlangıç toobuild kod ve hello bulutta bir güçlü ilişkisel veritabanı Azure SQL Database tarafından yedeklenen."
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>TooSQL bağlanmak C ve C++ kullanarak veritabanı
Bu post C ve C++ geliştiricileri tooconnect tooAzure SQL DB çalışırken amaçlamaktadır. En iyi ilginize yakalar toohello bölümüne atlayabilirsiniz şekilde bölümlere ayrılmıştır. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Merhaba C/C++ öğreticisi için Önkoşullar
Aşağıdaki öğelerindeki hello bulunduğundan emin olun:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [Ücretsiz Azure Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* [Visual Studio](https://www.visualstudio.com/downloads/). Merhaba C++ dili bileşenleri toobuild yükleyin ve bu örneği çalıştırmak.
* [Visual Studio Linux geliştirme](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e). Linux'ta geliştiriyorsanız hello Visual Studio Linux uzantısını yüklemeniz gerekir. 

## <a id="AzureSQL"></a>Azure SQL Database ve SQL Server sanal makineler
Azure SQL Microsoft SQL Server üzerinde oluşturulur ve bir yüksek kullanılabilirlik, kullanıcı ve ölçeklenebilir hizmet tasarlanmış tooprovide olur. Birçok avantajları toousing SQL Azure çalıştıran şirket içi, özel bir veritabanı üzerinde vardır. SQL Azure ile yok tooinstall sahip, ayarlamak, korumak veya veritabanı ancak yalnızca hello içerik ve veritabanınızın hello yapısını yönetin. Biz hata toleransı ve artıklık tüm yerleşiktir gibi veritabanlarıyla endişe hakkında tipik şey. 

Azure şu anda SQL server iş yüklerini barındırmak için iki seçenek vardır: Azure SQL veritabanı, veritabanı hizmeti ve SQL server üzerinde sanal makine (VM) olarak. Biz bu iki hello farklarını hakkında ayrıntılı bilgi içine Azure SQL veritabanı, en iyi sonuç için maliyet tasarrufu hello yeni bulut tabanlı uygulamalar tootake avantajlarından ve bulut Hizmetleri performans iyileştirmesinden dışında almazsınız. Geçiş veya şirket içi uygulamalar toohello bulut genişletme düşünüyorsanız, Azure sanal makinesinde SQL server sizin için daha iyi çıkışı çalışabilir. tookeep şeyler basit bu makalede, Azure SQL veritabanını oluşturalım. 

## <a id="ODBC"></a>Veri erişim teknolojileri: ODBC ve OLE DB
Bağlantı tooAzure SQL DB farklı olduğundan ve şu anda iki yolu vardır tooconnect toodatabases: ODBC (açık veritabanı bağlantısı) ve OLE DB (Nesne Bağlama ve Katıştırma veritabanı). Son yıllarda Microsoft ile hizalı [yerel ilişkisel veri erişimi için ODBC](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/). ODBC görece basit ve ayrıca çok daha hızlı OLE DB ' dir. Burada yalnızca uyarısıyla Hello ODBC eski bir C tarzı API kullanma ' dir. 

## <a id="Create"></a>1. adım: Azure SQL veritabanınızı oluşturma
Merhaba bkz [sayfa Başlarken](sql-database-get-started-portal.md) toolearn nasıl toocreate bir örnek veritabanı.  Alternatif olarak, bu izleyebilirsiniz [kısa iki dakikalık video](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) kullanarak bir Azure SQL veritabanı toocreate hello Azure portalı.

## <a id="ConnectionString"></a>2. adım: Get bağlantı dizesi
Azure SQL veritabanınızı sağlandıktan sonra aşağıdaki adımları toodetermine bağlantı bilgilerle hello çıkışı toocarry gerekir ve güvenlik duvarı erişim için istemci IP ekleyin. 

İçinde [Azure portal](https://portal.azure.com/), Git tooyour Azure SQL veritabanı ODBC bağlantı dizesi hello kullanarak **veritabanı bağlantı dizelerini Göster** hello genel bakış bölümünde veritabanınız için bir parçası olarak listelenen: 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Merhaba Hello içeriğini kopyalayın **ODBC (Node.js içerir) [SQL kimlik doğrulaması]** dize. Bu dize kullanırız bizim C++ ODBC komut satırı yorumlayıcı gelen sonraki tooconnect. Bu dize hello sürücü, sunucu ve diğer veritabanı bağlantı parametrelerini gibi ayrıntıları sağlar. 

## <a id="Firewall"></a>3. adım: IP toohello duvarınızın ekleme
Veritabanı sunucunuz için toohello güvenlik duvarı bölümüne gidin ve ekleyin, [istemci IP toohello Güvenlik Duvarı şu adımları kullanarak](sql-database-configure-firewall-settings.md) toomake biz başarılı bir bağlantı kurmak emin: 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

Bu noktada, Azure SQL DB yapılandırmış ve C++ kodunuzdan hazır tooconnect şunlardır. 

## <a id="Windows"></a>4. adım: bir Windows C/C++ uygulamasından bağlanma
Tooyour kolayca bağlanabilir [Bu örneği kullanarak Windows üzerinde ODBC kullanarak Azure SQL DB](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) Visual Studio ile oluşturur. Merhaba örnek kullanılan tooconnect tooour Azure SQL DB olabilir bir ODBC komut satırı yorumlayıcı uygular. Bu örnek, bir veritabanı kaynağı adı (DSN) dosyasından komut satırı bağımsız değişkeni olarak veya biz hello Azure portal ' daha önce kopyaladığınız hello ayrıntılı bağlantı dizesini alır. Bu proje için hello özellik sayfası açmak ve aşağıda gösterildiği gibi bir komut bağımsız değişkeni hello bağlantı dizesini yapıştırın: 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

Bu veritabanı bağlantı dizesi bir parçası olarak veritabanınız için hello doğru kimlik doğrulama ayrıntıları sağladığınızdan emin olun. 

Merhaba uygulama toobuild başlatın. Başarılı bir bağlantı doğrulama penceresi aşağıdaki hello görmeniz gerekir. Bazı temel SQL komutları gibi bile çalıştırabilirsiniz **tablo oluşturma** toovalidate veritabanı bağlantınızı:

![SQL komutları](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

Alternatif olarak, hiçbir komut bağımsız değişkenleri sağlandığında, başlatılan hello Sihirbazı'nı kullanarak bir DSN dosyası oluşturabilirsiniz. Bu seçeneği de deneyin öneririz. Otomasyon ve kimlik doğrulama ayarlarınızı koruma için bu DSN dosyası kullanabilirsiniz: 

![DSN dosyası oluşturma](./media/sql-database-develop-cplusplus-simple/datasource.png)

Tebrikler! Şimdi tooAzure SQL başarıyla bağlandıysanız C++ ve ODBC Windows kullanarak. Okuma devam toodo hello aynı de Linux platformuna. 

## <a id="Linux"></a>5. adım: bir Linux C/C++ uygulamasından bağlanma
Merhaba haber henüz heard henüz durumunda, Visual Studio toodevelop C++ Linux uygulama artık sağlar. Bu yeni hello senaryoda hakkında bilgi edinebilirsiniz [Linux geliştirmesi için Visual C++](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blogu. Linux için toobuild, Linux distro çalıştığı bir uzak makine gerekir. Yoksa, kullanılabilir bir hızlı şekilde kullanmaya ayarlayabileceğiniz [Linux Azure sanal makineleri](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Bu öğretici için bize ayarlanan bir Ubuntu 16.04 Linux dağıtım olduğunu varsayalım. Merhaba adımlar burada da tooUbuntu 15.10, Red Hat 6 ve Red Hat 7 uygulamalıdır. 

Merhaba aşağıdaki adımları için distro SQL ve ODBC için gerekli hello kitaplıklarını yükle:

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Visual Studio'yu başlatın. Altında Araçlar -> Seçenekler -> platformlar arası bağlantı Yöneticisi ->, bir bağlantı tooyour Linux kutusu ekleyin: 

![Araçlar Seçenekler](./media/sql-database-develop-cplusplus-simple/tools.png)

SSH üzerinden bağlantı kurulduktan sonra boş bir proje (Linux) şablonu oluşturun: 

![Yeni Proje şablonu](./media/sql-database-develop-cplusplus-simple/template.png)

Daha sonra ekleyebilirsiniz bir [yeni C kaynak dosyası ve bu içerikle değiştirin](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c). Hello ODBC API SQLAllocHandle, SQLSetConnectAttr komutu ve SQLDriverConnect kullanarak mümkün tooinitialize olması ve bir bağlantı tooyour veritabanı oluşturun. Gibi hello Windows ODBC örnekle, Itanium tabanlı sistemler için tooreplace hello SQLDriverConnect çağrısı hello ayrıntıları ile hello Azure portal ' daha önce kopyaladığınız, veritabanı bağlantı dizesi parametrelerinden gerekir. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

derleme tooadd önce son şey toodo hello **odbc** kitaplığı bağımlılık olarak: 

![ODBC giriş kitaplık olarak ekleme](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch, uygulamanızın Linux Konsolu hello hello Getir **hata ayıklama** menüsü: 

![Linux Konsolu](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

Bağlantınızın başarılı olduysa, şimdi hello Linux Konsolu yazdırılan hello geçerli veritabanı adını görmeniz gerekir: 

![Linux konsol penceresi çıktısı](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

Tebrikler! Merhaba öğreticisini başarıyla tamamladınız ve tooyour Azure SQL DB Windows ve Linux platformlarına C++ içinden şimdi bağlanabilir.

## <a id="GetSolution"></a>Merhaba tam C/C++ Öğreticisi çözümünü edinme
Github'da bu makaledeki tüm hello örnekleri içeren GetStarted çözümünü hello bulabilirsiniz:

* [ODBC C++ Windows örnek](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), hello Windows C++ ODBC örnek tooconnect tooAzure SQL indirin
* [ODBC C++ Linux örnek](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), hello Linux C++ ODBC örnek tooconnect tooAzure SQL indirin

## <a name="next-steps"></a>Sonraki adımlar
* Gözden geçirme hello [SQL veritabanı geliştirme genel bakış](sql-database-develop-overview.md)
* Merhaba hakkında daha fazla bilgi [ODBC API Başvurusu](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>Ek kaynaklar
* [Azure SQL Veritabanı ile Çok Kiracılı SaaS Uygulamaları için Tasarım Desenleri](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Tüm hello keşfedin [SQL veritabanı özellikleri](https://azure.microsoft.com/services/sql-database/)

