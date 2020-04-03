# HangTime / Trusted Web Activity

This project uses the
[Trusted Web Activities](https://developers.google.com/web/updates/2017/10/using-twa) technology
to wrap [HangTime](https://hangtime.stevie-ray.nl/) in an Android Application.

## Requirements
- [Node.js](https://nodejs.org/en/) 10.0 or above

## Setting up the Environment

### Get the Java Development Kit (JDK) 8.
The Android Command line tools requires the correct version of the JDK to run. To prevent version
conflicts with a JDK version that is already installed, Bubblewrap uses a JDK that can unzipped in
a separate folder.

Download a version of JDK 8 that is compatible with your OS from
[AdoptOpenJDK](https://adoptopenjdk.net/releases.html?variant=openjdk8&jvmVariant=hotspot)
and extract it in its own folder.

**Warning:** Using a version lower than 8 will make it impossible to compile the project and higher
versions are incompatible with the Android command line tools.

### Get the Android command line tools
Download a version of Android command line tools that is compatible with your OS from
[https://developer.android.com/studio#command-tools](https://developer.android.com/studio#command-tools).
Create a folder and extract the downloaded file into it.

### Updating the location of the JDK and / or the Android command line tools.
If the location for the JDK or the Android command line tools have been setup with the wrong path or
if their location has changed after the initial configuration, the location for either of those can
be changed by editing the configuration file at `${USER_HOME}/.llama-pack/llama-pack-config.json`.

Settings used: `OpenJDK 14 (Latest) / Hotspot: jdk-14+36 - AdoptOpenJDK macOS`

llama-pack-config:
```json
{
  "jdkPath": "/Library/Java/JavaVirtualMachines/adoptopenjdk-14.jdk",
  "androidSdkPath": "/Users/stevie-ray/Library/Android/sdk"
}

```

## Using Bubblewrap

### Installing Bubblewrap

```shell
npm i -g @bubblewrap/cli
```

### Initializing an Android Project
Generate an Android project from an existing Web Manifest:

```shell
bubblewrap init --manifest https://hangtime.stevie-ray.nl/manifest.json
```

When initalizing a project, Bubblewrap will download the Web Manifest and ask you to confirm
the values that should be used when building the Android project.

It will also ask you for the details needed to generate a signing key, used to sign the
app before uploading to the Play Store.

### Building the Android Project
```shell
bubblewrap build
```

#### OpenJDK 14 / Gradle support issue: 
in `gradle/wrapper/gradle-wrapper.properties` set: `distributionUrl=https\://services.gradle.org/distributions/gradle-6.3-all.zip` to support `adoptopenjdk-14` 

When building the project for the first time, the Android Build Tools will need to be installed.
The tool will invoke the installation process for the build tools. Make sure to read and accept
the license agreement before proceeding.

As a result of the build step, the tool will generate a signed APK (`app-release-signed.apk`)
that can be uploaded to the Play Store. You will also need to deploy a Digital Asset Links file to
validate your domain. The
[TWA Quick Start Guide](https://developers.google.com/web/updates/2019/08/twas-quickstart#creating-your-asset-link-file)
explains how to extract the information needed to generate it.
