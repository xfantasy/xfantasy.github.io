---
layout: post
title: iOS sensor detection
---

<pre>
// 检测是否存在摄像头
- (BOOL)isCameraAvailable
{
	return [UIImagePickerController isSourceTypeAvailable:UIImagePickerControllerSourceTypeCamera];
}

// 检测前置摄像头是否存在
- (BOOL)isFrontCameraAvailabel
{
#ifdef __IPHONE_4_0 // iPhone加入了前置摄像头
	return [UIImagePickerController isCameraDeviceAvailable:UIImagePickerControllerCameraDeviceFront];
#else
	return NO;
#endif
}

// 后置摄像头是否可用
- (BOOL)isRearCameraAvailabel
{
#ifdef __IPHONE_4_0
	return [UIImagePickerController isCameraDeviceAvailable:UIImagePickerControllerCameraDeviceRear];
#else
	return NO;
#endif
}

// 判断是否支持某种多媒体类型：拍照，视频
- (BOOL)isCameraSupportsMedia:(NSString *)paramMediaType
                   sourceType:(UIImagePickerControllerSourceType)paramSourceType
{
	__block BOOL result = NO;
	if ([paramMediaType length] == 0) {
		return NO;
	}
	NSArray *availableMediaTypes = [UIImagePickerController availableMediaTypesForSourceType:paramSourceType];
	[availableMediaTypes enumerateObjectsUsingBlock: ^(id obj, NSUInteger idx, BOOL *stop) {
	    NSString *mediaType = (NSString *)obj;
	    if ([mediaType isEqualToString:paramMediaType]) {
	        result = YES;
	        *stop = YES;
		}
	}];
	return result;
} /* cameraSupportsMedia */

// 检查摄像头是否支持录像
- (BOOL)isCameraSupportShootingVideos
{
	return [self isCameraSupportsMedia:(NSString *)kUTTypeMovie
	                        sourceType:UIImagePickerControllerSourceTypeCamera];
}

// 检查摄像头是否支持拍照
- (BOOL)isCameraSupportTakingPhotos
{
	return [self isCameraSupportsMedia:(NSString *)kUTTypeImage
	                        sourceType:UIImagePickerControllerSourceTypeCamera];
}

// 相册是否可用
- (BOOL)isPhotoLibraryAvailable
{
	return [UIImagePickerController isSourceTypeAvailable:UIImagePickerControllerSourceTypePhotoLibrary];
}

// 照片流是否可用
- (BOOL)isPhotoLiabaryAvailable
{
	return [UIImagePickerController isSourceTypeAvailable:UIImagePickerControllerSourceTypeSavedPhotosAlbum];
}

// 是否可以在相册中选择视频
- (BOOL)canUserPickVideosFromPhotoLibrary
{
	return [self isCameraSupportsMedia:(NSString *)kUTTypeMovie
	                        sourceType:UIImagePickerControllerSourceTypePhotoLibrary];
}

// 是否可以在相册中选择视频
- (BOOL)canUserPickPhotosFromPhotoLibrary
{
	return [self isCameraSupportsMedia:(NSString *)kUTTypeImage
	                        sourceType:UIImagePickerControllerSourceTypePhotoLibrary];
}

// 闪光灯是否可用
- (BOOL) isCameraFlashAvailable
{
#ifdef __IPHONE_4_0
    return [UIImagePickerController isFlashAvailableForCameraDevice:UIImagePickerControllerCameraDeviceRear];
#else
    return NO;
#endif
}

// 检测陀螺仪是否可用
- (BOOL) isGyroscopeAvailable
{
    CMMotionManager *motionManager = [[CMMotionManager alloc] init];
    if ([motionManager respondsToSelector:@selector(gyroAvailable)]) {
        return motionManager.gyroAvailable;
    } else {
        return NO;
    }
}

// 检测指南针或磁力计
- (BOOL) isHandingAvailable
{
    CLLocationManager *locationManager = [[CLLocationManager alloc] init];
    if ([locationManager respondsToSelector:@selector(headingAvailable)]) {
        return locationManager.headingAvailable;
    } else {
        return NO;
    }
}

// 检测视网膜屏
- (BOOL) isRetinaDisplay
{
    UIScreen *screen = [UIScreen mainScreen];
    if ([screen respondsToSelector:@selector(scale)]) {
        return screen.scale >= 2.0;
    }
    return NO;
}

// 实现远程控制(耳机线上的按钮)
// 接受 [[UIApplication sharedApplication] beginReceivingRemoteControlEvents];
// 实现 remoteControlReceivedWithEvent:
// 取消 endReceivingRemoteControlEvents;

// 检测拨打电话功能
- (BOOL) canMakeCalls
{
    return [[UIApplication sharedApplication] canOpenURL:[NSURL URLWithString:@"tel://"]];
}
</pre>
