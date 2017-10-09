---
title: "aaaConfigure Azure Active Directory kimlik doğrulaması - SQL | Microsoft Docs"
description: "Bilgi nasıl tooconnect tooSQL veritabanı ve Azure Active Directory kimlik doğrulamasını kullanarak SQL Data Warehouse."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Yapılandırma ve SQL Database veya SQL Data Warehouse ile Azure Active Directory kimlik doğrulaması yönetme

Bu makale size nasıl gösterir toocreate ve Azure AD doldurun ve ardından Azure SQL Database ve SQL Data Warehouse ile Azure AD kullanın. Genel bir bakış için bkz: [Azure Active Directory kimlik doğrulaması](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Bir Azure VM çalıştıran sunucu bir Azure Active Directory hesabı kullanarak desteklenmiyor tooSQL bağlanılıyor. Etki alanı Active Directory hesabı kullanın.

## <a name="create-and-populate-an-azure-ad"></a>Oluşturma ve Azure AD doldurma
Azure AD oluşturabilir ve kullanıcılar ve gruplar ile doldurabilirsiniz. Azure AD hello ilk etki alanı Azure AD yönetilen etki alanı olabilir. Azure AD, bir şirket içi Active Directory etki alanı hello Azure AD ile Federasyon Hizmetleri de olabilir.

Daha fazla bilgi için bkz: [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](../active-directory/active-directory-aadconnect.md), [kendi etki alanı adı tooAzure AD eklemek](../active-directory/active-directory-add-domain.md), [Microsoft Azure artık, Federasyon ile destekler Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Azure AD dizininizi yönetme](https://msdn.microsoft.com/library/azure/hh967611.aspx), [Yönet Windows PowerShell kullanarak Azure AD](/powershell/azure/overview?view=azureadps-2.0), ve [karma kimlik Gerekli bağlantı noktalarını ve protokolleri](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>İsteğe bağlı: İlişkilendir ya da şu anda Azure aboneliğinizle ilişkili hello active directory değiştirme
tooassociate veritabanınızı, kuruluşunuz için hello Azure AD diziniyle hello dizin hello Azure aboneliği barındırma hello veritabanı için güvenilen bir dizin olun. Daha fazla bilgi için bkz. [Azure aboneliklerinin Azure AD ile ilişkisi](https://msdn.microsoft.com/library/azure/dn629581.aspx).

**Ek bilgi:** her Azure aboneliği Azure AD örneğiyle birlikte bir güven ilişkisi vardır. Bu dizin tooauthenticate güvenler bu anlamına gelir kullanıcılar, hizmetler ve cihazlar. Birden çok abonelik hello güvenebileceği aynı dizinde, ancak bir abonelik yalnızca bir dizine güvenir. Aboneliğinizi hello altında hangi dizine güvendiği görebilirsiniz **ayarları** adresindeki sekmesinde [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Bir aboneliğin bir dizinle arasındaki bu güven ilişkisini daha fazla abonelik alt kaynakları gibi olan tüm diğer azure'deki kaynaklarla (Web siteleri, veritabanları ve benzeri) bir aboneliğe sahip hello ilişki benzemez. Bir abonelik süresi dolmadan sonra toothose hello aboneliği ile ilişkili diğer kaynaklara erişim de durdurulur. Ancak hello dizin Azure içinde kalır ve başka bir aboneliği bu dizinle ilişkilendirebilir ve toomanage hello dizin kullanıcılar devam edebilirsiniz. Kaynaklar hakkında daha fazla bilgi için bkz: [azure'da kaynak erişimini anlama](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Merhaba aşağıdaki yordamlar belirli bir aboneliğe ilişkin dizin toochange hello nasıl ilişkili gösterir.
1. Tooyour bağlanmak [Klasik Azure portalı](https://manage.windowsazure.com/) Azure Abonelik Yöneticisi kullanarak.
2. Merhaba sol başlığında, seçin **ayarları**.
3. Aboneliklerinizi hello ayarları ekranında görüntülenir. Hello abonelik görünmez isterseniz tıklayın **abonelikleri** hello hello üstünde bırakma **FİLTRESİ tarafından dizin** kutusunda ve aboneliklerinizi içeren hello dizin seçin ve ardından **UYGULA**.
   
    ![Abonelik seç][4]
4. Merhaba, **ayarları** alanında, aboneliğinizi tıklayın ve ardından **dizini Düzenle** hello sayfanın hello sonundaki.
   
    ![ad ayarları portalı][5]
5. Merhaba, **dizini Düzenle** kutusunda, hello SQL Server veya SQL Data Warehouse ile ilişkili Azure Active Directory seçin ve ardından İleri hello oka tıklayın.
   
    ![Düzen dizini seçin][6]
6. Merhaba, **Onayla** dizin eşleme iletişim kutusunu Onayla "**tüm ortak Yöneticiler kaldırılır.**"
   
    ![Edit directory onaylayın][7]
7. Merhaba onay tooreload hello portal'ı tıklatın.

   > [!NOTE]
   > Ne zaman hello dizin, erişim tooall ortak Yöneticiler, Azure AD kullanıcıları ve grupları, değiştirmek ve yedeklenen dizin kaynak kullanıcıları kaldırılır ve artık erişim toothis abonelik veya kaynaklarına sahiptir. Yalnızca, Hizmet Yöneticisi olarak, erişim hello yeni dizinine göre Sorumlular için yapılandırabilirsiniz. Bu değişiklik, önemli miktarda zaman toopropagate tooall kaynak sürebilir. Merhaba dizinini değiştirme, ayrıca değişiklikleri SQL Database ve SQL Data Warehouse için Azure AD Yöneticisi hello ve mevcut Azure AD kullanıcısı için veritabanı erişimine izin vermeyecek. Azure AD Hello Yöneticisi olması gerekir (aşağıda açıklandığı gibi) sıfırlama ve yeni Azure AD kullanıcıları oluşturulmalıdır.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Azure SQL server için Azure AD Yöneticisi oluşturma
(Bu, bir SQL veritabanı ya da SQL veri ambarı barındıran) her bir Azure SQL server hello tüm Azure SQL server'ın hello yöneticisi olan bir tek sunucu yöneticisi hesabı ile başlar. İkinci bir SQL Server Yöneticisi, bir Azure AD hesabı olan oluşturulması gerekir. Bu asıl hello ana veritabanında bir kapsanan veritabanı kullanıcı olarak oluşturulur. Yönetici olarak hello server yönetici hesabı hello üyesi **db_owner** her kullanıcı rolünde veritabanı ve her bir kullanıcı veritabanını hello girin **dbo** kullanıcı. Merhaba sunucu yönetici hesapları hakkında daha fazla bilgi için bkz: [yönetme veritabanları ve oturum açma bilgileri Azure SQL veritabanında](sql-database-manage-logins.md).

Azure Active Directory coğrafi çoğaltma ile kullanırken, hello Azure Active Directory Yöneticisi hello birincil ve ikincil sunucular hello için yapılandırılması gerekir. Daha sonra bir sunucu bir Azure Active Directory yönetici yoksa, Azure Active Directory oturumları ve kullanıcıları bir "bağlanılamıyor" tooserver hatası alırsınız.

> [!NOTE]
> (Hello Azure SQL server yönetici hesabı dahil) bir Azure AD hesabında dayalı olmayan kullanıcılar hello Azure AD ile veritabanı kullanıcıları önerilen izni toovalidate olmadığı için Azure AD tabanlı kullanıcılar, oluşturamıyor.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Azure Active Directory yönetici Azure SQL sunucunuzun sağlama

Aşağıdaki iki yordamlarını hello Göster, nasıl tooprovision Azure SQL sunucunuza hello Azure portal ve PowerShell kullanarak Azure Active Directory Yöneticisi.

### <a name="azure-portal"></a>Azure portalına
1. Merhaba, [Azure portal](https://portal.azure.com/), buna hello sağ üst köşesinde, olası Active dizinlerin listesini aşağı, bağlantı toodrop'ı tıklatın. Merhaba seçin Azure AD hello varsayılan olarak Active Directory düzeltin. Bu adım bağlantılar hello abonelik ilişkisi Active Directory ile aynı abonelik hello emin Azure SQL server ile her ikisi için kullanılan Azure AD ve SQL Server. (hello Azure SQL Azure SQL Database veya Azure SQL Data Warehouse barındırma sunucusu.)   
    ![ad seçin][8]   
    
2. Başlık seçin sol hello içinde **SQL sunucuları**seçin, **SQL server**ve ardından hello **SQL Server** dikey penceresinde tıklatın **Active Directory Yöneticisi**.   
3. Merhaba, **Active Directory Yönetim** dikey penceresinde tıklatın **ayarlamak yönetici**.   
    ![Active Directory'yi seçin](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. Merhaba, **yönetici ekleme** dikey penceresinde, bir kullanıcı, select hello kullanıcı veya grup toobe yönetici için arama yapın ve ardından **seçin**. (tüm üyeleri ve grupları, Active Directory hello Active Directory Yönetim dikey gösterir. Kullanıcıları veya gri renkte grupları Azure AD Yöneticiler desteklenmediği için seçilemez. (Merhaba desteklenen admins hello listesini **Azure AD özelliklerini ve sınırlamalarını** bölümünü [Azure Active Directory kimlik doğrulamasını kullan SQL Database veya SQL Data Warehouse ile kimlik doğrulaması için](sql-database-aad-authentication.md).) Rol tabanlı erişim denetimi (RBAC) yalnızca toohello portalı uygular ve yayılan tooSQL sunucusu değil.   
    ![yönetici seçin](./media/sql-database-aad-authentication/select-admin.png)  
    
5. Merhaba hello üstündeki **Active Directory Yöneticisi** dikey penceresinde tıklatın **KAYDETMEK**.   
    ![Yönetici Kaydet](./media/sql-database-aad-authentication/save-admin.png)   

hello Yöneticisi değiştirme hello işlemi birkaç dakika sürebilir. Merhaba yeni yönetici hello görünür sonra **Active Directory Yöneticisi** kutusu.

   > [!NOTE]
   > Hello Azure AD yönetim ayarlarken hello yeni yönetici adı (kullanıcı veya grup) zaten bir SQL Server kimlik doğrulama kullanıcı olarak hello sanal ana veritabanında var olamaz. Varsa, hello Azure AD yönetim kurulum başarısız olur; Bu oluşturma geri alınıyor ve böyle bir yöneticinin (ad) zaten belirten bulunmaktadır. Böyle bir SQL Server kimlik doğrulama kullanıcı hello Azure AD parçası olmadığından, Azure AD kimlik doğrulaması kullanan tüm çaba tooconnect toohello server başarısız olur.
   > 


toolater kaldırmak hello hello üstündeki bir yönetici **Active Directory Yönetim** dikey penceresinde tıklatın **kaldırmak yönetici**ve ardından **kaydetmek**.

### <a name="powershell"></a>PowerShell
toorun PowerShell cmdlet'leri, toohave Azure yüklü ve çalışan PowerShell gerekir. Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

bir Azure AD yönetim tooprovision Azure PowerShell komutlarını aşağıdaki hello yürütün:

* Add-AzureRmAccount
* Select-AzureRmSubscription

Cmdlet'leri tooprovision kullanılan ve Azure AD yönetim yönetebilirsiniz:

| Cmdlet adı | Açıklama |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Azure SQL server veya Azure SQL Data Warehouse için Azure Active Directory yönetici sağlar. (Merhaba geçerli abonelikten olması gerekir.) |
| [Remove-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Azure SQL server veya Azure SQL Data Warehouse için Azure Active Directory yönetici kaldırır. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Hello Azure SQL sunucusu veya Azure SQL Data Warehouse için yapılandırılmış bir Azure Active Directory Yöneticisi hakkında bilgi verir. |

PowerShell komutu get-help toosee daha ayrıntılı her bu komutları için örneğin kullanma ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Azure AD yönetici grubuna adlı komut dosyası hazırlar aşağıdaki hello **DBA_Group** (nesne kimliği `40b79501-b343-44ed-9ce7-da4c8cc7353f`) hello için **demo_server** adlı bir kaynak grubunda sunucu **Grup 23** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Merhaba **DisplayName** giriş parametresi hello Azure AD görünen adı veya kullanıcı asıl adı hello kabul eder. Örneğin, ``DisplayName="John Smith"`` ve ``DisplayName="johns@contoso.com"``. Azure AD grupları yalnızca hello için Azure AD görünen adı desteklenir.

> [!NOTE]
> Hello Azure PowerShell komutunu ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` desteklenmeyen kullanıcılar için Azure AD yöneticileri sağlama engellemez. Desteklenmeyen bir kullanıcı sağlanabilir ancak tooa veritabanına bağlanamıyor. 
> 

Merhaba aşağıdaki örnek kullanır hello isteğe bağlı **objectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Hello Azure AD **objectID** hello gereklidir **DisplayName** benzersiz değil. tooretrieve hello **objectID** ve **DisplayName** değerleri, Klasik Azure portalı hello Active Directory bölümünü kullanın ve bir kullanıcı veya grup hello özelliklerini görüntüleme.
> 

Aşağıdaki örnek hello Azure SQL server için geçerli Azure AD hello Yöneticisi hakkında bilgi verir:

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

Aşağıdaki örnek hello Azure AD yönetici kaldırır:

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

Azure Active Directory yönetici hello REST API'lerini kullanarak da sağlayabilirsiniz. Daha fazla bilgi için bkz: [Hizmet Yönetimi REST API Başvurusu ve Azure SQL veritabanları için Azure SQL veritabanı işlemleri için işlemler](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>CLI  
Ayrıca, bir Azure AD yönetim CLI komutları aşağıdaki arama hello tarafından sağlayabilirsiniz:
| Komut | Açıklama |
| --- | --- |
|[az sql server ad-Yöneticisi oluşturma](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Azure SQL server veya Azure SQL Data Warehouse için Azure Active Directory yönetici sağlar. (Merhaba geçerli abonelikten olması gerekir.) |
|[az sql server yönetici ad silme](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Azure SQL server veya Azure SQL Data Warehouse için Azure Active Directory yönetici kaldırır. |
|[az sql server yönetici ad listesi](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Hello Azure SQL sunucusu veya Azure SQL Data Warehouse için yapılandırılmış bir Azure Active Directory Yöneticisi hakkında bilgi verir. |
|[az sql server ad Yönetim Güncelleştirme](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Bir Azure SQL sunucusu veya Azure SQL Data Warehouse için Hello Active Directory Yöneticisi güncelleştirir. |

CLI komutları hakkında daha fazla bilgi için bkz: [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>İstemci bilgisayarları yapılandırın
Uygulama veya kullanıcıların tooAzure SQL veritabanı veya Azure SQL Data Warehouse kullanarak Azure AD kimlikleri bağlanmak tüm istemci bilgisayarlarında yazılım aşağıdaki hello yüklemeniz gerekir:

* .NET framework 4.6 veya sonrası gelen [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* SQL Server için Azure Active Directory kimlik doğrulama kitaplığı (**ADALSQL. DLL**) birden çok dilde kullanılabilir (x86 ve amd64) hello İndirme Merkezi'nden [Microsoft Active Directory kimlik doğrulama kitaplığı için Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

Tarafından bu gereksinimleri karşılayabilirsiniz:

* Ya da yükleme [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) veya [SQL Server veri araçları Visual Studio 2015 için](https://msdn.microsoft.com/library/mt204009.aspx) hello .NET Framework 4.6 gereksinimi karşılar.
* SSMS hello x86 sürümünü yükler **ADALSQL. DLL**.
* SSDT hello amd64 sürümünü yükler **ADALSQL. DLL**.
* Merhaba en son Visual Studio'dan [Visual Studio indirmeleri](https://www.visualstudio.com/downloads/download-visual-studio-vs) hello .NET Framework 4.6 gereksinimini karşılıyor ancak hello gerekli amd64 sürümü yüklemez **ADALSQL. DLL**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Kapsanan veritabanı kullanıcıları, eşlenen veritabanı tooAzure AD kimlikleri oluşturma

Azure Active Directory kimlik doğrulaması kapsanan veritabanı kullanıcıları oluşturulan veritabanı kullanıcıları toobe gerektirir. Bir Azure AD kimliğine göre bir kapsanan veritabanı kullanıcı, bir oturum açma hello ana veritabanında yok ve hangi eşlemeleri tooan kimliğinde hello hello veritabanıyla ilişkili Azure AD dizini bir veritabanı kullanıcısı değil. Hello Azure AD kimlik bireysel bir kullanıcı hesabı veya bir grup olabilir. Kapsanan veritabanı kullanıcıları hakkında daha fazla bilgi için bkz: [bulunan veritabanı kullanıcıları yapma bilgisayarınızı veritabanı taşınabilir](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Portal kullanarak veritabanı kullanıcıları (Yöneticiler hello durumla) oluşturulamıyor. RBAC rolleri yayılan tooSQL Server, SQL Database veya SQL Data Warehouse değildir. Azure RBAC rolleri Azure kaynaklarını yönetmek için kullanılır ve toodatabase izinleri geçerli değildir. Örneğin, hello **SQL Server Katılımcısı** rol erişim tooconnect toohello SQL Database veya SQL Data Warehouse vermez. Transact-SQL deyimlerini kullanarak doğrudan hello veritabanında Hello erişim izni verilmesi gerekir.
>

en az bir Azure AD tabanlı bulunan veritabanı kullanıcı (Merhaba veritabanı sahibi hello sunucu yönetici dışında), bir kullanıcı olarak bir Azure AD kimlik ile toohello veritabanı bağlanmak toocreate hello **ALTER herhangi bir kullanıcı** izni. Ardından, Transact-SQL söz dizimi aşağıdaki hello kullanın:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* hello kullanıcı asıl adı bir Azure AD kullanıcı veya hello görünen adı Azure AD grubu ile ilgili olabilir.

**Örnekler:** toocreate Azure AD temsil eden bir kapsanan veritabanı kullanıcı federe veya yönetilen etki alanı kullanıcısı:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

Azure AD temsil eden veya etki alanı grubu federe bir kapsanan veritabanı kullanıcı toocreate hello görünen bir güvenlik grubu adını sağlayın:
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate bir uygulamayı temsil eden bir kapsanan veritabanı kullanıcısı, bir Azure AD belirteci kullanarak bağlanır:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  Merhaba, Azure aboneliğinizle ilişkili Azure Active Directory dışındaki bir Azure Active Directory'den kullanıcı doğrudan oluşturulamıyor. Ancak, Active Directory hello içeri aktarılan kullanıcılar olan diğer etkin dizinleri üyeleri ilişkili (dış kullanıcılar olarak bilinir) eklenebilir tooan Active Directory grubu hello Kiracı Active Directory. Bu AD grubu için kapsanan veritabanı kullanıcı oluşturarak hello hello kullanıcılardan dış Active Directory erişim tooSQL veritabanı kaynaklara erişebilir.   

Bulunan oluşturma hakkında daha fazla bilgi için veritabanı kullanıcıları Azure Active Directory kimliği temel, bakın [kullanıcı oluştur (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Azure SQL server kaldırma hello Azure Active Directory Yöneticisi herhangi bir Azure AD kimlik doğrulama kullanıcı toohello sunucu bağlanmasını engeller. Gerekli olduğunda, kullanılamaz Azure AD kullanıcıları bırakılan el ile bir SQL veritabanı yöneticisi tarafından.   

>  [!NOTE]
>  Alırsanız, bir **bağlantı zaman aşımı süresi doldu**, tooset hello gerekebilir `TransparentNetworkIPResolution` hello bağlantı dizesi toofalse parametresi. Daha fazla bilgi için bkz: [bağlantı zaman aşımı .NET Framework 4.6.1 - TransparentNetworkIPResolution sorun](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).   

   
Bir veritabanı kullanıcısı oluşturduğunuzda, bu kullanıcının hello aldığı **BAĞLAN** izni ve toothat veritabanı hello bir üyesi olarak bağlanabilir **ortak** rol. Başlangıçta yalnızca kullanılabilir toohello kullanıcı olan tüm izinlerin toohello izinleri hello **ortak** rol ya da herhangi bir izin verilen tooany Windows gruplarının bir üyesi olduğundan emin. Hello kullanıcı ek izinler vermeniz bir Azure AD tabanlı bulunan veritabanı kullanıcısı, sağlama sonra aynı şekilde türdeki başka kullanıcı izni tooany vermek gibi hello. Genellikle toodatabase rolleri izinleri ve kullanıcıların tooroles ekleyin. Daha fazla bilgi için bkz: [veritabanı altyapısı izni Temelleri](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx). Özel SQL veritabanı rolleri hakkında daha fazla bilgi için bkz: [yönetme veritabanları ve oturum açma bilgileri Azure SQL veritabanında](sql-database-manage-logins.md).
Bir Yönet etki alanına içe aktarılan bir Federasyon etki alanı kullanıcısı hello yönetilen etki alanı kimliği kullanmanız gerekir.

> [!NOTE]
> Azure AD kullanıcıları hello veritabanı meta verilerde E (EXTERNAL_USER) türüyle ve grupları için türü X (EXTERNAL_GROUPS) ile işaretlenir. Daha fazla bilgi için bkz: [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>SSMS veya SSDT kullanarak bağlantı toohello kullanıcı veritabanı veya veri ambarı  
tooconfirm hello Azure AD yönetici düzgün ayarlandığından, toohello bağlanmak **ana** hello Azure AD yönetici hesabını kullanarak veritabanı.
tooprovision bir Azure AD tabanlı bulunan veritabanı kullanıcı (Merhaba veritabanı sahibi hello sunucu yönetici dışında), access toohello veritabanı olan bir Azure AD kimlik toohello veritabanı bağlayın.

> [!IMPORTANT]
> Azure Active Directory kimlik doğrulaması için destek ile kullanılabilir [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) ve [SQL Server veri Araçları](https://msdn.microsoft.com/library/mt204009.aspx) Visual Studio 2015'te. Merhaba SSMS Ağustos 2016 sürümünü de Active Directory Evrensel yöneticilerin sağlayan kimlik doğrulaması için destek içerir toorequire bir telefon araması, SMS mesajı, akıllı kart PIN ya da mobil uygulama bildirimi kullanarak çok faktörlü kimlik doğrulaması.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>SSMS veya SSDT kullanarak bir Azure AD kimlik tooconnect kullanma  

yordamları izleyerek hello nasıl tooconnect tooa SQL veritabanı SQL Server Management Studio veya SQL Server veritabanı araçları kullanarak bir Azure AD kimlik ile gösterir.

### <a name="active-directory-integrated-authentication"></a>Active Directory tümleşik kimlik doğrulaması

Bir Federasyon etki alanına ait Azure Active Directory kimlik bilgilerinizi kullanarak tooWindows kaydedilir, bu yöntemi kullanın.

1. Management Studio veya veri araçları başlatın ve hello **tooServer bağlanmak** (veya **tooDatabase altyapısı bağlanmak**) iletişim kutusunda hello **kimlik doğrulaması** kutusunda, seçin**Active Directory - tümleşik**. Parolasız gerekli olduğunu veya varolan kimlik bilgilerinizi hello bağlantı için sunulur çünkü girilebilir.   

    ![AD tümleşik kimlik doğrulaması seçin][11]
2. Merhaba tıklatın **seçenekleri** düğmesi ve hello **bağlantı özelliklerini** sayfasında hello **toodatabase bağlanmak** kutusu, tür hello adı tooconnect istediğiniz hello kullanıcı veritabanı Hedef. (Merhaba **AD etki alanı adı veya Kiracı kimliği**"seçeneği için desteklenen yalnızca **MFA bağlantısıyla Evrensel** seçenekleri, aksi takdirde, griyse.)  

    ![Merhaba veritabanı adını seçin][13]

## <a name="active-directory-password-authentication"></a>Active Directory parola kimlik doğrulaması

Bir Azure AD asıl adı Hello Azure AD kullanarak bağlanma etki alanı yönetildiğinde bu yöntemi kullanın. Uzaktan çalışırken, örneğin erişim toohello etki alanı olmayan birleştirilmiş hesap için de kullanabilirsiniz.

Azure ile Federasyon olmayan bir etki alanı kimlik bilgilerini kullanarak tooWindows kaydedilir veya Azure AD kimlik doğrulaması kullanarak kullanırken, Azure AD hello ilk dayalı'yı veya istemci etki alanı hello bu yöntemi kullanın.

1. Management Studio veya veri araçları başlatın ve hello **tooServer bağlanmak** (veya **tooDatabase altyapısı bağlanmak**) iletişim kutusunda hello **kimlik doğrulaması** kutusunda, seçin**Active Directory - parola**.
2. Merhaba, **kullanıcı adı** hello biçiminde Azure Active Directory kullanıcı adınızı yazın  **username@domain.com** . Bu bir hesaptan hello Azure Active Directory olmalıdır veya bir etki alanındaki bir hesabı hello Azure Active Directory ile birleştirmek.
3. Merhaba, **parola** kutusunda hello Azure Active Directory hesabı için kullanıcı parolanızı yazın veya Federasyon etki alanı hesabı.

    ![AD parola kimlik doğrulaması][12]
4. Merhaba tıklatın **seçenekleri** düğmesi ve hello **bağlantı özelliklerini** sayfasında hello **toodatabase bağlanmak** kutusu, tür hello adı tooconnect istediğiniz hello kullanıcı veritabanı Hedef. (Merhaba önceki seçenek hello grafikte bakın.)

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>Bir istemci uygulamadan bir Azure AD kimlik tooconnect kullanma

yordamları izleyerek hello nasıl tooconnect tooa SQL veritabanı ile bir istemci uygulamadan bir Azure AD kimlik gösterir.

###  <a name="active-directory-integrated-authentication"></a>Active Directory tümleşik kimlik doğrulaması

toouse tümleşik Windows kimlik doğrulaması, etki alanınızın Active Directory, Azure Active Directory ile Federasyon gerekir. Toohello veritabanına bağlanma istemci uygulamanız (veya bir hizmeti), bir etki alanına katılmış makinede kullanıcının etki alanı kimlik bilgileri altında çalışmalıdır.

tümleşik kimlik doğrulaması ve Azure AD kimlik tooconnect tooa veritabanı kullanarak, hello kimlik doğrulama anahtar sözcüğü hello veritabanı bağlantı dizesinde tooActive Directory tümleşik ayarlamanız gerekir. Merhaba aşağıdaki C# kod örneği ADO .NET kullanır.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

bağlantı dizesi anahtar sözcüğü hello ``Integrated Security=True`` tooAzure SQL veritabanına bağlanmak için desteklenmiyor. ODBC bağlantısı yaparken tooremove alanları ihtiyacınız ve kimlik doğrulama too'ActiveDirectoryIntegrated ayarlayın '.

### <a name="active-directory-password-authentication"></a>Active Directory parola kimlik doğrulaması

tümleşik kimlik doğrulaması ve Azure AD kimlik tooconnect tooa veritabanı kullanarak, hello kimlik doğrulama anahtar sözcüğü tooActive dizin parolası ayarlamanız gerekir. Merhaba bağlantı dizesi, kullanıcı kimliği/kullanıcı kimliği ve parola/PWD anahtar sözcükleri ve değerleri içermesi gerekir. Merhaba aşağıdaki C# kod örneği ADO .NET kullanır.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Merhaba demo kod örnekleri adresinde kullanarak Azure AD kimlik doğrulama yöntemleri hakkında daha fazla bilgi [Azure AD kimlik doğrulama GitHub Demo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Azure AD simgesi
Bu kimlik doğrulama yöntemi, Azure Active Directory (AAD gelen) bir belirteç elde ederek orta katman Hizmetleri tooconnect tooAzure SQL veritabanına veya Azure SQL Data Warehouse sağlar. Sertifika tabanlı kimlik doğrulaması dahil olmak üzere Gelişmiş senaryoları etkinleştirir. Dört temel adımlar toouse Azure AD belirteci kimlik doğrulaması tamamlamanız gerekir:

1. Azure Active Directory ile uygulamanızı kaydetme ve kodunuz için hello istemci kimliği alın. 
2. Bir veritabanı kullanıcı temsil eden hello uygulaması oluşturun. (6. adımda daha önce tamamlandı.)
3. Bir sertifika hello istemci bilgisayar çalışır Merhaba uygulaması oluşturun.
4. Uygulamanız için bir anahtar olarak Hello sertifika ekleyin.

Örnek bağlantı dizesi:

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Daha fazla bilgi için bkz: [SQL Server güvenlik blogu](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).

### <a name="sqlcmd"></a>sqlcmd

Merhaba deyimleri, hello kullanılabilir sqlcmd 13,1 sürümünü kullanarak bağlan [Yükleme Merkezi'nden](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Sonraki adımlar
- SQL Veritabanında erişim ve denetime genel bakış için bkz. [SQL Veritabanında erişim ve denetim](sql-database-control-access.md).
- SQL Veritabanındaki oturum açma bilgileri, kullanıcılar ve veritabanı rollerine genel bakış için bkz. [Oturum açma bilgileri, kullanıcılar ve veritabanı rolleri](sql-database-manage-logins.md).
- Veritabanı sorumluları hakkında daha fazla bilgi için bkz. [Sorumlular](https://msdn.microsoft.com/library/ms181127.aspx).
- Veritabanı rolleri hakkında daha fazla bilgi için bkz. [Veritabanı rolleri](https://msdn.microsoft.com/library/ms189121.aspx).
- SQL Veritabanındaki güvenlik duvarı kuralları hakkında daha fazla bilgi için bkz. [SQL Veritabanı güvenlik duvarı kuralları](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

