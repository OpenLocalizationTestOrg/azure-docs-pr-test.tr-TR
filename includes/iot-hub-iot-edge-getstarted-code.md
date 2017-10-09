## <a name="typical-output"></a><span data-ttu-id="cbf59-101">Normal çıktı</span><span class="sxs-lookup"><span data-stu-id="cbf59-101">Typical output</span></span>

<span data-ttu-id="cbf59-102">Merhaba aşağıdaki örnekte toohello günlük dosyası hello Hello World örnek tarafından yazılmış hello çıktısı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cbf59-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="cbf59-103">Merhaba çıktı için okunabilirliği biçimlendirilmiş:</span><span class="sxs-lookup"><span data-stu-id="cbf59-103">hello output is formatted for legibility:</span></span>

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a><span data-ttu-id="cbf59-104">Kod parçacıkları</span><span class="sxs-lookup"><span data-stu-id="cbf59-104">Code snippets</span></span>

<span data-ttu-id="cbf59-105">Bu bölümde bazı anahtar bölümler hello hello hello kod ele alınmaktadır\_world örneği.</span><span class="sxs-lookup"><span data-stu-id="cbf59-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="cbf59-106">IOT sınır ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbf59-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="cbf59-107">Uygulamanız gereken bir *ağ geçidi işlem*.</span><span class="sxs-lookup"><span data-stu-id="cbf59-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="cbf59-108">Bu program hello iç altyapı (Merhaba Aracısı) oluşturur, hello IOT kenar modüllerini yükler ve hello ağ geçidi işlem yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="cbf59-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="cbf59-109">IOT kenar sağlar hello **ağ geçidi\_oluşturma\_gelen\_JSON** tooenable işlev bir JSON dosyası bir ağ geçidi toobootstrap.</span><span class="sxs-lookup"><span data-stu-id="cbf59-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="cbf59-110">toouse hello **ağ geçidi\_oluşturma\_gelen\_JSON** işlev, hello IOT kenar modülleri tooload belirtir hello yol tooa JSON dosyası geçirin.</span><span class="sxs-lookup"><span data-stu-id="cbf59-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="cbf59-111">Merhaba ağ geçidi hello işleminde hello kod bulabilirsiniz *Hello World* hello örnek [main.c] [ lnk-main-c] dosya.</span><span class="sxs-lookup"><span data-stu-id="cbf59-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="cbf59-112">Okunabilirliği için hello aşağıdaki kod parçacığında hello ağ geçidi işlem kodu kısaltılmış bir sürümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="cbf59-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="cbf59-113">Bu örnek program bir ağ geçidi oluşturur ve hello kullanıcı toopress Merhaba bekler **ENTER** hello ağ geçidi çıkarır önce anahtar.</span><span class="sxs-lookup"><span data-stu-id="cbf59-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

<span data-ttu-id="cbf59-114">Merhaba JSON ayarları dosyası IOT kenar modülleri tooload ve hello modülleri arasında hello bağlantılar listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="cbf59-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="cbf59-115">Her IOT kenar modülü a: belirtmeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="cbf59-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="cbf59-116">**ad**: hello modülü için benzersiz bir ad.</span><span class="sxs-lookup"><span data-stu-id="cbf59-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="cbf59-117">**Yükleyici**: tooload hello modülü nasıl istenen bildiği bir yükleyicisi.</span><span class="sxs-lookup"><span data-stu-id="cbf59-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="cbf59-118">Yükleyiciler, farklı türlerdeki modüllerin yüklenmesi için bir uzantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="cbf59-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="cbf59-119">IOT kenar yükleyicilerini kullanım için yerel C, Node.js, Java ve .NET içinde yazılmış modüller sağlar.</span><span class="sxs-lookup"><span data-stu-id="cbf59-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="cbf59-120">Bu örnekteki tüm hello modülleri dinamik kitaplıkları c dilinde yazılmış olduğundan hello Hello World örnek hello yerel C yükleyicisi yalnızca kullanır. Hakkında daha fazla bilgi için bkz: hello farklı dillerde yazılmış toouse IOT kenar modülleri [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), veya [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) örnekleri.</span><span class="sxs-lookup"><span data-stu-id="cbf59-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="cbf59-121">**ad**: kullanılan tooload hello modülü hello yükleyicisi hello adı.</span><span class="sxs-lookup"><span data-stu-id="cbf59-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="cbf59-122">**EntryPoint**: hello modülü içeren hello yolu toohello kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="cbf59-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="cbf59-123">Linux için bu kitaplık bir .so dosyası, Windows'ta ise bir .dll dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="cbf59-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="cbf59-124">Merhaba giriş noktası belirli toohello kullanılan yükleyicisi türüdür.</span><span class="sxs-lookup"><span data-stu-id="cbf59-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="cbf59-125">Merhaba Node.js yükleyicisi giriş noktası bir .js dosya yok.</span><span class="sxs-lookup"><span data-stu-id="cbf59-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="cbf59-126">Merhaba Java yükleyicisi giriş noktası bir sınıf ve sınıf adı ' dir.</span><span class="sxs-lookup"><span data-stu-id="cbf59-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="cbf59-127">Merhaba .NET yükleyicisi giriş noktası bir derleme adı ve bir sınıf adıdır.</span><span class="sxs-lookup"><span data-stu-id="cbf59-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="cbf59-128">**bağımsız değişken**: herhangi bir yapılandırma bilgileri hello modülü gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="cbf59-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="cbf59-129">Aşağıdaki kodu gösterir hello kullanılan JSON toodeclare tüm hello IOT kenar modülleri hello Hello World Örnek Linux için hello.</span><span class="sxs-lookup"><span data-stu-id="cbf59-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="cbf59-130">Bir modül herhangi bir bağımsız değişken gerektirip gerektirmediğini hello modülü hello tasarımına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="cbf59-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="cbf59-131">Bu örnekte, hello Günlükçü modülü hello yolu toohello çıkış dosyasını ve hello hello olmayan bir bağımsız değişken alan\_world modülü bir bağımsız değişken içeriyor.</span><span class="sxs-lookup"><span data-stu-id="cbf59-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

