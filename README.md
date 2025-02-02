# SaveImage (only iOS)

This plugin allows you to save local JPEG image files to the iOS Camera Roll/Photo Library or Android Gallery. Other image mime types are currently not supported.
The image file to be saved to the Library/Gallery must be available on the device.

The plugin is based on code seen in several other existing plugins:

1. Canvas2ImagePlugin (https://github.com/devgeeks/Canvas2ImagePlugin) by Tommy-Carlos Williams (https://github.com/devgeeks)
2. ImgDownloader (https://github.com/Nomia/ImgDownloader) by "Nomia" (https://github.com/Nomia)
3. cordova-camera-roll (https://github.com/driftyco/cordova-camera-roll) by Max Lynch (https://github.com/mlynch)

Thanks to all of the above mentioned authors for sharing their code openly.

    cordova plugin add https://github.com/Qik-Company/cordova-plugin-save-image.git

## Methods

### cordova.plugins.imagesaver.saveImageToGallery

Save a local JPEG image to the device gallery / camera roll.

### cordova.plugins.imagesaver.saveVideoToGallery (iOS only)

Save a local video to the camera roll.

### cordova.plugins.imagesaver.scanPhoto (Android only)

Making picture available in the Android Gallery application and other apps.

## Usage Example

```

// iOS with file prefix: var nativePathToJpegImage = 'file:///var/mobile/Containers/Data/Application/<UUID>/Library/NoCloud/some_dir/some_image.jpg'
// iOS without file prefix: var nativePathToJpegImage = '/var/mobile/Containers/Data/Application/<UUID>/Library/NoCloud/some_dir/some_image.jpg'

window.cordova.plugins.imagesaver.saveImageToGallery(nativeImagePath, onSaveImageSuccess, onSaveImageError);

window.cordova.plugins.imagesaver.saveVideoToGallery(nativeVideoPath, onSaveImageSuccess, onSaveImageError);

window.cordova.plugins.imagesaver.scanPhoto(nativeImageVideoPath, onSaveImageSuccess, onSaveImageError);

function onSaveImageSuccess() {
    console.log('--------------success');
}

function onSaveImageError(error) {
    console.log('--------------error: ' + error);
}
```

## iOS Quirks

Since iOS 10 it's mandatory to provide an usage description in the `info.plist` if trying to access privacy-sensitive data. When the system prompts the user to allow access, this usage description string will displayed as part of the permission dialog box, but if you didn't provide the usage description, the app will crash before showing the dialog. Also, Apple will reject apps that access private data but don't provide an usage description.

This plugins requires the following usage descriptions:

- `NSPhotoLibraryAddUsageDescription` specifies the reason for your app to get write-only access to the user's photo library

To add these entries into the `info.plist`, you can use the `edit-config` tag in the `config.xml` like this:

```
<edit-config target="NSPhotoLibraryAddUsageDescription" file="*-Info.plist" mode="merge">
    <string>need to photo library access to save pictures there</string>
</edit-config>
```

## License

The MIT License

Copyright (c) 2016 Quiply Technologies GmbH (http://www.quiply.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
