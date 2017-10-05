---
title: "Azure Remoteapp'te SQL Server Management Studio'yu kullanarak SQL veritabanına bağlanma | Microsoft Docs"
description: "SQL Server Management Studio Azure Remoteapp'te güvenlik ve performans için SQL veritabanına bağlanırken kullanmayı öğrenmek için bu öğreticiyi kullanın"
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
ms.openlocfilehash: ae1f2fa38d38fe6c10bc7960fddb07ae330d1eeb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-to-connect-to-sql-database"></a>Azure RemoteApp SQL veritabanına bağlanmak için SQL Server Management Studio'yu kullanın

> [!IMPORTANT]
> Azure RemoteApp kullanımdan kaldırılıyor. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
>

## <a name="introduction"></a>Giriş
Bu öğretici, SQL Server Management Studio (SSMS) Azure Remoteapp'te SQL veritabanına bağlanmak için nasıl kullanılacağını gösterir. Azure RemoteApp SQL Server Management Studio'da ayarlama işleminde size yol göstermektedir, yararlarını açıklar ve Azure Active Directory'de kullanabileceğiniz güvenlik özellikleri gösterir.

**Tahmini tamamlanma süresi:** 45 dakika

## <a name="ssms-in-azure-remoteapp"></a>Azure RemoteApp SSMS
Azure RemoteApp, uygulamalar sunuyor Azure RDS hizmetidir. Daha fazla bilgi aşağıda öğrenebilirsiniz: [RemoteApp nedir?](../remoteapp/remoteapp-whatis.md)

Azure Remoteapp'te çalıştıran SSMS SSMS yerel olarak çalışan olarak aynı deneyimi sağlar.

