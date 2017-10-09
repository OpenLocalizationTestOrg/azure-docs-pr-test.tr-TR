## <a name="specify-hello-behavior-of-hello-iot-device"></a><span data-ttu-id="3584d-101">Merhaba IOT cihaz Hello davranışını belirtin</span><span class="sxs-lookup"><span data-stu-id="3584d-101">Specify hello behavior of hello IoT device</span></span>

<span data-ttu-id="3584d-102">Merhaba IOT Hub seri hale getirici istemci kitaplığı IOT Hub ile bir model toospecify hello biçimi hello iletileri hello aygıt alışverişi kullanır.</span><span class="sxs-lookup"><span data-stu-id="3584d-102">hello IoT Hub serializer client library uses a model toospecify hello format of hello messages hello device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="3584d-103">Değişken bildirimleri hello sonra aşağıdaki hello eklemek `#include` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="3584d-103">Add hello following variable declarations after hello `#include` statements.</span></span> <span data-ttu-id="3584d-104">Yerine Hello yer tutucu değerler [aygıt kimliği] ve [aygıt anahtarı] aygıtınızın hello Uzaktan izleme çözüm panosunu not ettiğiniz değerlerle.</span><span class="sxs-lookup"><span data-stu-id="3584d-104">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="3584d-105">Merhaba çözüm Panosu tooreplace [Iothub adı] öğesinden Hello IOT Hub ana bilgisayar adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3584d-105">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="3584d-106">Örneğin, IoT Hub Ana Bilgisayar Adınız **contoso.azure-devices.net** şeklindeyse [IoTHub Adı] yerine **contoso** yazın:</span><span class="sxs-lookup"><span data-stu-id="3584d-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="3584d-107">IOT Hub ile Merhaba aygıt toocommunicate sağlayan kod toodefine hello modeli izleyen hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3584d-107">Add hello following code toodefine hello model that enables hello device toocommunicate with IoT Hub.</span></span> <span data-ttu-id="3584d-108">Bu model hello aygıt belirtir:</span><span class="sxs-lookup"><span data-stu-id="3584d-108">This model specifies that hello device:</span></span>

   - <span data-ttu-id="3584d-109">Sıcaklık, dış ortam sıcaklığı, nem oranı ve cihaz kimliğini telemetri olarak gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="3584d-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="3584d-110">Merhaba aygıt tooIoT Hub hakkında meta veriler gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="3584d-110">Can send metadata about hello device tooIoT Hub.</span></span> <span data-ttu-id="3584d-111">Merhaba cihaz temel meta verileri gönderir bir **Deviceınfo** başlangıçta nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3584d-111">hello device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="3584d-112">Bildirilen özellikleri, IOT Hub cihaz çiftine toohello gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3584d-112">Can send reported properties, toohello device twin in IoT Hub.</span></span> <span data-ttu-id="3584d-113">Bildirilen bu özellikler yapılandırma, cihaz ve sistem özellikleri olarak gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="3584d-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="3584d-114">Alabilir ve IOT Hub cihaz çiftine hello kümesindeki istenen özellikleri hareket.</span><span class="sxs-lookup"><span data-stu-id="3584d-114">Can receive and act on desired properties set in hello device twin in IoT Hub.</span></span>
   - <span data-ttu-id="3584d-115">Toohello yanıtlayabilir **yeniden** ve **InitiateFirmwareUpdate** doğrudan yöntemleri hello çözüm Portalı aracılığıyla çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3584d-115">Can respond toohello **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through hello solution portal.</span></span> <span data-ttu-id="3584d-116">Merhaba aygıt bildirilen özelliklerini kullanmayı destekler hello doğrudan yöntemleri hakkında bilgi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3584d-116">hello device sends information about hello direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define hello Model
    BEGIN_NAMESPACE(Contoso);

    /* Reported properties */
    DECLARE_STRUCT(SystemProperties,
      ascii_char_ptr, Manufacturer,
      ascii_char_ptr, FirmwareVersion,
      ascii_char_ptr, InstalledRAM,
      ascii_char_ptr, ModelNumber,
      ascii_char_ptr, Platform,
      ascii_char_ptr, Processor,
      ascii_char_ptr, SerialNumber
    );

    DECLARE_STRUCT(LocationProperties,
      double, Latitude,
      double, Longitude
    );

    DECLARE_STRUCT(ReportedDeviceProperties,
      ascii_char_ptr, DeviceState,
      LocationProperties, Location
    );

    DECLARE_MODEL(ConfigProperties,
      WITH_REPORTED_PROPERTY(double, TemperatureMeanValue),
      WITH_REPORTED_PROPERTY(uint8_t, TelemetryInterval)
    );

    /* Part of DeviceInfo */
    DECLARE_STRUCT(DeviceProperties,
      ascii_char_ptr, DeviceID,
      _Bool, HubEnabledState
    );

    DECLARE_DEVICETWIN_MODEL(Thermostat,
      /* Telemetry (temperature, external temperature and humidity) */
      WITH_DATA(double, Temperature),
      WITH_DATA(double, ExternalTemperature),
      WITH_DATA(double, Humidity),
      WITH_DATA(ascii_char_ptr, DeviceId),

      /* DeviceInfo */
      WITH_DATA(ascii_char_ptr, ObjectType),
      WITH_DATA(_Bool, IsSimulatedDevice),
      WITH_DATA(ascii_char_ptr, Version),
      WITH_DATA(DeviceProperties, DeviceProperties),

      /* Device twin properties */
      WITH_REPORTED_PROPERTY(ReportedDeviceProperties, Device),
      WITH_REPORTED_PROPERTY(ConfigProperties, Config),
      WITH_REPORTED_PROPERTY(SystemProperties, System),

      WITH_DESIRED_PROPERTY(double, TemperatureMeanValue, onDesiredTemperatureMeanValue),
      WITH_DESIRED_PROPERTY(uint8_t, TelemetryInterval, onDesiredTelemetryInterval),

      /* Direct methods implemented by hello device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-hello-behavior-of-hello-device"></a><span data-ttu-id="3584d-117">Merhaba aygıt Hello davranışını uygulama</span><span class="sxs-lookup"><span data-stu-id="3584d-117">Implement hello behavior of hello device</span></span>
<span data-ttu-id="3584d-118">Şimdi hello modelde tanımlanmış hello davranışı uygulayan kodunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3584d-118">Now add code that implements hello behavior defined in hello model.</span></span>

1. <span data-ttu-id="3584d-119">İstenen hello özelliklerini hello çözüm panosunda Ayarla işlemek işlevleri aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3584d-119">Add hello following functions that handle hello desired properties set in hello solution dashboard.</span></span> <span data-ttu-id="3584d-120">İstenen bu özellikleri hello modelinde tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="3584d-120">These desired properties are defined in hello model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="3584d-121">Merhaba IOT hub'ı aracılığıyla çağrılan hello doğrudan yöntemlerini işlemek işlevleri aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3584d-121">Add hello following functions that handle hello direct methods invoked through hello IoT hub.</span></span> <span data-ttu-id="3584d-122">Doğrudan bu yöntemleri hello modelinde tanımlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="3584d-122">These direct methods are defined in hello model:</span></span>

    ```c
    /* Handlers for direct methods */
    METHODRETURN_HANDLE Reboot(Thermostat* thermostat)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Rebooting\"");
      printf("Received reboot request\r\n");
      return result;
    }

    METHODRETURN_HANDLE InitiateFirmwareUpdate(Thermostat* thermostat, ascii_char_ptr FwPackageURI)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Initiating Firmware Update\"");
      printf("Recieved firmware update request. Use package at: %s\r\n", FwPackageURI);
      return result;
    }
    ```

1. <span data-ttu-id="3584d-123">Bir ileti toohello önceden yapılandırılmış çözümü gönderir işlevi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3584d-123">Add hello following function that sends a message toohello preconfigured solution:</span></span>
   
    ```c
    /* Send data tooIoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable toocreate a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted hello message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="3584d-124">Merhaba aygıt yeni bildirilen özellik değerlerinin toohello önceden yapılandırılmış çözümü gönderildiğinde çalıştırılan geri çağırma işleyici aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3584d-124">Add hello following callback handler that runs when hello device has sent new reported property values toohello preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="3584d-125">Merhaba aşağıdaki cihaz toohello önceden yapılandırılmış çözümünüz hello bulutta tooconnect işlev ve veri değişimi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3584d-125">Add hello following function tooconnect your device toohello preconfigured solution in hello cloud, and exchange data.</span></span> <span data-ttu-id="3584d-126">Bu işlev hello aşağıdaki adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="3584d-126">This function performs hello following steps:</span></span>

    - <span data-ttu-id="3584d-127">Merhaba platform başlatır.</span><span class="sxs-lookup"><span data-stu-id="3584d-127">Initializes hello platform.</span></span>
    - <span data-ttu-id="3584d-128">Merhaba Contoso ad hello seri hale getirme kitaplığı ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3584d-128">Registers hello Contoso namespace with hello serialization library.</span></span>
    - <span data-ttu-id="3584d-129">Merhaba istemci hello cihaz bağlantı dizesiyle başlatır.</span><span class="sxs-lookup"><span data-stu-id="3584d-129">Initializes hello client with hello device connection string.</span></span>
    - <span data-ttu-id="3584d-130">Merhaba örneğini oluşturmak **Thermostat** modeli.</span><span class="sxs-lookup"><span data-stu-id="3584d-130">Create an instance of hello **Thermostat** model.</span></span>
    - <span data-ttu-id="3584d-131">Bildirilen özellik değerlerini oluşturur ve gönderir.</span><span class="sxs-lookup"><span data-stu-id="3584d-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="3584d-132">Bir **DeviceInfo** nesnesi gönderir.</span><span class="sxs-lookup"><span data-stu-id="3584d-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="3584d-133">Döngü toosend telemetri saniyede oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3584d-133">Creates a loop toosend telemetry every second.</span></span>
    - <span data-ttu-id="3584d-134">Tüm kaynakların başlatılmasını geri alır.</span><span class="sxs-lookup"><span data-stu-id="3584d-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed tooinitialize hello platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable tooSERIALIZER_REGISTER_NAMESPACE\n");
          }
          else
          {
            IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, MQTT_Protocol);
            if (iotHubClientHandle == NULL)
            {
              printf("Failure in IoTHubClient_CreateFromConnectionString\n");
            }
            else
            {
      #ifdef MBED_BUILD_TIMESTAMP
              // For mbed add hello certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed tooset option \"TrustedCerts\"\n");
              }
      #endif // MBED_BUILD_TIMESTAMP
              Thermostat* thermostat = IoTHubDeviceTwin_CreateThermostat(iotHubClientHandle);
              if (thermostat == NULL)
              {
                printf("Failure in IoTHubDeviceTwin_CreateThermostat\n");
              }
              else
              {
                /* Set values for reported properties */
                thermostat->Config.TemperatureMeanValue = 55.5;
                thermostat->Config.TelemetryInterval = 3;
                thermostat->Device.DeviceState = "normal";
                thermostat->Device.Location.Latitude = 47.642877;
                thermostat->Device.Location.Longitude = -122.125497;
                thermostat->System.Manufacturer = "Contoso Inc.";
                thermostat->System.FirmwareVersion = "2.22";
                thermostat->System.InstalledRAM = "8 MB";
                thermostat->System.ModelNumber = "DB-14";
                thermostat->System.Platform = "Plat 9.75";
                thermostat->System.Processor = "i3-7";
                thermostat->System.SerialNumber = "SER21";
                /* Specify hello signatures of hello supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot hello device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file\"}";

                /* Send reported properties tooIoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object tooIoT Hub at startup\n");
      
                  thermostat->ObjectType = "DeviceInfo";
                  thermostat->IsSimulatedDevice = 0;
                  thermostat->Version = "1.0";
                  thermostat->DeviceProperties.HubEnabledState = 1;
                  thermostat->DeviceProperties.DeviceID = (char*)deviceId;

                  unsigned char* buffer;
                  size_t bufferSize;

                  if (SERIALIZE(&buffer, &bufferSize, thermostat->ObjectType, thermostat->Version, thermostat->IsSimulatedDevice, thermostat->DeviceProperties) != CODEFIRST_OK)
                  {
                    (void)printf("Failed serializing DeviceInfo\n");
                  }
                  else
                  {
                    sendMessage(iotHubClientHandle, buffer, bufferSize);
                  }

                  /* Send telemetry */
                  thermostat->Temperature = 50;
                  thermostat->ExternalTemperature = 55;
                  thermostat->Humidity = 50;
                  thermostat->DeviceId = (char*)deviceId;

                  while (1)
                  {
                    unsigned char*buffer;
                    size_t bufferSize;

                    (void)printf("Sending sensor value Temperature = %f, Humidity = %f\n", thermostat->Temperature, thermostat->Humidity);

                    if (SERIALIZE(&buffer, &bufferSize, thermostat->DeviceId, thermostat->Temperature, thermostat->Humidity, thermostat->ExternalTemperature) != CODEFIRST_OK)
                    {
                      (void)printf("Failed sending sensor value\r\n");
                    }
                    else
                    {
                      sendMessage(iotHubClientHandle, buffer, bufferSize);
                    }

                    ThreadAPI_Sleep(1000);
                  }

                  IoTHubDeviceTwin_DestroyThermostat(thermostat);
                }
              }
              IoTHubClient_Destroy(iotHubClientHandle);
            }
            serializer_deinit();
          }
        }
        platform_deinit();
      }
    ```
   
    <span data-ttu-id="3584d-135">Başvuru için örnek bir işte **Telemetri** gönderilen ileti toohello önceden yapılandırılmış çözüm:</span><span class="sxs-lookup"><span data-stu-id="3584d-135">For reference, here is a sample **Telemetry** message sent toohello preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```