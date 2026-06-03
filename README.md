## EX:NO:05:Develop a program to create a simple calculator using android studio.
## Aim:
To create and design an android application for a simple calculator using android studio.
## EQUIPMENTS REQUIRED:
Android Studio(Latest Version)
## ALGORITHM:
Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as smsintent and click Next.

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6:Display details give in MainActivity file.

Step 7: Save and run the application.
## PROGRAM:
```
/*
Program to create and design an android application simple calculator using Intent.
Developed by:SHIVAANI R
Registeration Number :212224220097
*/
```
## MainActivity.java:
```
package com.example.calculator;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    EditText editText;
    TextView resultText;
    Button addButton, subtractButton, multiplyButton, divideButton, equalButton, clearButton, dotButton;
    Button[] numButtons = new Button[10];

    double num1 = 0, num2 = 0;
    String operator = "";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Linking with layout IDs
        editText = findViewById(R.id.editText2);
        resultText = findViewById(R.id.resultText);
        clearButton = findViewById(R.id.clear_text);

        addButton = findViewById(R.id.add);
        subtractButton = findViewById(R.id.sub);
        multiplyButton = findViewById(R.id.mul);
        divideButton = findViewById(R.id.div);
        equalButton = findViewById(R.id.submit);
        dotButton = findViewById(R.id.dot);

        // Number button IDs (make sure these exist in your XML)
        numButtons[0] = findViewById(R.id.num0);
        numButtons[1] = findViewById(R.id.num1);
        numButtons[2] = findViewById(R.id.num2);
        numButtons[3] = findViewById(R.id.num3);
        numButtons[4] = findViewById(R.id.num4);
        numButtons[5] = findViewById(R.id.num5);
        numButtons[6] = findViewById(R.id.num6);
        numButtons[7] = findViewById(R.id.num7);
        numButtons[8] = findViewById(R.id.num8);
        numButtons[9] = findViewById(R.id.num9);

        // Number buttons logic
        for (int i = 0; i <= 9; i++) {
            int finalI = i;
            numButtons[i].setOnClickListener(v -> editText.append(String.valueOf(finalI)));
        }

        // Decimal point
        dotButton.setOnClickListener(v -> {
            String text = editText.getText().toString();
            if (!text.contains(".")) {
                editText.append(".");
            }
        });

        // Clear button
        clearButton.setOnClickListener(v -> {
            editText.setText("");
            resultText.setText("Result");
            num1 = num2 = 0;
            operator = "";
        });

        // Operation buttons
        addButton.setOnClickListener(v -> setOperator("+"));
        subtractButton.setOnClickListener(v -> setOperator("-"));
        multiplyButton.setOnClickListener(v -> setOperator("*"));
        divideButton.setOnClickListener(v -> setOperator("/"));

        // Equal button
        equalButton.setOnClickListener(v -> calculateResult());
    }

    private void setOperator(String op) {
        try {
            num1 = Double.parseDouble(editText.getText().toString());
            operator = op;
            editText.setText("");
        } catch (NumberFormatException e) {
            Toast.makeText(this, "Enter a valid number first", Toast.LENGTH_SHORT).show();
        }
    }

    private void calculateResult() {
        try {
            num2 = Double.parseDouble(editText.getText().toString());
            double result = 0;

            switch (operator) {
                case "+": result = num1 + num2; break;
                case "-": result = num1 - num2; break;
                case "*": result = num1 * num2; break;
                case "/":
                    if (num2 == 0) {
                        Toast.makeText(this, "Cannot divide by zero", Toast.LENGTH_SHORT).show();
                        return;
                    }
                    result = num1 / num2;
                    break;
                default:
                    Toast.makeText(this, "Select an operation", Toast.LENGTH_SHORT).show();
                    return;
            }

            resultText.setText("Result: " + result);
            editText.setText("");
            operator = "";

        } catch (NumberFormatException e) {
            Toast.makeText(this, "Enter a valid number", Toast.LENGTH_SHORT).show();
        }
    }
}
```
## activity_main.xml:
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/white"
    android:orientation="vertical"
    android:padding="16dp"
    tools:context=".MainActivity">

    <!-- Input Field -->
    <EditText
        android:id="@+id/editText2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter Value"
        android:gravity="center"
        android:inputType="numberDecimal"
        android:textSize="24sp"
        android:textColor="@color/black"
        android:backgroundTint="@color/black"
        android:padding="10dp"
        android:layout_marginBottom="10dp" />

    <!-- Result Display -->
    <TextView
        android:id="@+id/resultText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Result"
        android:textSize="22sp"
        android:textColor="@color/black"
        android:gravity="center"
        android:layout_marginBottom="16dp" />

    <!-- Buttons Grid -->
    <GridLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:columnCount="4"
        android:rowCount="5"
        android:alignmentMode="alignMargins"
        android:rowOrderPreserved="false"
        android:layout_gravity="center">

        <!-- Row 1 -->
        <Button
            android:id="@+id/num7"
            android:text="7"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/num8"
            android:text="8"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/num9"
            android:text="9"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/div"
            android:text="/"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <!-- Row 2 -->
        <Button
            android:id="@+id/num4"
            android:text="4"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/num5"
            android:text="5"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/num6"
            android:text="6"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/mul"
            android:text="×"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <!-- Row 3 -->
        <Button
            android:id="@+id/num1"
            android:text="1"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/num2"
            android:text="2"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/num3"
            android:text="3"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/sub"
            android:text="−"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <!-- Row 4 -->
        <Button
            android:id="@+id/num0"
            android:text="0"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/dot"
            android:text="."
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/submit"
            android:text="="
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <Button
            android:id="@+id/add"
            android:text="+"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_columnWeight="1"
            android:layout_margin="4dp"
            android:textSize="20sp"
            android:backgroundTint="@color/yellow"
            android:textColor="@color/black" />

        <!-- Row 5 (Clear button) -->
        <Button
            android:id="@+id/clear_text"
            android:text="C"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:backgroundTint="@color/purple_500"
            android:textColor="@color/white"
            android:textSize="22sp"
            android:layout_marginTop="8dp"
            android:padding="10dp"
            android:layout_columnSpan="4" />

    </GridLayout>

</LinearLayout>
```
## OUTPUT

<img width="1919" height="1019" alt="Screenshot 2025-10-29 093129" src="https://github.com/user-attachments/assets/4d97e350-e0f9-4301-94fa-7987435f6c4e" />
<img width="1919" height="1019" alt="Screenshot 2025-10-29 093646" src="https://github.com/user-attachments/assets/005d4e9e-5a9c-4c02-a7b7-7f0ea0e9d3dd" />


## RESULT
Thus a Simple Android Application create a simple calculator using Android Studio is developed and executed successfully.
