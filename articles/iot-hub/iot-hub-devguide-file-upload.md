---
title: "aaaUnderstand Azure IOT Hub dosya karşıya yükleme | Microsoft Docs"
description: "Geliştirici Kılavuzu - kullanım hello dosya karşıya yükleme özelliğini IOT hub'ı toomanage bir aygıt tooan Azure depolama blob kapsayıcısından dosyaları karşıya yükleme."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a><span data-ttu-id="9c4f0-103">IOT Hub ile dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="9c4f0-103">Upload files with IoT Hub</span></span>

<span data-ttu-id="9c4f0-104">Merhaba ayrıntılı olarak [IOT Hub uç noktaları] [ lnk-endpoints] makale, bir cihaz başlatabilir dosyanın karşıya bir aygıt'e yönelik uç noktası aracılığıyla bir bildirim göndererek (**/devices/ {DeviceID} /dosyaları**).</span><span class="sxs-lookup"><span data-stu-id="9c4f0-104">As detailed in hello [IoT Hub endpoints][lnk-endpoints] article, a device can initiate a file upload by sending a notification through a device-facing endpoint (**/devices/{deviceId}/files**).</span></span> <span data-ttu-id="9c4f0-105">Bir cihaz IOT hub'ı bir karşıya yükleme tamamlanana bildirdiğinde, IOT hub'ı hello aracılığıyla dosya karşıya yükleme bildirim iletisi gönderir **/messages/servicebound/filenotifications** service'e yönelik uç noktası.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-105">When a device notifies IoT Hub that an upload is complete, IoT Hub sends a file upload notification message through hello **/messages/servicebound/filenotifications** service-facing endpoint.</span></span>

<span data-ttu-id="9c4f0-106">Azure depolama hesabı dağıtıcısı tooan ilişkili olarak iletileri IOT Hub kendisi aracılığıyla aracılığı yapmaktan yerine IOT Hub yerine davranır.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-106">Instead of brokering messages through IoT Hub itself, IoT Hub instead acts as a dispatcher tooan associated Azure Storage account.</span></span> <span data-ttu-id="9c4f0-107">Bir cihaz IOT Hub'belirli toohello dosya hello cihaz depolama belirtecinden tooupload istediği ister.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-107">A device requests a storage token from IoT Hub that is specific toohello file hello device wishes tooupload.</span></span> <span data-ttu-id="9c4f0-108">Merhaba SAS URI'sini tooupload hello dosya toostorage Hello aygıt kullanır ve hello karşıya yükleme tamamlandığında hello cihaz tamamlama tooIoT Hub ilişkin bir bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-108">hello device uses hello SAS URI tooupload hello file toostorage, and when hello upload is complete hello device sends a notification of completion tooIoT Hub.</span></span> <span data-ttu-id="9c4f0-109">IOT hub'ı denetler: hello dosya karşıya yükleme tamamlandıktan ve bir dosya karşıya yükleme bildirim iletisi toohello hizmet dönük dosya bildirim uç noktası ekler.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-109">IoT Hub checks hello file upload is complete and then adds a file upload notification message toohello service-facing file notification endpoint.</span></span>

<span data-ttu-id="9c4f0-110">Bir CİHAZDAN dosya tooIoT Hub karşıya yüklemeden önce tarafından hub'ınızı yapılandırmanız gerekir [bir Azure Storage ilişkilendirme] [ lnk-associate-storage] tooit hesap.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-110">Before you upload a file tooIoT Hub from a device, you must configure your hub by [associating an Azure Storage][lnk-associate-storage] account tooit.</span></span>

