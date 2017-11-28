---
title: "Bağlayıcısı sürüm yayımlama geçmişi | Microsoft Docs"
description: "Bu konu bağlayıcıları tüm sürümleri, Forefront Identity Manager (FIM) ve Microsoft Identity Manager (MIM) için listeler."
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="0d870-103">Bağlayıcı Sürümü Yayınlama Geçmişi</span><span class="sxs-lookup"><span data-stu-id="0d870-103">Connector Version Release History</span></span>
<span data-ttu-id="0d870-104">Forefront Identity Manager (FIM) ve Microsoft Identity Manager (MIM) bağlayıcıları sık sık güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="0d870-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="0d870-105">Bu konuda FIM ve MIM yalnızca bilinmiyor.</span><span class="sxs-lookup"><span data-stu-id="0d870-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="0d870-106">Bu bağlayıcıların üzerinde Azure AD Connect yüklemesi için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0d870-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="0d870-107">Yükseltme yapı belirtildiğinde yayımlanan bağlayıcılar AADConnect üzerinde önceden yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="0d870-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="0d870-108">Bu konuda çıkarılan bağlayıcılarının tüm sürümlerini listeler.</span><span class="sxs-lookup"><span data-stu-id="0d870-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="0d870-109">İlgili bağlantılar:</span><span class="sxs-lookup"><span data-stu-id="0d870-109">Related links:</span></span>

