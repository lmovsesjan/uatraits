#C++ interface
API contains `uatraits` namespase with `detector` class.

Member functions of `detector` class:

|Function|Description|
|-----|--------|
|[detector](#constructor)|Constructor.|
|[detect](#detect)|Returns description of user application and device.|

##Constructor

```
detector(char const *file);
detector(char const *file, char const *profiles);
```

**Parameters**

|**Parameter**|**Description**|
|------------|------------|
|file|Path to `browsers.xml`. |
|profiles|Path to `profiles.xml`.|

##detect
Returns description of user application and device.

```
	result_type detect(char const *agent) const;
	result_type detect(std::string const &agent) const;

	void detect(char const *agent, result_type &result) const;
	void detect(std::string const &agent, result_type &result) const;

	void detect(const std::map<std::string, std::string> &headers, result_type &result) const;
```

**Parameters**

|Parameter|Description|
|--------|--------|
|agent|`User-Agent` HTTP-header.|
|result|Output. `result_type` defined in `detector` class|
|headers|HTTP-headers `User-Agent`, `X-Wap-Profile`, `X-Operamini-Phone-Ua`.|

**Return value**
User device and application description as a `map`. Map keys are described in [overview](overview.md) section of the document.

**Example**

```
#include <iostream>
#include "uatraits/detector.hpp"

using namespace uatraits;
using namespace std;

int main(int argc, char *argv[]) {
	detector dtc("browser.xml", "profiles.xml");
	
	detector::result_type res, res1;
	detector::result_type::iterator resIt;
	map<string, string> headers;
	
	res = dtc.detect("Mozilla/5.0 (Linux; U; Android 2.2; ru-ru; Desire_A8181 Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1");
		
	cout<<"res --------\n";
	for(resIt = res.begin(); resIt != res.end(); resIt++ ){
		cout << (*resIt).first <<" : "<< (*resIt).second << endl;
	}
		
	headers["User-Agent"] = "Mozilla/5.0 (X11; U; Linux armv5tejl; en; rv:1.9.0.19) Gecko/2010072023 Firefox/3.0.6 (Debian-3.0.6-3)";
	headers["X-Wap-Profile"] = "http://nds1.nds.nokia.com/uaprof/N6020r100.xml";
	headers["X-Operamini-Phone-Ua"] = "Mozilla/5.0 (SymbianOS/9.4; Series60/5.0 NokiaN97-1/10.0.012; Profile/MIDP-2.1 Configuration/CLDC-1.1; en-us) AppleWebKit/525 (KHTML, like Gecko) WicKed/7.1.12344";
	
	dtc.detect(headers, res1);
	cout<<endl<<"res1 --------\n";
	for(resIt = res1.begin(); resIt != res1.end(); resIt++ ){
		cout << (*resIt).first <<" : "<< (*resIt).second << endl;
	}

	return 0;
}
```

**Result**

```
res --------
BrowserEngine : WebKit
BrowserEngineVersion : 533.1
BrowserName : AndroidBrowser
BrowserVersion : 4.0
MultiTouch : true
OSFamily : Android
OSName : Android Froyo
OSVersion : 2.2
PreferMobile : true
isBrowser : true
isMobile : true
isTouch : true

res1 --------
BitsPerPixel : 16
BrowserEngine : Gecko
BrowserEngineVersion : 1.9.0.19
BrowserName : Firefox
BrowserVersion : 3.0
DeviceKeyboard : PhoneKeyPad
DeviceModel : 6020
DeviceVendor : Nokia
OSFamily : Linux
OSName : Debian
ScreenHeight : 128
ScreenSize : 128x128
ScreenWidth : 128
isBrowser : true
isMobile : false
```
