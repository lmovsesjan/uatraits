#Python
Interface consists of `detector` class. The class provides information of user device and application as a `dictionary`. Dictionary keys are described in [overview](overview.md) section of the document. Constructor of the class has two paramaters: a path to `browsers.xml` and (optionally) a path to `profiles.xml`.

Methods:

|Function|Description|
|-----|--------|
|[detect](#detect)|Returns user application and device descriprion, based on the `User-Agent` HTTP-header value.|
|[detect_by_headers](#detect_by_headers)|Returns user application and device descriprion, based on the `User-Agent`, `X-Wap-Profile`, `X-Operamini-Phone-Ua` HTTP-headers values.|

##detect
Returns user application and device descriprion.

**Parameters**

|Parameter|Description|
|--------|--------|
|uah|`User_Agent` HTTP-header.|

**Return value**
User application and device description as a `dictionary`. Dictionary keys are desctibed in [overview](overview.md) section of the document.

##detect_by_headers
Returns user application and device descriprion.

**Parameter**

|Parameter|Description|
|--------|--------|
|headers|`User-Agent`, `X-Wap-Profile`, `X-Operamini-Phone-Ua` HTTP-headers. Headers can be used in any combinations, all of them together or just some of them.|

**Return value**
User application and device description as a `dictionary`. Dictionary keys are desctibed in [overview](overview.md) section of the document.

## Example

```
import json
import uatraits

dtc = uatraits.detector('browser.xml', 'profiles.xml')
res = dtc.detect('Mozilla/5.0 (Linux; U; Android 2.2; ru-ru; Desire_A8181 Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1')
print 'res --------\n', json.dumps(res, indent=4)

res1 = dtc.detect_by_headers({
					"User-Agent":"Mozilla/5.0 (X11; U; Linux armv5tejl; en; rv:1.9.0.19) Gecko/2010072023 Firefox/3.0.6 (Debian-3.0.6-3)",
					"X-Wap-Profile":"http://nds1.nds.nokia.com/uaprof/N6020r100.xml",
					"X-Operamini-Phone-Ua":"Mozilla/5.0 (SymbianOS/9.4; Series60/5.0 NokiaN97-1/10.0.012; Profile/MIDP-2.1 Configuration/CLDC-1.1; en-us) AppleWebKit/525 (KHTML, like Gecko) WicKed/7.1.12344"
					})
print 'res1 --------\n', json.dumps(res1, indent=4)
```

**Result**

```
res --------
{
    "BrowserVersion": "4.0", 
    "BrowserEngine": "WebKit", 
    "isBrowser": true, 
    "PreferMobile": true, 
    "BrowserName": "AndroidBrowser", 
    "OSName": "Android Froyo", 
    "OSFamily": "Android", 
    "isTouch": true, 
    "BrowserEngineVersion": "533.1", 
    "MultiTouch": true, 
    "OSVersion": "2.2", 
    "isMobile": true
}

res1 --------
{
    "BrowserVersion": "3.0", 
    "BrowserEngine": "Gecko", 
    "DeviceModel": "6020", 
    "isBrowser": true, 
    "BitsPerPixel": "16", 
    "DeviceVendor": "Nokia", 
    "OSFamily": "Linux", 
    "OSName": "Debian", 
    "ScreenHeight": "128", 
    "BrowserName": "Firefox", 
    "ScreenSize": "128x128", 
    "BrowserEngineVersion": "1.9.0.19", 
    "ScreenWidth": "128", 
    "DeviceKeyboard": "PhoneKeyPad", 
    "isMobile": false
}
```