![Azure Remoteapp'te çalıştıran SSMS gösteren ekran görüntüsü][1]

## <a name="benefits"></a>Avantajlar
Azure Remoteapp'te SSMS kullanarak birçok avantajları vardır dahil olmak üzere:

* Azure SQL Server 1433 numaralı bağlantı noktasını (Azure dışında) harici olarak gösterilmesine izin yok.
* Ekleme ve IP adreslerini Azure SQL server Güvenlik Duvarı'nda kaldırma tutmak gerek yoktur.
* Tüm Azure RemoteApp bağlantıları HTTPS üzerinden gerçekleşmesi 443 numaralı bağlantı noktasını kullanarak şifrelenmiş Uzak Masaüstü Protokolü
* Çok kullanıcılı ve ölçeklendirebilirsiniz.
* SQL veritabanı ile aynı bölgede SSMS sahip öğesinden bir performans kazancı yoktur.
* Azure RemoteApp kullanımı kullanıcı etkinlik raporları olan Azure Active Directory Premium sürümü ile denetleyebilirsiniz.
* Çok faktörlü kimlik doğrulamasını (MFA) etkinleştirebilirsiniz.
* Herhangi bir yerden herhangi bir iOS, Android, Mac, Windows Phone ve Windows bilgisayarın içeren desteklenen Azure RemoteApp istemcisinde kullanırken SSMS erişim.

## <a name="create-the-azure-remoteapp-collection"></a>Azure RemoteApp koleksiyonu oluşturun
Azure RemoteApp koleksiyonunuzun SSMS ile oluşturmak için adımlar şunlardır:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Yeni bir Windows VM görüntüsünü oluşturma
"Windows Server Uzak Masaüstü Oturumu Ana bilgisayar Windows Server 2012 R2" görüntü galeriden yeni VM yapmak için kullanın.

### <a name="2-install-ssms-from-sql-express"></a>2. SSMS SQL hızlı yükleme
Yeni VM gidin ve bu indirme sayfasına gidin: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Yalnızca SSMS indirmek için bir seçenek yoktur. Yükleme sonra yükleme dizinine gidin ve SSMS yüklemek için Kurulumu çalıştırın.

Ayrıca SQL Server 2014 Service Pack 1 yüklemeniz gerekir. Buradan indirebilirsiniz: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 Azure SQL veritabanı ile çalışmak için gerekli işlevselliği içerir.

### <a name="3-run-validate-script-and-sysprep"></a>3. Doğrulama betiği çalıştırma ve Sysprep
VM masaüstünde bir PowerShell Betiği doğrula adı verilir. Bu, çift tıklayarak dosyayı çalıştırın. VM uzak uygulamaları barındırmak için kullanıma hazır olduğunu doğrular. Doğrulama tamamlandıktan sonra ister Sysprep'i-çalıştırmak seçin.

Sysprep tamamlandığında VM kapatma.

Azure RemoteApp görüntüsü oluşturma hakkında daha fazla bilgi için bkz: [Azure RemoteApp şablon görüntüsü oluşturma](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Yansıma Yakalama
VM çalışmayı durdurdu geçerli portalında bulun ve yakalayın.

Yansıma yakalama hakkında daha fazla bilgi için bkz: [Klasik dağıtım modeli kullanılarak oluşturulmuş bir Azure Windows sanal makine bir görüntüsünü yakalama](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-to-azure-remoteapp-template-images"></a>5. Azure RemoteApp şablon görüntüleri ekleme
Geçerli portal Azure RemoteApp bölümünde, şablon görüntüleri sekmesine gidin ve Ekle'yi tıklatın. Açılır kutusunda "bir görüntü, sanal makineleri kitaplıktan Al" seçin ve ardından yeni oluşturduğunuz görüntüyü seçin.

### <a name="6-create-cloud-collection"></a>6. Bulut koleksiyonu oluşturma
Geçerli portalında yeni bir Azure RemoteApp bulut koleksiyonu oluşturun. Yeni içeri aktardığınız şablon görüntüsü yüklü SSMS ile seçin.

![Yeni bulut koleksiyonu oluşturma][2]

### <a name="7-publish-ssms"></a>7. SSMS yayımlama
Yayımlama, yeni bulut koleksiyonu seçme sekmesinde Başlat menüsünden uygulama yayımlama ve SSMS listeden seçin.

![Uygulama yayımlama][5]

### <a name="8-add-users"></a>8. Kullanıcı ekle
Kullanıcı erişim sekmesinde yalnızca SSMS içeren bu Azure RemoteApp koleksiyonu erişebilecek kullanıcıları seçebilirsiniz.

![Kullanıcı Ekleme][6]

### <a name="9-install-the-azure-remoteapp-client-application"></a>9. Azure RemoteApp istemci uygulaması yükleme
Bir Azure RemoteApp istemcisini yükleyip: [karşıdan | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Azure SQL server yapılandırma
Gerekli yalnızca Azure Hizmetleri için güvenlik duvarını etkinleştirildiğinden emin olmak için yapılandırmadır. Ardından bu çözümü kullanıyorsanız, Güvenlik Duvarı'nı açmak için herhangi bir IP adresi eklemek gerekmez. SQL Server için izin verilen ağ trafiği Azure hizmetlerinden tutulur.

![Azure izin ver][4]

## <a name="multi-factor-authentication-mfa"></a>Çok faktörlü kimlik doğrulaması (MFA)
MFA bu uygulama için özel olarak etkinleştirilebilir. Azure Active Directory'yi uygulamalar sekmesine gidin. Microsoft Azure RemoteApp için bir giriş bulacaksınız. Bu uygulama'yı tıklatın ve ardından yapılandırın, bu uygulama için MFA etkinleştirebilirsiniz sayfası aşağıdaki görürsünüz.

![MFA'yı etkinleştirin][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Azure Active Directory Premium ile kullanıcı etkinliğini denetleyin
Azure AD Premium yoksa dizininize lisansları bölümünde Aç sahip. Etkin Premium ile Premium düzeyine kullanıcılar atayabilirsiniz.

Azure Active Directory'de bir kullanıcıya gidin, sonra Azure RemoteApp için oturum açma bilgilerini görmek için etkinlik sekmesini gidebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Yukarıdaki adımları tamamladıktan sonra Azure RemoteApp istemci çalıştırılabilir ve oturum açma atanmış bir kullanıcı ile olacaktır. SSMS ile uygulamalarınızı biri olarak sunulur ve Azure SQL sunucusuna erişimi olan bilgisayarınızda yüklenmişse, gibi çalıştırabilirsiniz.

SQL veritabanına bağlantı yapma hakkında daha fazla bilgi için bkz: [SQL Server Management Studio ile SQL veritabanına bağlanma ve örnek T-SQL sorgusu gerçekleştirmeyi](sql-database-connect-query-ssms.md).

Her şeyi şimdilik olmasıdır. Keyfini çıkarın!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png