# Smiley Rating
SmileyRating is a simple rating bar for android. It displays animated smileys as rating icon.
  - Drawn completely using android canvas
  - Inspired by [Bill Labus](https://dribbble.com/shots/2790473-Feedback)

## Demo

 <img src="https://raw.githubusercontent.com/sujithkanna/SmileyRating/master/app/src/main/assets/demo.gif" alt="" data-canonical-src="https://gyazo.com/eb5c5741b6a9a16c692170a41a49c858.png" width="575" height="205" />

## Integration
Integrating SmileyRating in your project is very simple.
### Step 1:
Add this dependency in your project's build.gradle file which is in your app folder
```groovy
implementation 'com.github.venugopalachary:SmilyRatingExample'
```
add this to your dependencies.
## Step 2:
Now place the SmileyRating in your layout.
###### *Note: The height of the SmileyRating will be automatically adjusted according to the width of this component.*
```xml
< com.play4deal.hello.SmileRating
        android:id="@+id/smile_rating"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
```
## Step 3:
### Initialize your view
```java
SmileRating smileRating = (SmileRating) findViewById(R.id.smile_rating);
```
### Set this SmileySelectionListener to get notified when user selects a smiley
*By default the selected smiley will be NONE*
```java
smileRating.setOnSmileySelectionListener(new SmileRating.OnSmileySelectionListener() {
            @Override
            public void onSmileySelected(@BaseRating.Smiley int smiley, boolean reselected) {
	            // reselected is false when user selects different smiley that previously selected one
		        // true when the same smiley is selected.
		        // Except if it first time, then the value will be false.
                switch (smiley) {
                    case SmileRating.BAD:
                        Log.i(TAG, "Bad");
                        break;
                    case SmileRating.GOOD:
                        Log.i(TAG, "Good");
                        break;
                    case SmileRating.GREAT:
                        Log.i(TAG, "Great");
                        break;
                    case SmileRating.OKAY:
                        Log.i(TAG, "Okay");
                        break;
                    case SmileRating.TERRIBLE:
                        Log.i(TAG, "Terrible");
                        break;
                }
            }
        });
```
### If you want to know the level of user rating, You can listen for OnRatingSelectedListener
```java
smileRating.setOnRatingSelectedListener(new SmileRating.OnRatingSelectedListener() {
            @Override
            public void onRatingSelected(int level, boolean reselected) {
                // level is from 1 to 5 (0 when none selected)
                // reselected is false when user selects different smiley that previously selected one
		        // true when the same smiley is selected.
		        // Except if it first time, then the value will be false.
            }
        });
```

### Get current selection
```java
@Smiley int smiley = mSmileRating.getSelectedSmile();
switch (smiley) {
    case SmileRating.BAD:
        Log.i(TAG, "Bad");
        break;
    case SmileRating.GOOD:
        Log.i(TAG, "Good");
        break;
    case SmileRating.GREAT:
        Log.i(TAG, "Great");
        break;
    case SmileRating.OKAY:
        Log.i(TAG, "Okay");
        break;
    case SmileRating.TERRIBLE:
        Log.i(TAG, "Terrible");
        break;
    case SmileyRating.NONE:
	    Log.i(TAG, "None");
	    break;
}
```
this will return you an int value which indicated the current selected smiley
### Get current rating level
```java
int level = mSmileRating.getRating(); // level is from 1 to 5
// Will return 0 if NONE selected
```
### You can set selected smiley without user interaction
#### Without animation
```java
smileRating.setSelectedSmile(BaseRating.GREAT);
```
#### OR
```java
smileRating.setSelectedSmile(BaseRating.GREAT, false);
```
*The smiley will be selected without any animation and the listeners won't be triggered*
#### With animation
```java
smileRating.setSelectedSmile(BaseRating.GREAT, true);
```
*Smiley will be selected with animation and listeners will also be triggered(Only if the second param is true)*

You can even set the smiley to NONE with/without animation by passing NONE using same API.

#### You can change the smiley name also
Raw string
```java
mSmileRating.setNameForSmile(BaseRating.TERRIBLE, "Angry");
```
String resources
```java
mSmileRating.setNameForSmile(BaseRating.TERRIBLE, R.string.anyTitle);
```

![Angry](https://raw.githubusercontent.com/sujithkanna/SmileyRating/master/app/src/main/assets/angry.jpg)

#### Custom font
You can change the title color of smileys.
```java
mSmileRating.setTypeface(yourTypeface);
```

#### Change colors
You can set change the colors by xml
```xml
<com.hsalf.smilerating.SmileRating
        android:id="@+id/ratingView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_centerVertical="true"
        app:angryColor="#f29a68"
        app:drawingColor="#353431"
        app:normalColor="#f2dd68"
        app:isIndicator="false"
        app:placeHolderBackgroundColor="#e6e8ed"
        app:placeHolderSmileColor="#ffffff"
        app:textNonSelectionColor="#AEB3B5"
        app:textSelectionColor="#000000" />
```

| Params  | Description |
| ------------- | ------------- |
| `app:angryColor`  | To set the color of the Angry/Terrible smiley's background color.  |
| `app:normalColor`  | To change the color of all smileys background color except Angry/Terrible smiley.  |
| `app:drawingColor`  | To change the color of all smileys (Smile and eyes).  |
| `app:placeHolderSmileColor`  | To set the color of all placeholder smiley's (Smile and eyes) color.  |
| `app:placeHolderBackgroundColor`  | To set the color of all placeholder smiley's background color.  |
| `app:textSelectionColor`  | To set the color of the selected smiley's text color.  |
| `app:textNonSelectionColor`  | To set the color of the non-selected smiley's text color  |
| `app:isIndicator` | A boolean to switch modes between editable and non editable bar|




Or, you can change colors on runtime also
```java
smileyRating.setAngryColor(int color);
smileRating.setNormalColor(int color);
smileRating.setDrawingColor(int color);
smileRating.setPlaceHolderSmileColor(int color);
smileRating.setPlaceHolderBackgroundColor(int color);
smileRating.setTextSelectionColor(int color);
smileRating.setTextNonSelectionColor(int color);
```

All colors should have be provided as color int.

*Example*
```java
smileRating.setAngryColor(Color.RED);
smileRating.setAngryColor(Color.parseColor("#f29a68"));
smileRating.setNormalColor(ContextCompat.getColor(context, R.color.your_color));
```
#### Show/Hide line
You can customize wheather to show or hide the line behind smileys.
```java
mSmileRating.setShowLine(true/false);
```
or
```xml
app:showLine="true/false"
```
passing true will show the line and passig false will hide the line. You can get the current visibility of the line by calling
```java
boolean showing = mSmileRating.isShowingLine();
```
####Indicator
To set the mode of the RatingBar.
```java mSmileyRating.setIndicator(false);```
passing false will allow the user to set smiley rating. passing true will make the RatingBar just an inticator which is untouchable and will be used to just show some rating by default.