* [<span data-ttu-id="0d870-110">En son bağlayıcılar indirin</span><span class="sxs-lookup"><span data-stu-id="0d870-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="0d870-111">[Genel LDAP Bağlayıcısı](active-directory-aadconnectsync-connector-genericldap.md) başvuru belgelerini</span><span class="sxs-lookup"><span data-stu-id="0d870-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="0d870-112">[Genel SQL bağlayıcı](active-directory-aadconnectsync-connector-genericsql.md) başvuru belgelerini</span><span class="sxs-lookup"><span data-stu-id="0d870-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="0d870-113">[Web Hizmetleri Bağlayıcısı](http://go.microsoft.com/fwlink/?LinkID=226245) başvuru belgelerini</span><span class="sxs-lookup"><span data-stu-id="0d870-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="0d870-114">[PowerShell Bağlayıcısı](active-directory-aadconnectsync-connector-powershell.md) başvuru belgelerini</span><span class="sxs-lookup"><span data-stu-id="0d870-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="0d870-115">[Lotus Domino Bağlayıcısı](active-directory-aadconnectsync-connector-domino.md) başvuru belgelerini</span><span class="sxs-lookup"><span data-stu-id="0d870-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="0d870-116">1.1.604.0 (sürüm bekleyen AADConnect)</span><span class="sxs-lookup"><span data-stu-id="0d870-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="0d870-117">Giderilen sorunlar:</span><span class="sxs-lookup"><span data-stu-id="0d870-117">Fixed issues:</span></span>

* <span data-ttu-id="0d870-118">Genel Web Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="0d870-118">Generic Web Services:</span></span>
  * <span data-ttu-id="0d870-119">İki veya daha fazla uç noktaları zamanki oluşturulan bir SOAP proje engelleyen bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0d870-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="0d870-120">Genel SQL:</span><span class="sxs-lookup"><span data-stu-id="0d870-120">Generic SQL:</span></span>
  * <span data-ttu-id="0d870-121">Alma işleminde GSQL saati doğru bağlayıcı alanı kaydedildiğinde dönüştürülürken değil.</span><span class="sxs-lookup"><span data-stu-id="0d870-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="0d870-122">GSQL bağlayıcı alanı için varsayılan tarih ve saat Biçim 'yyyy-aa-gg: ssZ ', 'yyyy-aa-gg için: ssZ' değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="0d870-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="0d870-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="0d870-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="0d870-124">Giderilen sorunlar:</span><span class="sxs-lookup"><span data-stu-id="0d870-124">Fixed issues:</span></span>

* <span data-ttu-id="0d870-125">Genel Web Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="0d870-125">Generic Web Services:</span></span>
  * <span data-ttu-id="0d870-126">Wsconfig Aracı'nı doğru şekilde isteğinden"örnek" REST hizmeti yöntemi için Json dizisi dönüştürmemenizi.</span><span class="sxs-lookup"><span data-stu-id="0d870-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="0d870-127">Bu, bu Json dizisi REST isteği için seri hale getirme sorunlara neden oldu.</span><span class="sxs-lookup"><span data-stu-id="0d870-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="0d870-128">Web Hizmeti Bağlayıcısı Yapılandırması aracını JSON öznitelik adları alanı simgeleri kullanımını desteklemiyor</span><span class="sxs-lookup"><span data-stu-id="0d870-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="0d870-129">Değiştirme deseni el ile WSConfigTool.exe.config dosyasına örneğin eklenebilir```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="0d870-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="0d870-130">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="0d870-130">Lotus Notes:</span></span>
  * <span data-ttu-id="0d870-131">Zaman seçeneği **kuruluşun/kuruluş birimleri için özel certifiers izin** Bağlayıcısı'nı (güncelleştirme) dışa aktarma sırasında başarısız sonra tüm öznitelikleri Domino ancak dışarı aktarma zamanında dışarı verme akış sonra devre dışı bir KeyNotFoundException eşitlemeye izin verilir.</span><span class="sxs-lookup"><span data-stu-id="0d870-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="0d870-132">Aşağıdaki öznitelikler birini değiştirerek DN (kullanıcı adı özniteliği) değiştirmeye çalışırsa yeniden adlandırma işlemi başarısız olduğu için bu gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="0d870-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="0d870-133">Soyadı</span><span class="sxs-lookup"><span data-stu-id="0d870-133">LastName</span></span>
      - <span data-ttu-id="0d870-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="0d870-134">FirstName</span></span>
      - <span data-ttu-id="0d870-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="0d870-135">MiddleInitial</span></span>
      - <span data-ttu-id="0d870-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="0d870-136">AltFullName</span></span>
      - <span data-ttu-id="0d870-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="0d870-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="0d870-138">OU</span><span class="sxs-lookup"><span data-stu-id="0d870-138">ou</span></span>
      - <span data-ttu-id="0d870-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="0d870-139">altcommonname</span></span>

  * <span data-ttu-id="0d870-140">Zaman **kuruluşun/kuruluş birimleri için özel certifiers izin** seçeneği etkin ancak gerekli certifiers hala boş sonra KeyNotFoundException oluşur.</span><span class="sxs-lookup"><span data-stu-id="0d870-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="0d870-141">Geliştirmeleri:</span><span class="sxs-lookup"><span data-stu-id="0d870-141">Enhancements:</span></span>

* <span data-ttu-id="0d870-142">Genel SQL:</span><span class="sxs-lookup"><span data-stu-id="0d870-142">Generic SQL:</span></span>
  * <span data-ttu-id="0d870-143">**Senaryo: Gerçekleştirilmedi yeniden tasarlanmıştır:** "*" özelliği</span><span class="sxs-lookup"><span data-stu-id="0d870-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="0d870-144">**Çözüm açıklaması:** değiştirilmiş bir yaklaşım [birden çok değerli başvuru öznitelikleri işleme](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="0d870-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="0d870-145">Giderilen sorunlar:</span><span class="sxs-lookup"><span data-stu-id="0d870-145">Fixed issues:</span></span>

* <span data-ttu-id="0d870-146">Genel Web Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="0d870-146">Generic Web Services:</span></span>
  * <span data-ttu-id="0d870-147">Web Hizmeti Bağlayıcısı varsa, sunucu yapılandırmasını içeri aktarılamıyor</span><span class="sxs-lookup"><span data-stu-id="0d870-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="0d870-148">Web Hizmeti Bağlayıcısı ile birden çok Web Hizmetleri çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="0d870-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="0d870-149">Genel SQL:</span><span class="sxs-lookup"><span data-stu-id="0d870-149">Generic SQL:</span></span>
  * <span data-ttu-id="0d870-150">Tek değer başvurulan özniteliği için hiçbir nesne türleri listelenir</span><span class="sxs-lookup"><span data-stu-id="0d870-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="0d870-151">Delta içeri aktarma nesnesindeki değeri birden çok değerli tablosundan kaldırıldığında değişiklik izleme stratejisi siler</span><span class="sxs-lookup"><span data-stu-id="0d870-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="0d870-152">OverflowException GSQL Bağlayıcısı ile DB2 AS / 400</span><span class="sxs-lookup"><span data-stu-id="0d870-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="0d870-153">Lotus:</span><span class="sxs-lookup"><span data-stu-id="0d870-153">Lotus:</span></span>
  * <span data-ttu-id="0d870-154">OU'lar GlobalParameters sayfa açmadan önce arama enable\disable eklenen seçeneği</span><span class="sxs-lookup"><span data-stu-id="0d870-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="0d870-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="0d870-155">1.1.443.0</span></span>

<span data-ttu-id="0d870-156">Yayımlanma tarihi: 2017 Mart</span><span class="sxs-lookup"><span data-stu-id="0d870-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="0d870-157">Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="0d870-157">Enhancements</span></span>

* <span data-ttu-id="0d870-158">Genel SQL:</span><span class="sxs-lookup"><span data-stu-id="0d870-158">Generic SQL:</span></span></br><span data-ttu-id="0d870-159">
  **Senaryo Belirtiler:** SQL burada biz yalnızca bir nesne türüne bir başvuru izin ve çapraz başvuru üyeleriyle gerektiren Bağlayıcısı ile iyi bilinen bir sınırlama geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0d870-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="0d870-160">
**Çözüm açıklaması:** başvuruları için işlem adımda olan "*" seçeneği seçildiğinde, nesne türlerinin tüm bileşimleri eşitleme altyapısında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0d870-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="0d870-161">Bu çok sayıda yer tutucuları oluşturur</span><span class="sxs-lookup"><span data-stu-id="0d870-161">This will create many placeholders</span></span>
- <span data-ttu-id="0d870-162">Adlandırma nesne türleri benzersiz olduğundan emin olmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0d870-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="0d870-163">Genel LDAP:</span><span class="sxs-lookup"><span data-stu-id="0d870-163">Generic LDAP:</span></span></br><span data-ttu-id="0d870-164">
 **Senaryo:** yalnızca birkaç kapsayıcıları belirli bir bölüm seçildiğinde sonra arama hala tüm bölümünde yapılır.</span><span class="sxs-lookup"><span data-stu-id="0d870-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="0d870-165">Özel eşitleme hizmeti, ancak bir değil, performans düşüşüne neden MA filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="0d870-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="0d870-166">**Çözüm açıklaması:** tüm kapsayıcıları aracılığıyla olası Git yapmak ve her biri tüm bölümünde arama yerine nesneleri aramak için değiştirilmiş GLDAP bağlayıcı'nın kodu.</span><span class="sxs-lookup"><span data-stu-id="0d870-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="0d870-167">Lotus Domino:</span><span class="sxs-lookup"><span data-stu-id="0d870-167">Lotus Domino:</span></span>

  <span data-ttu-id="0d870-168">**Senaryo:** Domino posta silme bir dışa aktarma sırasında kişi kaldırma desteği.</span><span class="sxs-lookup"><span data-stu-id="0d870-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="0d870-169">
  **Çözüm:** bir dışa aktarma sırasında kişi kaldırılmak üzere yapılandırılabilir posta silme desteği.</span><span class="sxs-lookup"><span data-stu-id="0d870-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="0d870-170">Giderilen sorunlar:</span><span class="sxs-lookup"><span data-stu-id="0d870-170">Fixed issues:</span></span>
* <span data-ttu-id="0d870-171">Genel Web Hizmetleri:</span><span class="sxs-lookup"><span data-stu-id="0d870-171">Generic Web Services:</span></span>
 * <span data-ttu-id="0d870-172">Aşağıdaki hata olur sonra hizmet URL'si varsayılan değiştirirken SAP wsconfig WebService yapılandırma aracı aracılığıyla projeleri: yolunun bir bölümü bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="0d870-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="0d870-173">Genel LDAP:</span><span class="sxs-lookup"><span data-stu-id="0d870-173">Generic LDAP:</span></span>
 * <span data-ttu-id="0d870-174">AD LDS tüm öznitelikleri GLDAP bağlayıcı görmez</span><span class="sxs-lookup"><span data-stu-id="0d870-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="0d870-175">LDAP dizini şemadan UPN özniteliklere algılandığında Sihirbazı sonları</span><span class="sxs-lookup"><span data-stu-id="0d870-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="0d870-176">Delta içeri aktarmalar başarısız bulma hatalı "objectclass" özniteliği seçilmediğinde tam içeri aktarma sırasında mevcut değil</span><span class="sxs-lookup"><span data-stu-id="0d870-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="0d870-177">Bir "Bölümleri ve hiyerarşileri Yapılandır" yapılandırma sayfası değil Göster herhangi bir nesne türü için genel yeni sunucuları bölümü eşittir</span><span class="sxs-lookup"><span data-stu-id="0d870-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="0d870-178">LDAP MA.</span><span class="sxs-lookup"><span data-stu-id="0d870-178">LDAP MA.</span></span> <span data-ttu-id="0d870-179">Bunlar yalnızca nesneleri RootDSE bölümünden gösterdi.</span><span class="sxs-lookup"><span data-stu-id="0d870-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="0d870-180">Genel SQL:</span><span class="sxs-lookup"><span data-stu-id="0d870-180">Generic SQL:</span></span>
 * <span data-ttu-id="0d870-181">Delta içeri aktarma öznitelikte içeri hata Genel SQL filigran için düzeltme</span><span class="sxs-lookup"><span data-stu-id="0d870-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="0d870-182">Birden çok değerli öznitelik deleted\added değerlerini verilirken deleted\added veri kaynağındaki değiller.</span><span class="sxs-lookup"><span data-stu-id="0d870-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="0d870-183">Lotus Notes:</span><span class="sxs-lookup"><span data-stu-id="0d870-183">Lotus Notes:</span></span>
 * <span data-ttu-id="0d870-184">Belirli bir alan "Tam adı" için Notlar verilirken özniteliğinin değeri Null veya boş. ancak meta veri deposunda doğru şekilde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="0d870-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="0d870-185">Yinelenen Certifier hata düzeltme</span><span class="sxs-lookup"><span data-stu-id="0d870-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="0d870-186">Lotus Domino Bağlayıcısı diğer nesnelerle üzerinde herhangi bir veri olmadan nesne seçildiğinde sonra bulma hatası tam içeri aktarma işlemi gerçekleştirilirken aldığımız.</span><span class="sxs-lookup"><span data-stu-id="0d870-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="0d870-187">Delta içeri aktarma olduğunda Lotus Domino Bağlayıcısı, o çalışma sonunda Microsoft.IdentityManagement.MA.LotusDomino.Service.exe çalıştıran hizmet bazen döndürür bir uygulama hatası.</span><span class="sxs-lookup"><span data-stu-id="0d870-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="0d870-188">Genel grup üyelikleri düzgün çalışır ve bir kullanıcıyı üyelikten kaldırmak denemek için dışa aktarma çalıştırırken içeren bir güncelleştirme başarılı olarak gösterir, ancak kullanıcının gerçekten Lotus Notes üyeliğinin kaldırılmaları değil dışında tutulur.</span><span class="sxs-lookup"><span data-stu-id="0d870-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="0d870-189">Dışarı aktarma modunu "Append öğesi en altındaki" GUI, birden çok değerli öznitelikler için dışa aktarma sırasında en altındaki yeni öğeler eklemek için Lotus MA yapılandırmasında eklendiği gibi seçmek için bir fırsat.</span><span class="sxs-lookup"><span data-stu-id="0d870-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="0d870-190">Bağlayıcı posta klasörü ve kimliği kasası dosyayı silmek için gerekli mantığı ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0d870-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="0d870-191">Üyelik için NAB üye çalışmıyor silin.</span><span class="sxs-lookup"><span data-stu-id="0d870-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="0d870-192">Değerleri başarıyla birden çok değerli özniteliğinden silinmelidir</span><span class="sxs-lookup"><span data-stu-id="0d870-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="0d870-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="0d870-193">1.1.117.0</span></span>
<span data-ttu-id="0d870-194">Yayımlanma tarihi: 2016 Mart</span><span class="sxs-lookup"><span data-stu-id="0d870-194">Released: 2016 March</span></span>

<span data-ttu-id="0d870-195">**Yeni bir bağlayıcı**</span><span class="sxs-lookup"><span data-stu-id="0d870-195">**New Connector**</span></span>  
<span data-ttu-id="0d870-196">İlk sürümü [Genel SQL bağlayıcı](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="0d870-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="0d870-197">**Yeni Özellikler:**</span><span class="sxs-lookup"><span data-stu-id="0d870-197">**New features:**</span></span>

* <span data-ttu-id="0d870-198">Genel LDAP Bağlayıcısı:</span><span class="sxs-lookup"><span data-stu-id="0d870-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="0d870-199">Delta içeri aktarma Isode ile desteği eklendi.</span><span class="sxs-lookup"><span data-stu-id="0d870-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="0d870-200">Web Hizmetleri Bağlayıcısı:</span><span class="sxs-lookup"><span data-stu-id="0d870-200">Web Services Connector:</span></span>
  * <span data-ttu-id="0d870-201">CsEntryChangeResult ve nesne düzeyi hataları eşitleme altyapısında döndürülecek izin vermek için setImportErrorCode etkinliğiyle güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="0d870-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="0d870-202">Yeni nesne düzeyinde hata işlevselliği kullanmak için SAP6 ve SAP6User şablonları güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="0d870-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="0d870-203">Lotus Domino Bağlayıcısı:</span><span class="sxs-lookup"><span data-stu-id="0d870-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="0d870-204">Dışarı aktarma için adres defteri başına bir certifier gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d870-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="0d870-205">Artık tüm certifiers için aynı parola yönetimini kolaylaştırmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d870-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="0d870-206">**Giderilen sorunlar:**</span><span class="sxs-lookup"><span data-stu-id="0d870-206">**Fixed issues:**</span></span>

* <span data-ttu-id="0d870-207">Genel LDAP Bağlayıcısı:</span><span class="sxs-lookup"><span data-stu-id="0d870-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="0d870-208">IBM Tivoli DS için bazı başvuru öznitelikleri doğru algılanmadı.</span><span class="sxs-lookup"><span data-stu-id="0d870-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="0d870-209">Delta içeri aktarma sırasında açık LDAP için başında ve dizeleri sonuna boşluk kesildi.</span><span class="sxs-lookup"><span data-stu-id="0d870-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="0d870-210">Novell ve NetIQ için OU/kapsayıcıları arasında ve aynı zamanda bir nesne taşındı verme başarısız nesne yeniden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="0d870-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="0d870-211">Web Hizmetleri Bağlayıcısı:</span><span class="sxs-lookup"><span data-stu-id="0d870-211">Web Services Connector:</span></span>
  * <span data-ttu-id="0d870-212">Ardından web hizmeti aynı bağlama için birden çok uç noktalarının olsaydı, bağlayıcı Bu uç noktalarının doğru bulamadı.</span><span class="sxs-lookup"><span data-stu-id="0d870-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="0d870-213">Lotus Domino Bağlayıcısı:</span><span class="sxs-lookup"><span data-stu-id="0d870-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="0d870-214">Bir verme bir posta veritabanına fullName özniteliğinin çalışmadı.</span><span class="sxs-lookup"><span data-stu-id="0d870-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="0d870-215">Hem eklendi ve üye bir gruptan kaldırılan bir dışa aktarma yalnızca eklenen üyelerin verildi.</span><span class="sxs-lookup"><span data-stu-id="0d870-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="0d870-216">Notlar belge geçersiz (öznitelik IsValid false olarak ayarlayın), bağlayıcı başarısız ise.</span><span class="sxs-lookup"><span data-stu-id="0d870-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="0d870-217">Eski sürümleri</span><span class="sxs-lookup"><span data-stu-id="0d870-217">Older releases</span></span>
<span data-ttu-id="0d870-218">Mart 2016 öncesinde bağlayıcıları destek konuları yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0d870-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="0d870-219">**Genel LDAP**</span><span class="sxs-lookup"><span data-stu-id="0d870-219">**Generic LDAP**</span></span>

* <span data-ttu-id="0d870-220">[KB3078617](https://support.microsoft.com/kb/3078617) -1.0.0597, Eylül 2015</span><span class="sxs-lookup"><span data-stu-id="0d870-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="0d870-221">[KB3044896](https://support.microsoft.com/kb/3044896) -1.0.0549, Mart 2015</span><span class="sxs-lookup"><span data-stu-id="0d870-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="0d870-222">[KB3031009](https://support.microsoft.com/kb/3031009) -1.0.0534, Ocak 2015</span><span class="sxs-lookup"><span data-stu-id="0d870-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="0d870-223">[KB3008177](https://support.microsoft.com/kb/3008177) -1.0.0419, 2014 Eylül</span><span class="sxs-lookup"><span data-stu-id="0d870-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="0d870-224">[KB2936070](https://support.microsoft.com/kb/2936070) -4.3.1082, Mart 2014</span><span class="sxs-lookup"><span data-stu-id="0d870-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="0d870-225">**Webservices'a**</span><span class="sxs-lookup"><span data-stu-id="0d870-225">**WebServices**</span></span>

* <span data-ttu-id="0d870-226">[KB3008178](https://support.microsoft.com/kb/3008178) -1.0.0419, 2014 Eylül</span><span class="sxs-lookup"><span data-stu-id="0d870-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="0d870-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="0d870-227">**PowerShell**</span></span>

* <span data-ttu-id="0d870-228">[KB3008179](https://support.microsoft.com/kb/3008179) -1.0.0419, 2014 Eylül</span><span class="sxs-lookup"><span data-stu-id="0d870-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="0d870-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="0d870-229">**Lotus Domino**</span></span>

* <span data-ttu-id="0d870-230">[KB3096533](https://support.microsoft.com/kb/3096533) -1.0.0597, Eylül 2015</span><span class="sxs-lookup"><span data-stu-id="0d870-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="0d870-231">[KB3044895](https://support.microsoft.com/kb/3044895) -1.0.0549, Mart 2015</span><span class="sxs-lookup"><span data-stu-id="0d870-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="0d870-232">[KB2977286](https://support.microsoft.com/kb/2977286) -5.3.0712, 2014 Ağustos</span><span class="sxs-lookup"><span data-stu-id="0d870-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="0d870-233">[KB2932635](https://support.microsoft.com/kb/2932635) -5.3.1003, Şubat 2014</span><span class="sxs-lookup"><span data-stu-id="0d870-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="0d870-234">[KB2899874](https://support.microsoft.com/kb/2899874) -5.3.0721, Ekim 2013</span><span class="sxs-lookup"><span data-stu-id="0d870-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="0d870-235">[KB2875551](https://support.microsoft.com/kb/2875551) -5.3.0534, 2013 Ağustos</span><span class="sxs-lookup"><span data-stu-id="0d870-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d870-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0d870-236">Next steps</span></span>
<span data-ttu-id="0d870-237">Daha fazla bilgi edinmek [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="0d870-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="0d870-238">[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="0d870-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
