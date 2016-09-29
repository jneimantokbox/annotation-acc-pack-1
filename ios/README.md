![logo](../tokbox-logo.png)

# OpenTok Annotations Accelerator Pack for iOS<br/>Version 1.1.0

## Quick start

This section shows you how to prepare and use the OpenTok Annotations Accelerator Pack as part of an application.

## Add the sample library

To get up and running quickly with your development, go through the following steps using CocoaPods:

1. Add the following line to your pod file: ` pod ‘OTAnnotationKit’  `
2. In a terminal prompt, navigate into your project directory and type `pod install`.
3. Reopen your project using the new `*.xcworkspace` file.

For more information about CocoaPods, including installation instructions, visit [CocoaPods Getting Started](https://guides.cocoapods.org/using/getting-started.html#getting-started).


## Exploring the code

This section describes how the sample app code design uses recommended best practices to deploy the annotations features.

For detail about development with the SDK, as well as the APIs used to develop this sample, see [Requirements](#requirements), the [OpenTok iOS SDK Requirements](https://tokbox.com/developer/sdks/ios/) and the [OpenTok iOS SDK Reference](https://tokbox.com/developer/sdks/ios/reference/).



### Class design

The following classes represent the software design for the OpenTok Annotations Accelerator Pack.

| Class        | Description  |
| ------------- | ------------- |
| `OTAnnotationScrollView` | Provides the initializers and methods for the client annotating views. |
| `OTAnnotationToolbarView`   | A convenient annotation toolbar that is optionally available for your development. As an alternative, you can create your own toolbar using `OTAnnotationScrollView`. |
| `OTFullScreenAnnotationViewController`   | Combines both the scroll and annotation toolbar views. |


### Annotation features

The `OTAnnotationScrollView` class is the backbone of the annotation features in this Sample.


```objc
@interface OTAnnotationScrollView : UIView

@property (nonatomic, getter = isAnnotating) BOOL annotating;
@property (nonatomic, getter = isZoomEnabled) BOOL zoomEnabled;

- (instancetype)init;
- (instancetype)initWithFrame:(CGRect)frame;
- (void)addContentView:(UIView *)view;  // this will enable scrolling if image is larger than actual device screen

@property (readonly, nonatomic) OTAnnotationToolbarView *toolbarView;
- (void)initializeToolbarView;

#pragma mark - annotation
- (void)startDrawing;
@property (nonatomic) UIColor *annotationColor;
- (void)addTextAnnotation:(OTAnnotationTextView *)annotationTextView;
- (UIImage *)captureScreen;
- (void)erase;
- (void)eraseAll;

@end
```


## Requirements

To be prepared to develop with the Annotations Accelerator Pack for iOS:

1. Install Xcode version 5 or later, with ARC enabled.
2. Your device must be running iOS 8 or later.
