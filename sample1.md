# Alamofire

I've been working with concurrency and Grand Central Dispatch. I was looking for a background task that would take some time, something more realistic than a loop sending 1 second sleep statements. Most of the GCD references cite networking tasks as the poster child for async activity. So I thought I'd construct a demo project to get an image from a web URL, only to discover that this is not readily done in SwiftUI without using something like Alamofire to manage the network activity. So maybe it's time to take a peak down this rabbit hole and see what Alamofire has to offer.

[Alamofire 5 Tutorial for iOS: Getting Started](https://www.raywenderlich.com/6587213-alamofire-5-tutorial-for-ios-getting-started)

Starter project already includes Alamofire CocoaPod

[CocoaPods Tutorial for Swift: Getting Started](https://www.raywenderlich.com/7076593-cocoapods-tutorial-for-swift-getting-started)

This uses Alamofire 4.9.1 as the example CocoaPod

- Install `Alamofire` using `CocoaPods`

    The Wenderlich CocoaPods Tutorial is out of date ... it specifies iOS 9.0 and Alamofire 4.9.1. Here's the process I actually used:

    (1) Start a project in Xcode called `cocoapod01`. Exit Xcode.

    (2) In Terminal, navigate to the project folder: `cd ~/desktop/cocoapod01`. use `ls -a` to confirm we are "in" the project folder.

    (3) Use `pod init` to create a podfile

    (4) Use BBEdit to edit the podfile as follows, and save it:

    ```swift
    platform :ios, '13.0'

    target 'cocoapod01' do
      use_frameworks!
      pod 'Alamofire', '~> 5.2'

    end
    ```

    (5) In Terminal, run `pod install` and the following should result:

    ![Alamofire%2036da70dec9da4602a83c6f5b0e13e3b1/Screen_Shot_2020-08-20_at_7.28.47_AM.jpg](Alamofire%2036da70dec9da4602a83c6f5b0e13e3b1/Screen_Shot_2020-08-20_at_7.28.47_AM.jpg)

    (6) Open the file `cocoapod01.xcworkspace`

    (7) Add the statement `import Alamofire` to the project, most likely, right after `import SwiftUI`

    Alamofire should now be available to the project.

- Use `Alamofire` to download `JSON` data from APIAlamoFire get String from website

    This is a very simple example, just to demonstrate that a request can be made to AF and that data is downloaded to the app. This is the site accessed from the first RW tutorial above.

    ```swift
    import SwiftUI
    import Alamofire

    struct ContentView: View {
      var body: some View {
        Text("Hello, world!")
          .padding()
          .onTapGesture(count: 1, perform: {
            let request = AF.request("https://swapi.dev/api/films")
            // 2
            request.responseJSON { (data) in
              print(data)
            }
          })
      }

    }
    ```

    This downloads a bunch of data from the Star Wars API and interprets it using the JSON decoder.

    ![Alamofire%2036da70dec9da4602a83c6f5b0e13e3b1/Screen_Shot_2020-08-20_at_5.40.00_PM.jpg](Alamofire%2036da70dec9da4602a83c6f5b0e13e3b1/Screen_Shot_2020-08-20_at_5.40.00_PM.jpg)

    This works fine for data that is already on the internet and is accessible to the public. And there seems to be quite a bit of data out there in various APIs. But what if i'd like to access my own files from some internet site?

- Use AlamoFire to download `String` from `Github` website

    This demo was a breakthrough. I created a plain text file using BBEdit, called `test01.txt`. I placed it on a GitHub Pages repository, in a Resources folder. It is now accessible as `https://terryg99.github.io/Resources/test01.txt`. In this demo, we use `Alamofire` to access the plain text file from GitHub website.

    Don't forget to install the `AlamoFire CocoaPod`

    ```html
    import SwiftUI
    import Alamofire

    struct ContentView: View {
      var body: some View {
        Text("Hello, world!")
          .padding()
          .onTapGesture(count: 1, perform: {
            let request = AF.request("https://terryg99.github.io/Resources/test01.txt")
            // 2
            request.responseString { (data) in
              print(data)
            }
          })
      }
    }
    ```

    and the result is ...

    ![Alamofire%2036da70dec9da4602a83c6f5b0e13e3b1/Screen_Shot_2020-08-24_at_10.21.42_PM.jpg](Alamofire%2036da70dec9da4602a83c6f5b0e13e3b1/Screen_Shot_2020-08-24_at_10.21.42_PM.jpg)