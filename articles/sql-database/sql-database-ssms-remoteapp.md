---
title: "Azure Remoteapp'te SQL Server Management Studio kullanarak veritabanı aaaConnect tooSQL | Microsoft Docs"
description: "Bu öğretici toolearn kullanma toouse SQL Server Management Studio'da Azure RemoteApp üzerinde güvenlik ve tooSQL veritabanına bağlanırken performansı"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>Azure RemoteApp tooconnect tooSQL veritabanı SQL Server Management Studio'yu kullanın

> [!IMPORTANT]
> Azure RemoteApp kullanımdan kaldırılıyor. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
>

## <a name="introduction"></a>Giriş
Bu öğretici şunların nasıl yapıldığını gösterir Azure RemoteApp tooconnect tooSQL veritabanı içinde toouse SQL Server Management Studio (SSMS). SQL Server Management Studio'da Azure RemoteApp kurma hello işlem size yol göstermektedir, hello avantajlar açıklanır ve Azure Active Directory'de kullanabileceğiniz güvenlik özellikleri gösterir.

**Zaman toocomplete tahmini:** 45 dakika

## <a name="ssms-in-azure-remoteapp"></a>Azure RemoteApp SSMS
Azure RemoteApp, uygulamalar sunuyor Azure RDS hizmetidir. Daha fazla bilgi aşağıda öğrenebilirsiniz: [RemoteApp nedir?](../remoteapp/remoteapp-whatis.md)

Azure RemoteApp verir çalıştıran SSMS SSMS yerel olarak çalışan olarak aynı deneyimi hello.

