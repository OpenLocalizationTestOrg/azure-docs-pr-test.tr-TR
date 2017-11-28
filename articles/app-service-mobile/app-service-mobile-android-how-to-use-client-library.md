---
title: "aaaHow toouse hello Android için Azure Mobile Apps SDK | Microsoft Docs"
description: "Nasıl toouse hello Azure Mobile Apps SDK'sı Android için"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="09142-103">Nasıl toouse hello Azure Mobile Apps SDK'sı Android için</span><span class="sxs-lookup"><span data-stu-id="09142-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="09142-104">Bu kılavuz size nasıl toouse hello Mobile Apps tooimplement ortak senaryolar için Android istemci SDK gibi gösterir:</span><span class="sxs-lookup"><span data-stu-id="09142-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="09142-105">Verileri (ekleme, güncelleştirme ve silme) sorgulama.</span><span class="sxs-lookup"><span data-stu-id="09142-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="09142-106">Kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="09142-106">Authentication.</span></span>
* <span data-ttu-id="09142-107">Hataları işleme.</span><span class="sxs-lookup"><span data-stu-id="09142-107">Handling errors.</span></span>
* <span data-ttu-id="09142-108">Merhaba istemci özelleştirme.</span><span class="sxs-lookup"><span data-stu-id="09142-108">Customizing hello client.</span></span>

<span data-ttu-id="09142-109">Bu kılavuz hello istemci tarafında Android SDK odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="09142-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="09142-110">toolearn hakkında daha fazla bilgi mobil uygulamaları için sunucu tarafı SDK'ları Merhaba, bkz: [iş .NET arka SDK] [ 10] veya [nasıl toouse hello Node.js arka ucu SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="09142-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="09142-111">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="09142-111">Reference Documentation</span></span>

<span data-ttu-id="09142-112">Merhaba bulabilirsiniz [Javadocs API Başvurusu] [ 12] github'da hello Android istemci kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="09142-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="09142-113">Desteklenen platformlar</span><span class="sxs-lookup"><span data-stu-id="09142-113">Supported Platforms</span></span>

<span data-ttu-id="09142-114">Merhaba Android için Azure Mobile Apps SDK telefon ve tablet form faktörleri için API düzey 19 24 (KitKat Nougat aracılığıyla) aracılığıyla destekler.</span><span class="sxs-lookup"><span data-stu-id="09142-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="09142-115">Kimlik doğrulaması, özellikle, bir ortak web framework yaklaşım toogather kimlik kullanır.</span><span class="sxs-lookup"><span data-stu-id="09142-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="09142-116">Sunucu akış kimlik doğrulaması saatlerde gibi küçük form faktörü cihazlarla çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="09142-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="09142-117">Kurulum ve Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="09142-117">Setup and Prerequisites</span></span>

