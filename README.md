###1. File - > New Project- >Empty Activity - >MemeShare
	In main.actovity.xml -> design - > add an avatar via Image View
	Go to Split - Edit the code. Add Buttons for share and next , Add Vertical Guideline to indicate the right parent of SHARE and left parent of NEXT

 	<ImageView
       	android:id="@+id/imageView3"
        android:layout_width="0dp" 
        android:layout_height="0dp"			 - height and width as 0 dp makes the image a single line 
        app:layout_constraintBottom_toBottomOf="parent"	 - making left , right , top , bottom constraint as parent so that the image spread outs evenly  on screen
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:srcCompat="@tools:sample/avatars" />

    	<Button
        android:id="@+id/shareButton" 
        android:layout_width="0dp" 			- makes the width as long as free space is there.
       	 android:layout_height="wrap_content"		- make the heigh according to the content	
        android:padding="32dp"				- giving padding to make button size bigger
        android:text="Share"				- text in button
        app:layout_constraintBottom_toBottomOf="parent" - bottom to share is parent
        app:layout_constraintLeft_toLeftOf="parent"	- left to share is parent
        app:layout_constraintRight_toLeftOf="@id/guideline2" - need a vertical guideline - righ of share is guideline and left of guideline is share => button right to left of is guideline
        android:onClick="shareMeme"/>

    	<Button
        android:id="@+id/nextButton"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:padding="32dp"
        android:text="Next"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toRightOf="@id/guideline2"
        app:layout_constraintRight_toRightOf="parent"
        android:onClick="nextMeme"/>


    <androidx.constraintlayout.widget.Guideline   - there was nothing to make the parent of right of share button and left of next button - guidelines are used 
        android:id="@+id/guideline2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_percent="0.5" /> - using percent =0.5 to make the vertical line exact in the middle of screen

<img src="https://github.com/AkshayAnil1080/MemeShareApp/blob/main/images/ms1.jpg" width==350 height=200/>
	Also, Extract String resorce for android:text="Share" and android:text="Next"

### 2. Volley 

	open source library -Volley is an HTTP library that makes networking for Android apps easier and most importantly, faster. Volley is available on GitHub.
	Need to add dependecies in our app, specifically in gradle.
		dependencies {
    				...
   			 implementation 'com.android.volley:volley:1.2.0'
				}
	Go to Gradle Scrips -> build.gradle - > add above dependencies

	https://developer.android.com/training/volley/simple

	TO SEND A SIMPLE REQUEST
	1. ADD INTERNET PERMISSION - To use Volley, you must add the android.permission.INTERNET permission to your app's manifest. Without this, your app won't be able to connect to the network.
	Go to manifests file write one line     <uses-permission android:name="android.permission.INTERNET"/>

	2. Create JsonObjectRequest
	
#### 2a.CREATING AND CHECKING StringRequest
 	private fun loadMeme(){  // copy the code for android documentation
        	// Instantiate the RequestQueue.
       		val queue = Volley.newRequestQueue(this)
        	val url = "https://www.google.com"

	// Request a string response from the provided URL.
        	val stringRequest = StringRequest(
            	  Request.Method.GET, url,
            	  Response.Listener<String> { response ->
               		Log.d("success Request" , response.substring(0,500))   // same as doing debugging via println in java - printing first 500 characters
            	},
           	  Response.ErrorListener {
              		Log.d("error", it.localizedMessage)
            	})

success image

	Now, lets make  JSON object request

 		private fun loadMeme(){  // copy the code for android documentation
        	// Instantiate the RequestQueue.
        	val queue = Volley.newRequestQueue(this)
        	val url = "https://meme-api.herokuapp.com/gimme"  		// using meme api

		// Request a string response from the provided URL.
        	val jsonObjectRequest = JsonObjectRequest(			// changing to JsonObjectRequest
            	   Request.Method.GET, url, null,   				// we dont want to send anything ie. null
            	   Response.Listener { response ->				// output stored in response

                	val url = response.getString("url")			// we need to url string of json file
			Glide.with(this).load(url).into(imageView3)		// refer step 3	
            	},	
            	   Response.ErrorListener {

            	})

	success image
	
### 3. Glide - for images - to pass the images getting from api to image view.

	https://github.com/bumptech/glide
	repositories { 					// in build.grade(Project...)
  	google()
  	mavenCentral()
	}

	dependencies {					// in build.grade(Module...)
  	implementation 'com.github.bumptech.glide:glide:4.12.0'
  	annotationProcessor 'com.github.bumptech.glide:compiler:4.12.0'
	}
	Add these repositories and dependencies in gradle - SYNC NOW

### 4. NEXT button for next memes
	
	Just call the loadmeme() function under the nextmeme function
	 fun nextMeme(view: View) {
        	loadMeme()
   	 }



