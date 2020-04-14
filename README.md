# Masking-ImageView-Image
Masking Image of ImageView in Android Studio

## MainActivity.class
```
import androidx.appcompat.app.AppCompatActivity;

import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.graphics.Canvas;
import android.graphics.Paint;
import android.graphics.PorterDuff;
import android.graphics.PorterDuffXfermode;
import android.os.Bundle;
import android.widget.ImageView;

public class MainActivity extends AppCompatActivity {
    ImageView main_img;
    Bitmap result, mask_bitmap;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        main_img = (ImageView)findViewById(R.id.main_img);

        //Create a method for masking image

        Bitmap finalMasking = MaskingProcess();


    }

    private Bitmap MaskingProcess() {

        try {
            Bitmap orginal, mask_b;

            orginal = BitmapFactory.decodeResource(getResources(),R.drawable.main_img);
            mask_b = BitmapFactory.decodeResource(getResources(),R.drawable.frame_mask2);

            if(orginal != null){

                int iv_width = orginal.getWidth();
                int iv_height = orginal.getHeight();

                result = Bitmap.createBitmap(iv_width,iv_height,Bitmap.Config.ARGB_8888);
                mask_bitmap = Bitmap.createScaledBitmap(mask_b,iv_width,iv_height,true);

                Canvas canvas = new Canvas(result);

                Paint paint = new Paint(Paint.ANTI_ALIAS_FLAG);
                paint.setXfermode(new PorterDuffXfermode(PorterDuff.Mode.DST_IN));

                canvas.drawBitmap(orginal,0,0,null);
                canvas.drawBitmap(mask_bitmap,0,0,paint);

                paint.setXfermode(null);
                paint.setStyle(Paint.Style.STROKE);

            }
        }catch (OutOfMemoryError outOfMemoryError){
                outOfMemoryError.printStackTrace();
        }

        main_img.setImageBitmap(result);
        return result;
    }
}

```

## activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    tools:context=".MainActivity">

    <ImageView
        android:id="@+id/main_img"
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:background="@drawable/button_selector" />

</LinearLayout>
```
