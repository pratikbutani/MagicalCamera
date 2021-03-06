[![alt tag](https://github.com/fabian7593/MagicalCamera/blob/master/cameraHighQ.png)](https://github.com/fabian7593/MagicalCamera)

A Magic library to take photos and select pictures in Android. In a simple way and if you need it also save the pictures in device.
<br>
[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-MagicalCamera-green.svg?style=true)](https://android-arsenal.com/details/1/3623)
<br>
## SDK
* It requires **14+ API**.
<br>

## Getting Started

### Download Sources
use git (sourcetree or others)

```bash
git clone https://github.com/fabian7593/MagicalCamera.git
```

Download from [Here](https://github.com/fabian7593/MagicalCamera/zipball/master)

Another type download by Bintray from   [ ![Download](https://api.bintray.com/packages/fabian7593/maven/MagicalCamera/images/download.svg) ](https://bintray.com/fabian7593/maven/MagicalCamera/_latestVersion)
 
<br>
### What you need?
You need for usage the library in the best way, call any permissions in Android Manifest.xml
```bash
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.CAMERA"/>
```
<br>
### How to use
#####Add dependecies
If you need to take photo or select picture, this is your solution.
This library give a magical solution for take a picture, you only need to download this and integrate this in your project, maybe downloading it or import in your gradle, like this.

```bash
repositories {
    jcenter()
}

dependencies {
    compile 'com.frosquivel:magicalcamera:1.0'
}
```

If you have any problem with this dependence, because the library override any styles or others, please change the last line for this code:
```bash
 compile('com.frosquivel:magicalcamera:1.0@aar') {
        transitive = false;
    }
```

<br>
#####Import library
You need to import the library
```bash
import com.frosquivel.magicalcamera.MagicalCamera;
```

<br>
#####Declare variable to resize photo ( with pixels percentage )
You need to declare and constant or a simple int variable for the quality of the photo, while greater be, greater be the quality, and otherwise, worst be the quality, like this
```bash
//a regular quality, if you declare with 50 is a worst quality and if you declare with 4000 is the better quality
//only need to play with this variable (0 to 4000 ... or in other words, worst to better :D)

private int RESIZE_PHOTO_PIXELS_PERCENTAGE = 1000;
```

<br>
#####Instance Class MagicalCamera
You need to instance the MagicalCamera Class, like this:
The fisrt param is the current Activity, and the second the resize percentage photo
```bash
 MagicalCamera magicalCamera = new MagicalCamera(this,RESIZE_PHOTO_PIXELS_PERCENTAGE);
```

<br>
#####Activities Methods
You need to call the methods for take or select pictures in activities that this form:

```bash
//take photo
magicalCamera.takePhoto();

//select picture
magicalCamera.selectedPicture("my_header_name");
```

<br>
#####Fragments Methods
You need to call the methods for take or select pictures in fragments that this form:

```bash
//take photo
 if(magicalCamera.takeFragmentPhoto()){
        startActivityForResult(magicalCamera.getIntentFragment(),MagicalCamera.TAKE_PHOTO);
 }
 
 //select picture
 if(magicalCamera.selectedFragmentPicture()){
      startActivityForResult(Intent.createChooser(magicalCamera.getIntentFragment(),  "My Header Example"),
                            MagicalCamera.SELECT_PHOTO);
   }
```

<br>
#####Remeber override the event onActivityResult
You need to override the method onActivityResult in your activity or fragment like this
```bash
 @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        //call this method ever
        magicalCamera.resultPhoto(requestCode, resultCode, data);
        
        //with this form you obtain the bitmap
        imageView.setImageBitmap(magicalCamera.getMyPhoto());

       //if you need save your bitmap in device use this method
       if(magicalCamera.savePhotoInMemoryDevice(magicalCamera.getMyPhoto(),"myTestMagicalCameraPhoto", MagicalCamera.JPEG, true)){
           Toast.makeText(MainActivity.this, "The photo is save in device, please check this", Toast.LENGTH_SHORT).show();
       }else{
           Toast.makeText(MainActivity.this, "Sorry your photo dont write in devide, please contact with fabian7593@gmail and say this error", Toast.LENGTH_SHORT).show();
       }
    }
```

<br>
#####The savePhotoInMemoryDevice Method
This method save your bitmap in internal memory device or if the internal memory is full this library save in sdcard (if you have anything :'D)
This method have a lot of params that you can need to use the library:
* **Bitmap:** This is the bitmap that you need to save in memory device.
* **PhotoName:** The name of the photo
* **DirectoryName:** The name of directory that you need to save the image
* **Format:** the format of the photo, maybe png, jpeg or webp. Depends of that you need.
* **AutoIncrementNameByDate:** This variable save the photo with the photo name and the current date and hour. (Only if is true).

For example: myTestMagicalCameraPhoto_20160520131344 -> This is the year 2016, month 5, day 20, hour 13, minute 13 and second 44.

The method:
```bash
 public boolean savePhotoInMemoryDevice(Bitmap bitmap, String photoName, String directoryName,
 Bitmap.CompressFormat format, boolean autoIncrementNameByDate)
```

<br>
#####Types of Formats for save photos
You have any type of formats for save the pictures and the bitmaps.
You can use, the static variables of the library MagicalCamera.
```bash
 Bitmap.CompressFormat jpeg = MagicalCamera.JPEG;
 Bitmap.CompressFormat png = MagicalCamera.PNG;
 Bitmap.CompressFormat webp = MagicalCamera.WEBP;
```

<br>
#####Resize photo in real time
You can resize the photo in any moment with this:
```bash
   magicalCamera.setResizePhoto(newResizeInteger);
```

<br>
#####Conversion Methods
The library have any methods to convert the bitmap in other formats that you need.
All of this methods are public statics, I mean that you dont have to instance the library for usage this.
* **bitmapToBytes:** Convert the bitmap to array bytes, only need the bitmap param and the compress format, return array bytes.
* **bytesToBitmap:** Convert the array bytes to bitmap, only need the array bytes in param, return bitmap.
* **bytesToStringBase64:** Convert the array bytes to String base 64, only need the array bytes format in param, return String.
* **stringBase64ToBytes:** Convert string to array bytes, only need the String in param, return array bytes.

<br><br>
##Internal documentation
All the code has a internal documentation for more explanation of this example.

<br><br>
##Preview of Example
![alt tag](https://github.com/fabian7593/MagicalCamera/blob/master/magicalcamera.gif)


<br><br>
## License
Source code can be found on [github](https://github.com/fabian7593/MagicalCamera)<br>
Licenced under [APACHE 2.0](http://www.apache.org/licenses/LICENSE-2.0).
<br><br>

## About Developer
Developed by [Fabian Rosales](http://www.frosquivel.com)<br>
Known as [Frosquivel Developer](http://www.frosquivel.com)<br>
Web Page [www.frosquivel.com](http://www.frosquivel.com)<br>
Blog (Spanish) [www.frosquivel.com/blog](http://www.frosquivel.com/blog)<br>