<span data-ttu-id="9c4f0-111">Cihazınızı böylece [karşıya yükleme başlatma] [ lnk-initialize] ve ardından [IOT hub'ı bildir] [ lnk-notify] hello karşıya yükleme tamamlandığında.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-111">Your device can then [initialize an upload][lnk-initialize] and then [notify IoT hub][lnk-notify] when hello upload completes.</span></span> <span data-ttu-id="9c4f0-112">İsteğe bağlı olarak, bir cihaz IOT hub'ı bu hello karşıya yükleme tamamlandığında bildirdiğinde, hello hizmet oluşturabilir bir [bildirim iletisi][lnk-service-notification].</span><span class="sxs-lookup"><span data-stu-id="9c4f0-112">Optionally, when a device notifies IoT Hub that hello upload is complete, hello service can generate a [notification message][lnk-service-notification].</span></span>

### <a name="when-toouse"></a><span data-ttu-id="9c4f0-113">Zaman toouse</span><span class="sxs-lookup"><span data-stu-id="9c4f0-113">When toouse</span></span>

<span data-ttu-id="9c4f0-114">Dosya karşıya yükleme toosend medya dosyaları ve zaman zaman bağlı cihazları veya sıkıştırılmış toosave bant genişliği tarafından karşıya yüklenen büyük telemetri toplu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-114">Use file upload toosend media files and large telemetry batches uploaded by intermittently connected devices or compressed toosave bandwidth.</span></span>

<span data-ttu-id="9c4f0-115">Çok başvuran[cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] IF bildirilen özellikleri, cihaz bulut iletilerini veya karşıya dosya yükleme kullanarak arasında şüpheli.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-115">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using reported properties, device-to-cloud messages, or file upload.</span></span>

## <a name="associate-an-azure-storage-account-with-iot-hub"></a><span data-ttu-id="9c4f0-116">Bir Azure Storage hesabı IOT Hub ile ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="9c4f0-116">Associate an Azure Storage account with IoT Hub</span></span>

<span data-ttu-id="9c4f0-117">toouse hello dosya karşıya yükleme işlevselliği, ilk Azure Storage hesabı toohello IOT hub'ı bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-117">toouse hello file upload functionality, you must first link an Azure Storage account toohello IoT Hub.</span></span> <span data-ttu-id="9c4f0-118">Merhaba aracılığıyla bu görevi tamamlayabilirsiniz [Azure portal][lnk-management-portal], veya program aracılığıyla hello aracılığıyla [IOT hub'ı kaynak sağlayıcısı REST API'leri] [ lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="9c4f0-118">You can complete this task either through hello [Azure portal][lnk-management-portal], or programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="9c4f0-119">Bir Azure Storage hesabı IOT Hub'ınıza ilişkilendirdikten sonra hello hizmeti hello aygıt dosya karşıya yükleme isteği başlattığında tooa aygıt SAS URI'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-119">Once you have associated an Azure Storage account with your IoT Hub, hello service returns a SAS URI tooa device when hello device initiates a file upload request.</span></span>

> [!NOTE]
> <span data-ttu-id="9c4f0-120">Merhaba [Azure IOT SDK'ları] [ lnk-sdks] otomatik olarak tanıtıcı alma izin ver hello SAS hello dosya karşıya yükleme ve tamamlanan karşıya yükleme, IOT Hub bildirme URI.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-120">hello [Azure IoT SDKs][lnk-sdks] automatically handle retrieving hello SAS URI, uploading hello file, and notifying IoT Hub of a completed upload.</span></span>


## <a name="initialize-a-file-upload"></a><span data-ttu-id="9c4f0-121">Bir dosyayı karşıya yükleme başlatma</span><span class="sxs-lookup"><span data-stu-id="9c4f0-121">Initialize a file upload</span></span>
<span data-ttu-id="9c4f0-122">IOT Hub cihazları toorequest depolama tooupload bir dosya için bir SAS URI'si için özellikle bir uç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-122">IoT Hub has an endpoint specifically for devices toorequest a SAS URI for storage tooupload a file.</span></span> <span data-ttu-id="9c4f0-123">tooinitiate hello dosya karşıya yükleme işlemi, hello cihaz gönderen bir POST isteği çok`{iot hub}.azure-devices.net/devices/{deviceId}/files` JSON gövdesi aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-123">tooinitiate hello file upload process, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files` with hello following JSON body:</span></span>

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

<span data-ttu-id="9c4f0-124">IOT hub'ı veri hangi hello aygıt tooupload hello dosyasını kullanır, aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-124">IoT Hub returns hello following data, which hello device uses tooupload hello file:</span></span>

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a><span data-ttu-id="9c4f0-125">Kullanım dışı: karşıya dosya yükleme GET ile başlatma</span><span class="sxs-lookup"><span data-stu-id="9c4f0-125">Deprecated: initialize a file upload with a GET</span></span>

> [!NOTE]
> <span data-ttu-id="9c4f0-126">Bu bölümde nasıl kullanım dışı bırakılan işlevsellik açıklanmaktadır tooreceive IOT hub'dan bir SAS URI'si.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-126">This section describes deprecated functionality for how tooreceive a SAS URI from IoT Hub.</span></span> <span data-ttu-id="9c4f0-127">Daha önce açıklanan hello POST yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-127">Use hello POST method described previously.</span></span>

<span data-ttu-id="9c4f0-128">IOT hub'ı karşıya yükleme, bir tooget hello SAS URI'sini depolama ve diğer toonotify hello IOT hub'ını tamamlanan karşıya yükleme hello iki REST uç noktaları toosupport dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-128">IoT Hub has two REST endpoints toosupport file upload, one tooget hello SAS URI for storage and hello other toonotify hello IoT hub of a completed upload.</span></span> <span data-ttu-id="9c4f0-129">Merhaba aygıt hello dosya karşıya yükleme işlemi bir GET toohello IOT hub'ına göndererek başlatır `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-129">hello device initiates hello file upload process by sending a GET toohello IoT hub at `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`.</span></span> <span data-ttu-id="9c4f0-130">Merhaba IOT hub'ı döndürür:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-130">hello IoT hub returns:</span></span>

* <span data-ttu-id="9c4f0-131">Bir SAS URI'sini belirli toohello dosya toobe karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-131">A SAS URI specific toohello file toobe uploaded.</span></span>
* <span data-ttu-id="9c4f0-132">Merhaba karşıya yükleme tamamlandığında kullanılan bağıntı kimliği toobe.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-132">A correlation ID toobe used once hello upload is completed.</span></span>

## <a name="notify-iot-hub-of-a-completed-file-upload"></a><span data-ttu-id="9c4f0-133">IOT hub'ı bir tamamlanmış dosyanın karşıya yüklenmesi bildir</span><span class="sxs-lookup"><span data-stu-id="9c4f0-133">Notify IoT Hub of a completed file upload</span></span>

<span data-ttu-id="9c4f0-134">Merhaba aygıt hello dosya toostorage hello Azure depolama SDK'ları kullanarak yüklemek için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-134">hello device is responsible for uploading hello file toostorage using hello Azure Storage SDKs.</span></span> <span data-ttu-id="9c4f0-135">Merhaba karşıya yükleme tamamlandığında, hello aygıt bir POST isteği çok gönderir`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` JSON gövdesi aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-135">When hello upload is complete, hello device sends a POST request too`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` with hello following JSON body:</span></span>

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

<span data-ttu-id="9c4f0-136">Merhaba değerini `isSuccess` hello dosyası başarıyla karşıya yüklendi olup olmadığını Boolean temsil eden bir değil.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-136">hello value of `isSuccess` is a Boolean representing whether hello file was uploaded successfully.</span></span> <span data-ttu-id="9c4f0-137">Merhaba durum kodunu `statusCode` hello hello dosya toostorage hello karşıya yükleme durumu ve hello `statusDescription` toohello karşılık gelen `statusCode`.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-137">hello status code for `statusCode` is hello status for hello upload of hello file toostorage, and hello `statusDescription` corresponds toohello `statusCode`.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="9c4f0-138">Başvuru konuları:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-138">Reference topics:</span></span>

<span data-ttu-id="9c4f0-139">Merhaba aşağıdaki başvuru konuları aygıttan dosyaları karşıya yükleme hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-139">hello following reference topics provide you with more information about uploading files from a device.</span></span>

## <a name="file-upload-notifications"></a><span data-ttu-id="9c4f0-140">Dosya karşıya yükleme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="9c4f0-140">File upload notifications</span></span>

<span data-ttu-id="9c4f0-141">Bir cihaz IOT hub'ı bir karşıya yükleme tamamlandığını bildirir, isteğe bağlı olarak, IOT hub'ı hello adı ve depolama hello dosyasının konumunu içeren bir bildirim iletisi oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-141">Optionally, when a device notifies IoT Hub that an upload is complete, IoT Hub can generate a notification message that contains hello name and storage location of hello file.</span></span>

<span data-ttu-id="9c4f0-142">İçinde anlatıldığı gibi [uç noktaları][lnk-endpoints], IOT hub'ı sunan bir hizmet'e yönelik uç noktası aracılığıyla dosya karşıya yükleme bildirimleri (**/messages/servicebound/fileuploadnotifications**) iletileri olarak.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-142">As explained in [Endpoints][lnk-endpoints], IoT Hub delivers file upload notifications through a service-facing endpoint (**/messages/servicebound/fileuploadnotifications**) as messages.</span></span> <span data-ttu-id="9c4f0-143">Merhaba alma semantiğini dosya karşıya yükleme bildirimlerini aynı bulut-cihaz iletilerini ettirilmesi hello ve sahip, hello aynı için [ileti yaşam döngüsü][lnk-lifecycle].</span><span class="sxs-lookup"><span data-stu-id="9c4f0-143">hello receive semantics for file upload notifications are hello same as for cloud-to-device messages and have hello same [message lifecycle][lnk-lifecycle].</span></span> <span data-ttu-id="9c4f0-144">Merhaba dosya karşıya yükleme bildirim uç noktasından alınan her iletinin hello aşağıdaki özelliklere sahip bir JSON kaydıdır:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-144">Each message retrieved from hello file upload notification endpoint is a JSON record with hello following properties:</span></span>

| <span data-ttu-id="9c4f0-145">Özellik</span><span class="sxs-lookup"><span data-stu-id="9c4f0-145">Property</span></span> | <span data-ttu-id="9c4f0-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9c4f0-146">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9c4f0-147">EnqueuedTimeUtc</span><span class="sxs-lookup"><span data-stu-id="9c4f0-147">EnqueuedTimeUtc</span></span> |<span data-ttu-id="9c4f0-148">Merhaba bildirim ne zaman oluşturulduğunu belirten bir zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-148">Timestamp indicating when hello notification was created.</span></span> |
| <span data-ttu-id="9c4f0-149">Cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="9c4f0-149">DeviceId</span></span> |<span data-ttu-id="9c4f0-150">**DeviceID** hello dosya karşıya hello cihazın.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-150">**DeviceId** of hello device which uploaded hello file.</span></span> |
| <span data-ttu-id="9c4f0-151">BlobUri</span><span class="sxs-lookup"><span data-stu-id="9c4f0-151">BlobUri</span></span> |<span data-ttu-id="9c4f0-152">Merhaba URI'sini dosyası karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-152">URI of hello uploaded file.</span></span> |
| <span data-ttu-id="9c4f0-153">BlobName</span><span class="sxs-lookup"><span data-stu-id="9c4f0-153">BlobName</span></span> |<span data-ttu-id="9c4f0-154">Merhaba adını dosyası karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-154">Name of hello uploaded file.</span></span> |
| <span data-ttu-id="9c4f0-155">LastUpdatedTime</span><span class="sxs-lookup"><span data-stu-id="9c4f0-155">LastUpdatedTime</span></span> |<span data-ttu-id="9c4f0-156">Merhaba dosyasının en son güncelleştirildiği belirten bir zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-156">Timestamp indicating when hello file was last updated.</span></span> |
| <span data-ttu-id="9c4f0-157">BlobSizeInBytes</span><span class="sxs-lookup"><span data-stu-id="9c4f0-157">BlobSizeInBytes</span></span> |<span data-ttu-id="9c4f0-158">Merhaba boyutunu dosyası karşıya yüklendi.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-158">Size of hello uploaded file.</span></span> |

<span data-ttu-id="9c4f0-159">**Örnek**.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-159">**Example**.</span></span> <span data-ttu-id="9c4f0-160">Bu örnek, bir dosya hello gövdesi karşıya bildirim iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-160">This example shows hello body of a file upload notification message.</span></span>

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a><span data-ttu-id="9c4f0-161">Dosya karşıya yükleme bildirim yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="9c4f0-161">File upload notification configuration options</span></span>

<span data-ttu-id="9c4f0-162">Her IOT hub'ı dosya karşıya yükleme bildirimleri için yapılandırma seçenekleri aşağıdaki hello sunar:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-162">Each IoT hub exposes hello following configuration options for file upload notifications:</span></span>

| <span data-ttu-id="9c4f0-163">Özellik</span><span class="sxs-lookup"><span data-stu-id="9c4f0-163">Property</span></span> | <span data-ttu-id="9c4f0-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9c4f0-164">Description</span></span> | <span data-ttu-id="9c4f0-165">Aralık ve varsayılan</span><span class="sxs-lookup"><span data-stu-id="9c4f0-165">Range and default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c4f0-166">**enableFileUploadNotifications**</span><span class="sxs-lookup"><span data-stu-id="9c4f0-166">**enableFileUploadNotifications**</span></span> |<span data-ttu-id="9c4f0-167">Dosya karşıya yükleme bildirimlerini toohello dosya bildirimleri uç noktası yazılmış olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-167">Controls whether file upload notifications are written toohello file notifications endpoint.</span></span> |<span data-ttu-id="9c4f0-168">Bool.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-168">Bool.</span></span> <span data-ttu-id="9c4f0-169">Varsayılan: True.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-169">Default: True.</span></span> |
| <span data-ttu-id="9c4f0-170">**fileNotifications.ttlAsIso8601**</span><span class="sxs-lookup"><span data-stu-id="9c4f0-170">**fileNotifications.ttlAsIso8601**</span></span> |<span data-ttu-id="9c4f0-171">Dosya karşıya yükleme bildirimleri için varsayılan TTL değeri.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-171">Default TTL for file upload notifications.</span></span> |<span data-ttu-id="9c4f0-172">Too48H ISO_8601 aralığı (en az 1 dakika).</span><span class="sxs-lookup"><span data-stu-id="9c4f0-172">ISO_8601 interval up too48H (minimum 1 minute).</span></span> <span data-ttu-id="9c4f0-173">Varsayılan: 1 saat.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-173">Default: 1 hour.</span></span> |
| <span data-ttu-id="9c4f0-174">**fileNotifications.lockDuration**</span><span class="sxs-lookup"><span data-stu-id="9c4f0-174">**fileNotifications.lockDuration**</span></span> |<span data-ttu-id="9c4f0-175">Merhaba dosya karşıya yükleme bildirimleri sırası süresince kilitleyin.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-175">Lock duration for hello file upload notifications queue.</span></span> |<span data-ttu-id="9c4f0-176">5 too300 saniye (en az 5 saniye).</span><span class="sxs-lookup"><span data-stu-id="9c4f0-176">5 too300 seconds (minimum 5 seconds).</span></span> <span data-ttu-id="9c4f0-177">Varsayılan: 60 saniye sayısı.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-177">Default: 60 seconds.</span></span> |
| <span data-ttu-id="9c4f0-178">**fileNotifications.maxDeliveryCount**</span><span class="sxs-lookup"><span data-stu-id="9c4f0-178">**fileNotifications.maxDeliveryCount**</span></span> |<span data-ttu-id="9c4f0-179">Maksimum teslimat sayısı hello dosyası için bildirim sırası karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-179">Maximum delivery count for hello file upload notification queue.</span></span> |<span data-ttu-id="9c4f0-180">1 too100.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-180">1 too100.</span></span> <span data-ttu-id="9c4f0-181">Varsayılan: 100.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-181">Default: 100.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="9c4f0-182">Ek başvuru bilgileri</span><span class="sxs-lookup"><span data-stu-id="9c4f0-182">Additional reference material</span></span>

<span data-ttu-id="9c4f0-183">Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-183">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="9c4f0-184">[IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-184">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="9c4f0-185">[Azaltma ve kotaları] [ lnk-quotas] hello kotaları açıklar ve IOT Hub hizmeti toohello uygulamak davranışları azaltma.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-185">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="9c4f0-186">[Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-186">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="9c4f0-187">[IOT hub'ı sorgu dili] [ lnk-query] tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz hello sorgu dili açıklar.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-187">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="9c4f0-188">[IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c4f0-188">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c4f0-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c4f0-189">Next steps</span></span>

<span data-ttu-id="9c4f0-190">IOT hub'ı kullanarak aygıtlardan tooupload nasıl dosyaları öğrendiniz artık IOT Hub Geliştirici Kılavuzu konuları aşağıdaki hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-190">Now you have learned how tooupload files from devices using IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="9c4f0-191">[IOT Hub cihaz kimliklerini yönetme][lnk-devguide-identities]</span><span class="sxs-lookup"><span data-stu-id="9c4f0-191">[Manage device identities in IoT Hub][lnk-devguide-identities]</span></span>
* <span data-ttu-id="9c4f0-192">[Denetim erişim tooIoT Hub][lnk-devguide-security]</span><span class="sxs-lookup"><span data-stu-id="9c4f0-192">[Control access tooIoT Hub][lnk-devguide-security]</span></span>
* <span data-ttu-id="9c4f0-193">[Cihaz çiftlerini toosynchronize durumu ve yapılandırmaları kullanacak][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="9c4f0-193">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="9c4f0-194">[Bir cihazda doğrudan bir yöntem çağırma][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="9c4f0-194">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="9c4f0-195">[Birden çok aygıta işleri zamanla][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="9c4f0-195">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="9c4f0-196">Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticiyi izleyerek hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="9c4f0-196">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="9c4f0-197">[Aygıtları toohello tooupload dosyalarından IOT Hub ile nasıl bulut][lnk-fileupload-tutorial]</span><span class="sxs-lookup"><span data-stu-id="9c4f0-197">[How tooupload files from devices toohello cloud with IoT Hub][lnk-fileupload-tutorial]</span></span>

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
