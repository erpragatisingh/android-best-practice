# android-best-practice
## Overview

There are many third-party libraries for Android but several of them are "must have" libraries that are extremely popular and are often used in almost any Android project. Each has different purposes but all of them make life as a developer much more pleasant. The major libraries are listed below in a few categories.

### Standard Pack

This "standard pack" listed below are libraries that are quite popular, widely applicable and should probably be setup within most Android apps:

| Name            | Description                                                 |  
| ----            | ------------                                                |
| [Retrofit|Consuming-APIs-with-Retrofit]] | A type-safe REST client for Android which intelligently maps an API into a client interface using annotations.            |
|[Glide|Displaying-Images-with-the-Glide-Library]] | A powerful image downloading and caching library for Android. |
| [ButterKnife|Reducing-View-Boilerplate-with-Butterknife]] | Using Java annotations, makes Android development better by simplifying common tasks. |
| [Parceler|Using-Parceler]] | Android Parcelable made easy through code generation |
| [IcePick](https://github.com/frankiesardo/icepick) | Android Instance State made easy |
| [LeakCanary](https://github.com/square/leakcanary) | Catch memory leaks in your apps | 
| [Espresso|UI-Testing-with-Espresso]] | Powerful DSL for Android integration testing |
| [Robolectric|Unit-Testing-with-Robolectric]] | Efficient unit testing for Android |

### Advanced Pack

The "advanced pack" listed below are additional libraries that are more advanced to use but are popular amongst some of the best Android teams. Note that these libraries may not be suitable for your first app. These advanced libraries include:

