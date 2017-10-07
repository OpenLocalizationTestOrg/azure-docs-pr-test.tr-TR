---
title: "Azure automation'da aaaRole tabanlı erişim denetimi | Microsoft Docs"
description: "Rol tabanlı erişim denetimi (RBAC), Azure kaynakları için erişim yönetimi sağlar. Bu makalede nasıl tooset Azure automation'da RBAC."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "otomasyon rbac, rol tabanlı erişim denetimi, azure rbac"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Azure Automation’da Rol Tabanlı Erişim Denetimi
## <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi
Rol tabanlı erişim denetimi (RBAC), Azure kaynakları için erişim yönetimi sağlar. Kullanarak [RBAC](../active-directory/role-based-access-control-configure.md), ekibiniz içinde görevleri ayırabilirsiniz ve grant yalnızca hello miktarını erişim toousers, grupları ve uygulamaları tooperform işlerini gerekir. Rol tabanlı erişim toousers hello Azure portal, Azure komut satırı araçları ve Azure Management API'leri kullanılarak verilebilir.

## <a name="rbac-in-automation-accounts"></a>Automation Hesaplarında RBAC
Azure Otomasyonu'nda hello uygun RBAC rolü toousers, grupları ve hello Otomasyon hesabı kapsamında uygulamaları atanarak erişim verilir. Aşağıda Automation hesabının desteklediği yerleşik roller hello:  

| **Rol** | **Açıklama** |
|:--- |:--- |
| Sahip |Merhaba sahibi rolü tooall kaynaklarına erişmek ve erişim tooother kullanıcılar, gruplar ve uygulamalar toomanage hello Otomasyon hesabı sağlama dahil olmak üzere bir Otomasyon hesabı içinde eylemler sağlar. |
| Katılımcı |Merhaba katkıda bulunan rolü sağlar, toomanage diğer kullanıcının değiştirme dışında her şeyi erişim izinleri tooan Otomasyon hesabı. |
| Okuyucu |Merhaba okuyucu rolü, tüm hello kaynakları bir Otomasyon hesabı ancak değişiklik yapamazsınız tooview sağlar. |
| Otomasyon Operatörü |Merhaba Automation operatörü rolü gibi başlangıç tooperform işletimsel görevleri sağlar, durdurmak, askıya alma, sürdürme ve işleri zamanlamak. Bu rol tooprotect kimlik bilgileri varlıkları ve engeller runbook'ları gibi Automation hesabı kaynaklarınızın görüntülenemez veya değiştiren istiyorsanız yararlıdır, ancak yine de bu runbook'lar, kuruluş tooexecute üyeleri izin. |
| Kullanıcı Erişimi Yöneticisi |Merhaba kullanıcı erişimi yöneticisi rolü toomanage kullanıcı erişimi tooAzure Automation hesapları sağlar. |

> [!NOTE]
> Erişim hakları tooa belirli runbook'u veya runbook'ları, yalnızca toohello kaynakları ve eylemleri hello Otomasyon hesabı içinde veremezsiniz.  
> 
> 

Bu makalede biz nasıl anlatılır Azure automation'da RBAC tooset. Ancak önce böylece biz herkes vermeden önce bir iyi anlamak daha yakın bir ara hello tek tek izinleri verilen toohello katkıda bulunan, okuyucu, Automation operatörü ve kullanıcı erişimi Yöneticisi Al toohello Otomasyon hesabı şimdi hakları.  Aksi takdirde istenmeyen sonuçlara neden olabilir.     

## <a name="contributor-role-permissions"></a>Katkıda Bulunan rol izinleri
Merhaba aşağıdaki tabloda Otomasyon hello katkıda bulunan rolü tarafından gerçekleştirilen hello belirli eylemleri gösterir.

| **Kaynak Türü** | **Okuma** | **Yazma** | **Silme** | **Diğer Eylemler** |
|:--- |:--- |:--- |:--- |:--- |
| Azure Otomasyonu Hesabı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Otomasyon Sertifika Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Otomasyon Bağlantı Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Otomasyon Bağlantı Türü Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Otomasyon Kimlik Bilgisi Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Otomasyon Zamanlama Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Otomasyon Değişken Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Otomasyon İstenen Durum Yapılandırması | | | |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |
| Karma Runbook Çalışanı Kaynak Türü |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Azure Otomasyonu İşi |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |
| Otomasyon İş Akışı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon İş Zamanlaması |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Otomasyon Modülü |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |
| Azure Otomasyonu Runbook |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |
| Otomasyon Runbook Taslağı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |
| Otomasyon Runbook Taslağı Test İşi |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |
| Otomasyon Web Kancası |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>Okuyucu rol izinleri
Merhaba aşağıdaki tabloda hello okuyucu rolüne Automation tarafından gerçekleştirilen hello belirli eylemleri gösterir.

