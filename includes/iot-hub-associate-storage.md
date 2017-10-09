## <a name="associate-an-azure-storage-account-tooiot-hub"></a>Bir Azure depolama hesabı tooIoT Hub ilişkilendirme

Merhaba sanal cihaz uygulamasının bir dosya tooa blob'u karşıya çünkü olmalıdır bir [Azure Storage](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) hesabı ilişkili tooIoT Hub. Bir Azure depolama hesabı bir IOT hub ile ilişkilendirdiğinizde, hello IOT hub'ı bir SAS URI'sini oluşturur. Bir aygıt bu SAS URI'sini toosecurely karşıya bir dosya tooa blob kapsayıcısı kullanabilirsiniz. Merhaba IOT Hub hizmeti ve hello cihaz SDK'ları hello SAS URI'sini oluşturur ve kullanılabilir tooa aygıt toouse tooupload bir dosya kolaylaştırır hello işlem koordinatı.

Merhaba yönergeleri izleyin [yapılandırma dosya yüklemeleri hello Azure portal kullanarak](../articles/iot-hub/iot-hub-configure-file-upload.md) tooassociate Azure depolama hesabı tooyour IOT hub'ı. Bir blob kapsayıcısını, IOT hub ile ilişkili olduğunu ve dosya bildirimlerini etkin olduğundan emin olun.

![Portalda dosya bildirimlerini etkinleştir](media/iot-hub-associate-storage/enable-file-notifications.png)