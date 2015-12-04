**1) You will need two private git repositories**   
*One to hold the project you’d like to turn into a pod (henceforth called the* **project repo***). Make sure it contains your Xcode project before we start.
The other repo will later hold your podspec file (henceforth called the* **spec repo***). Make sure it is empty now (readme doesn’t matter).*

**2) Add your spec repo to your local cocoapods**
```
pod repo add [SPEC_REPO_NAME] [SPEC_REPO_URL]
```
*This lets your local cocoapods know about your spec repo. This does not publicize anything, the spec repo is only cloned to your computer. To verify the above command worked, navigate to ~/.cocoapods/repos in Terminal and print out the contents. You should see a folder with the name you used for [SPEC_REPO_NAME].*

**3) Navigate to your project repo**
```
cd [PROJECT_REPO_DIRECTORY]
```
*The rest of our work will be done here*

**4) Create a podspec file**
```
pod spec create [FILE_NAME] [PROJECT_REPO_URL]
```
*This creates a template podspec file for you to use. We will edit this podspec here, in our project repo, and later push a copy to our spec repo.*

**5) Fill out the podspec file**  
*Here is an example of a completed podspec file:*
```
Pod::Spec.new do |s|

  s.name         = “Spec-Example”
  s.version      = “0.0.1”
  s.summary      = “This is an example podspec file”
  s.homepage     = "https://github.com/MY_ACCOUNT”
  s.author             = { “John Smith” => "john.smith@gmail.com" }

  s.license      = { :type => "MIT", :file => "MIT-License.txt" }

  s.requires_arc = true
  s.platform     = :ios, "7.1"

  s.source       = { :git => "https://github.com/MY_ACCOUNT/MY_PROJECT.git", :tag => s.version.to_s }

# Any pods which your project uses
  s.dependency “AFNetworking”

end
```
*Under ’s.source’ field, you’ll need to specify a ‘tag’ parameter. Using ’s.version.to_s’ tells the podspec to use the ’s.version’ field as the tag. It is recommended that you use this. We’ll talk more about tagging later in the tutorial.*  

**6) Add a license file to your project repo**  
*Even though this will be a private pod, it still needs a license file. In the above podspec, the ’s.license’ field points to an MIT type license contained in a text file named ‘MIT-License.txt’ in the project repo. You’ll need to manually add your own. For a basic MIT license, you can simply copy the text [here](http://opensource.org/licenses/MIT) into a txt file, fill out your name and date, and save it in your project repo.*

**7) Tag your project repo**
```
git tag ‘PODSPEC_VERSION’
git push --tags
```
*Cocoapods uses git tags to tell what version of your project it should use. It looks under the ’s.source’ podspec field for the tag. Using ’s.version.to_s’ tells cocoapods to use the podspec ‘version’ field as the git tag it should look for. So when you tag your project repo, make sure your tag matches the ‘version’ field in the podspec file.*

**8) Try to push your podspec file and check for errors**
```
pod repo push [SPEC_REPO_NAME] [SPEC_FILE_NAME].podspec
```
*This command will probably fail, and that’s ok. It checks for errors in your podspec (by performing a lint), which looks at both the podspec file and your Xcode project. By default, this command will fail on both errors and warnings. Make sure to fix any errors, and check that any warnings are not a big deal. Once you’re satisfied, you can run this command again, and tell it not to fail on warnings:*
```
pod repo push [SPEC_REPO_NAME] [SPEC_FILE_NAME].podspec --allow-warnings
```
