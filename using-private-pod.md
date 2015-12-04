**1) Make sure anyone using your pod has access to your spec repo**

**2) Anyone using this pod will also need to run the terminal command**  
```
pod repo add [SPEC_REPO_NAME] [SPEC_REPO_URL]
```  
*This is the same command you ran when creating the private pod. It clones your spec repo to your local cocoapods.*  

  
**3) At the very top of the podfile, you must add two lines**
```
source ‘[SPEC_REPO_GIT_URL]’
source ‘https://github.com/CocoaPods/Specs.git’
```
*The first line tells cocoapods where to look for your private pods. The second line tells cocoapods where to look for all public pods. Without declaring a source in your podfile, cocoapods uses the ‘https://github.com/CocoaPods/Specs.git’ source by default. However you must make this explicit when you declare a new source.*

**4) Use your private pod like any other pod**  
```pod ‘PRIVATE_POD_NAME’```
