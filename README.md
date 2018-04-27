WORD SEARCH APP
---------------

This app downloads a dictionary file and provides suggestions based on input sequence

DICTIONARY
----------
We use a dictionary file containing 235886 words. File is hosted at https://raw.githubusercontent.com/fatihsokmen/word-search-db/master/words.txt

In real world app, we have to use E-Tag mechanism to avoid downloading file evertime. If content is not changed, web server should return HTTP 304 (NOT MODIFIED) otherwise we are supposed to get the file content with HTTP 200. For this example app, we download everytime when the app is launched.



ASSUMPTIONS
-----------
- Because dictionary size is not specified in requirenmets, we implemented an app to handle hundred thousands of words, in terms of insertion and search.
- App uses SQLite database directly to avoid any out of memory issues as we are inserting huge amount data. 
- App reads dictionary file by a buffered reader so it likely avoids out of memory issues.
- We choose CursorLoader (support lib) to fecth results performed better than other SQL clients. Support Loaders are internally uses Live Data (Android Archtitecture Component) and cache cursor data. When screen orientation changes, It restores view states quickly and redelivery cached cursor data in main thread, so user experice is very fluent.
- Using LoaderCallbacks in the app potentially breaks some MVP contracts as activity does too much operations rather than only setting view states. 
- General idea of MVP presenters is that presenters should only contain Java code and it should not import android specific class.
- Dagger is heavily used to make app components testable.

TOOLS
-----
- RxJava for download and dobounce operation (dobounce is indeed not necessary for this app as Loaders performs really well, regarding low end devices we choose to use this operator)
- Dagger: Depedency injection
- Retrofit and OkHttp: For network operations
- ButterKnife: View binding
- Android support and Design libraries