| **Kaynak Türü** | **Okuma** | **Yazma** | **Silme** | **Diğer Eylemler** |
|:--- |:--- |:--- |:--- |:--- |
| Klasik abonelik yöneticisi |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Yönetim kilidi |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| İzin |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Sağlayıcı işlemleri |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Rol ataması |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Rol tanımı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>Otomasyon Operatörü rol izinleri
Merhaba aşağıdaki tabloda Otomasyon hello Automation operatörü rolü tarafından gerçekleştirilen hello belirli eylemleri gösterir.

| **Kaynak Türü** | **Okuma** | **Yazma** | **Silme** | **Diğer Eylemler** |
|:--- |:--- |:--- |:--- |:--- |
| Azure Otomasyonu Hesabı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Sertifika Varlığı | | | | |
| Otomasyon Bağlantı Varlığı | | | | |
| Otomasyon Bağlantı Türü Varlığı | | | | |
| Otomasyon Kimlik Bilgisi Varlığı | | | | |
| Otomasyon Zamanlama Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | |
| Otomasyon Değişken Varlığı | | | | |
| Otomasyon İstenen Durum Yapılandırması | | | | |
| Karma Runbook Çalışanı Kaynak Türü | | | | |
| Azure Otomasyonu İşi |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |
| Otomasyon İş Akışı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon İş Zamanlaması |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | |
| Otomasyon Modülü | | | | |
| Azure Otomasyonu Runbook |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Runbook Taslağı | | | | |
| Otomasyon Runbook Taslağı Test İşi | | | | |
| Otomasyon Web Kancası | | | | |