<span data-ttu-id="09142-118">Tam hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="09142-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="09142-119">Bu görev, Azure Mobile Apps geliştirmek için tüm ön koşulların yerine sağlar.</span><span class="sxs-lookup"><span data-stu-id="09142-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="09142-120">Hello hızlı başlangıç ayrıca hesabınızı yapılandırma ve ilk mobil uygulama arka oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="09142-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="09142-121">Değil toocomplete hello hızlı başlangıç Öğreticisi karar verirseniz, hello aşağıdaki görevleri tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="09142-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="09142-122">[bir mobil uygulama arka ucu oluşturma] [ 13] toouse Android uygulamanızı ile.</span><span class="sxs-lookup"><span data-stu-id="09142-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="09142-123">Android Studio'da [güncelleştirme hello Gradle derleme dosyalarını](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="09142-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="09142-124">[Internet izni etkinleştirmek](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="09142-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="09142-125"><a name="gradle-build"></a>Güncelleştirme hello Gradle derleme dosyası</span><span class="sxs-lookup"><span data-stu-id="09142-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="09142-126">Her ikisi de değiştirme **build.gradle** dosyaları:</span><span class="sxs-lookup"><span data-stu-id="09142-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="09142-127">Bu kod toohello ekleme *proje* düzeyi **build.gradle** hello içindeki dosyanın *buildscript* etiketi:</span><span class="sxs-lookup"><span data-stu-id="09142-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="09142-128">Bu kod toohello ekleme *modülü uygulama* düzeyi **build.gradle** hello içindeki dosyanın *bağımlılıkları* etiketi:</span><span class="sxs-lookup"><span data-stu-id="09142-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="09142-129">Şu anda hello son 3.3.0 sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="09142-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="09142-130">Merhaba desteklenen sürümleri listelenir [bintray'deki üzerinde][14].</span><span class="sxs-lookup"><span data-stu-id="09142-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="09142-131"><a name="enable-internet"></a>Internet izin etkinleştir</span><span class="sxs-lookup"><span data-stu-id="09142-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="09142-132">tooaccess Azure, uygulamanızın etkin hello Internet izninizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="09142-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="09142-133">Zaten etkinleştirilmişse, kod tooyour satırının aşağıdaki hello eklemek **AndroidManifest.xml** dosyası:</span><span class="sxs-lookup"><span data-stu-id="09142-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="09142-134">İstemci bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="09142-134">Create a Client Connection</span></span>

<span data-ttu-id="09142-135">Azure Mobile Apps tooyour mobil uygulama dört işlevleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="09142-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="09142-136">Veri erişimi ve bir Azure mobil uygulamalar hizmeti ile çevrimdışı eşitleme.</span><span class="sxs-lookup"><span data-stu-id="09142-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="09142-137">Özel hello Azure mobil uygulamalar sunucusu SDK'sı ile yazılmış API'leri çağırın.</span><span class="sxs-lookup"><span data-stu-id="09142-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="09142-138">Azure uygulama hizmeti kimlik doğrulama ve yetkilendirme ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="09142-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="09142-139">Anında iletme bildirimi kaydı Notification Hubs ile.</span><span class="sxs-lookup"><span data-stu-id="09142-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="09142-140">Bu işlevlerin her biri ilk oluşturduğunuz gerektiren bir `MobileServiceClient` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="09142-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="09142-141">Yalnızca bir `MobileServiceClient` nesne içinde mobil istemci oluşturulmalıdır (diğer bir deyişle, bir Singleton deseni olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="09142-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="09142-142">toocreate bir `MobileServiceClient` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="09142-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="09142-143">Merhaba `<MobileAppUrl>` bir dize ya da tooyour mobil arka uç noktaları bir URL nesnesi.</span><span class="sxs-lookup"><span data-stu-id="09142-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="09142-144">Azure uygulama hizmeti toohost mobil arka kullanıyorsanız, kullandığınız hello güvenli olduğundan emin olun `https://` hello URL sürümü.</span><span class="sxs-lookup"><span data-stu-id="09142-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="09142-145">Merhaba istemci de gerektirir erişim toohello etkinlik veya Context - hello `this` hello örnekte parametresi.</span><span class="sxs-lookup"><span data-stu-id="09142-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="09142-146">Merhaba MobileServiceClient yapım hello içinde gerçekleştirileceği `onCreate()` etkinlik başvurulan hello hello yöntemi `AndroidManifest.xml` dosya.</span><span class="sxs-lookup"><span data-stu-id="09142-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="09142-147">En iyi uygulama, sunucu iletişimi kendi (singleton deseni) sınıfına soyut.</span><span class="sxs-lookup"><span data-stu-id="09142-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="09142-148">Bu durumda, geçirmelisiniz hello etkinlik hello Oluşturucusu tooappropriately içinde hello hizmeti yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09142-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="09142-149">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="09142-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="09142-150">Şimdi Ara `AzureServiceAdapter.Initialize(this);` hello içinde `onCreate()` ana etkinlik yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="09142-151">Erişim toohello istemcisi gerektiren herhangi bir yöntem kullanmak `AzureServiceAdapter.getInstance();` tooobtain başvuru toohello hizmet bağdaştırıcısı.</span><span class="sxs-lookup"><span data-stu-id="09142-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="09142-152">Veri işlemleri</span><span class="sxs-lookup"><span data-stu-id="09142-152">Data Operations</span></span>

<span data-ttu-id="09142-153">Merhaba çekirdeği hello Azure Mobile Apps SDK'sı, hello mobil uygulama arka uçta SQL Azure içinde depolanan tooprovide erişim toodata olur.</span><span class="sxs-lookup"><span data-stu-id="09142-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="09142-154">Kesin türü belirtilmiş sınıfları (tercih edilen) kullanarak bu verilere erişebilir veya türsüz sorgular (önerilmez).</span><span class="sxs-lookup"><span data-stu-id="09142-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="09142-155">Bu bölümün Hello toplu kesin türü belirtilmiş sınıflarını kullanma ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="09142-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="09142-156">İstemci veri sınıflarını tanımlamak</span><span class="sxs-lookup"><span data-stu-id="09142-156">Define client data classes</span></span>

<span data-ttu-id="09142-157">SQL Azure tablolardaki tooaccess verileri hello mobil uygulama arka ucu toohello tablolarda karşılık gelen istemci veri sınıflarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="09142-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="09142-158">Bu konudaki örnekler varsayar adlı bir tablo **MyDataTable**, sütunları aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="09142-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="09142-159">id</span><span class="sxs-lookup"><span data-stu-id="09142-159">id</span></span>
* <span data-ttu-id="09142-160">Metin</span><span class="sxs-lookup"><span data-stu-id="09142-160">text</span></span>
* <span data-ttu-id="09142-161">Tamamlayın</span><span class="sxs-lookup"><span data-stu-id="09142-161">complete</span></span>

<span data-ttu-id="09142-162">Merhaba karşılık gelen yazılan istemci-tarafı nesnenin bulunduğundan adlı bir dosyaya **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="09142-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="09142-163">Eklediğiniz her bir alan için'Set ' yordamı yöntemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09142-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="09142-164">SQL Azure tablonuz daha fazla sütun içeriyorsa hello karşılık gelen alanları toothis sınıfı eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="09142-165">Örneğin, hello DTO (veri aktarımı nesne) sahip bir tamsayı öncelik sütunu ve'Set ' yordamı yöntemlerinin yanı sıra bu alanı ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09142-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="09142-166">toocreate ek, Mobile Apps arka uç tablolarda nasıl görürüm toolearn [nasıl yapılır: bir tablo denetleyicisi tanımlamak] [ 15] (.NET arka ucu) veya [dinamik bir şema kullanarak tabloları tanımlayın] [ 16] (Node.js arka ucu).</span><span class="sxs-lookup"><span data-stu-id="09142-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="09142-167">Bir Azure Mobile Apps arka uç tablosu dört biri kullanılabilir tooclients beş özel alanları, tanımlar:</span><span class="sxs-lookup"><span data-stu-id="09142-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="09142-168">`String id`: Merhaba hello kaydı için genel benzersiz kimliği.</span><span class="sxs-lookup"><span data-stu-id="09142-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="09142-169">En iyi uygulama, hello kimliği hello dize gösterimini yapmak bir [UUID] [ 17] nesnesi.</span><span class="sxs-lookup"><span data-stu-id="09142-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="09142-170">`DateTimeOffset updatedAt`: hello son güncelleştirme tarihi/saati hello.</span><span class="sxs-lookup"><span data-stu-id="09142-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="09142-171">Merhaba updatedAt alan hello sunucu tarafından ayarlanır ve istemci kodunuz tarafından hiçbir zaman ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09142-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="09142-172">`DateTimeOffset createdAt`: hello tarih hello nesne oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="09142-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="09142-173">Merhaba createdAt alan hello sunucu tarafından ayarlanır ve istemci kodunuz tarafından hiçbir zaman ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09142-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="09142-174">`byte[] version`: Normal olarak bir dize olarak gösterilen, hello sürüm hello sunucu tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="09142-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="09142-175">`boolean deleted`: Hello kayıt silindi ancak henüz temizlendi değil olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="09142-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="09142-176">Kullanmayın `deleted` sınıfınız özelliği olarak.</span><span class="sxs-lookup"><span data-stu-id="09142-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="09142-177">Merhaba `id` alan gereklidir.</span><span class="sxs-lookup"><span data-stu-id="09142-177">hello `id` field is required.</span></span>  <span data-ttu-id="09142-178">Merhaba `updatedAt` alan ve `version` alan çevrimdışı eşitleme için kullanılan (Artımlı eşitleme ve Çakışma çözümlemesi için sırasıyla).</span><span class="sxs-lookup"><span data-stu-id="09142-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="09142-179">Merhaba `createdAt` alan başvurusu alan ve hello istemci tarafından kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="09142-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="09142-180">Merhaba adları "arasında hat" Merhaba özellik adlarını ve ayarlanabilir değil.</span><span class="sxs-lookup"><span data-stu-id="09142-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="09142-181">Ancak, nesne ve hello arasında bir eşleme hello kullanarak "arasında hat" adları oluşturabilirsiniz [gson] [ 3] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="09142-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="09142-182">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="09142-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="09142-183">Bir tablo başvurusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="09142-183">Create a Table Reference</span></span>

<span data-ttu-id="09142-184">ilk tooaccess bir tablo oluşturun bir [MobileServiceTable] [ 8] arama hello nesnesiyle **getTable** hello yöntemi [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="09142-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="09142-185">Bu yöntem iki aşırı yüklemeye sahip:</span><span class="sxs-lookup"><span data-stu-id="09142-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="09142-186">Kod, aşağıdaki hello içinde **mClient** bir başvuru tooyour MobileServiceClient nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="09142-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="09142-187">Hello ilk aşırı hello sınıf adı ve hello tablo adı aynı hello ve hello hello hızlı başlangıç kullanılır nerede kullanılır:</span><span class="sxs-lookup"><span data-stu-id="09142-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="09142-188">Merhaba tablo adı hello sınıfı adından farklı olduğunda hello ikinci aşırı kullanılır: hello ilk parametredir hello tablo adı.</span><span class="sxs-lookup"><span data-stu-id="09142-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="09142-189"><a name="query"></a>Arka uç tablosu sorgulama</span><span class="sxs-lookup"><span data-stu-id="09142-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="09142-190">İlk olarak, bir tablo başvurusu edinin.</span><span class="sxs-lookup"><span data-stu-id="09142-190">First, obtain a table reference.</span></span>  <span data-ttu-id="09142-191">Ardından hello tablo başvurusu üzerinde bir sorgu yürütün.</span><span class="sxs-lookup"><span data-stu-id="09142-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="09142-192">Bir sorgu herhangi bir bileşimini şöyledir:</span><span class="sxs-lookup"><span data-stu-id="09142-192">A query is any combination of:</span></span>

* <span data-ttu-id="09142-193">A `.where()` [filtre yan tümcesi](#filtering).</span><span class="sxs-lookup"><span data-stu-id="09142-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="09142-194">Bir `.orderBy()` [yan tümcesinin sıralama](#sorting).</span><span class="sxs-lookup"><span data-stu-id="09142-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="09142-195">A `.select()` [alan seçimi yan tümcesi](#selection).</span><span class="sxs-lookup"><span data-stu-id="09142-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="09142-196">A `.skip()` ve `.top()` için [sonuçları disk belleği](#paging).</span><span class="sxs-lookup"><span data-stu-id="09142-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="09142-197">Merhaba yan tümceleri sipariş önceki hello sunulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09142-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="09142-198"><a name="filter"></a>Sonuçları filtreleme</span><span class="sxs-lookup"><span data-stu-id="09142-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="09142-199">Merhaba genel bir sorgu şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="09142-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="09142-200">Merhaba önceki örnekte tüm sonuçları (yukarı toohello en fazla sayfa boyutu hello sunucu tarafından ayarını) döndürür.</span><span class="sxs-lookup"><span data-stu-id="09142-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="09142-201">Merhaba `.execute()` yöntemi hello arka uçta hello sorgu yürütür.</span><span class="sxs-lookup"><span data-stu-id="09142-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="09142-202">Merhaba dönüştürülmüş tooan sorgudur [OData v3] [ 19] iletim toohello Mobile Apps arka önce sorgu.</span><span class="sxs-lookup"><span data-stu-id="09142-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="09142-203">Giriş üzerinde hello Mobile Apps arka hello sorgu hello SQL Azure örneğinde yürütmeden önce bir SQL deyimi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="09142-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="09142-204">Ağ etkinliği biraz zaman alır beri hello `.execute()` yöntemi döndürür bir [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="09142-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="09142-205"><a name="filtering"></a>Döndürülen veri filtreleme</span><span class="sxs-lookup"><span data-stu-id="09142-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="09142-206">sorgu yürütme aşağıdaki hello hello tüm öğeleri döndürür **Todoıtem** tablo nerede **tam** eşittir **false**.</span><span class="sxs-lookup"><span data-stu-id="09142-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="09142-207">**mToDoTable** daha önce oluşturduğumuz hello başvuru toohello mobil hizmeti tablo.</span><span class="sxs-lookup"><span data-stu-id="09142-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="09142-208">Hello kullanarak bir filtre tanımlar **burada** hello tablo başvurusu üzerinde yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="09142-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="09142-209">Merhaba **nerede** yöntemi tarafından izlenen bir **alan** yöntemi ve ardından bir yöntemle hello mantıksal koşulu belirtir.</span><span class="sxs-lookup"><span data-stu-id="09142-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="09142-210">Olası koşul yöntemleri dahil **eq** (eşittir) **ne** (eşit değildir), **gt** (büyük), **ge** (büyük veya eşittir) **lt** (küçüktür), **le** (küçük veya eşittir).</span><span class="sxs-lookup"><span data-stu-id="09142-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="09142-211">Bu yöntemler numarası karşılaştırmanıza olanak tanır ve toospecific değerleri dize alanları.</span><span class="sxs-lookup"><span data-stu-id="09142-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="09142-212">Tarihleri filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-212">You can filter on dates.</span></span> <span data-ttu-id="09142-213">Merhaba aşağıdaki yöntemlerden hello tüm tarih alanı veya hello tarih kısımlarını karşılaştırmanıza olanak tanır: **yıl**, **ay**, **gün**, **saat**, **minute**, ve **ikinci**.</span><span class="sxs-lookup"><span data-stu-id="09142-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="09142-214">Merhaba aşağıdaki örnek, öğe için bir filtre, *son tarih* 2013'e eşittir.</span><span class="sxs-lookup"><span data-stu-id="09142-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="09142-215">Merhaba aşağıdaki yöntemlerden karmaşık filtreler dize alanları destekler: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **Değiştir**, **toLower**, **toUpper**, **kırpma**, ve  **Uzunluk**.</span><span class="sxs-lookup"><span data-stu-id="09142-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="09142-216">Merhaba burada tablo satır için örnek filtreleri aşağıdaki hello *metin* sütun "PRI0" ile başlar</span><span class="sxs-lookup"><span data-stu-id="09142-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="09142-217">işleç yöntemler aşağıdaki hello numara alanları desteklenir: **ekleme**, **alt**, **mul**, **div**, **mod**, **kat**, **tavan**, ve **yuvarlak**.</span><span class="sxs-lookup"><span data-stu-id="09142-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="09142-218">Merhaba burada tablo satır için örnek filtreleri aşağıdaki hello **süresi** bir çift sayı.</span><span class="sxs-lookup"><span data-stu-id="09142-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="09142-219">Bu mantıksal yöntemlerle koşulları birleştirebilirsiniz: **ve**, **veya** ve **değil**.</span><span class="sxs-lookup"><span data-stu-id="09142-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="09142-220">Aşağıdaki örnek hello iki örnekler önceki hello birleştirir.</span><span class="sxs-lookup"><span data-stu-id="09142-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="09142-221">Mantıksal işleçler: Grup ve iç içe geçirme</span><span class="sxs-lookup"><span data-stu-id="09142-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="09142-222">Daha ayrıntılı tartışma ve filtreleme örnekleri için bkz: [hello Android istemci sorgu modelini hello zenginliğinin keşfetme][20].</span><span class="sxs-lookup"><span data-stu-id="09142-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="09142-223"><a name="sorting"></a>Döndürülen veriler sıralama</span><span class="sxs-lookup"><span data-stu-id="09142-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="09142-224">Merhaba aşağıdaki kod tüm öğeleri bir tablodan döndürür **Todoıtems** hello göre artan *metin* alan.</span><span class="sxs-lookup"><span data-stu-id="09142-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="09142-225">*mToDoTable* daha önce oluşturduğunuz hello başvuru toohello arka uç tablosu:</span><span class="sxs-lookup"><span data-stu-id="09142-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="09142-226">Merhaba öğesinin ilk parametresi, hello **orderBy** yöntemi hangi toosort hello alanının bir dize eşit toohello adıdır.</span><span class="sxs-lookup"><span data-stu-id="09142-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="09142-227">Merhaba ikinci parametre kullanan hello **QueryOrder** numaralandırma toospecify olup olmadığını artan veya azalan toosort.</span><span class="sxs-lookup"><span data-stu-id="09142-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="09142-228">Hello kullanarak filtre ***nerede*** yöntemi, hello ***nerede*** önce hello yöntemi çağrıldıktan ***orderBy*** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="09142-229"><a name="selection"></a>Belirli sütunları seçin</span><span class="sxs-lookup"><span data-stu-id="09142-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="09142-230">Merhaba aşağıdaki kod bir tablodan nasıl tooreturn tüm öğeleri gösterir **Todoıtems**, ancak yalnızca, hello görüntüler **tam** ve **metin** alanları.</span><span class="sxs-lookup"><span data-stu-id="09142-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="09142-231">**mToDoTable** daha önce oluşturduğumuz hello başvuru toohello arka uç tablo.</span><span class="sxs-lookup"><span data-stu-id="09142-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="09142-232">Merhaba parametreleri toohello select işlevi tooreturn istediğiniz Merhaba tablonun sütunlarının hello dize adları var.</span><span class="sxs-lookup"><span data-stu-id="09142-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="09142-233">Merhaba **seçin** yönteminin gerekir toofollow yöntemler gibi **nerede** ve **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="09142-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="09142-234">Disk belleği yöntemler gibi tarafından izlenebilir **atla** ve **üst**.</span><span class="sxs-lookup"><span data-stu-id="09142-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="09142-235"><a name="paging"></a>Dönüş verileri sayfalarında</span><span class="sxs-lookup"><span data-stu-id="09142-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="09142-236">Veri **her zaman** sayfalarında döndürdü.</span><span class="sxs-lookup"><span data-stu-id="09142-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="09142-237">Merhaba en fazla döndürülen kayıt sayısını hello sunucu tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="09142-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="09142-238">Daha fazla kayıt Hello istemci isteklerini varsa hello sunucu hello en fazla kayıt sayısı değerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="09142-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="09142-239">Varsayılan olarak, hello sunucuda hello en büyük sayfa boyutu 50 kayıttır.</span><span class="sxs-lookup"><span data-stu-id="09142-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="09142-240">Merhaba ilk örneği, nasıl tooselect hello bir tablodan en üstteki beş öğelerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="09142-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="09142-241">Merhaba sorgunun döndürdüğü hello öğeleri bir tablodan **Todoıtems**.</span><span class="sxs-lookup"><span data-stu-id="09142-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="09142-242">**mToDoTable** daha önce oluşturduğunuz hello başvuru toohello arka uç tablosu:</span><span class="sxs-lookup"><span data-stu-id="09142-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="09142-243">İlk beş öğeleri atlar hello ve ardından sonraki beş döndürür hello bir sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="09142-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="09142-244">Bir tablodaki tüm kayıtları tooget isterseniz, kod tooiterate tüm sayfalar kullanın:</span><span class="sxs-lookup"><span data-stu-id="09142-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="09142-245">Bir istek bu yöntemi kullanarak tüm kayıtlar için en az iki isteği toohello Mobile Apps arka oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09142-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="09142-246">Seçme hello sağ sayfa hello isteği sürerken bellek kullanımı, bant genişliği kullanımı ve hello veri tamamen alma gecikme arasında bir denge boyutudur.</span><span class="sxs-lookup"><span data-stu-id="09142-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="09142-247">Merhaba varsayılan (50 kayıtları) tüm aygıtlar için uygundur.</span><span class="sxs-lookup"><span data-stu-id="09142-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="09142-248">Özellikle büyük bellek cihazlarda çalışmazsa, too500 artırın.</span><span class="sxs-lookup"><span data-stu-id="09142-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="09142-249">500 sonuçlarını kaydeder, artan hello sayfa boyutu kabul edilebilir gecikme ve büyük bellek sorunları bulunan.</span><span class="sxs-lookup"><span data-stu-id="09142-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="09142-250"><a name="chaining"></a>Nasıl yapılır: Sorgu yöntemleri birleştirme</span><span class="sxs-lookup"><span data-stu-id="09142-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="09142-251">arka uç tabloları sorgulama kullanılan hello yöntemler art arda eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="09142-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="09142-252">Zincirleme sorgu yöntemleri tooselect belirli sütunlardaki sıralanır ve disk belleği filtrelenmiş satır sağlar.</span><span class="sxs-lookup"><span data-stu-id="09142-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="09142-253">Karmaşık mantıksal filtreler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-253">You can create complex logical filters.</span></span>  <span data-ttu-id="09142-254">Her sorgu yöntemi, bir sorgu nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="09142-254">Each query method returns a Query object.</span></span> <span data-ttu-id="09142-255">tooend hello dizi yöntem ve gerçekte çalışma hello sorgu, çağrı hello **yürütme** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="09142-256">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="09142-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="09142-257">Merhaba yöntemleri şöyle sıralanmalıdır sorgu zincirleme:</span><span class="sxs-lookup"><span data-stu-id="09142-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="09142-258">Filtreleme (**burada**) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="09142-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="09142-259">Sıralama (**orderBy**) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="09142-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="09142-260">Seçim (**seçin**) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="09142-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="09142-261">disk belleği (**atla** ve **üst**) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="09142-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="09142-262"><a name="binding"></a>Veri toohello kullanıcı arabirimi bağlama</span><span class="sxs-lookup"><span data-stu-id="09142-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="09142-263">Veri bağlama üç bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="09142-263">Data binding involves three components:</span></span>

* <span data-ttu-id="09142-264">Merhaba veri kaynağı</span><span class="sxs-lookup"><span data-stu-id="09142-264">hello data source</span></span>
* <span data-ttu-id="09142-265">Başlangıç ekranı düzeni</span><span class="sxs-lookup"><span data-stu-id="09142-265">hello screen layout</span></span>
* <span data-ttu-id="09142-266">Merhaba bağdaştırıcısı TIES iki birlikte hello olduğunu.</span><span class="sxs-lookup"><span data-stu-id="09142-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="09142-267">Bizim örnek kodda hello veri hello Mobile Apps SQL Azure tablosundan döndürürüz **Todoıtem** bir dizi içine.</span><span class="sxs-lookup"><span data-stu-id="09142-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="09142-268">Veri uygulamaları için genel bir desen etkinliktir.</span><span class="sxs-lookup"><span data-stu-id="09142-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="09142-269">Veritabanı sorguları genellikle bir liste veya dizideki istemci alır hello satır koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="09142-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="09142-270">Bu örnekte, hello dizi hello veri kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="09142-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="09142-271">Merhaba kod hello aygıtta görünür hello verilerinin hello görünümü tanımlayan bir ekran düzenini belirtir.</span><span class="sxs-lookup"><span data-stu-id="09142-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="09142-272">Merhaba iki hello uzantısıdır, bu kodda bir bağdaştırıcı ile birlikte bağlı **ArrayAdapter&lt;Todoıtem&gt;**  sınıfı.</span><span class="sxs-lookup"><span data-stu-id="09142-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="09142-273"><a name="layout"></a>Merhaba düzeni tanımlayın</span><span class="sxs-lookup"><span data-stu-id="09142-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="09142-274">Merhaba düzeni birkaç XML kodu parçacıkları tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="09142-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="09142-275">Varolan bir düzeni verilen, koddan hello hello temsil **ListView** sunucusunu verilerimizi toopopulate istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="09142-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="09142-276">Kod önceki hello hello *LISTITEM* özniteliği hello listesinde tek bir satır için hello düzeni hello kimliğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="09142-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="09142-277">Bu kod bir onay kutusu ve ilgili metin belirtir ve hello listesindeki her bir öğe için bir kez örneği.</span><span class="sxs-lookup"><span data-stu-id="09142-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="09142-278">Bu düzen hello görüntülemez **kimliği** alan ve daha karmaşık bir düzen belirtirsiniz ek alanlar hello görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="09142-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="09142-279">Bu kodu hello **row_list_to_do.xml** dosya.</span><span class="sxs-lookup"><span data-stu-id="09142-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="09142-280"><a name="adapter"></a>Merhaba bağdaştırıcısı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="09142-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="09142-281">Bizim görünümünün Hello veri kaynağı bir dizi olduğundan **Todoıtem**, biz alt bizim bağdaştırıcısından bir **ArrayAdapter&lt;Todoıtem&gt;**  sınıfı.</span><span class="sxs-lookup"><span data-stu-id="09142-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="09142-282">Bu alt sınıf için bir görünüm üreten her **Todoıtem** hello kullanarak **row_list_to_do** düzeni.</span><span class="sxs-lookup"><span data-stu-id="09142-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="09142-283">Bizim kodda hello uzantısıdır sınıfı aşağıdaki hello tanımlarız **ArrayAdapter&lt;E&gt;**  sınıfı:</span><span class="sxs-lookup"><span data-stu-id="09142-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="09142-284">Merhaba bağdaştırıcıları geçersiz kılma **getView** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="09142-285">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="09142-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="09142-286">Biz bu sınıfının bir örneği bizim etkinliğinde gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="09142-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="09142-287">Merhaba ikinci parametre toohello ToDoItemAdapter Oluşturucusu bir başvuru toohello düzeni ' dir.</span><span class="sxs-lookup"><span data-stu-id="09142-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="09142-288">Biz şimdi hello örneğini oluşturabilirsiniz **ListView** ve hello bağdaştırıcısı toohello Ata **ListView**.</span><span class="sxs-lookup"><span data-stu-id="09142-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="09142-289"><a name="use-adapter"></a>Merhaba bağdaştırıcısı tooBind toohello UI kullanın</span><span class="sxs-lookup"><span data-stu-id="09142-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="09142-290">Hazır toouse veri bağlama sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="09142-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="09142-291">Merhaba aşağıdaki kod tooget öğeler hello tablo ve dolgular yerel bağdaştırıcı öğeleri döndürülen hello ile nasıl hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="09142-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="09142-292">Merhaba bağdaştırıcısı hello değiştirmek istediğiniz zaman arama **Todoıtem** tablo.</span><span class="sxs-lookup"><span data-stu-id="09142-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="09142-293">Bir kayıt kayıt temelinde yapılır ve değişiklikleri olduğundan, bir koleksiyon yerine tek bir satır işleyici.</span><span class="sxs-lookup"><span data-stu-id="09142-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="09142-294">Bir öğe eklediğinizde, hello çağrısı **eklemek** yöntemi üzerinde hello bağdaştırıcısı; silerken hello çağrısı **kaldırmak** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="09142-295">Hello tam bir örnek bulabilirsiniz [Android hızlı başlangıç projesi][21].</span><span class="sxs-lookup"><span data-stu-id="09142-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="09142-296"><a name="inserting"></a>Hello arka uç veri Ekle</span><span class="sxs-lookup"><span data-stu-id="09142-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="09142-297">Merhaba bir örneği *Todoıtem* sınıfını ve özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09142-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="09142-298">Ardından **INSERT()** tooinsert nesneyi:</span><span class="sxs-lookup"><span data-stu-id="09142-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="09142-299">Merhaba hello arka uç tablo, dahil edilen hello kimliği ve diğer tüm değerler eklenen hello veri varlığı eşleşme döndürdü (Merhaba gibi `createdAt`, `updatedAt`, ve `version` alanları) hello arka uçta ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="09142-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="09142-300">Mobile Apps tabloları gerektiren adlı birincil anahtar sütunu **kimliği**. Bu sütun bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09142-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="09142-301">Merhaba kimliği sütunun Hello varsayılan değeri bir GUID değeridir.</span><span class="sxs-lookup"><span data-stu-id="09142-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="09142-302">E-posta adresleri veya kullanıcı adları gibi diğer benzersiz değerler sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="09142-303">Bir dize kimliği değeri için eklenen bir kaydı sağlanmadığında hello arka uç yeni bir GUID oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09142-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="09142-304">Dize kimliği değerleri hello aşağıdaki avantajları sağlar:</span><span class="sxs-lookup"><span data-stu-id="09142-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="09142-305">Gidiş dönüş toohello veritabanı yapmadan kimlikleri oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="09142-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="09142-306">Farklı tablolar veya veritabanlarına daha kolay toomerge kayıtlarıdır.</span><span class="sxs-lookup"><span data-stu-id="09142-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="09142-307">KOD değerleri daha iyi bir uygulama mantığı ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="09142-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="09142-308">Dize kimliği değerler **gerekli** çevrimdışı eşitleme desteği.</span><span class="sxs-lookup"><span data-stu-id="09142-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="09142-309">Merhaba arka uç veritabanında depolandıktan sonra bir kimliğini değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="09142-310"><a name="updating"></a>Bir mobil uygulama verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="09142-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="09142-311">bir tabloda tooupdate veri iletmek hello yeni nesne toohello **update()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="09142-312">Bu örnekte, *öğesi* hello başvuru tooa sırada *Todoıtem* bazı yapılan değişiklikler tooit dolmadığı tablo.</span><span class="sxs-lookup"><span data-stu-id="09142-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="09142-313">Merhaba satır hello ile aynı **kimliği** güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="09142-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="09142-314"><a name="deleting"></a>Bir mobil uygulama verilerini sil</span><span class="sxs-lookup"><span data-stu-id="09142-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="09142-315">koddan hello nasıl toodelete veri belirterek bir tablodan veri nesnesi hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="09142-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="09142-316">Merhaba belirterek öğeyi silebilirsiniz **kimliği** hello satır toodelete alanı.</span><span class="sxs-lookup"><span data-stu-id="09142-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="09142-317"><a name="lookup"></a>Belirli bir öğeyi kimliğe göre arayın</span><span class="sxs-lookup"><span data-stu-id="09142-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="09142-318">Belirli bir sahip bir öğe aramak **kimliği** hello ile alan **lookUp()** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="09142-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="09142-319"><a name="untyped"></a>Nasıl yapılır: türsüz verilerle çalışma</span><span class="sxs-lookup"><span data-stu-id="09142-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="09142-320">Merhaba türsüz programlama modeli, JSON seri hale getirme üzerinde tam denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="09142-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="09142-321">Burada türsüz programlama modeli toouse isteyebilir bazı yaygın senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="09142-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="09142-322">Örneğin, arka uç tablonuz fazla sayıda sütun içeriyorsa ve tooreference hello bir sütun alt kümesini yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="09142-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="09142-323">Merhaba yazılan modeli tüm hello sütunları hello Mobile Apps arka uç veri sınıfınızda tanımlanan toodefine gerektirir.</span><span class="sxs-lookup"><span data-stu-id="09142-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="09142-324">API çağrıları verilerine erişmek için hello çoğu benzer toohello programlama çağrıları belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="09142-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="09142-325">Merhaba ana hello türsüz modelinde, hello yöntemleri çağırma farktır **MobileServiceJsonTable** hello yerine **MobileServiceTable** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="09142-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="09142-326"><a name="json_instance"></a>Türsüz tablo örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="09142-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="09142-327">Benzer toohello yazılan modeli, bir tablo başvurusu alarak başlatılır, ancak bu durumda olduğu bir **MobileServicesJsonTable** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="09142-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="09142-328">Merhaba başvuru tarafından arama hello elde **getTable** hello istemci örneği üzerinde yöntemi:</span><span class="sxs-lookup"><span data-stu-id="09142-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="09142-329">Merhaba örneği oluşturduktan sonra **MobileServiceJsonTable**, onu sahip neredeyse hello aynı API hello yazılan programlama modeli olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="09142-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="09142-330">Bazı durumlarda, hello yöntemleri türü belirsiz bir parametre türü belirtilmiş bir parametre yerine getirin.</span><span class="sxs-lookup"><span data-stu-id="09142-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="09142-331"><a name="json_insert"></a>Türü belirsiz bir tabloya ekleme</span><span class="sxs-lookup"><span data-stu-id="09142-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="09142-332">kodun gösterdiği nasıl aşağıdaki hello toodo ekleme.</span><span class="sxs-lookup"><span data-stu-id="09142-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="09142-333">Merhaba ilk toocreate adımdır bir [JsonObject][1], hello parçası olduğu [gson] [ 3] kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="09142-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="09142-334">Ardından, **INSERT()** tooinsert hello türsüz nesnesine hello tablo.</span><span class="sxs-lookup"><span data-stu-id="09142-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="09142-335">Eklenen hello nesnesinin tooget hello kimliği gerekirse hello kullanın **getAsJsonPrimitive()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="09142-336"><a name="json_delete"></a>Türü belirsiz bir tablodan silin</span><span class="sxs-lookup"><span data-stu-id="09142-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="09142-337">Merhaba aşağıdaki kod nasıl toodelete bir örnek, bu durumda, hello aynı örneği gösterir bir **JsonObject** hello önceden oluşturulmuş *Ekle* örnek.</span><span class="sxs-lookup"><span data-stu-id="09142-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="09142-338">Merhaba kodudur hello aynı hello olarak yazılmış durumda, ancak hello yöntem sahip farklı bir imza başvurduğu bu yana bir **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="09142-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="09142-339">Doğrudan Kimliğini kullanarak bir örneği daha da silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09142-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="09142-340"><a name="json_get"></a>Türü belirsiz bir tablodan tüm satırları döndürür</span><span class="sxs-lookup"><span data-stu-id="09142-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="09142-341">kodun gösterdiği nasıl aşağıdaki hello tooretrieve tüm bir tabloyu.</span><span class="sxs-lookup"><span data-stu-id="09142-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="09142-342">Bir JSON tablo kullandığından, seçmeli olarak yalnızca bazı Merhaba tablonun sütunlarının alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="09142-343">Merhaba filtreleme, filtreleme ve disk belleği'hello yazılan model için kullanılabilir yöntemleri aynı kümesini hello türsüz model için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="09142-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="09142-344"><a name="offline-sync"></a>Çevrimdışı eşitleme uygulama</span><span class="sxs-lookup"><span data-stu-id="09142-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="09142-345">Hello Azure Mobile Apps istemci SDK'sı bir SQLite veritabanı toostore hello sunucu verilerin bir kopyasını kullanarak yerel olarak çevrimdışı veri eşitlemeyi de uygular.</span><span class="sxs-lookup"><span data-stu-id="09142-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="09142-346">Çevrimdışı bir tablo üzerinde gerçekleştirilen işlemler mobil bağlantı toowork gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="09142-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="09142-347">Çevrimdışı eşitleme yardımları esnekliği ve çakışma çözümü için daha karmaşık mantığı hello gider performans.</span><span class="sxs-lookup"><span data-stu-id="09142-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="09142-348">Hello Azure Mobile Apps istemci SDK'sı özellikler aşağıdaki hello uygular:</span><span class="sxs-lookup"><span data-stu-id="09142-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="09142-349">Artımlı eşitleme: Bant genişliği ve bellek tüketimi kaydetme yalnızca güncelleştirilmiş ve yeni kayıtlar indirilir.</span><span class="sxs-lookup"><span data-stu-id="09142-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="09142-350">İyimser eşzamanlılık: İşlemleri toosucceed varsayılır.</span><span class="sxs-lookup"><span data-stu-id="09142-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="09142-351">Çakışma çözümü, güncelleştirmelerinin hello sunucuda gerçekleştirilir kadar ertelenir.</span><span class="sxs-lookup"><span data-stu-id="09142-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="09142-352">Çakışma çözümü: çakışan değişikliği hello sunucuda yapılan ve SDK algılar hello tooalert hello kullanıcı kanca oluşturur.</span><span class="sxs-lookup"><span data-stu-id="09142-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="09142-353">Geçici silme: Silinen kayıtlar, diğer aygıtlar tooupdate çevrimdışı önbelleklerini izin vererek, silinen işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="09142-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="09142-354">Çevrimdışı eşitleme başlatılamadı</span><span class="sxs-lookup"><span data-stu-id="09142-354">Initialize Offline Sync</span></span>

<span data-ttu-id="09142-355">Çevrimdışı her tablo hello Çevrimdışı Önbellek kullanmadan önce tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="09142-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="09142-356">Normalde, tablo tanımı hemen hello istemcisinin hello oluşturulduktan sonra gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="09142-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="09142-357">Başvuru toohello çevrimdışı önbellek tablosunu alın</span><span class="sxs-lookup"><span data-stu-id="09142-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="09142-358">Çevrimiçi bir tablo için kullandığınız `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="09142-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="09142-359">Çevrimdışı bir tablo için kullanın `.getSyncTable()`:</span><span class="sxs-lookup"><span data-stu-id="09142-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="09142-360">Tüm iş eşit çevrimiçi tabloları (filtreleme, sıralama, disk belleği, veri ekleme, verilerini güncelleştirmek ve verileri silme dahil) için kullanılabilen yöntemleri hello iyi tablolarda çevrimiçi ve çevrimdışı.</span><span class="sxs-lookup"><span data-stu-id="09142-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="09142-361">Merhaba yerel Çevrimdışı Önbellek Eşitle</span><span class="sxs-lookup"><span data-stu-id="09142-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="09142-362">Eşitleme Merhaba, uygulamanızın içinde denetimdir.</span><span class="sxs-lookup"><span data-stu-id="09142-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="09142-363">Bir örnek eşitleme yöntemi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="09142-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="09142-364">Bir sorgu adı toohello sağladıysanız `.pull(query, queryname)` yöntemi Artımlı eşitleme olduğundan oluşturulan veya son başarıyla tamamlandı hello çekme beri değiştirilen kullanılan tooreturn yalnızca kaydeder.</span><span class="sxs-lookup"><span data-stu-id="09142-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="09142-365">Çevrimdışı eşitleme sırasında çakışmalarını işleme</span><span class="sxs-lookup"><span data-stu-id="09142-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="09142-366">Sırasında bir çakışma olursa bir `.push()` işlemi, bir `MobileServiceConflictException` oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09142-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="09142-367">Hello sunucusu verilen öğesi hello özel durum katıştırılır ve tarafından alınan `.getItem()` hello özel durumunda.</span><span class="sxs-lookup"><span data-stu-id="09142-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="09142-368">Merhaba MobileServiceSyncContext nesnesinde öğeleri aşağıdaki arama hello tarafından Hello itme ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="09142-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="09142-369">İstediğiniz gibi tüm çakışmaları işaretlenmiş sonra çağrı `.push()` yeniden tooresolve tüm çakışmaları hello.</span><span class="sxs-lookup"><span data-stu-id="09142-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="09142-370"><a name="custom-api"></a>Özel bir API çağrısı</span><span class="sxs-lookup"><span data-stu-id="09142-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="09142-371">Özel bir API değil tooan INSERT eşleme, güncelleştirme, silme veya okuma işlemi sunucusu işlevselliği kullanıma toodefine özel uç noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="09142-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="09142-372">Özel bir API kullanarak, okuma ve HTTP ileti üstbilgilerini ayarlama ve JSON dışında bir ileti gövdesinin biçimi tanımlama gibi Mesajlaşma üzerinde daha fazla denetim olabilir.</span><span class="sxs-lookup"><span data-stu-id="09142-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="09142-373">Bir Android istemciden hello çağrısı **invokeApi** yöntemi toocall hello özel API uç noktası.</span><span class="sxs-lookup"><span data-stu-id="09142-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="09142-374">Merhaba aşağıdaki örnekte nasıl toocall bir API uç noktası adlı gösterir **completeAll**, adlı bir koleksiyon sınıfı döndürür **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="09142-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="09142-375">Merhaba **invokeApi** yöntemi, bir POST isteği toohello yeni özel API gönderir hello istemcide çağrılır.</span><span class="sxs-lookup"><span data-stu-id="09142-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="09142-376">hataları gibi hello sonuç hello özel API tarafından döndürülen bir ileti iletişim kutusunda görüntülenmez.</span><span class="sxs-lookup"><span data-stu-id="09142-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="09142-377">Diğer sürümleri **invokeApi** isteğe bağlı olarak nesneyi hello istek gövdesinde gönderme, hello HTTP yöntemini belirtin ve sorgu parametreleri hello isteği ile Gönder olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="09142-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="09142-378">Türsüz sürümlerini **invokeApi** de sağlanır.</span><span class="sxs-lookup"><span data-stu-id="09142-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="09142-379"><a name="authentication"></a>Kimlik doğrulama tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="09142-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="09142-380">Öğreticiler zaten ayrıntılı olarak açıklayan nasıl tooadd bu özellikleri.</span><span class="sxs-lookup"><span data-stu-id="09142-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="09142-381">Uygulama hizmetini destekleyen [uygulama kullanıcıların kimlik doğrulaması](app-service-mobile-android-get-started-users.md) çeşitli dış kimlik sağlayıcılarını kullanarak: Facebook, Google, Microsoft Account, Twitter ve Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="09142-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="09142-382">Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="09142-383">Arka ucunuza kimliği doğrulanmış kullanıcılar tooimplement yetkilendirme kuralları hello kimliğini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="09142-384">İki kimlik doğrulama akışı desteklenir: bir **server** akış ve **istemci** akış.</span><span class="sxs-lookup"><span data-stu-id="09142-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="09142-385">Merhaba kimlik sağlayıcıları web arabirimine alacağından hello sunucu akış hello Basit kimlik doğrulama deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="09142-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="09142-386">Hiçbir ek SDK'ları gerekli tooimplement sunucu akış kimlik doğrulaması ' dir.</span><span class="sxs-lookup"><span data-stu-id="09142-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="09142-387">Kimlik doğrulaması akışı hello mobil cihaz derin bir tümleştirmeye sağlamaz ve yalnızca kavram senaryoları kanıtı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="09142-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="09142-388">hello kimlik sağlayıcısı tarafından sağlanan SDK'ları kullanır gibi hello istemci akışı çoklu oturum açma gibi aygıta özgü özellikleri ile daha derin tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="09142-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="09142-389">Örneğin, mobil uygulamanıza hello Facebook SDK tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="09142-390">Merhaba mobil istemci hello Facebook uygulamaya değiştirir ve, mobil uygulama arka tooyour takas önce oturum onaylar.</span><span class="sxs-lookup"><span data-stu-id="09142-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="09142-391">Gerekli tooenable kimlik doğrulaması, uygulamanızda dört adımlardır:</span><span class="sxs-lookup"><span data-stu-id="09142-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="09142-392">Uygulamanızın kimlik doğrulaması için bir kimlik sağlayıcısı ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="09142-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="09142-393">Uygulama hizmeti arka yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09142-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="09142-394">Tablo izinleri tooauthenticated kullanıcıları yalnızca hello uygulama hizmeti arka uç kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="09142-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="09142-395">Kimlik doğrulama kodu tooyour uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="09142-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="09142-396">Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="09142-397">Merhaba kimliği doğrulanmış kullanıcı toomodify SID'si de kullanabilirsiniz istekleri.</span><span class="sxs-lookup"><span data-stu-id="09142-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="09142-398">Daha fazla bilgi için gözden [kimlik doğrulamayı kullanmaya başlama] ve hello Server SDK nasıl yapılır belgeleri.</span><span class="sxs-lookup"><span data-stu-id="09142-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="09142-399"><a name="caching"></a>Kimlik doğrulaması: Sunucu akışı</span><span class="sxs-lookup"><span data-stu-id="09142-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="09142-400">Merhaba aşağıdaki kod hello Google sağlayıcısını kullanarak bir sunucu akış oturum açma işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="09142-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="09142-401">Ek yapılandırma hello Google sağlayıcısı için hello güvenlik gereksinimleri nedeniyle gereklidir:</span><span class="sxs-lookup"><span data-stu-id="09142-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="09142-402">Ayrıca, yöntem toohello ana etkinlik sınıfıyla aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="09142-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="09142-403">Merhaba `GOOGLE_LOGIN_REQUEST_CODE` , ana tanımlanan etkinliği hello için kullanılan `login()` yöntemi ve hello içinde `onActivityResult()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="09142-404">Merhaba aynı numarası hello içinde kullanılan sürece herhangi bir benzersiz sayı seçebilirsiniz `login()` yöntemi ve hello `onActivityResult()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="09142-405">(Daha önce gösterildiği gibi) bir hizmet bağdaştırıcısı hello istemci kodu soyut, hello hizmet bağdaştırıcısında hello uygun yöntemleri çağırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="09142-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="09142-406">Ayrıca tooconfigure hello proje için customtabs gerekir.</span><span class="sxs-lookup"><span data-stu-id="09142-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="09142-407">Önce bir yeniden yönlendirme URL'si belirtin.</span><span class="sxs-lookup"><span data-stu-id="09142-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="09142-408">Kod parçacığında çok aşağıdaki hello eklemek`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="09142-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="09142-409">Merhaba eklemek **redirectUriScheme** toohello `build.gradle` dosya uygulamanız için:</span><span class="sxs-lookup"><span data-stu-id="09142-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="09142-410">Son olarak, ekleme `com.android.support:customtabs:23.0.1` hello toohello bağımlılıkları listesinde `build.gradle` dosyası:</span><span class="sxs-lookup"><span data-stu-id="09142-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="09142-411">Kullanıcı oturum açma hello Hello kimliği elde bir **MobileServiceUser** hello kullanarak **getuserıd öğesini** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="09142-412">Nasıl toouse vadeli toocall hello zaman uyumsuz oturum açma API'leri ilişkin bir örnek için bkz: [kimlik doğrulamayı kullanmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="09142-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="09142-413">Merhaba URL belirtilen düzeni büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="09142-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="09142-414">Emin tüm oluşumlarını `{url_scheme_of_you_app}` eşleşen durumda.</span><span class="sxs-lookup"><span data-stu-id="09142-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="09142-415"><a name="caching"></a>Önbellek kimlik doğrulama belirteçleri</span><span class="sxs-lookup"><span data-stu-id="09142-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="09142-416">Kimlik doğrulama belirteçleri önbelleğe alma toostore hello kullanıcı kimliği ve kimlik doğrulama belirteci hello cihazda yerel olarak gerektirir.</span><span class="sxs-lookup"><span data-stu-id="09142-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="09142-417">Merhaba hello uygulama, bir sonraki başlatılışında, hello önbellek denetleyin ve bu değerleri varsa hello günlüğüne yordamı atlayın ve bu verilerle hello istemci rehydrate.</span><span class="sxs-lookup"><span data-stu-id="09142-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="09142-418">Ancak bu verileri duyarlıdır ve hello telefon çalınırsa durumda güvenliği şifrelenmiş depolanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="09142-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="09142-419">İçinde nasıl toocache kimlik doğrulama belirteçleri, tam bir örnek görebilirsiniz [önbelleğe kimlik doğrulama belirteçleri bölümü][7].</span><span class="sxs-lookup"><span data-stu-id="09142-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="09142-420">Toouse süresi dolmuş bir belirteci çalıştığınızda aldığınız bir *yetkisiz 401* yanıt.</span><span class="sxs-lookup"><span data-stu-id="09142-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="09142-421">Filtreleri kullanarak kimlik doğrulama hataları işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="09142-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="09142-422">Filtreler istekleri toohello uygulama hizmeti arka uç kesebilir.</span><span class="sxs-lookup"><span data-stu-id="09142-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="09142-423">Merhaba filtre kodu bir 401 hello yanıtı testleri, hello oturum açma işlemini tetikler ve hello 401 oluşturulan hello isteği sürdürür.</span><span class="sxs-lookup"><span data-stu-id="09142-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="09142-424"><a name="refresh"></a>Yenileme belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="09142-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="09142-425">Azure App Service kimlik doğrulaması ve yetkilendirme tarafından döndürülen hello belirteci tanımlı yaşam süresi bir saat sahip.</span><span class="sxs-lookup"><span data-stu-id="09142-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="09142-426">Bu süre hello kullanıcı sağlamalarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="09142-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="09142-427">Kullanıyorsanız istemci akışı kimlik doğrulaması yoluyla aldığınız ardından sağlamalarını uzun süreli bir belirteç ile Azure App Service kimlik doğrulaması kullanarak ve yetkilendirme kullanarak aynı belirteci hello.</span><span class="sxs-lookup"><span data-stu-id="09142-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="09142-428">Başka bir Azure uygulama hizmeti belirteci ile yeni bir yaşam süresi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09142-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="09142-429">Merhaba sağlayıcısı toouse yenileme belirteçleri da kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="09142-430">Bir yenileme belirteci her zaman kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="09142-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="09142-431">Ek yapılandırma gerekli değildir:</span><span class="sxs-lookup"><span data-stu-id="09142-431">Additional configuration is required:</span></span>

* <span data-ttu-id="09142-432">İçin **Azure Active Directory**, gizli hello Azure Active Directory uygulaması için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09142-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="09142-433">Merhaba istemci parolası, Azure Active Directory kimlik doğrulamasını yapılandırırken hello Azure uygulama hizmeti belirtin.</span><span class="sxs-lookup"><span data-stu-id="09142-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="09142-434">Çağrılırken `.login()`, geçirmek `response_type=code id_token` bir parametre olarak:</span><span class="sxs-lookup"><span data-stu-id="09142-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="09142-435">İçin **Google**, hello geçirmek `access_type=offline` bir parametre olarak:</span><span class="sxs-lookup"><span data-stu-id="09142-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="09142-436">İçin **Microsoft Account**seçin hello `wl.offline_access` kapsam.</span><span class="sxs-lookup"><span data-stu-id="09142-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="09142-437">toorefresh bir belirteç çağrı `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="09142-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="09142-438">En iyi uygulama, bir 401 yanıtına hello sunucusundan algılar ve toorefresh hello kullanıcı belirteci çalışır bir filtre oluşturun.</span><span class="sxs-lookup"><span data-stu-id="09142-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="09142-439">Oturum akış olmayan istemci kimlik doğrulaması ile oturum</span><span class="sxs-lookup"><span data-stu-id="09142-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="09142-440">Merhaba akış olmayan istemci kimlik doğrulaması oturum açma için genel işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="09142-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="09142-441">Azure App Service kimlik doğrulama ve yetkilendirme akışı sunucu kimlik doğrulaması gibi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09142-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="09142-442">Kimlik doğrulama tooproduce bir erişim belirteci için Hello kimlik doğrulama sağlayıcısı SDK tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="09142-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="09142-443">Merhaba çağrı `.login()` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="09142-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="09142-444">Hello yerine `onSuccess()` , kod ile yöntemi başarılı oturum açma toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="09142-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="09142-445">Merhaba `{provider}` dizedir geçerli bir sağlayıcısı: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, veya **twitter**.</span><span class="sxs-lookup"><span data-stu-id="09142-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="09142-446">Özel kimlik doğrulama uyguladıysanız, hello özel kimlik doğrulama sağlayıcısı etiketi de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09142-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="09142-447"><a name="adal"></a>Kullanıcılar hello Active Directory Authentication Library (ADAL) ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="09142-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="09142-448">Azure Active Directory'yi kullanarak uygulamanıza hello Active Directory Authentication Library (ADAL) toosign kullanıcılar kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="09142-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="09142-449">Bir istemci akış oturum kullanmaktır genellikle tercih toousing hello `loginAsync()` yöntemleri olarak daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar.</span><span class="sxs-lookup"><span data-stu-id="09142-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="09142-450">Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna AAD oturum açma için yapılandırma [tooconfigure App Service nasıl Active Directory oturum açma için] [ 22] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="09142-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="09142-451">Yerel istemci uygulaması kaydı emin toocomplete hello isteğe bağlı adım olun.</span><span class="sxs-lookup"><span data-stu-id="09142-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="09142-452">ADAL tanımları izleyerek, build.gradle dosya tooinclude hello değiştirerek yükleyin:</span><span class="sxs-lookup"><span data-stu-id="09142-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="09142-453">Aşağıdaki kod tooyour uygulama, değişiklikleri izleyen hello yapmadan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="09142-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="09142-454">Değiştir **INSERT yetkilisi burada** uygulamanızı sağlanan hello Kiracı hello adı.</span><span class="sxs-lookup"><span data-stu-id="09142-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="09142-455">Merhaba biçiminde https://login.microsoftonline.com/contoso.onmicrosoft.com olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="09142-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="09142-456">Değiştir **Ekle-RESOURCE-kimliği-Buraya** , mobil uygulamanızın arka ucuna için hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="09142-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="09142-457">Hello hello istemci kimliği elde edebilirsiniz **Gelişmiş** altında sekmesinde **Azure Active Directory ayarları** hello Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="09142-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="09142-458">Değiştir **Ekle-istemci-kimliği-Buraya** hello yerel istemci uygulamasından kopyaladığınız hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="09142-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="09142-459">Değiştir **Ekle-REDIRECT-URI-Buraya** sitenizin ile */.auth/login/done* hello HTTPS şeması kullanarak uç nokta.</span><span class="sxs-lookup"><span data-stu-id="09142-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="09142-460">Bu değer çok benzer olmalıdır*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="09142-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="09142-461"><a name="filters"></a>Merhaba istemci-sunucu iletişimi Ayarla</span><span class="sxs-lookup"><span data-stu-id="09142-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="09142-462">Merhaba istemci bağlantısı normalde HTTP kitaplığı hello Android SDK ile sağlanan temel hello kullanarak temel bir HTTP bağlantısı olur.</span><span class="sxs-lookup"><span data-stu-id="09142-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="09142-463">Neden istediğiniz toochange birkaç nedeni vardır:</span><span class="sxs-lookup"><span data-stu-id="09142-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="09142-464">Alternatif bir HTTP kitaplığı tooadjust zaman aşımları toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="09142-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="09142-465">Bir ilerleme çubuğu tooprovide istiyor.</span><span class="sxs-lookup"><span data-stu-id="09142-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="09142-466">Bir özel üstbilgi toosupport API management işlevselliği tooadd istiyor.</span><span class="sxs-lookup"><span data-stu-id="09142-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="09142-467">Böylece, yeniden kimlik doğrulamanın uygulayabileceğiniz başarısız bir yanıt toointercept istiyor.</span><span class="sxs-lookup"><span data-stu-id="09142-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="09142-468">Toolog arka uç istekleri tooan analytics hizmeti istiyor.</span><span class="sxs-lookup"><span data-stu-id="09142-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="09142-469">Alternatif bir HTTP kitaplığı kullanma</span><span class="sxs-lookup"><span data-stu-id="09142-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="09142-470">Merhaba çağrı `.setAndroidHttpClientFactory()` istemci başvurusu oluşturduktan sonra hemen yöntemi.</span><span class="sxs-lookup"><span data-stu-id="09142-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="09142-471">Örneğin, tooset hello bağlantı zaman aşımı too60 saniye (yerine hello varsayılan 10 saniye):</span><span class="sxs-lookup"><span data-stu-id="09142-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="09142-472">Bir ilerleme filtre uygulama</span><span class="sxs-lookup"><span data-stu-id="09142-472">Implement a Progress Filter</span></span>

<span data-ttu-id="09142-473">Her istek bir kesme noktası uygulayarak uygulayabilirsiniz bir `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="09142-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="09142-474">Örneğin, bir önceden oluşturulmuş ilerleme çubuğu hello aşağıdaki güncelleştirmeler:</span><span class="sxs-lookup"><span data-stu-id="09142-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="09142-475">Bu filtre toohello istemci aşağıdaki gibi ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09142-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="09142-476">İstek üstbilgilerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="09142-476">Customize Request Headers</span></span>

<span data-ttu-id="09142-477">Merhaba aşağıdaki kullanın `ServiceFilter` ve hello hello filtresi ekleme hello aynı şekilde `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="09142-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="09142-478"><a name="conversions"></a>Otomatik serileştirme yapılandırın</span><span class="sxs-lookup"><span data-stu-id="09142-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="09142-479">Hello kullanarak tooevery sütunu geçerli bir dönüştürme stratejisi belirtebilirsiniz [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="09142-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="09142-480">Merhaba Android istemci kitaplığını kullanan [gson] [ 3] hello veri tooAzure uygulama hizmeti gönderilmeden önce hello arka planda tooserialize Java tooJSON veri nesneleri.</span><span class="sxs-lookup"><span data-stu-id="09142-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="09142-481">Merhaba aşağıdaki kod kullanır hello **setFieldNamingStrategy()** yöntemi tooset hello stratejisi.</span><span class="sxs-lookup"><span data-stu-id="09142-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="09142-482">Bu örnek hello ilk karakter ("m") ve her alan adı için ardından küçük hello sonraki karakteri siler.</span><span class="sxs-lookup"><span data-stu-id="09142-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="09142-483">Örneğin, "id" "Orta" etkinleştirmeniz</span><span class="sxs-lookup"><span data-stu-id="09142-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="09142-484">Bir dönüştürme stratejisi tooreduce hello gereken uygulama `SerializedName()` çoğu alanlara ek açıklamaları.</span><span class="sxs-lookup"><span data-stu-id="09142-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="09142-485">Bu kod hello kullanan bir mobil istemci başvuru oluşturmadan önce yürütülmelidir **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="09142-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[kimlik doğrulamayı kullanmaya başlama]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
