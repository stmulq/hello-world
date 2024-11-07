# HTML Best Practices

![](https://brightsign.atlassian.net/wiki/images/icons/grey_arrow_down.png)

Table of Contents

*   [Content Restrictions](#content-restrictions)
    *   [Web Browsing](#web-browsing)
    *   [Flash Content](#flash-content)
    *   [Video](#video)
    *   [4K Graphics](#4k-graphics)
        *   [XTx44, XTx43](#xtx44-xtx43)
        *   [XDx34, XDx33, HDx24, HDx23, LS424, LS423, 4Kx42](#xdx34-xdx33-hdx24-hdx23-ls424-ls423-4kx42)
    *   [Pixel Sizes and Coordinates with 4K Modes](#pixel-sizes-and-coordinates-with-4k-modes)
    *   [Image Sizes](#image-sizes)
    *   [Memory and Performance](#memory-and-performance)
    *   [Web Fonts](#web-fonts)
*   [Creating HTML Pages](#creating-html-pages)
*   [BrightSign Extensions](#brightsign-extensions)
    *   [GPU Rasterization](#gpu-rasterization)
    *   [Optimized Image Rendering](#optimized-image-rendering)
*   [Renderer Versions and Support](#renderer-versions-and-support)
*   [Animations and Add-on Libraries](#animations-and-add-on-libraries)
    *   [JavaScript Animations](#javascript-animations)
    *   [WebGL](#webgl)
    *   [Vector Animations](#vector-animations)
    *   [Canvas Animations](#canvas-animations)
    *   [Push Technology](#push-technology)
    *   [File Storage](#file-storage)
    *   [File Downloads](#file-downloads)
    *   [CSS Transforms](#css-transforms)
*   [HTML Storage](#html-storage)
    *   [Initialization](#initialization)
    *   [Storage Path](#storage-path)
    *   [Storage Quota](#storage-quota)
*   [Touchscreen Support](#touchscreen-support)
*   [Debugging Webpages](#debugging-webpages)
    *   [Web Inspector](#web-inspector)
        *   [Enabling the Web Inspector](#enabling-the-web-inspector)
        *   [Inspecting a Webpage](#inspecting-a-webpage)
        *   [Chromium Version Compatibility](#chromium-version-compatibility)
    *   [Trace Events](#trace-events)
        *   [Creating a TraceEvent Directory](#creating-a-traceevent-directory)
        *   [Enabling the TraceEvent System](#enabling-the-traceevent-system)
            *   [Example (JavaScript):](#example-javascript)
        *   [Viewing Trace Events](#viewing-trace-events)
        *   [Additional Documentation](#additional-documentation)
*   [Disabling Staged ES6 Features](#disabling-staged-es6-features)

This page covers the content requirements, abilities, and restrictions of the HTML rendering engine on BrightSign players.

## Content Restrictions

The following are content restrictions associated with HTML pages:

### Web Browsing

BrightSign players are *not* intended for use as general-purpose web browsers. It is best to think of BrightSign units as HTML players with interactive capabilities, not web-surfing tools: Each page should be thoroughly tested before being used as digital signage.

### Flash Content

BrightSign players do not support Flash content. Any HTML pages that have embedded flash content will not display correctly. Most Flash authoring applications, including the Adobe Creative Suite, have tools that allow you to export flash content as HTML.

### Video

See the [HTML Video](../html-development/html-video.md) page for usage rules regarding HTML video.

### 4K Graphics

While many BrightSign models can output 4K video modes (3840x2160), not all of these models can render HTML at 4K:

#### XTx44, XTx43

The XTx44 and XTx43 models support a native 4K HTML graphics plane (see [this page](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370678836/Full-Resolution+Graphics) for more details). Note the following performance restrictions when using native 4K HTML graphics:

*   Animations will not exceed 20 FPS (and intensive animations may exhibit very low framerates).
    
*   Non-HWZ video is likewise limited to 20 FPS, so [HWZ](../html-development/html-video.md) should be enabled for video elements in native 4K.
    
*   We recommend displaying only one or two 4K images at a time (for example, a slideshow with one image displayed and next image preloaded). Images should not exceed 3840x2160 in size. 
    
*   We recommend using [swap memory](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370677463/roVirtualMemory) if possible. 
    
*   Pages that use many layers may run out of memory in native 4K. Enabling the [gfxmemlarge](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672969/roVideoMode#roVideoMode-setmode) setting may help mitigate this issue.
    

#### XDx34, XDx33, HDx24, HDx23, LS424, LS423, 4Kx42

The XD, HD, LS, and 4K models support graphics up to 1920x1200 (see [this page](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370678836/Full-Resolution+Graphics) for more details), which can then be upscaled to a 4K video mode. Pages must be specified as 1920x1080 (or 2048x1080 for DCI 4K); they can then be upscaled to 4K.

### Pixel Sizes and Coordinates with 4K Modes

As noted above, webpages are often upscaled when outputting a 4K video mode. Relative CSS property values will scale automatically, but pixel values may need to be modified to account for differences between 4K video and graphics. See [here](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672927/roRectangle#roRectangle-4k_modes) for more information about using coordinates with upscaled video modes.

### Image Sizes

Images larger than 2048x1280x32bpp (or 3840x2160x32bpp for XT, 4K, XTx34, and XDx33 players) will not be displayed by default. If a 4K video mode is used, the player will upscale images from HD resolution accordingly (though [native 4K graphics](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370678836/Full-Resolution+Graphics) can be enabled on the XTx43). The default limit can be increased in BrightScript using the [*roVideoMode.SetImageSizeThreshold()*](http://docs.brightsign.biz/display/DOC/roVideoMode#roVideoMode-SetImageSizeThreshold(parametersAsroAssociativeArray)AsBoolean) method.

Without altering the default maximum resolution, you can increase the maximum width of images by sacrificing height (e.g. using a 3840x640x32bpp image on non-4K players is allowed). You can also increase the maximum width/height by reducing the bpp value (e.g. using a 3840x2160x16bpp on non-4K players is allowed).

> [!NOTE]
> For performance reasons, we recommend against downscaling images. This consumes considerably more resources than either displaying images at their native size or upscaling them.

### Memory and Performance

The amount of memory available for HTML applications varies by model and player series:

**Series 5 Players**

Unlike Series 4 and older players, Series 5 players don’t have pre-allocated graphics and system memory. There are limitations on GPU memory in Chromium so that demanding GPU applications don’t deplete that memory.

**Series 4 and Older Players**

*   **XTx43, XTx44**: 512MB for graphics; 512MB for JavaScript
    
*   **XDx33, XDx34**: 256MB for graphics; 512MB for JavaScript
    
*   **HDx23/LS423/HO523**: 256MB for graphics; 128MB for JavaScript
    

**Notes**

*   The memory available for graphics can be reduced by a number of factors, including the number of CSS layers, the complexity of animations, and the use of WebGL.
    
*   The JavaScript memory is subject to a hard limit: If there is no JavaScript memory after garbage collection, Chromium will terminate the active process.
    
*   Each HTML widget has its own JavaScript heap, so it's possible to overcommit JavaScript memory if multiple HTML widgets are active.
    

> [!TIP]
> Often, the best way to improve graphics performance is to ensure that images are scaled to the desired output resolution before they are rendered in HTML.

> [!NOTE]
> Use the [Chromium Web Inspector](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672286/HTML+Best+Practices#Debugging-Webpages) to determine the amount of resources being used by a webpage.

### Web Fonts

If a font file is not included and referenced by the HTML page, text will be rendered using a default system font. While functional, the default font has little aesthetic appeal, so we recommend including font files for most digital-signage applications. Supported font types include TrueType Font files (*.ttf*), OpenType Font (*.otf*), and Web Open Font files (*.woff*, *.woff2*).

## Creating HTML Pages

Follow these steps when creating HTML pages:

1.  Make sure the HTML page has the same aspect ratio as your signage display. If you are using HTML content in a BrightAuthor zone that is smaller than the screen, fit the page to the same aspect ratio as the zone.
    
2.  Use a master Div aligned to 0,0 when building an HTML page. This will ensure correct alignment.
    
3.  When creating an HTML site, make sure that all webpage assets (image files, video files, etc.) are contained within the same folder on your local disk. This folder is a “site folder,” meaning that all assets in this folder and its subfolders will be used in the production of the webpage. If these assets are not in the folder, they will not display when the project is published.
    
4.  You can test the layout and appearance of a page locally by opening it with Google Chrome, which has similar rendering capabilities to BrightSign players.
    
5.  If you want to publish resource-intensive presentations (e.g. `<video>` elements or multiple transforms) using HTML, we recommend using a Class 10 (10Mb/s) SD card.
    

## BrightSign Extensions

The BrightSign implementation of the Chromium engine includes several platform-specific extensions. Extensions for <video> elements are covered on the [HTML Video](../html-development/html-video.md) page.

### GPU Rasterization

GPU rasterization is enabled by default in firmware versions 6.2.x and later. 

### Optimized Image Rendering

The `image-rendering` CSS property can be assigned the `optimizeSpeedBS` value. Using this value ensures that Chromium uses lower-quality but faster bilinear filtering when scaling images to 50% or less. We recommend using this value with pages that scale a lot of images at runtime.

## Renderer Versions and Support

The following table describes which version of web-rendering engine is used in each version of BrightSign firmware:

| Rendering Engine | Version | BrightSign FW Versions |
| --- | --- | --- |
| Chromium | 87  | 8.5.x, 9.0x |
| Chromium | 69  | 8.4.x, 8.3.x, 8.2.x, 8.1.x |
| Chromium | 65  | 8.0.x |
| Chromium | 45  | 7.1.x, 7.0.x, 6.2.x |
| Chromium | 37  | 6.1.x, 6.0.x |
| WebKit | \-- | 5.1.x, 5.0.x, 4.8.x, 4.7.x |

See [this page](https://docs.brightsign.biz/space/DOC/2303000608/Previous+Chromium+Downloads+for+Older+OS+Versions) to download any of the listed Chromium versions. Use [this page](http://caniuse.com/) to determine if specific function calls and extensions are supported in a corresponding version of Chrome.

> [!NOTE]
> Chromium version 69 or later will refuse SHA-1 certificates. See [this page](https://www.chromium.org/Home/chromium-security/education/tls/sha-1/) for more information.

## Animations and Add-on Libraries

This section outlines support for animations and add-on libraries for the Chromium engine on BrightSign players.

> [!TIP]
> Limit file directory depth to prevent issues caused by overly complex folder structures.

### JavaScript Animations

Animations that use JavaScript timers, including the jQuery® .animate() library, do not make efficient use of GPU resources and are not accurate enough to achieve smooth animations. For this reason, we recommend using CSS animations whenever possible. The jQuery® [Transit library](https://github.com/rstacruz/jquery.transit) uses CSS animations and provides an API similar to the .animate() library.

> [!NOTE]
> For best results when animating images, we recommend using images at their original size instead of scaling them first. For example, a 480x270 icon will rotate more smoothly if you use an image that is originally 480x270, rather than scaling down a 1280x720 image and then attempting to rotate it.

### WebGL

BrightSign players support the OpenGL API for JavaScript (i.e. WebGL). 

> [!NOTE]
> Textures will sometimes fail to load in WebGL because they exceed the [maximum allowed image size](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/2307784705/Supported+Image+Formats) on BrightSign Players. In these cases, you can use [*roVideoMode.SetImageSizeThreshold()*](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672969/roVideoMode#roVideoMode-setimagesizethreshold()) BrightScript method to increase the maximum size for textures.

### Vector Animations

The SVG protocol should be used to specify vector animations.

### Canvas Animations

Bitmap animations display smoothly when they are 1/3 or less of a 1080p HTML canvas. Setting the canvas size to 720p allows for larger high-quality animations to occupy the screen.

### Push Technology

The long polling technique has been tested and proven to work on BrightSign players.

The Websocket protocol is fully supported via the [Node.js](../html-development/nodejs.md) implementation on the BrightSign Chromium instance. In production environments, we recommend using HTTPS to initiate Websocket connections with a server (i.e using a WSS connection rather than a WS connection).

An example Websocket application is available on the [BrightSign Github](https://github.com/brightsign/websocket-test) page.

### File Storage

BrightSign players support several file storage/indexing technologies, including Web SQL, IndexedDB, the HTML Filesystem API, and the JavaScript *storage* class. The location and size of the web storage database should be set [during initialization of the *roHtmlWidget*](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672896/roHtmlWidget#roHtmlWidget-storage_path) .

### File Downloads

If you're using JavaScript to download files, we reccomend using the Fetch API and Node.js® File System module to perform downloads. See [this page](../html-development/nodejs.md) for more details

### CSS Transforms

All CSS transforms should be specified as WebKit transforms. When performing a transform on a <div> or graphics element, you should not specify the transform in-line.

The following code shows an example of an effective CSS transform for a BrightSign player:

**Example:**

```
<style>
 
                .flipme{
                -webkit-animation-name:flipon;
                -webkit-animation-fill-mode:forwards;
                -webkit-animation-iteration-count:1;
                -webkit-animation-duration:2s;
                }
 
 
@-webkit-keyframes flipon
{
0% {-webkit-transform:rotateY(0deg);}
30% {-webkit-transform:rotateY(-90deg);}
100% {-webkit-transform: rotateY(360deg);}
}
 
</style>
```

## HTML Storage

The following [*roHtmlWidget*](https://docs.brightsign.biz/display/DOC/roHtmlWidget#roHtmlWidget-setlocalstoragedir()) methods are used to configure HTML storage on the BrightSign player:

*   `SetLocalStorageDir()`
    
*   `SetLocalStorageQuota()`
    
*   `SetWebDatabaseDir()`
    
*   `SetWebStorageQuota()`
    
*   `SetAppCacheDir()`
    
*   `SetAppCacheQuota()`
    

> [!NOTE]
> The behavior of *roHtmlWidget* storage methods has changed in OS8. The new behavior is described below. Updating a player to OS8 from 7.1.x or earlier will cause stored HTML data on the player to be reset.

### Initialization

The above methods take effect when a new *roHtmlWidget* instance is created; they don't apply to the *roHtmlWidget* instance on which they are called (this is not the case for the the `storage_path` and `storage_quota` [initialization parameters](https://docs.brightsign.biz/display/DOC/roHtmlWidget#roHtmlWidget-initialization_parameters)).

### Storage Path

The `SetLocalStorageDir()`, `SetWebDatabaseDir()`, and `SetAppCacheDir()` methods all configure the same storage path, so calling one of these methods will overwrite the storage path configured by the other methods.

Without a storage path (for example, when you are using an 'incognito' browser), nothing will persist when you are finished with the Chromium instance. If you want data to persist through reboot and widget creation, you must set a storage path. When non-persistent (incognito) mode is used, 10% of the total system memory is reserved for browser storage. This memory will be shared between multiple roHtmlWidget instances.

### Storage Quota

The `SetLocalStorageQuota()`, `SetWebStorageQuota()`, and `SetAppCacheQuota()` methods all configure the same storage quota, which applies to all persistent HTML storage on the player. If the storage path is specified without a storage quota, Chromium defaults to reserving 1GB plus 10% of the total size of the storage device.

If there are multiple *roHtmlWidget* instances, the configured or default quota is shared among them.

## Touchscreen Support

BrightSign players are compatible with touchscreens that use standard HID drivers. Note that some manufacturers claim support for HID but still use custom drivers. See [this FAQ](http://support.brightsign.biz/hc/en-us/articles/218065617-Supported-touchscreens) for further discussion and a list of touchscreen models that have been tested with BrightSign players.

## Debugging Webpages

### Web Inspector

You can use the [Web Inspector](https://trac.webkit.org/wiki/WebInspector) to debug webpages over the local network.

> [!NOTE]
> The JavaScript console should only be used in non-production presentations and it should be disabled before you publish in a production environment because it uses more memory, which can lead to frequent reboots, and it compromises security.

#### Enabling the Web Inspector

The Web Inspector can be enabled using BrightAuthor:connected, BrightAuthor, or BrightScript:

*   **BrightAuthor:connected**: Select **Allow JavaScript console** in the [**Chromium Debugging**](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/404620688/Remote+Diagnostic+Web+Server#Diagnostics) section of the DWS and [**Enable Javascript console**](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/1632600407/HTML5+State) in **Presentation tab > State Properties > Options**. To disable Chromium debugging, uncheck either of these boxes.
    
*   **BrightAuthor**: In your BrightAuthor presentation, navigate to **File > Presentation Properties > HTML** and check the **Enable Javascript console** box. Note that as of BOS 8.5.31 you will need to also set the enable\_web\_inspector registry key (in the "html" section) to enable the JavaScript console. See the "inspector\_server" in [roHtmlWidget](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672896/roHtmlWidget) for more information.
    
*   **BrightScript**: When creating the *roHtmlWidget* instance, include the [inspector\_server](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672896/roHtmlWidget#roHtmlWidget-inspector_server) initialization parameter and specify a port number. Note that as of BOS 8.5.31, you must set the `enable_web_inspector` registry key to “1” to enable the web inspector for Chromium on the player (if it is set to “0” or nothing, the web inspector is disabled). For example:
    

```
reg = CreateObject("roRegistrySection","html")
reg.Write("enable_web_inspector", "1")
reg.Flush()
```

If you want to change the web inspector port, you must edit the configuration of *roHtmlWidget*. See the "inspector\_server" in [roHtmlWidget](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370672896/roHtmlWidget) for more information.

> [!NOTE]
> Enabling the Web Inspector creates a security vulnerability on BrightSign players. See [this page](https://docs.brightsign.biz/display/DOC/BrightSign+Player+Security#BrightSignPlayerSecurity-advanced_topics) for more details.

#### Inspecting a Webpage

Once HTML content is running on a BrightSign player, follow these steps to inspect it:

1.  Open Chrome on a desktop computer connected to the same local network.
    
2.  Enter the following URL into the address bar: chrome://inspect/devices
    
3.  In the **Devices** section, click **Configure**.
    
4.  Enter the player IP address and Web Inspector port in the field (see the image below). The page(s) being run on the BrightSign player will be displayed at the bottom of the page.
    
    1.  If you don't know the player IP address, power on the player with the microSD card (and other storage devices) removed. After a few moments, the IP address will be displayed on screen.
        
    2.  If you enabled the Web Inspector in BrightAuthor, use port 2999 (e.g. [http://192.168.1.62:2999/](http://192.168.1.62:2999/)).
        
5.  Click the **Inspect** button next to a page. A debugging session will be launched in a new window. Unlike local pages, the page contents are not displayed in the left pane, but the inspector window on the right can be used to debug the page.
    

![](./attachments/Inspector.png)

> [!NOTE]
> Adding more than one device in your list can cause performance issues, especially if the devices are not online, because the Chrome client will continue to search for any offline devices.

#### Chromium Version Compatibility

Because BrightSign players use an older version of Chromium than recent desktop versions, newer desktop Chrome releases may not work with the Web Inspector. If you're having trouble using the Web Inspector with your version of Chrome, download and install one of these versions:

*   **Linux**: [https://www.googleapis.com/download/storage/v1/b/chromium-browser-snapshots/o/Linux\_x64/576753/chrome-linux.zip?generation=1532051976706023&alt=media](https://www.googleapis.com/download/storage/v1/b/chromium-browser-snapshots/o/Linux_x64%2F576753%2Fchrome-linux.zip?generation=1532051976706023&alt=media)
    
*   **OSX:** [https://www.googleapis.com/download/storage/v1/b/chromium-browser-snapshots/o/Mac/576753/chrome-mac.zip?generation=1532055270387578&alt=media](https://www.googleapis.com/download/storage/v1/b/chromium-browser-snapshots/o/Mac%2F576753%2Fchrome-mac.zip?generation=1532055270387578&alt=media)
    
*   **Windows 64-bit**: [https://www.googleapis.com/download/storage/v1/b/chromium-browser-snapshots/o/Win\_x64/576753/chrome-win32.zip?generation=1532053193483102&alt=media](https://www.googleapis.com/download/storage/v1/b/chromium-browser-snapshots/o/Win_x64%2F576753%2Fchrome-win32.zip?generation=1532053193483102&alt=media)
    

> [!NOTE]
> If you're using the Web Inspector to manually step through JavaScript code, encountering an uncaught error in the debugger may cause the player to crash. This is a known bug with the Web Inspector.

A larger collection of supported Chromium downloads can be found [here.](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/2303000608/Chromium+Downloads+for+Current+Older+OS+Versions)

### Trace Events

The Chromium TraceEvent system allows you to debug JavaScript memory leaks, performance issues, and rendering problems. This feature is available in firmware versions 7.0.82 and later. Unlike PCs, where the trace/debugger is run in the same browser as the content, BrightSign players write JSON trace files to the local storage, which you can then import to Chrome on your PC.

When trace events are enabled on a BrightSign player, Chromium captures trace messages to a circular buffer. The player takes regular snapshots of this buffer and writes them to the root directory of the microSD card or SSD as JSON files. 

> [!NOTE]
> The TraceEvent system can easily generate gigabytes of log data on local storage, so we recommend disabling it in production environments.

> [!NOTE]
> See this StackOverflow [page](https://stackoverflow.com/questions/12996129/memory-leak-when-logging-complex-objects) for more information about memory leaks when using console.log to log complex objects.

#### Creating a TraceEvent Directory

Before enabling the TraceEvent system, create a directory named "brightsign-webinspector" in the root directory of the microSD card or SSD on the player. If this directory is missing, the player will not record trace events when they are enabled in the registry. Conversely, you can disable trace events by deleting the "brightsign-webinspector" directory from the storage device.

#### Enabling the TraceEvent System

The TraceEvent system is enabled and configured by writing to the BrightSign player registry (via [BrightScript](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370673016/roRegistry) or [JavaScript](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370678545/registry)). To enable the TraceEvent system, write the following keys to the `html` section of the registry:

*   `[string] tracecategories`: A comma-separated list of trace event categories to enable. The category names are documented in the link below.
    
*   `[int] tracemaxsnapshots`: The maximum number of JSON-trace snapshot files in the "brightsign-webinspector" directory. When the limit is reached, the counter wraps around and begins writing over the oldest trace file.
    
*   `[int] tracemonitorinterval`: The frequency (in seconds) with which the player will take snapshots of the TraceEvent buffer. We recommend 60 seconds as a default value.
    

##### Example (JavaScript):

```
var registryClass = require("@brightsign/registry");
var registry = new registryClass();
registry.write("html", {
    "tracecategories": "toplevel,blink_gc,disabled-by-default-memory-infra,disabled-by-default-blink_gc,disabled-by-default.skia.gpu.cache",
    "tracemaxsnapshots": "25",
    "tracemonitorinterval": "60"
}).then(
    function() {
        console.log("Write Successful");
    });
```

#### Viewing Trace Events

Follow these steps to view the trace events:

1.  Transfer the JSON trace files from the "brightsign-webinspector" directory to your PC.
    
2.  Open [chrome://tracing](#) on your PC Chromium instance.
    
3.  Import the JSON trace files.
    

You can merge multiple trace files; however, in a long trace capture, there will be too many trace events to view at once (you'll likely need to write a script to process them).

#### Additional Documentation

See the following links for further explanation of trace events:

*   [https://www.chromium.org/developers/how-tos/trace-event-profiling-tool](https://www.chromium.org/developers/how-tos/trace-event-profiling-tool)
    
*   [https://chromium.googlesource.com/chromium/src/+/lkcr/docs/memory-infra/README.md](https://chromium.googlesource.com/chromium/src/+/lkcr/docs/memory-infra/README.md)
    
*   [https://developers.google.com/web/tools/chrome-devtools/memory-problems/](https://developers.google.com/web/tools/chrome-devtools/memory-problems/)
    

## Disabling Staged ES6 Features

Some ES6 features have not been finalized and may still contain bugs in the Chromium version(s) used by BrightSign. A crash may occur if your JavaScript application (or the framework code used to build the application) uses one of these features: For example, [this](https://bugs.chromium.org/p/v8/issues/detail?id=3923) is a known issue in Chromium version 45 that will cause a crash on BrightSign XTx44 and XDx34 players. 

To bypass such issues, you can disable all staged (i.e. experimental) ES6 features using the `disable-javascript-harmony-shipping` registry flag (which requires firmware version 7.1.49 or later). The following example shows how to set this registry flag using the  [*registry*](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370678545/registry) JavaScript module (you can also use the  [*roRegistry*](https://brightsign.atlassian.net/wiki/spaces/DOC/pages/370673016/roRegistry) BrightScript object).

```
var registryClass = require("@brightsign/registry");
var registry = new registryClass();


var systemClass = require("@brightsign/system");
var system = new systemClass();


registry.write("html", {js-disable-harmony-shipping:"1"}).then(
    function(){console.log("Write Successful");});


system.reboot()
```

Enabling this registry flag will limit the available JavaScript syntax. However, for ES6 features to be available, an application must be written to be compatible with both ES5 and ES6, so enabling this flag should not cause syntax errors or similar issues.
