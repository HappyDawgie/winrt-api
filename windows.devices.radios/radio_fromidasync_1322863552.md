---
-api-id: M:Windows.Devices.Radios.Radio.FromIdAsync(System.String)
-api-type: winrt method
-api-device-family-note: xbox
---

<!-- Method syntax
public Windows.Foundation.IAsyncOperation<Windows.Devices.Radios.Radio> FromIdAsync(System.String deviceId)
-->

# Windows.Devices.Radios.Radio.FromIdAsync

## -description
A static method that retrieves a [Radio](radio.md) object. The method accepts the 'Device.Id' found  through [Windows.Devices.Enumeration.DeviceInformation.FindAllAsync](../windows.devices.enumeration/deviceinformation_findallasync_1257462890.md). This procedure is more reliable than using Radio.GetRadiosAsync() to obtain a radio in situations where a USB Radio has failed or been removed on a Windows10 workstation.  In this instance, Radio.GetRadiosAsync() returns no bluetooth radio.  DeviceInformation.FindAllAsync, in contrast, returns the radio object, which will report itself as being in the state of 'Disabled'.

## -parameters
### -param deviceId
A string that identifies a particular radio device.

## -returns
An asynchronous retrieval operation. On successful completion, it contains a [Radio](radio.md) object that represents the specified radio device. Otherwise it throws an exception.

## -remarks

## -examples

## -see-also
