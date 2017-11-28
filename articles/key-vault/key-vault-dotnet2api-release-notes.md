---
title: "Anahtar kasası .NET 2.x API Sürüm Notları | Microsoft Docs"
description: ".NET geliştiricileri için Azure anahtar kasası bu API için kod kullanır"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: c5b5fd7f16faf17d16ecc82269fb1264adf4dd06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="5811b-103">Azure anahtar kasası .NET 2.0 - sürüm notları ve Geçiş Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="5811b-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="5811b-104">Azure anahtar kasası .NET ile birlikte çalışan geliştiricilere aşağıdaki notları ve rehberlik içindir / C# Kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5811b-104">The following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="5811b-105">1.0 sürümünden 2.0 sürümüne geçiş içinde güncelleştirme sayısı kodunuzu işlevsel iyileştirmeler yararlanabilir ve ekler gibi özellik için sırayla geçiş işlerinde gerektiren bu yapıldı **anahtar kasası sertifikaları**  destekler.</span><span class="sxs-lookup"><span data-stu-id="5811b-105">In the transition from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="5811b-106">Anahtar kasası sertifikaları</span><span class="sxs-lookup"><span data-stu-id="5811b-106">Key Vault certificates</span></span>

<span data-ttu-id="5811b-107">Anahtar kasası sertifikaları destek sağlar, x509 yönetimi için sertifikaları ve aşağıdaki davranışları:</span><span class="sxs-lookup"><span data-stu-id="5811b-107">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span></span>  

* <span data-ttu-id="5811b-108">Bir anahtar kasası oluşturma işlemi veya varolan bir sertifikayı alma aracılığıyla bir sertifika oluşturmak bir sertifika sahibinin verir.</span><span class="sxs-lookup"><span data-stu-id="5811b-108">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span></span> <span data-ttu-id="5811b-109">Bu otomatik olarak imzalanan hem de içerir ve sertifika yetkilisi sertifikaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5811b-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="5811b-110">Güvenli Depolama ve X509 Yönetimi uygulamak bir anahtar kasası sertifika sahibinin verir sertifikaları özel anahtar malzemesi etkileşim olmadan.</span><span class="sxs-lookup"><span data-stu-id="5811b-110">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="5811b-111">Bir sertifika yaşam döngüsünü yönetmek için anahtar kasası yönlendiren bir ilke oluşturmak bir sertifika sahibinin verir.</span><span class="sxs-lookup"><span data-stu-id="5811b-111">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span></span>  
* <span data-ttu-id="5811b-112">Kişi hakkında bilgi için bildirim yaşam döngüsü olayları geçerlilik süresi ve sertifikanın yenilenmesini sağlamak sertifika sahipleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="5811b-112">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="5811b-113">Otomatik olarak yenilenmesi destekler seçili verenler - anahtar kasası iş ortağı X509 ile sertifika sağlayıcıları / sertifika yetkilileri.</span><span class="sxs-lookup"><span data-stu-id="5811b-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="5811b-114">Not - ortaklık olmayan sağlayıcıları/yetkilileri de izin verilir ancak, otomatik yenileme özelliği desteklemez.</span><span class="sxs-lookup"><span data-stu-id="5811b-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="5811b-115">.NET desteği</span><span class="sxs-lookup"><span data-stu-id="5811b-115">.NET support</span></span>

* <span data-ttu-id="5811b-116">**.NET 4.0** Azure anahtar kasası .NET 2.0 sürümü tarafından desteklenmeyen / C# Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="5811b-116">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="5811b-117">**.NET core** Azure anahtar kasası .NET 2.0 sürümü tarafından desteklenen / C# Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="5811b-117">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="5811b-118">ad alanları</span><span class="sxs-lookup"><span data-stu-id="5811b-118">Namespaces</span></span>

* <span data-ttu-id="5811b-119">Ad alanı için **modelleri** değiştirilirse **Microsoft.Azure.KeyVault** için **Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="5811b-119">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="5811b-120">**Microsoft.Azure.KeyVault.Internal** ad alanı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="5811b-120">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="5811b-121">Azure SDK'sı bağımlılıkları ad alanı değiştirildi **Hyak.Common** ve **Hyak.Common.Internals** için **Microsoft.Rest** ve  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="5811b-121">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="5811b-122">Türü değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="5811b-122">Type changes</span></span>

* <span data-ttu-id="5811b-123">*Gizli* değiştirildi *SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="5811b-123">*Secret* changed to *SecretBundle*</span></span>
* <span data-ttu-id="5811b-124">*Sözlük* değiştirildi *IDictionary*</span><span class="sxs-lookup"><span data-stu-id="5811b-124">*Dictionary* changed to *IDictionary*</span></span>
* <span data-ttu-id="5811b-125">*Liste<T>, string []* değiştirildi *IList<T>*</span><span class="sxs-lookup"><span data-stu-id="5811b-125">*List<T>, string []* changed to *IList<T>*</span></span>
* <span data-ttu-id="5811b-126">*NextList* değiştirildi *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="5811b-126">*NextList* changed to  *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="5811b-127">Dönüş türleri</span><span class="sxs-lookup"><span data-stu-id="5811b-127">Return types</span></span>

