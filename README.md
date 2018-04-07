
VideoRecorder
=========

## VideoRecorder.
------------
 Added Some screens here.
 
[![](https://github.com/pawankv89/VideoRecorder/blob/master/Screens/1.png)]
[![](https://github.com/pawankv89/VideoRecorder/blob/master/Screens/2.png)]
[![](https://github.com/pawankv89/VideoRecorder/blob/master/Screens/3.png)]


## Usage
------------
 iOS 9 Demo showing how to droodown on iPhone X Simulator in  Objective-C.


```objective-c


#import "ViewController.h"
@import MediaPlayer;
#import <MobileCoreServices/UTCoreTypes.h>
@import AVFoundation;
@import AVKit;

@interface ViewController ()<UIImagePickerControllerDelegate, UINavigationControllerDelegate>

@end

@implementation ViewController

- (void)viewDidLoad {
[super viewDidLoad];
// Do any additional setup after loading the view, typically from a nib.
}


- (void)didReceiveMemoryWarning {
[super didReceiveMemoryWarning];
// Dispose of any resources that can be recreated.
}

-(IBAction)playVideoTap:(id)sender{

// pick a video from the documents directory
NSURL *video = [self grabFileURL:@"video.mov"];

// create an AVPlayer
AVPlayer *player = [AVPlayer playerWithURL:video];

// create a player view controller
AVPlayerViewController *controller = [[AVPlayerViewController alloc]init];
controller.player = player;
[player play];

[self presentViewController:controller animated:YES completion:^{

}];
}

-(IBAction)recordVideoTap:(id)sender{

if ([UIImagePickerController isSourceTypeAvailable:UIImagePickerControllerSourceTypeCamera]) {

UIImagePickerController *picker = [[UIImagePickerController alloc]init];
picker.sourceType = UIImagePickerControllerSourceTypeCamera;
picker.delegate = self;
picker.allowsEditing = NO;

NSArray *mediaTypes = [[NSArray alloc]initWithObjects:(NSString *)kUTTypeMovie, nil];

picker.mediaTypes = mediaTypes;

[self presentViewController:picker animated:YES completion:nil];

} else {

UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:@"I'm afraid there's no camera on this device!" delegate:nil cancelButtonTitle:@"Dang!" otherButtonTitles:nil, nil];
[alertView show];
}
}

#pragma mark - Delegate Methods

- (void)imagePickerControllerDidCancel:(UIImagePickerController *)picker {

// user hit cancel
[self dismissViewControllerAnimated:YES completion:nil];
}

- (void)imagePickerController:(UIImagePickerController *)picker didFinishPickingMediaWithInfo:(NSDictionary *)info {

// grab our movie URL
NSURL *chosenMovie = [info objectForKey:UIImagePickerControllerMediaURL];

// save it to the documents directory
NSURL *fileURL = [self grabFileURL:@"video.mov"];
NSData *movieData = [NSData dataWithContentsOfURL:chosenMovie];
[movieData writeToURL:fileURL atomically:YES];

// save it to the Camera Roll
UISaveVideoAtPathToSavedPhotosAlbum([chosenMovie path], nil, nil, nil);

// and dismiss the picker
[self dismissViewControllerAnimated:YES completion:nil];
}

- (NSURL*)grabFileURL:(NSString *)fileName {

// find Documents directory
NSURL *documentsURL = [[[NSFileManager defaultManager] URLsForDirectory:NSDocumentDirectory inDomains:NSUserDomainMask] lastObject];

// append a file name to it
documentsURL = [documentsURL URLByAppendingPathComponent:fileName];

return documentsURL;
}


```

```objective-c

```

## License

This code is distributed under the terms and conditions of the [MIT license](LICENSE).

## Change-log

A brief summary of each this release can be found in the [CHANGELOG](CHANGELOG.mdown). 
