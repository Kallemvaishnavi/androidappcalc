# androidappcalc

package com.example.calculator;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private TextView result_tv_;  // Displays the current input
    private TextView solution_tv_;  // Displays the final result
    private String currentInput = "";
    private String operator = "";
    private double firstValue = 0;
    private boolean operatorClicked = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initialize both TextViews
        result_tv_ = findViewById(R.id.result_tv_);
        solution_tv_ = findViewById(R.id.solution_tv_);

        // Number buttons
        setUpNumberButton(R.id.button0, "0");
        setUpNumberButton(R.id.button1, "1");
        setUpNumberButton(R.id.button2, "2");
        setUpNumberButton(R.id.button3, "3");
        setUpNumberButton(R.id.button4, "4");
        setUpNumberButton(R.id.button5, "5");
        setUpNumberButton(R.id.button6, "6");
        setUpNumberButton(R.id.button7, "7");
        setUpNumberButton(R.id.button8, "8");
        setUpNumberButton(R.id.button9, "9");
        setUpNumberButton(R.id.button_openbracket, "(");
        setUpNumberButton(R.id.button_closedbracket, ")");



        // Operator buttons
        setUpOperatorButton(R.id.buttonAdd, "+");
        setUpOperatorButton(R.id.buttonSubtract, "-");
        setUpOperatorButton(R.id.buttonMultiply, "*");
        setUpOperatorButton(R.id.buttonDivide, "/");

        // AC button (All Clear)
        Button acButton = findViewById(R.id.button_allclear);
        acButton.setOnClickListener(v -> clear());

        // Equals button
        Button equalsButton = findViewById(R.id.buttonEquals);
        equalsButton.setOnClickListener(v -> calculate());
    }

    private void setUpNumberButton(int buttonId, String number) {
        Button button = findViewById(buttonId);
        button.setOnClickListener(v -> {
            if (operatorClicked) {
                currentInput = number;
                operatorClicked = false;
            } else {
                currentInput += number;
            }
            result_tv_.setText(currentInput); // Display current input
        });
    }

    private void setUpOperatorButton(int buttonId, String operatorSymbol) {
        Button button = findViewById(buttonId);
        button.setOnClickListener(v -> {
            if (!currentInput.isEmpty()) {
                if (operator.isEmpty()) {
                    firstValue = Double.parseDouble(currentInput);
                } else {
                    calculate();  // If there's an operator already, perform calculation first
                }
                operator = operatorSymbol;
                operatorClicked = true;
            }
        });
    }

    private void calculate() {
        if (!currentInput.isEmpty() && !operator.isEmpty()) {
            double secondValue = Double.parseDouble(currentInput);
            double result = 0;

            switch (operator) {
                case "+":
                    result = firstValue + secondValue;
                    break;
                case "-":
                    result = firstValue - secondValue;
                    break;
                case "*":
                    result = firstValue * secondValue;
                    break;
                case "/":
                    if (secondValue != 0) {
                        result = firstValue / secondValue;
                    } else {
                        solution_tv_.setText("Error");  // Show error in solution_tv_
                        return;
                    }
                    break;
            }

            // Display the result in solution_tv_
            solution_tv_.setText(String.valueOf(result));
            result_tv_.setText("");  // Clear the current input
            firstValue = result;  // Store the result for further operations
            currentInput = "";  // Reset current input
            operator = "";  // Reset operator
        }
    }

    private void clear() {
        currentInput = "";
        operator = "";
        firstValue = 0;
        operatorClicked = false;
        result_tv_.setText("");  // Clear current input
        solution_tv_.setText("");  // Clear result TextView
    }
}









**main.xml code here**

<?xml version="1.0" encoding="utf-8"?>


<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical"
    android:padding="16dp"
    android:gravity="center"
    android:background="#394C5F">
    <TextView
        android:id="@+id/solution_tv_"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="0"
        android:textSize="80dp"
        android:textAlignment="textEnd"
        android:layout_above="@+id/result_tv_"
        android:textColor="@color/black"
        android:layout_marginBottom="20dp"/>
    <TextView
        android:id="@+id/result_tv_"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="0"
        android:textSize="80dp"
        android:textAlignment="textEnd"
        android:layout_above="@+id/result_tv_"
        android:textColor="@color/black"
        android:layout_marginBottom="20dp"/>


    <GridLayout
        android:layout_width="411dp"
        android:layout_height="477dp"
        android:columnCount="4"
        android:orientation="horizontal"
        android:rowCount="6">

        <Button
            android:id="@+id/button_allclear"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:backgroundTint="#D70B0B"
            android:padding="10dp"
            android:text="ac"
            android:textSize="60px"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button_openbracket"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="("
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button_closedbracket"
            android:layout_width="80dp"
            android:layout_height="80dp"

            android:layout_margin="10dp"
            android:padding="10dp"
            android:text=" ) "
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button_dot"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:backgroundTint="#057EF0"
            android:padding="10dp"
            android:text="."
            android:textSize="18sp"
            app:cornerRadius="36dp" />


        <Button
            android:id="@+id/button1"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="1"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button2"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="2"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button3"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="3"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/buttonAdd"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:backgroundTint="#057EF0"
            android:padding="10dp"
            android:text="+"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button4"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="4"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button5"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="5"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button6"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="6"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/buttonSubtract"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:backgroundTint="#057EF0"
            android:padding="10dp"
            android:text="-"
            android:textSize="18sp"
            app:cornerRadius="45dp" />

        <Button
            android:id="@+id/button7"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="7"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button8"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="8"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button9"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="9"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/buttonMultiply"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:backgroundTint="#057EF0"
            android:padding="10dp"
            android:text="*"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/buttonClear"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:backgroundTint="#B18706"
            android:padding="10dp"
            android:text="C"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/button0"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:padding="10dp"
            android:text="0"
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/buttonEquals"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:backgroundTint="#F44336"
            android:padding="10dp"
            android:text="="
            android:textSize="18sp"
            app:cornerRadius="36dp" />

        <Button
            android:id="@+id/buttonDivide"
            android:layout_width="80dp"
            android:layout_height="80dp"
            android:layout_margin="10dp"
            android:backgroundTint="#057EF0"
            android:padding="10dp"
            android:text="/"
            android:textSize="18sp"
            app:cornerRadius="36dp" />
    </GridLayout>
</LinearLayout>