Daha fazla ayrıntı için hello [Automation operatörü eylemleri](../active-directory/role-based-access-built-in-roles.md#automation-operator) listeleri hello hello Otomasyon hesabı ve kaynaklarındaki hello Automation operatörü rolünün desteklediği eylemlerin.

## <a name="user-access-administrator-role-permissions"></a>Kullanıcı Erişimi Yöneticisi rol izinleri
Merhaba aşağıdaki tabloda Otomasyon hello kullanıcı erişimi yöneticisi rolü tarafından gerçekleştirilen hello belirli eylemleri gösterir.

| **Kaynak Türü** | **Okuma** | **Yazma** | **Silme** | **Diğer Eylemler** |
|:--- |:--- |:--- |:--- |:--- |
| Azure Otomasyonu Hesabı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Sertifika Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Bağlantı Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Bağlantı Türü Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Kimlik Bilgisi Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Zamanlama Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Değişken Varlığı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon İstenen Durum Yapılandırması | | | | |
| Karma Runbook Çalışanı Kaynak Türü |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Azure Otomasyonu İşi |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon İş Akışı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon İş Zamanlaması |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Modülü |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Azure Otomasyonu Runbook |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Runbook Taslağı |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Runbook Taslağı Test İşi |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Otomasyon Web Kancası |![Yeşil Durum](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Azure Portal kullanarak Automation Hesabınız için RBAC yapılandırma
1. İçinde toohello oturum [Azure Portal](https://portal.azure.com/) ve hello Automation hesapları dikey penceresinden Automation hesabınızı açın.  
2. Tıklatın hello üzerinde **erişim** denetim sağ alt köşesinde hello üstünde. Merhaba açılır **kullanıcılar** ekleyebileceğiniz yeni kullanıcılar, gruplar ve uygulamalar toomanage Automation hesabınız dikey ve yapılandırılabilir görünüm varolan rolleri hello Automation hesabı.  
   
   ![Erişim düğmesi](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **Abonelik yöneticileri** hello varsayılan kullanıcı zaten mevcut. Merhaba abonelik yöneticileri active directory grubu hello hizmet yöneticileri ve ortak yöneticilerini Azure aboneliğiniz için içerir. Hello Hizmet Yöneticisi hello Azure aboneliğinizi ve kaynaklarının sahibidir ve hello sahip rolünü hello Otomasyon hesapları için de devralacaktır. Bu hello erişim anlamına gelir **devralınan** için **hizmet yöneticileri ve ortak yöneticileri** bir abonelik ve buna ait **atanan** tüm diğer kullanıcıların hello için. Tıklatın **abonelik yöneticileri** tooview izinlerini hakkında daha ayrıntılı.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>Yeni kullanıcı ekleme ve rol atama
1. Merhaba kullanıcılar dikey penceresinden tıklayın **Ekle** tooopen hello **erişim Ekle dikey** olduğu bir kullanıcı, Grup veya uygulama ekleyebileceğiniz ve rol toothem atayın.  
   
   ![Kullanıcı ekle](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Bir rolü hello kullanılabilir roller listesinden seçin. Merhaba seçeceğiz **okuyucu** rolü, ancak herhangi bir Otomasyon hesabı destekleyen hello kullanılabilir yerleşik roller veya tanımlamış olduğunuz özel bir rolü seçebilirsiniz.  
   
   ![Rol seç](media/automation-role-based-access-control/automation-03-select-role.png)  
3. Tıklayın **kullanıcıları eklemek** tooopen hello **kullanıcıları eklemek** dikey. Tüm kullanıcıların, grupların veya uygulamaları toomanage eklediyseniz aboneliğinizi sonra bu kullanıcılar listelenir ve tooadd erişim seçebilirsiniz. Kullanıcılar listelenen ya da eklemek hello kullanıcı listelenmemişse, ardından yoksa **davet** tooopen hello **Konuk davet** davet edebildiğiniz geçerli bir Microsoft hesabı olan bir kullanıcı dikey penceresinde e-posta adresi Outlook.com, OneDrive veya Xbox Live kimlikleri gibi. Merhaba kullanıcının hello e-posta adresini girdikten sonra tıklatın **seçin** tooadd hello kullanıcı ve ardından **Tamam**. 
   
   ![Kullanıcı ekle](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   Artık eklenen hello kullanıcı görmelisiniz toohello **kullanıcılar** hello dikey **okuyucu** atanan rolü.  
   
   ![Kullanıcıları listele](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   Merhaba rol toohello kullanıcıdan ayrıca atayabilirsiniz **rolleri** dikey. 
4. Tıklatın **rolleri** hello kullanıcılar dikey tooopen hello gelen **rolleri dikey**. Bu dikey pencereden hello rolünün hello sayısı kullanıcılar ve gruplar toothat rolü atanmış hello adı görüntüleyebilirsiniz.
   
    ![Kullanıcılar dikey penceresinden rol ata](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > Rol tabanlı erişim denetimi yalnızca Automation hesabı düzeyinde hello sırasında ayarlanabilir ve Automation hesabı olmayan herhangi bir kaynağın aşağıdaki hello.
   > 
   > 
   
    Birden fazla rol tooa kullanıcı, Grup veya uygulama atayabilirsiniz. Örneğin, biz hello eklerseniz **Automation operatörü** rolleri hello ile birlikte **okuyucu rolüne** toohello kullanıcı sonra bunlar tüm hello Automation kaynaklarını görüntüleyebilir yanı sıra hello runbook işlerini yürütebilirler. Merhaba açılır tooview atanan rollerin toohello kullanıcı listesini genişletebilirsiniz.  
   
    ![Birden çok rol görüntüle](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>Kullanıcıyı kaldırma
Merhaba kimin hello Automation hesabını yönetiyor değil ya da kimin artık hello kuruluş için çalışmayan bir kullanıcı için erişim izni kaldırabilirsiniz. Aşağıdaki olan hello adımları tooremove kullanıcı: 

1. Merhaba gelen **kullanıcılar** dikey penceresinde, select hello rol ataması tooremove istiyor.
2. Merhaba tıklatın **kaldırmak** hello atama ayrıntıları dikey düğmesini.
3. Tıklatın **Evet** tooconfirm kaldırma. 
   
   ![Kullanıcıları kaldır](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>Rol Atanmış Kullanıcı
Bir kullanıcı tarafından atanan tooa rolü tootheir Otomasyon hesabı açtığında artık hello listesinde listelenen hello sahibin hesabını görebilmeleri **varsayılan dizinler**. Sipariş tooview hello için eklenmiştir Automation hesabı, bunlar hello varsayılan dizin toohello sahibin varsayılan dizinine geçirmelidir.  

![Varsayılan dizin](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>Automation operatörü rolü için kullanıcı deneyimi
Olan bir kullanıcı, atandığı hello Otomasyon hesabı toohello Automation operatörü rolü görünümleri atandığında, runbook'ları yalnızca görünüm hello listesi için runbook işlerini ve zamanlamaları hello Otomasyon hesabı oluşturuldu ancak bunların tanımlarını görüntüleyemez. Bunlar başlatabilir, durdurmak, askıya alma, sürdürme veya hello runbook işi zamanlama. Merhaba kullanıcı yapılandırmalar, karma çalışan grupları veya DSC düğümleri gibi erişim tooother Automation kaynaklarına sahip olmaz.  

![Hiçbir erişim tooresourcres](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Hello kullanıcı hello runbook'a tıkladığında hello Automation operatörü rolü erişim toothem izin vermediğinden hello tooview kaynak hello veya hello runbook'u düzenleyecek komutlar sağlanmaz.  

![Hiçbir erişim tooedit runbook](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

Merhaba kullanıcı erişimi tooview ve toocreate takvimleri vardır ancak erişim tooany başka bir varlık türü sahip olmaz.  

![Hiçbir erişim tooassets](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

Bu kullanıcı erişimi tooview hello runbook'la ilişkili Web kancalarını da sahip değil

![Hiçbir erişim toowebhooks](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Azure PowerShell kullanarak Automation Hesabınız için RBAC yapılandırma
Rol tabanlı erişim de yapılandırılmış tooan Otomasyon hesabı olması hello aşağıdakileri kullanarak [Azure PowerShell cmdlet'lerini](../active-directory/role-based-access-control-manage-access-powershell.md).

• [Get-AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx), Azure Active Directory’de kullanılabilen tüm RBAC rollerini listeler. Bu komutu hello birlikte kullanabilirsiniz **adı** özelliği toolist tüm hello belirli bir rol tarafından gerçekleştirilen eylemler.  
    **Örnek:**  
    ![Rol tanımı al](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) listeleri hello adresindeki Azure AD RBAC rolü atamalarını Belirtilen kapsam. Hiçbir parametre olmadan, bu komut hello abonelik altında yapılan tüm hello rol atamalarını döndürür. Kullanım hello **ExpandPrincipalGroups** parametresi toolist erişim atamalarını hello grupların yanı sıra kullanıcı hello kullanıcı hello belirtilen için bir üyesidir.  
    **Örnek:** kullanım hello aşağıdaki tüm hello kullanıcıları ve rollerini Otomasyon hesabı içinde toolist komutu.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![Rol ataması al](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign erişim toousers, gruplar ve uygulamalar tooa belirli kapsamı.  
    **Örnek:** kullanım hello aşağıdaki tooassign hello "Automation operatör" rolü hello Otomasyon hesabı kapsamında bir kullanıcı için komutu.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![Yeni rol ataması](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• Kullanım [Remove-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) belirtilen kullanıcı, Grup veya belirli bir kapsam uygulamadan tooremove erişim.  
    **Örnek:** kullanım hello şu komutu tooremove hello kullanıcıdan hello Otomasyon hesabı kapsamında hello "Automation operatör" rolü.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

Örnekleri yukarıda Hello yerine **kimliğinde oturum**, **abonelik kimliği**, **kaynak grubu adı** ve **Automation hesabı adını** ile Hesap ayrıntıları. Seçin **Evet** zaman tooremove kullanıcı rol ataması devam etmeden önce tooconfirm istenir.   

## <a name="next-steps"></a>Sonraki Adımlar
* Azure otomasyonu için farklı yollar tooconfigure RBAC hakkında bilgi için çok başvuran[Azure PowerShell ile RBAC yönetme](../active-directory/role-based-access-control-manage-access-powershell.md).
* Farklı şekillerde toostart bir runbook hakkında daha fazla bilgi için bkz: [runbook başlatma](automation-starting-a-runbook.md)
* Farklı runbook türleri hakkında daha fazla bilgi için çok bakın[Azure Automation runbook türleri](automation-runbook-types.md)