<span data-ttu-id="cbf59-132">Merhaba JSON dosyası ayrıca toohello Aracısı geçirilen hello modülleri arasında hello bağlantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="cbf59-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="cbf59-133">Bir bağlantı iki özelliğe sahiptir:</span><span class="sxs-lookup"><span data-stu-id="cbf59-133">A link has two properties:</span></span>

* <span data-ttu-id="cbf59-134">**Kaynak**: hello modülü adından `modules` bölümünde veya `\*`.</span><span class="sxs-lookup"><span data-stu-id="cbf59-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="cbf59-135">**Havuz**: hello modülü adından `modules` bölümü.</span><span class="sxs-lookup"><span data-stu-id="cbf59-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="cbf59-136">Her bağlantı bir ileti yolu ve yönü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cbf59-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="cbf59-137">Merhaba iletilerden **kaynak** toohello modülü teslim edilen **havuz** modülü.</span><span class="sxs-lookup"><span data-stu-id="cbf59-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="cbf59-138">Merhaba ayarlayabilirsiniz **kaynak** modülü çok`\*`, o hello gösterir **havuz** modülü herhangi bir modül iletileri alır.</span><span class="sxs-lookup"><span data-stu-id="cbf59-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="cbf59-139">Merhaba aşağıdaki kod hello JSON tooconfigure bağlantılar hello hello kullanılan hello modülleri arasında kullanılan gösterir\_Linux'ta world örneği.</span><span class="sxs-lookup"><span data-stu-id="cbf59-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="cbf59-140">Her ileti hello tarafından üretilen `hello_world` modülü hello tarafından tüketilen `logger` modülü.</span><span class="sxs-lookup"><span data-stu-id="cbf59-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="cbf59-141">Merhaba\_dünya modülü ileti yayımlama</span><span class="sxs-lookup"><span data-stu-id="cbf59-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="cbf59-142">Merhaba hello tarafından kullanılan hello kodu bulabilirsiniz\_hello world modülü toopublish iletileri ['hello_world.c'] [ lnk-helloworld-c] dosya.</span><span class="sxs-lookup"><span data-stu-id="cbf59-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="cbf59-143">Merhaba aşağıdaki kod parçacığında hello kodu değiştirilmiş bir sürümünü eklenen açıklamalar ve bazı hata işleme için okunabilirliği kaldırılan kodunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="cbf59-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="cbf59-144">Merhaba\_dünya modülü ileti işleme</span><span class="sxs-lookup"><span data-stu-id="cbf59-144">Hello\_world module message processing</span></span>

<span data-ttu-id="cbf59-145">Merhaba hello\_world modülü iletileri diğer IOT kenar modüller toohello Aracısı yayımlama hiçbir zaman işler.</span><span class="sxs-lookup"><span data-stu-id="cbf59-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="cbf59-146">Bu nedenle, hello hello hello ileti geri uyarlamasını hello\_world modülüdür yok işlevi.</span><span class="sxs-lookup"><span data-stu-id="cbf59-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="cbf59-147">Günlükçü modülü ileti yayımlama ve işleme</span><span class="sxs-lookup"><span data-stu-id="cbf59-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="cbf59-148">Merhaba Günlükçü modülü hello Aracısı'ndan iletilerini alır ve bunları tooa dosyasına yazar.</span><span class="sxs-lookup"><span data-stu-id="cbf59-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="cbf59-149">Hiçbir zaman bir ileti yayımlamaz.</span><span class="sxs-lookup"><span data-stu-id="cbf59-149">It never publishes any messages.</span></span> <span data-ttu-id="cbf59-150">Bu nedenle, hello kod hello Günlükçü modülü hello hiçbir zaman çağırır **Broker_Publish** işlevi.</span><span class="sxs-lookup"><span data-stu-id="cbf59-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="cbf59-151">Merhaba **Logger_Receive** hello işlevinde [logger.c] [ lnk-logger-c] dosyasıdır hello geri çağırma hello Aracısı toodeliver iletileri toohello Günlükçü modülü çağırır.</span><span class="sxs-lookup"><span data-stu-id="cbf59-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="cbf59-152">Merhaba aşağıdaki kod parçacığında değiştirilmiş bir sürümünü eklenen açıklamalar ve bazı hata işleme için okunabilirliği kaldırılan kodunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="cbf59-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="cbf59-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cbf59-153">Next steps</span></span>

<span data-ttu-id="cbf59-154">Bu makalede, iletileri tooa günlük dosyasına yazar basit bir IOT sınır ağ geçidi verdi.</span><span class="sxs-lookup"><span data-stu-id="cbf59-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="cbf59-155">toorun iletileri tooIoT Hub, gönderdiği bir örnek görmek [IOT kenar – Linux kullanmak için sanal bir cihaz cihaz bulut iletilerini göndermek] [ lnk-gateway-simulated-linux] veya [IOT kenar – sahip cihaz bulut iletilerini göndermek bir Windows kullanarak sanal cihaz][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="cbf59-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md