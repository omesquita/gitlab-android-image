# gitlab-android-image
This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool like GitLab CI. Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs.

This repository is forked from [jangrewe/gitlab-ci-android](https://github.com/jangrewe/gitlab-ci-android) and contains some others tools added. 
  - Fastlane

Others tools will be added over time. 

A `.gitlab-ci.yml` with caching of your project's dependencies would look like this:

```
image: omesquita/gitlab-android

stages:
- build

before_script:
- export GRADLE_USER_HOME=$(pwd)/.gradle
- chmod +x ./gradlew

cache:
  key: ${CI_PROJECT_ID}
  paths:
  - .gradle/

build:
  stage: build
  script:
  - ./gradlew assembleDebug
  artifacts:
    paths:
    - app/build/outputs/apk/app-debug.apk
```
