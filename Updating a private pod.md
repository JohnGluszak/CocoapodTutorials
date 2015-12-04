*Remember that cocoapods uses git tags to know what version of your code it should use. 
We’ll need to update the project git tag, and the version field in the podspec file.*

**1) Navigate to your project repo**
```
cd [PROJECT_REPO_DIRECTORY]
```
*We are going to modify the podspec file in your project repo, then push that updated file to the spec repo.*
**DO NOT** *modify podspec files in your spec repo directly.*

**2) Open the podspec file and update the ‘version’ field**
```
version = ‘NEW_VERSION_NAME’
```

**3) Create a new git tag**
```
git tag ‘NEW_VERSION_NAME’
git push --tags
```
*Make sure your git tag matches the new version name in the podspec file.*

**4) Add this updated podspec file to your spec repo**
```
pod repo push [SPEC_REPO_NAME] [SPEC_FILE_NAME].podspec --allow-warnings
```
*Only include the ```--allow-warnings``` field if you are confident that your warnings are ok to ignore. It is recommended to run this command without the ```--allow-warnings``` flag first to be sure.*

**5) Anyone using the pod will need to run ‘pod update’**
