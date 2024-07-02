# Eyes QTP/UFT SDK

The Eyes QTP/UFT SDK is a library for Microfocus QTP/UFT which allows you to run tests using Applitools Eyes; a Visual Testing Platform. This repo hosts a version of the Eyes QTP/UFT SDK which includes updates to support continued functionality and compatibility with the underlying Applitools Eyes DotNet SDK components.

# Windows UFT Tutorial
The Applitools Eyes UFT/QTP SDK allows you to easily add visual checkpoints to your UFT/QTP tests. It takes care of getting screenshots of your application from the underlying UFT, sending them to the Eyes server for validation and failing the test in case differences are found.

## Install the SDK
1. Download the SDK of Applitools Eyes for UFT (download this repo as a zip file) and extract it into a folder of your choice.

2. Associate the Eyes.qfl function library located in the extracted folder with your test in `File > Settings > Resources > +`.

3. If you want Eyes to be included in all tests, make sure to check `‘Set As Default’`

## Run your first test
Applitools Eyes reports differences by comparing screenshots of your application with baseline images that define the expected appearance of the application at each step of the test. By default, the Eyes SDK detects the environment in which the application is running (namely, the operating system, the executable name and its window size) and compares the screenshots against baseline images that are specific to that environment. The first time you run a test in a given environment, its screenshots will be automatically saved as its baseline. Starting from the second run onward, you always have a baseline to compare against.

The test below is a simple UFT/QTP program that visually validates the default notepad program, before and after it types some text into it. It consists of two visual checkpoints, each validating the entire application window. The first time you run this test a new baseline will be created, and subsequent test runs will be compared to this baseline. If any screenshot mismatch its baseline image in a perceptible way, `eyes.Close()` will throw a `DiffsFoundException` which includes a URL that points to a detailed report where you can see the detected differences and take appropriate actions such as reporting bugs, updating the baseline and more.

Before running the test, make sure to set the API key that identifies your account in the environment variable `APPLITOOLS_API_KEY` or directly assign it to the `eyes.api_key` property. You can find your API key under the user menu located at the right hand side of the test manager toolbar. If you don't yet have an account [create it now](https://applitools.com/sign-up) to obtain your key.

```
' Make sure to include 'Eyes.qfl' via File -> Settings... -> Resources

' This is your api key, make sure you use it in all your tests.
eyes.ApiKey = "YOUR_API_KEY"

' Test setup - You should have 'Notepad' window object in your objects repository
Set testApp = Window("Notepad")
eyes.SetBaselineInfoFromWindow(testApp)

' Start visual UI testing - Open eyes test
eyes.Open "Hello World", "QTP Hello World Test"

' Visual checkpoint #1
eyes.CheckObject testApp, "Hello!"

' Write something
testApp.WinEditor("Edit").Type("Applitools UFT Demo")

' Visual checkpoint #2
eyes.CheckObject testApp, "Write!"

' End visual UI testing. Validate visual correctness.
eyes.Close()

' Report
If Not eyesReport.IsPassed Then
    If eyesReport.IsNew Then
        Reporter.ReportEvent micFail, eyesReport.TestName, "New test inserted, See " & eyesReport.Url & " for details."
    else
        Reporter.ReportEvent micFail, eyesReport.TestName, "See " & eyesReport.Url & " for details."
    End If
End If
```

## Analyze your test results
Congratulations! You've successfully run your first visual UI test with Applitools Eyes! A detailed report is ready for your inspection at the Applitools Eyes test manager. Watch this 5 minute video to get acquainted with the test manager and to learn the basics of baseline maintenance.

[Login to Applitools](https://applitools.com/users/login) and analyze the results.

[Getting started with the Applitools Eyes Test Manager (Youtube)](http://www.youtube.com/watch?v=W0GdsOdg7Xw)

[![Getting started with the Applitools Eyes Test Manager](https://i.ytimg.com/vi/W0GdsOdg7Xw/maxresdefault.jpg)](http://www.youtube.com/watch?v=W0GdsOdg7Xw "Getting started with the Applitools Eyes Test Manager")


## Learn more
Applitools Eyes is a powerful platform for automated visual UI testing that supports full page screenshots, page layout matching, cross-device and browser testing, test batching, baseline branching and merging, automated baseline maintenance, collaboration features, and much more. Applitools has over [40 SDKs](https://applitools.com/tutorial) supporting a broad range of testing environments.

### Reference documentation
To learn more, check out the Applitools Eyes [documentation](https://applitools.com/docs) and tutorials for other testing environments.

### Request a demo
If you want to see a demo of all our other features, you do [request a demo](https://applitools.com/request-demo/?utm_source=tutorials).

### Knowledge base and Support
You can search our [Knowldege base](https://help.applitools.com/hc/en-us/) for more information. You can also file a contact our support team and [file a Ticket](https://help.applitools.com/hc/en-us/requests/new).


# Documentation
Previously existing documentation for the Applitools Eyes QTP/UFT has been removed from the web. This repository contains PDF renderings from archived versions of this documentation.

Archived snapshots of the original documentation can also be accessed and viewed at the following links:

[Windows UFT Tutorial](https://github.com/rogerjefferiesEyes/eyes-uft/blob/master/Windows%20UFT%20Tutorial.pdf) (Original tutorial documentation)

[QTP/UFT Eyes SDK user guide](https://github.com/rogerjefferiesEyes/eyes-uft/blob/master/QTP_UFT%20Eyes%20SDK%20user%20guide.pdf)

[Running Eyes UFT tests on Perfecto Mobile](https://github.com/rogerjefferiesEyes/eyes-uft/blob/master/Running%20Eyes%20UFT%20tests%20on%20Perfecto%20Mobile%20%E2%80%93%20Applitools.pdf)