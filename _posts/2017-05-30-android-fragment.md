---
layout: post
title: "[Android App]   Activity vs Fragment"
excerpt: "안드로이드 앱개발 fragment"
data: 2017-05-30
comments: true

tag:

---

#  Why Fragment ?
**Activity** is a basic element of android app. When we make a app, Many Views are located in a **Activity**.
But after Tablet or large size Phone comes out, we need to put more Views in **Activity** and it can't cover complexity of many Views and can't be dynamic( reuse ,View hide, View translate . .).

So, we choose **Fragment** to resolve these problem.

I think **Fragment** is a Views gorup or a module of ViewGroup, So I call "**Fragment**" to "semi - Activity"

### Advantage
1. Reuse in every Activity.
2. Able to use Fragments more than one, in Activity.
3. If you change portrait to landscape mode, we can relocate Views.
4. if you use fragments, you can make app using few activity.
5. you can change the screen, not changing Activity.

### Disadvantage
1. one Fragment can be super related with one Activity. So it can't reuse.

#

### LifeCycle
![Fragment.LifeCycle](https://i.stack.imgur.com/fRxIQ.png)

**Reference**: http://baiduhix.blogspot.com.br/2015/08/android-how-to-do-findviewbyid-in.html


**OnCreate()** : When a Fragment is created, call this method. Through **savedInstanceState**, we can reuse "we don't need to define this method"

**OnCreateView()** : When the Fragment draws UI, call this method. In this method, we should inflate Layout to View. "we must define this method !!"

~~~ java
@Override
public void OnCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState)
{
  return inflater.inflate(R.layout.your_content,null);
}

~~~
**OnActivityCreated()** : After OnCreateView() ended, this method is called. Activity and Fragment have been created. So, We can change views.


## Code
**content_layout.xml**
~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent" >

    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/main_fragment">
    </FrameLayout>


</LinearLayout>
~~~


**fragment.xml**
~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Bitton
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/Button">
    </Button>
</FrameLayout>
~~~
 Note FrameLayout in fragment.xml. In content_layout.xml, FrameLayout exist. So  
<br/>



**fragment.java**
~~~java

public class button_fragment extends fragment{

  //member variables
  private Button mButton;

  //constructor
  public button_fragment(){

    //TODO: memver initialize

  }

  @Override
  public void OnCreate(Bundle savedInstanceState){
    super.onCreate(savedInstanceState);
  }

  @Override
  public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState)
  {
       // this object connects itself layout.
       return inflater.inflate(R.layout.fragment,container,false);

  }

   @Override
   public void OnActivityCreated(Bundle savedInstanceState){

       super.OnActivityCreated(savedInstanceState);

       this.mButton = (Button)getView().findViewById(R.id.Button);

       this.mButton.setText("my Button!");

       //TODO: you can set how views work  

  }
}
~~~

**MainActivity.java**
~~~java
public class MainActivity extends AppCompatActivity{

    @Override
    public void onCreate(Bundle savedInstanceState){

        // this activity connects itself layout
        super.onCreate(savedInstanceState);
        setContentView(R.layout.content_layout);


        // new Fragment Manager created
        FragmentManager fm = getFragmentManager();
        FragmentTransaction fragmentTransaction = fm.beginTransaction();

        button_fragment fg = new button_fragment();


        // Custom fragment is connected to Framelayout in content_layout.xml
        fragmentTransaction.add(R.id.main_fragment, fg);
        fragmentTransaction.commit();
    }
}
~~~
</br>
So, in order to use Fragment, we need to make at least four file. 
 **fragment.java, fragment.xml, MainActivity.java, MainActivity.xml**  
