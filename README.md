
# Ex.No:1 To create a employee details fields and to display the employee details using Firebase Database in Android Studio.


## AIM:

To create and display the employee details using Firebase Database in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as HelloWorld and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display the employee details in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the DatabaseTable using the firebasedatabase”.
Developed by:Nalini P
Registeration Number :212223220063
*/
```

```
## ACtivityMain.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <!-- USER ID -->
    <EditText
        android:id="@+id/editTextID"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="User ID"
        android:inputType="number" />

    <!-- USER NAME -->
    <EditText
        android:id="@+id/editTextUserName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="User Name"
        android:inputType="textPersonName" />

    <!-- PASSWORD -->
    <EditText
        android:id="@+id/editTextPassword"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Password"
        android:inputType="textPassword" />

    <!-- INSERT BUTTON -->
    <Button
        android:id="@+id/btnInsert"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="INSERT"
        android:onClick="btnInsertPressed" />

    <!-- FETCH BUTTON -->
    <Button
        android:id="@+id/btnFetch"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="FETCH"
        android:onClick="btnFetchPressed" />

    <!-- UPDATE BUTTON -->
    <Button
        android:id="@+id/btnUpdate"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="UPDATE"
        android:onClick="btnUpdatePressed" />

    <!-- DELETE BUTTON -->
    <Button
        android:id="@+id/btnDelete"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="DELETE"
        android:onClick="btnDeletePressed" />

</LinearLayout>

```

## Activitymain.java

```
package com.example.pmdex1;

import androidx.appcompat.app.AppCompatActivity;

import android.annotation.SuppressLint;
import android.database.Cursor;
import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    EditText editUserID, editUserName, editUserPassword;
    DatabaseManager dbManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editUserID = findViewById(R.id.editTextID);
        editUserName = findViewById(R.id.editTextUserName);
        editUserPassword = findViewById(R.id.editTextPassword);

        dbManager = new DatabaseManager(this);

        try {
            dbManager.open();
        } catch (Exception e) {
            Log.e("DB_ERROR", "Error opening database", e);
        }
    }

    // INSERT
    public void btnInsertPressed(View v) {
        String name = editUserName.getText().toString();
        String password = editUserPassword.getText().toString();

        if (name.isEmpty() || password.isEmpty()) {
            Toast.makeText(this, "Enter all fields", Toast.LENGTH_SHORT).show();
            return;
        }

        dbManager.insert(name, password);
        Toast.makeText(this, "Inserted Successfully", Toast.LENGTH_SHORT).show();
    }

    // FETCH
    public void btnFetchPressed(View v) {
        try (Cursor cursor = dbManager.fetch()) {

            if (cursor != null && cursor.moveToFirst()) {

                do {
                    @SuppressLint("Range")
                    String id = cursor.getString(cursor.getColumnIndex(DatabaseHelper.USER_ID));

                    @SuppressLint("Range")
                    String username = cursor.getString(cursor.getColumnIndex(DatabaseHelper.USER_NAME));

                    @SuppressLint("Range")
                    String password = cursor.getString(cursor.getColumnIndex(DatabaseHelper.USER_PASSWORD));

                    Log.i("DB_DATA", "ID: " + id + " Name: " + username + " Password: " + password);

                } while (cursor.moveToNext());

            } else {
                Toast.makeText(this, "No Data Found", Toast.LENGTH_SHORT).show();
            }

        } catch (Exception e) {
            Log.e("DB_ERROR", "Fetch error", e);
        }
    }

    // UPDATE
    public void btnUpdatePressed(View v) {
        try {
            long id = Long.parseLong(editUserID.getText().toString());
            String name = editUserName.getText().toString();
            String password = editUserPassword.getText().toString();

            dbManager.update(id, name, password);
            Toast.makeText(this, "Updated Successfully", Toast.LENGTH_SHORT).show();

        } catch (Exception e) {
            Log.e("DB_ERROR", "Update error", e);
            Toast.makeText(this, "Invalid ID", Toast.LENGTH_SHORT).show();
        }
    }

    // DELETE
    public void btnDeletePressed(View v) {
        try {
            long id = Long.parseLong(editUserID.getText().toString());

            dbManager.delete(id);
            Toast.makeText(this, "Deleted Successfully", Toast.LENGTH_SHORT).show();

        } catch (Exception e) {
            Log.e("DB_ERROR", "Delete error", e);
            Toast.makeText(this, "Invalid ID", Toast.LENGTH_SHORT).show();
        }
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        if (dbManager != null) {
            dbManager.close();
        }
    }
}
```
## OUTPUT

<img width="1920" height="1200" alt="Screenshot (76)" src="https://github.com/user-attachments/assets/9e4ddb3f-c764-44d9-a259-2cdfda4c5258" />

<img width="1920" height="1200" alt="Screenshot (77)" src="https://github.com/user-attachments/assets/d852a4fc-f476-467c-bc4a-e3a713715931" />





## RESULT
Thus a Simple Android Application create a firebase database and to display the employee details using Firbase Real Time Database in Android Studio is developed and executed successfully.
