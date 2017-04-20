mikelupo's fix:

"Before this change, the parser would just start over for a given
suite in the case where a crash occured during the run.
That being, if a suite contained 10 tests, and the app under test
crashed during test 5, XCUnit would restart
itself but OCUnit2Junit would lose the status of the previously
ran tests up to the point of the restart. Hence, we'd end up with
results for 6-10, The results from 1-4 would be lost as well as
from 5 (containing the crash info).

This commit attempts to handle this case."


Introduction
======================

OCUnit2JUnit is a script that converts output from OCUnit or [Kiwi](https://github.com/allending/Kiwi) to the format used by JUnit. The main purpose is to be able to parse output from Objective-C (OCUnit) test cases on a Java-based build server, such as [Jenkins](http://jenkins-ci.org/).


Installation
======================

* Install with 'gem install ocunit2junit' (possibly prepended by 'sudo' if your Ruby installation requires that)


Usage
======================

* Make sure your build server can access the xcodebuild executable
* Use this shell command to build: 

	`xcodebuild -target <target> -sdk <sdk> -configuration <config> 2>&1 | ocunit2junit`

* The output is, by default, in the `test-reports` folder
* If your build fails, this script will pass the error code
* All output is also passed along, so you will still see everything in your build log


Kiwi
======================

This script also generates human readable test results for [Kiwi BDD Testing Framework](https://github.com/allending/Kiwi):

![Example output](https://github.com/MattesGroeger/OCUnit2JUnit/raw/master/example.png "Example output")

However, if you don't want this, you can disable it in the header:

	SUPPORT_KIWI = false


More information
======================

* If you're having issues with character encoding, please upgrade to Ruby 1.9.2 or later.
* More info can be found in [this blog post](http://blog.jayway.com/2010/01/31/continuos-integration-for-xcode-projects/).


Licence
======================

Free to use however you want.


Author
======================

OCUnit2JUnit was created by Christian Hedin.
Twitter: @ciryon
Google Plus: https://plus.google.com/103286810504956788514/