| Name            | Description                                                 |  
| ----            | ------------                                                |
| [[Dagger 2|Dependency-Injection-with-Dagger-2]]  | A fast dependency injector for managing objects.           |
| [[RxJava|RxJava]] | Develop fully reactive components for Android.       |
| [[EventBus|Communicating-with-an-Event-Bus]] | Android event bus for easier component communication.             |
| [AndroidAnnotations](https://github.com/excilys/androidannotations) | Powerful annotations to reduce boilerplate code. |
| [[Retrolambda|Lambda Expressions]]| Bringing lambda block support to Android. |

Keep in mind that the combination of these libraries may not always play nicely with each other.  The following section highlights some of these issues.

#### Parceler and IcePick

Note that you cannot use IcePick at the current time to save state of Parceler objects. See [this GitHub issue](https://github.com/frankiesardo/icepick/pull/20) for more context on why they are incompatible. You will need to use explicitly Parcelable objects with IcePick. You may consider replacing Parceler with [AutoParcel](https://github.com/frankiesardo/auto-parcel) which works seamlessly with IcePick. 

#### ButterKnife and Parceler

Using the Butterknife library with the Parceler library causes multiple declarations of javax.annotation.processing.Processor.  In this case, you have to exclude this conflict in your `app/build.gradle` file:

```gradle
   packagingOptions {
        exclude 'META-INF/services/javax.annotation.processing.Processor'  // butterknife
    }
```

#### ButterKnife and Custom Views

Often you may find that using ButterKnife or Dagger injections defined in your constructor prevent Android Studio to preview your Custom View layout.  You may see an error about needing `isEditMode()` defined.
Essentially this method is used to enable your code to short-circuit before executing a section of code that might be used for run-time but cannot be executed within the preview window.

```java
  public ContentEditorView(Context context, AttributeSet attrs) {
        super(context, attrs);

        LayoutInflater inflater = (LayoutInflater) context
                .getSystemService(Context.LAYOUT_INFLATER_SERVICE);

        inflater.inflate(R.layout.view_custom, this, true);

        // short circuit here inside the layout editor
        if(isInEditMode()) {
            return;
        }

        ButterKnife.bind(this);
```

### Convenience

 * [Dagger](http://square.github.io/dagger/) - A fast dependency injector for Android and Java.  See this [video intro](http://www.infoq.com/presentations/Dagger) from Square.
 * [Spork](https://sporklibrary.github.io) - Spork is an annotation processing library to speed up development on your projects. It allows you to write less boilerplate code to make your code more readable and maintainable.
 * [AutoParcel](https://github.com/frankiesardo/auto-parcel) - Port of Google AutoValue for Android with Parcelable generation goodies.
 * [Hugo](https://github.com/JakeWharton/hugo) - Easier logging within your app
 * [Logger](https://github.com/orhanobut/logger) - Much cleaner and easier logcat trace messages
 * [LeakCanary](https://github.com/square/leakcanary) - Easily catch memory leaks as they occur
 * [AndroidAnnotations](https://github.com/excilys/androidannotations) - Framework that speeds up Android development. It takes care of the plumbing, and lets you concentrate on what's really important. By simplifying your code, it facilitates its maintenance
 * [Calligraphy](https://github.com/chrisjenx/Calligraphy) - Custom fonts made easy
 * [EasyFonts](https://github.com/vsvankhede/easyfonts) - Easy preloaded custom fonts in your app
 * [AndroidViewAnimations](https://github.com/daimajia/AndroidViewAnimations) - Common property animations made easy
 * [AboutLibraries](https://github.com/mikepenz/AboutLibraries) - Automatically generates an *About this app* section, with a list of used libraries 
 * [SDK Manager Plugin](https://github.com/JakeWharton/sdk-manager-plugin) - Helpful plugin especially for group projects if you're missing an SDK version, haven't downloaded an API version, or your support library is updated.  
 * [EasyDeviceInfo](https://github.com/nisrulz/easydeviceinfo) - Get device information in a super easy way

### Extensions 

 * [RxJava](https://github.com/ReactiveX/RxJava) - Reactive Extensions for the JVM
 * [EventBus](https://github.com/greenrobot/EventBus) - Android optimized event bus that simplifies communication between components.
 * [Tape](http://square.github.io/tape/) - Tape is a collection of queue-related classes for Android and Java
 * [Priority Job Queue](https://github.com/yigit/android-priority-jobqueue) - Easier background tasks
 * [ACRA](http://acra.ch/) - Crash reporting made easy and free. Check the [setup instructions](https://github.com/ACRA/acra/wiki/BasicSetup) and [open-source backend](https://github.com/ACRA/acralyzer).

### Networking

 * [Retrofit](http://square.github.io/retrofit/) - A type-safe REST client for Android and Java which intelligently maps an API into a client interface using annotations. 
 * [Picasso](http://square.github.io/picasso/) - A powerful image downloading and caching library for Android.
 * [Ion](https://github.com/koush/ion) - Powerful asynchronous networking library. [Download](https://github.com/koush/ion#get-ion) as a jar here.
 * [Android Async HTTP](http://loopj.com/android-async-http/) - Asynchronous networking client for loading remote content such as JSON.
 * [Volley](http://developer.android.com/training/volley/index.html) - Google's HTTP library that makes networking for Android apps easier and most importantly, faster.
 * [[OkHttp|Using OkHttp]] - Square's underlying networking library with support for asynchronous requests.
 * [[Glide|Displaying-Images-with-the-Glide-Library]] - Picasso image loading alternative endorsed by Google 
 * [Android Universal Image Loader](https://github.com/nostra13/Android-Universal-Image-Loader) - Popular alternative for image loading that can replace Picasso or Glide.
 * [Fresco](http://frescolib.org/) - An image management library from Facebook.
 * [Fast Android Networking](https://github.com/amitshekhariitbhu/Fast-Android-Networking) -Fast Android Networking is a powerful library for doing any type of networking in Android applications which is made on top of OkHttp Networking Layer.


### ListView

 * [EasyListViewAdapters](https://github.com/birajpatel/EasyListViewAdapters) - Building multi-row-type listview made much cleaner & easier.
 * [GridListViewAdapters](https://github.com/birajpatel/GridListViewAdapters) - Easily build unlimited Grid cards list like play-store. (ListView working as unlimited GridView)
 * [StickyListHeaders](https://github.com/emilsjolander/StickyListHeaders) - An android library for section headers that stick to the top of a ListView
 * [PinnedListView](https://github.com/beworker/pinned-section-listview) - Pinned Section with ListView
 * [ListViewAnimations](https://github.com/nhaarman/ListViewAnimations) - Easy way to animate ListView items
 * [Cardslib](https://github.com/gabrielemariotti/cardslib) - Card UI for Lists or Grids
 * [PullToRefresh-ListView](https://github.com/erikwt/PullToRefresh-ListView) - Easy to use pull-to-refresh functionality for ListViews. [Download](https://github.com/erikwt/PullToRefresh-ListView/archive/master.zip) and install as a [library project](http://imgur.com/a/N8baF).
 * [QuickReturn](https://github.com/lawloretienne/QuickReturn) - Reveal or hide a header or footer as the list is scrolled in a direction.
 * [Paginated Table](https://github.com/ojinxy/AndroidComponents) - This is a table which allows dynamic paging for any list of objects. Icons can be added to columns as well as custom items such as check boxes and buttons.

### RecyclerView

* [UltimateRecyclerView](https://github.com/cymcsg/UltimateRecyclerView) - Augmented RecyclerView with refreshing, loading more, animation and many other features.
* [AdvRecyclerView](https://github.com/h6ah4i/android-advancedrecyclerview) - Extended RecyclerView with swipe to dismiss, and draggable or expanding items. 
* [android-parallax-recyclerview](https://github.com/kanytu/android-parallax-recyclerview) - An adapter which could be used to achieve a parallax effect on RecyclerView.
* [sticky-headers-recyclerview](https://github.com/timehop/sticky-headers-recyclerview) - Sticky Headers decorator for Android's RecyclerView.
* [FastAdapter](https://github.com/mikepenz/FastAdapter) - Simplify and speed up the process of filling your RecyclerView with data
* [ItemAnimators](https://github.com/mikepenz/ItemAnimators) - RecyclerView animators to animate item add/remove/add/move
* [GreedoLayout](https://github.com/500px/greedo-layout-for-android) - Full aspect ratio grid LayoutManager for Android's RecyclerView
* [RecyclerViewHelper](https://github.com/nisrulz/recyclerviewhelper) - Provides the most common functions around recycler view like Swipe to dismiss, Drag and Drop, Divider in the ui, events for when item selected and when not selected, on-click listener for items.

### Easy Navigation 

 * [JazzyViewPager](https://github.com/jfeinstein10/JazzyViewPager) - Pager with more animations
 * [ParallaxPager](https://github.com/prolificinteractive/ParallaxPager) - ViewPager with Parallax scrolling effects
 * [ParallaxHeaderViewPager](https://github.com/kmshack/Android-ParallaxHeaderViewPager) - Another ViewPager with Parallax scrolling effects
 * [ParallaxPagerTransformer](https://github.com/xgc1986/ParallaxPagerTransformer) - A pager transformer for Android with parallax effect
 * [SlidingMenu](https://github.com/jfeinstein10/SlidingMenu) - Library that allows developers to easily create applications with sliding menus like those made popular in the Google+, YouTube, and Facebook apps.
 * [Android Satellite Menu](https://github.com/siyamed/android-satellite-menu/) - Radial menu which is configurable reminiscent of the "Path" menu style.
 * [ArcMenu](https://github.com/daCapricorn/ArcMenu) - Alternate radial menu modeled after the "Path" menu style.
 * [AndroidSlidingUpPanel](https://github.com/umano/AndroidSlidingUpPanel) - Sliding Up Panel 
 * [DraggablePanel](https://github.com/pedrovgs/DraggablePanel) - Panels that can be dragged
 * [MaterialDrawer](https://github.com/mikepenz/MaterialDrawer/) - Easily add a Navigation Drawer with Material style and AccountSwitcher

### UI Components
 * [SparkButton](https://github.com/varunest/SparkButton) - Library to create buttons with Twitter's heart like animation.
 * [Crouton](https://github.com/keyboardsurfer/Crouton) - Context-sensitive, configurable alert notices much better than toasts. Download jar [from here](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22de.keyboardsurfer.android.widget%22). See [working sample code](https://github.com/codepath/android-crouton-sample)
 * [BetterPickers](https://github.com/derekbrameyer/android-betterpickers) - BetterPickers for easy input selection
 * [android-shape-imageview](https://github.com/siyamed/android-shape-imageview) - Custom shaped android imageview components including bubble, star, heart, diamond.
 * [RoundedImageView](https://github.com/vinc3m1/RoundedImageView) - Easily round corners or create oval-shaped images with this popular library.
 * [Android StackBlur](https://github.com/kikoso/android-stackblur) - Dynamically blur images
 * [Android Bootstrap](https://github.com/Bearded-Hen/Android-Bootstrap) - Bootstrap UI widgets
 * [PhotoView](https://github.com/chrisbanes/PhotoView) - ImageView that supports touch gestures
 * [ShowcaseView](https://github.com/amlcurran/ShowcaseView) - Highlight the best bits of your app
 * [FadingActionBar](https://github.com/ManuelPeinado/FadingActionBar) - Cool actionbar fade effect
 * [AndroidViewAnimations](https://github.com/daimajia/AndroidViewAnimations) - Easily apply common animations
 * [ProgressWheel](https://github.com/Todd-Davies/ProgressWheel) - Better progress bar
 * [SmoothProgressBar](https://github.com/castorflex/SmoothProgressBar) - Horizontal indeterminate progress
 * [CircularFillableLoaders](https://github.com/lopspower/CircularFillableLoaders) - Beautiful animated fillable loaders
 * [Rebound](http://facebook.github.io/rebound/) - Easy spring dynamics
 * [AndroidImageSlider](https://github.com/daimajia/AndroidImageSlider) - Animated image transitions
 * [FloatingActionButton](https://github.com/makovkastar/FloatingActionButton) - Material design floating buttons made easy
 * [Foursquare-CollectionPicker](https://github.com/anton46/Foursquare-CollectionPicker) - Item Picker which looks like Foursquare Tastes picker
 * [NexusDialog](https://github.com/dkharrat/NexusDialog) - Create form dialogs easily
 * [dialogplus](https://github.com/orhanobut/dialogplus) - Simple, easy dialogs
 * [Iconify](https://github.com/JoanZapata/android-iconify) - Easily embed icons into your app
 * [Android StepsView](https://github.com/anton46/Android-StepsView) - A library to create StepsView for Android
 * [PhotoView](https://github.com/chrisbanes/PhotoView) - A library to pinch zoom in and zoom out and double tap zoom for Android
 * [Android-Iconics](https://github.com/mikepenz/Android-Iconics) - Add many scalable and styleable icons into your app
 * [Scissors](https://github.com/lyft/scissors) - An easy image cropping library developed by Lyft.
 * [Material-SearchView](https://github.com/MiguelCatalan/MaterialSearchView) - Beautiful Material SearchView made simple.
 * [PersistentSearchBar](https://github.com/arimorty/floatingsearchview) - Implementation of a persistent search bar.
 * [Android Material Intro Screen](https://github.com/TangoAgency/material-intro-screen/) - Library for easily adding intro screen to app.

### Drawing

 * [MPAndroidChart](https://github.com/PhilJay/MPAndroidChart) - A powerful Android chart view / graph view library, supporting line- bar- pie- radar- bubble- and candlestick charts as well as scaling, dragging and animations.
 * [HoloGraphLibrary](https://github.com/Androguide/HoloGraphLibrary) - Newer graphing library
 * [EazeGraph](https://github.com/blackfizz/EazeGraph) - Another newer library with potential
 * [AndroidCharts](https://github.com/dacer/AndroidCharts) - Easy to use charts
 * [AndroidGraphView](http://android-graphview.org/) - library to create flexible and nice-looking diagrams.
 * [AndroidPlot](http://androidplot.com/docs/quickstart/) - plotting library for Android
 * [WilliamChart](https://github.com/diogobernardino/WilliamChart) - Flexible charting library with useful motion capabilities.
 * [HelloCharts](https://github.com/lecho/hellocharts-android) - Charts/graphs library for Android with support for scaling, scrolling and animations.
 * [Leonids](https://github.com/plattysoft/Leonids) - Simple and easy particle effects ([See Tutorial](http://www.plattysoft.com/2014/05/30/leonids-particle-system-lib/))
 * [Confetti](https://github.com/jinatonic/confetti) - Newer particle effects library. 
 * [AChartEngine](http://jaxenter.com/effort-free-graphs-on-android-with-achartengine-46199.html) - This is a charting software library for Android applications

### Image Processing

* [AndroidPhotoFilters](https://github.com/zomato/androidphotofilters) - Library to create interesting effects on any image of your choice. Comes with prebuilt great sample effects.
* [android-gpuimage](https://github.com/CyberAgent/android-gpuimage) - Popular GPU Image Processing
* [android-image-filter](https://github.com/ragnraok/android-image-filter) - Older image filtering library
* [picasso-transformations](https://github.com/wasabeef/picasso-transformations) - Library for processing images via Picasso
* [glide-transformations](https://github.com/wasabeef/glide-transformations) - Process images via Glide
* [ImageEffectFilter](https://github.com/mnafian/ImageEffectFilter) - Sample code for processing images.
* [VidEffects](https://github.com/krazykira/VidEffects) - Apply manipulation effects to videos.

### Scanning

 * [ZXing](https://github.com/zxing/zxing) - Barcode or QR scanner
 * [ZXing Android Embedded](https://github.com/journeyapps/zxing-android-embedded) - Alternative zxing scanner
 * [barcodescanner](https://github.com/dm77/barcodescanner) - Newer alternative
 * [CamView](https://github.com/LivotovLabs/CamView) - ZXing alternative
 * [android-quick-response-code](https://code.google.com/p/android-quick-response-code/) - Another alternative

### Persistence

 * [[ActiveAndroid|ActiveAndroid-Guide]]
 * [[DBFlow|DBFlow Guide]] - A robust, powerful, and very simple ORM android database library with annotation processing.
 * [greenDAO](https://github.com/greenrobot/greenDAO)
 * [SugarORM](http://satyan.github.io/sugar/)
 * [RxCache](https://github.com/VictorAlbertos/RxCache) - Reactive caching library for Android
 * [ORMLite](http://ormlite.com/sqlite_java_android_orm.shtml)
 * [SQLBrite](https://github.com/square/sqlbrite) - Lightweight wrapper around SQLiteOpenHelper
 * [[Cupboard|Easier-SQL-with-Cupboard]] - Popular take on SQL wrapper
 * [StorIO](https://github.com/pushtorefresh/storio) - Fresh take on a light SQL wrapper
 * [Realm](https://github.com/realm/realm-java)
 * [NexusData](https://github.com/dkharrat/NexusData)
 * [Hawk](https://github.com/orhanobut/hawk) - Persistent secure key/value store
 * [Poetry](https://github.com/elastique/poetry) - Persist JSON directly into SQLite
 * [JDXA](http://softwaretree.com/v1/products/jdxa/jdxa.html) - The KISS ORM for Android - Simple, Non-intrusive, and Flexible

### Binding
 * [RecyclerViewBinding](https://github.com/radzio/android-data-binding-recyclerview) - Library for easily add recycler view data bindings.
 * [CommandDataBinding](https://github.com/radzio/android-data-binding-command) - Library for better handling onClick actions.

### Compatibility

 * [NineOldAndroids](http://nineoldandroids.com/) - Fully compatible animation library that works with all versions of Android. Widely used. [Download](https://github.com/JakeWharton/NineOldAndroids/zipball/master) and install as a [library project](http://imgur.com/a/N8baF).
 * [HoloEverywhere](https://github.com/Prototik/HoloEverywhere) - Backport Holo theme from Android 4.2 to 2.1+
 * [CropImage](https://github.com/biokys/cropimage) - Simple compatible cropping intent for images

### Scrolling and Parallax

This is a list of popular scrolling and parallax libraries:

* [QuickReturn](https://github.com/lawloretienne/QuickReturn) - Reveal or hide a header or footer as the list is scrolled in a direction.
* [ParallaxPagerTransformer](https://github.com/xgc1986/ParallaxPagerTransformer) - A pager transformer for Android with parallax effect
* [ParallaxHeaderViewPager](https://github.com/kmshack/Android-ParallaxHeaderViewPager) - Another ViewPager with Parallax scrolling effects
* [Android-ObservableScrollView](https://github.com/ksoichiro/Android-ObservableScrollView) - Android library to observe scroll events on scrollable views.
* [Scrollable](https://github.com/noties/Scrollable) - Automatic scrolling logic when implementing scrolling tabs
* [ParallaxPager](https://github.com/prolificinteractive/ParallaxPager) - ViewPager with Parallax scrolling effects
* [android-parallax-recyclerview](https://github.com/kanytu/android-parallax-recyclerview) - An adapter which could be used to achieve a parallax effect on RecyclerView.
 
### Debugging

* [Stetho](http://facebook.github.io/stetho/) - A debug bridge for Android applications which could be used for multiple purposes not limited to Network Inspection, Database Inspection and Javascript Console.
* [Bugfender](https://github.com/bugfender/bugfender-android-sample/) - Cloud storage for your app logs, track user behaviour to find problems in your mobile apps.

## Resources

Check out the following resources for finding libraries:

 * <http://android-arsenal.com>
 * [Wasabeef Core Libraries](https://github.com/wasabeef/awesome-android-libraries)
 * [Wasabeef UI Libraries](https://github.com/wasabeef/awesome-android-ui)
 * [Snowdream Android Library Repository](https://snowdream.github.io/awesome-android/)
 * [Android-Libs.com](http://android-libs.com)
 * <http://androidlibs.org/>
 * <http://appdevwiki.com/wiki/show/HomePage>
 * <http://www.libtastic.com>

## References

 * <http://www.vogella.com/tutorials/AndroidUsefulLibraries/article.html>
 * <http://actionbarsherlock.com/>
 * <http://nineoldandroids.com/>
 * <https://github.com/roboguice/roboguice/wiki>
 * <https://github.com/excilys/androidannotations/wiki>
 * <https://github.com/erikwt/PullToRefresh-ListView>
 * https://github.com/jfeinstein10/SlidingMenu
 * <http://square.github.io/picasso/>
