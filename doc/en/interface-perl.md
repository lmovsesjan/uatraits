#Perl

Interface contained in `uatraits` module. The class provides information of user device and application as a `hash`. Hash keys are described in [overview](overview.md) section of the document. Constructor of the class has two paramaters: a path to `browsers.xml` and (optionally) a path to `profiles.xml`.

Methods:

|Method|Description|
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
User application and device description as a `hash`. Hash keys are desctibed in [overview](overview.md) section of the document.

##detect_by_headers
Returns user application and device descriprion.

**Parameter**

|Parameter|Description|
|--------|--------|
|headers|`User-Agent`, `X-Wap-Profile`, `X-Operamini-Phone-Ua` HTTP-headers. Headers can be used in any combinations, all of them together or just some of them.|

**Return value**
User application and device description as a `hash`. Hash keys are desctibed in [overview](overview.md) section of the document.

## Example

```
use Data::Dumper;
use uatraits;

my $dtc = uatraits->new("browser.xml", "profiles.xml");

my $res = $dtc->detect('Mozilla/5.0 (Linux; U; Android 2.2; ru-ru; Desire_A8181 Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1');

print "res --------\n";
print Dumper($res);
			
my $res1 = $dtc->detect_by_headers({
					'User-Agent' => 'Mozilla/5.0 (X11; U; Linux armv5tejl; en; rv:1.9.0.19) Gecko/2010072023 Firefox/3.0.6 (Debian-3.0.6-3)',
					'X-Wap-Profile' => 'http://nds1.nds.nokia.com/uaprof/N6020r100.xml',
					'X-Operamini-Phone-Ua' => 'Mozilla/5.0 (SymbianOS/9.4; Series60/5.0 NokiaN97-1/10.0.012; Profile/MIDP-2.1 Configuration/CLDC-1.1; en-us) AppleWebKit/525 (KHTML, like Gecko) WicKed/7.1.12344'
		});

print "\nres1 --------\n";
print Dumper($res1);
```

**Result**

```
res --------
$VAR1 = {
          'OSFamily' => 'Android',
          'BrowserEngine' => 'WebKit',
          'PreferMobile' => 1,
          'BrowserEngineVersion' => '533.1',
          'OSName' => 'Android Froyo',
          'isBrowser' => 1,
          'isMobile' => 1,
          'MultiTouch' => 1,
          'OSVersion' => '2.2',
          'BrowserVersion' => '4.0',
          'BrowserName' => 'AndroidBrowser',
          'isTouch' => 1
        };

res1 --------
$VAR1 = {
          'OSFamily' => 'Linux',
          'BrowserEngine' => 'Gecko',
          'ScreenWidth' => '128',
          'BrowserEngineVersion' => '1.9.0.19',
          'ScreenSize' => '128x128',
          'OSName' => 'Debian',
          'isBrowser' => 1,
          'BitsPerPixel' => '16',
          'isMobile' => 0,
          'ScreenHeight' => '128',
          'DeviceVendor' => 'Nokia',
          'DeviceModel' => '6020',
          'BrowserVersion' => '3.0',
          'BrowserName' => 'Firefox',
          'DeviceKeyboard' => 'PhoneKeyPad'
        };
```