* <span data-ttu-id="5811b-128">**KeyList** ve **SecretList** döndürülecek *IPage<T>*  yerine *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="5811b-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="5811b-129">Oluşturulan **BackupKeyAsync** döndürülecek *BackupKeyResult* içeren *değeri* (Yedekleme blob).</span><span class="sxs-lookup"><span data-stu-id="5811b-129">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="5811b-130">Yöntem sarmalandı önce ve yalnızca değer döndürüyor.</span><span class="sxs-lookup"><span data-stu-id="5811b-130">Before the method was wrapped and returning only the value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="5811b-131">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="5811b-131">Exceptions</span></span>

* <span data-ttu-id="5811b-132">*KeyVaultClientException* değiştirilir *KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="5811b-132">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span></span>
* <span data-ttu-id="5811b-133">Hizmet hatası değiştirilirse *özel durum. Hata* için *özel durum. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="5811b-133">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="5811b-134">Ek bilgi için hata iletisini kaldırıldı **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="5811b-134">Removed additional info from the error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="5811b-135">Oluşturucular</span><span class="sxs-lookup"><span data-stu-id="5811b-135">Constructors</span></span>

* <span data-ttu-id="5811b-136">Kabul yerine bir *HttpClient* oluşturucu bağımsız değişkeni olarak yalnızca Oluşturucusu kabul *HttpClientHandler* veya *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="5811b-136">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="5811b-137">İndirilen paketler</span><span class="sxs-lookup"><span data-stu-id="5811b-137">Downloaded packages</span></span>

<span data-ttu-id="5811b-138">Bir istemci bir anahtar kasası bağımlılığı işlerken aşağıdaki yüklenen</span><span class="sxs-lookup"><span data-stu-id="5811b-138">When a client is processing a  dependency on Key Vault the following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="5811b-139">Önceki paket listesi</span><span class="sxs-lookup"><span data-stu-id="5811b-139">Previous package list</span></span>

* <span data-ttu-id="5811b-140">id="Hyak.Common paketini" Sürüm "1.0.2" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-141">id="Microsoft.Azure.Common paketini" Sürüm "2.0.4" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-142">id="Microsoft.Azure.common.Dependencies paketini" Sürüm "1.0.0" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-143">id="Microsoft.Azure.KeyVault paketini" Sürüm "1.0.0" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-144">id="Microsoft.BCL paketini" Sürüm "1.1.9" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-145">id="Microsoft.BCL.Async paketini" Sürüm "1.0.168" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-146">id="Microsoft.BCL.Build paketini" Sürüm "1.0.14" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-147">id="Microsoft.NET.http paketini" Sürüm "2.2.22" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="5811b-148">Geçerli paket listesi</span><span class="sxs-lookup"><span data-stu-id="5811b-148">Current package list</span></span>

* <span data-ttu-id="5811b-149">id="Microsoft.Azure.KeyVault paketini" Sürüm "2.0.0-preview" targetFramework = "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-150">id="Microsoft.REST.ClientRuntime paketini" Sürüm "2.2.0" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="5811b-151">id="Microsoft.REST.ClientRuntime.Azure paketini" Sürüm "3.2.0" = targetFramework "net45" =</span><span class="sxs-lookup"><span data-stu-id="5811b-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="5811b-152">Sınıf değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="5811b-152">Class changes</span></span>

* <span data-ttu-id="5811b-153">**UnixEpoch** sınıfı kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="5811b-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="5811b-154">**Base64UrlConverter** sınıfı yeniden adlandırılmış **Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="5811b-154">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="5811b-155">Diğer değişiklikler</span><span class="sxs-lookup"><span data-stu-id="5811b-155">Other changes</span></span>

* <span data-ttu-id="5811b-156">Bu API sürümüne KV işlemi geçici hataları yeniden deneme ilkesi yapılandırması için destek eklendi.</span><span class="sxs-lookup"><span data-stu-id="5811b-156">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="5811b-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="5811b-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="5811b-158">Döndürülen işlemleri için bir *kasa*, dönüş türü bir kasa özelliği bulunan bir sınıf oluştu.</span><span class="sxs-lookup"><span data-stu-id="5811b-158">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span></span> <span data-ttu-id="5811b-159">Dönüş türü sunulmuştur *kasa*.</span><span class="sxs-lookup"><span data-stu-id="5811b-159">The return type is now *Vault*.</span></span>
* <span data-ttu-id="5811b-160">*PermissionsToKeys* ve *PermissionsToSecrets* artık *Permissions.Keys* ve *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="5811b-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="5811b-161">Dönüş türleri değişikliklerden bazıları denetim-düzeyi için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5811b-161">Some of the return types changes apply to the control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="5811b-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="5811b-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="5811b-163">Paket kadar bozuk **Microsoft.Azure.KeyVault.Extensions** ve **Microsoft.Azure.KeyVault.Cryptography** şifreleme işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="5811b-163">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span></span>