![Azure Remoteapp'te çalıştıran SSMS gösteren ekran görüntüsü][1]

## <a name="benefits"></a>Avantajlar
Birçok avantajları toousing Azure RemoteApp SSMS vardır dahil olmak üzere:

* Azure SQL Server 1433 numaralı bağlantı noktasını (Azure dışında) dışarıdan kullanıma sunulan toobe yok.
* Ekleme ve IP adreslerini hello Azure SQL server Güvenlik Duvarı'nı kaldırma hiçbir gerek tookeep.
* Tüm Azure RemoteApp bağlantıları HTTPS üzerinden gerçekleşmesi 443 numaralı bağlantı noktasını kullanarak şifrelenmiş Uzak Masaüstü Protokolü
* Çok kullanıcılı ve ölçeklendirebilirsiniz.
* SSMS hello sahip öğesinden bir performans kazancı yoktur hello SQL veritabanı ile aynı bölgeye.
* Azure RemoteApp kullanımı hello Premium edition kullanıcı etkinlik raporları olan Azure Active Directory ile denetleyebilirsiniz.
* Çok faktörlü kimlik doğrulamasını (MFA) etkinleştirebilirsiniz.
* Erişim herhangi bir yere hello birini kullanırken SSMS, iOS, Android, Mac, Windows Phone ve Windows bilgisayarın içeren Azure RemoteApp istemcileri desteklenir.

## <a name="create-hello-azure-remoteapp-collection"></a>Hello Azure RemoteApp koleksiyonu oluşturun
Azure RemoteApp koleksiyonunuzun SSMS ile Merhaba adımları toocreate şunlardır:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Yeni bir Windows VM görüntüsünü oluşturma
Merhaba "Windows Server Uzak Masaüstü Oturumu Ana bilgisayar Windows Server 2012 R2" Merhaba galeri toomake görüntüden yeni VM'nin kullanın.

### <a name="2-install-ssms-from-sql-express"></a>2. SSMS SQL hızlı yükleme
Üzerine gidin yeni VM hello ve toothis indirme sayfasına gidin: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Bir seçenek tooonly indirme SSMS yoktur. Yükleme sonra hello yükleme dizinine gidin ve Kurulum tooinstall SSMS çalıştırın.

Ayrıca SQL Server 2014 Service Pack 1 tooinstall gerekir. Buradan indirebilirsiniz: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 Azure SQL veritabanı ile çalışmak için gerekli işlevselliği içerir.

### <a name="3-run-validate-script-and-sysprep"></a>3. Doğrulama betiği çalıştırma ve Sysprep
Üzerinde Hello hello VM masaüstünün doğrulama adlı bir PowerShell komut dosyasıdır. Bu, çift tıklayarak dosyayı çalıştırın. Bu hello VM uzak uygulamaları barındırmak için kullanılan hazır toobe olduğunu doğrular. Doğrulama tamamlandığında toorun sysprep - ister toorun seçin.

Sysprep tamamlandığında VM hello kapanır.

bir Azure RemoteApp görüntüsü oluşturma hakkında daha fazla toolearn bakın: [nasıl toocreate RemoteApp şablon görüntüsü ile Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Yansıma Yakalama
Ne zaman VM, durdu hello hello geçerli portalında bulun ve yakalayın.

bir görüntü yakalama hakkında daha fazla toolearn bakın [hello Klasik dağıtım modeli kullanılarak oluşturulmuş bir Azure Windows sanal makine bir görüntüsünü yakalama](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. TooAzure RemoteApp şablon görüntüleri ekleme
Hello hello geçerli portal Azure RemoteApp bölümü, toohello şablon görüntüleri sekmesine gidin ve Ekle'yi tıklatın. Hello açılır kutusunda "bir görüntü, sanal makineleri kitaplıktan Al" seçin ve ardından hello oluşturduğunuz görüntü seçin.

### <a name="6-create-cloud-collection"></a>6. Bulut koleksiyonu oluşturma
Hello geçerli Portalı'nda, yeni Azure RemoteApp bulut koleksiyonu oluşturma. Merhaba şablon görüntüsü yüklü SSMS ile aktardığınız seçin.

![Yeni bulut koleksiyonu oluşturma][2]

### <a name="7-publish-ssms"></a>7. SSMS yayımlama
Yeni bulut koleksiyonunuzu select Yayımla sekmesinde bir uygulama yayımlama hello üzerinde Başlat menüsü hello ve SSMS hello listeden seçin.

![Uygulama yayımlama][5]

### <a name="8-add-users"></a>8. Kullanıcı ekle
Merhaba kullanıcı erişimini sekmesinde yalnızca SSMS içeren erişim toothis Azure RemoteApp koleksiyonu vardır hello kullanıcılar seçebilir.

![Kullanıcı Ekleme][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Merhaba Azure RemoteApp istemci uygulaması yükleme
Bir Azure RemoteApp istemcisini yükleyip: [karşıdan | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Azure SQL server yapılandırma
Azure Hizmetleri tooensure gerekli yapılandırma, yalnızca hello hello Güvenlik Duvarı etkin. Ardından bu çözümü kullanıyorsanız tooadd tüm IP adresleri tooopen hello Güvenlik Duvarı'nı gerekmez. SQL Server toohello izin hello ağ trafiği Azure hizmetlerinden tutulur.

![Azure izin ver][4]

## <a name="multi-factor-authentication-mfa"></a>Çok faktörlü kimlik doğrulaması (MFA)
MFA bu uygulama için özel olarak etkinleştirilebilir. Azure Active Directory'yi toohello uygulamalar sekmesine gidin. Microsoft Azure RemoteApp için bir giriş bulacaksınız. Bu uygulama'yı tıklatın ve ardından yapılandırma hello sayfası aşağıdaki burada bu uygulama için MFA etkinleştirebilirsiniz görürsünüz.

![MFA'yı etkinleştirin][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Azure Active Directory Premium ile kullanıcı etkinliğini denetleyin
Tooturn sahip sonra Azure AD Premium, yoksa, üzerinde hello dizininizin lisansları bölümü. Etkin Premium ile toohello Premium düzeyi kullanıcılar atayabilirsiniz.

Azure Active Directory'yi tooa kullanıcı olduğunuzda, ardından toohello etkinlik sekmesini toosee oturum açma bilgileri tooAzure RemoteApp gidebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Tüm hello yukarıdaki adımları tamamladıktan sonra mümkün toorun hello Azure RemoteApp istemcisi ve olması atanmış bir kullanıcı ile oturum aç. SSMS ile uygulamalarınızı biri olarak sunulur ve bilgisayarınızda erişim tooAzure SQL server ile yüklenmişse, gibi çalıştırabilirsiniz.

Nasıl toomake hello bağlantı tooSQL veritabanı ile ilgili daha fazla bilgi için bkz: [tooSQL veritabanı SQL Server Management Studio ile bağlanma ve örnek T-SQL sorgusu gerçekleştirmeyi](sql-database-connect-query-ssms.md).

Her şeyi şimdilik olmasıdır. Keyfini çıkarın!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png