###1. File - > New Project- >Empty Activity - >MemeShare
	In main.actovity.xml -> design - > add an avatar via Image View
	Go to Split - Edit the code. Add Buttons for share and next , Add Vertical Guideline to indicate the right parent of SHARE and left parent of NEXT
	<img src="https://github.com/AkshayAnil1080/MemeShareApp/blob/main/images/1.jpg" width=150 height=100/>
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

	<img src="https://github.com/AkshayAnil1080/MemeShareApp/blob/main/images/ms1.jpg" width=150 height=100/>

Adding API