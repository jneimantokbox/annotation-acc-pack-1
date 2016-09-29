![logo](../tokbox-logo.png)

# OpenTok Annotations Accelerator Pack for JavaScript<br/>Version 1.1.0

## Quick start

This section shows you how to prepare and use the OpenTok Annotations Accelerator Pack as part of an application.

### Deploying and running

The web page that loads the sample app for JavaScript must be served over HTTP/HTTPS. Browser security limitations prevent you from publishing video using a `file://` path, as discussed in the OpenTok.js [Release Notes](https://www.tokbox.com/developer/sdks/js/release-notes.html#knownIssues). To support clients running [Chrome 47 or later](https://groups.google.com/forum/#!topic/discuss-webrtc/sq5CVmY69sc), HTTPS is required. A web server such as [MAMP](https://www.mamp.info/) or [XAMPP](https://www.apachefriends.org/index.html) will work, or you can use a cloud service such as [Heroku](https://www.heroku.com/) to host the application.

## Explore the code

This section describes best practices the sample code uses to implement the annotation features within the *Screensharing with Annotations Accelerator Pack*.

To develop your own application, emulate the steps shown here on how to add the toolbar to your container and create an annotation canvas for both the publisher and subscriber.

The following steps will help you get started, and you can refer to the [complete code example](./sample-app/public/index.html):

For detail about the APIs used to develop this sample, see the [OpenTok.js Reference](https://tokbox.com/developer/sdks/js/reference/).

To learn more about the annotation widget, visit [OpenTok Annotations Widget for JavaScript](https://github.com/opentok/annotation-widget/tree/js).


### Web page design

While TokBox hosts [OpenTok.js](https://tokbox.com/developer/sdks/js/), you must host the JavaScript Annotations widget yourself. You can specify toolbar items, colors, icons, and other options for the annotation widget via the common layer. The Sample includes the following:

* **[acc-pack-annotation.js](./opentok.js-ss-annotation/src/acc-pack-annotation.js)**: This contains the constructor for the annotation component used over video or a shared screen.

* **[CSS files](./sample-app/public/css)**: Defines the client UI style.

* **[Images](./opentok.js-ss-annotation/images)**: This contains the default icons used in the annotation toolbar.


### Initializing the session

The `AnnotationAccPack` constructor, located in `acc-pack-annotation.js`, sets the `accPack` property to register, trigger, and start events via the common layer API used for all Samples.

If you install the Annotation Sample with [npm](https://www.npmjs.com/package/opentok-annotation), you can instantiate the `AnnotationAccPack` instance with this approach:

```javascript
const annotation = require(‘opentok-annotation’);
const annotationAccPack = new annotation(options);
```

Otherwise, the following code shows how to initialize the `AnnotationAccPack` object:

```javascript
  // Trigger event via common layer API
  var _triggerEvent = function (event, data) {
    if (_accPack) {
      _accPack.triggerEvent(event, data);
    }
  };

  . . .

  var AnnotationAccPack = function (options) {
    _this = this;
    _this.options = _.omit(options, 'accPack');
    _accPack = _.property('accPack')(options); // Supports events in the common layer.
    _registerEvents();
    _setupUI();
  };
```

The events that may be triggered include:

 - Resizing the canvas
 - Closing the external annotation window
 - Starting an annotation
 - Linking the canvas to the annotation
 - Ending an annotation


For more information, see [Initialize, Connect, and Publish to a Session](https://tokbox.com/developer/concepts/connect-and-publish/).



### Best Practices for Resizing the Canvas

The `linkCanvas()` method, located in `acc-pack-annotation.js`, refers to a parent DOM element called the `absoluteParent`. This method maintains the information required to resize both the canvas and its container element as the window is resized. This recommended best practice mitigates potential issues with jQuery in which information may be lost upon multiple resize attempts.

## Requirements

To develop a screen a web-based application that uses the OpenTok Annotations Accelerator Pack for JavaScript:

1. Review the basic requirements for [OpenTok](https://tokbox.com/developer/requirements/) and [OpenTok.js](https://tokbox.com/developer/sdks/js/#browsers).
1. Include [jQuery](https://jquery.com/) and [Underscore](http://underscorejs.org/).
1. Install the OpenTok Annotations Accelerator Pack: <ol><li>Install with [npm](https://www.npmjs.com/package/opentok-annotation).</li><li>Run the [build.sh script](./build.sh).</li><li>Download and extract the **annotation-acc-pack.js** file from the [zip](https://s3.amazonaws.com/artifact.tokbox.com/solution/rel/annotations/JS/opentok-js-annotations-1.1.0.zip) file provided by TokBox.</li></ol>
1. Code the web page to load [OpenTok.js](https://tokbox.com/developer/sdks/js/) first, and then load [opentok-annotations.js](./sample-app/public/js/components/opentok-annotation.js).  
