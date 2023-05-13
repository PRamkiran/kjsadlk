3.AIM: Create a screen that has input boxes for User Name, Password, Address, Gender (radio buttons for male and female), Age (numeric), Date of Birth (Date Picket), State (Spinner) and a Submit button. On clicking the submit button, print all the data below the Submit Button. Use a. Linear Layout , b. Relative Layout and c. Grid Layout or Table Layout

XML CODE:


<?xml version="1.0" encoding="utf-8"?>
<LinearLayout  xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

        <EditText
            android:id="@+id/edt_username"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Username" />

        <EditText
            android:id="@+id/edt_password"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Password"
            android:inputType="textPassword" />

        <EditText
            android:id="@+id/edt_address"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Address" />

        <RadioGroup
            android:id="@+id/rdgroup"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">

                <RadioButton
                    android:id="@+id/rb_male"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="Male" />

                <RadioButton
                    android:id="@+id/rb_female"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:text="Female" />

        </RadioGroup>

        <EditText
            android:id="@+id/edt_age"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Age"
            android:inputType="number" />

        <EditText
            android:id="@+id/edt_dob"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Date of Birth"
            android:inputType="date" />

        <Spinner

            android:id="@+id/spinner_state"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            >

        </Spinner>

        <Button
            android:id="@+id/btn_submit"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:backgroundTint="#7AC5CF"
            android:text="Submit" />

        <TextView
            android:id="@+id/txt_result"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:textColor="#0520A5"
            android:textSize="20sp"
            android:textStyle="bold" />
</LinearLayout>


JAVA CODE:
package com.example.csbs03;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.EditText;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.Spinner;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    String []states = new String[]{"AndhraPradesh","Telangana","TamilNadu","Karnataka","Kerala"};
    Spinner spinner_state;
    EditText edtname,edtpassword,edtaddress,edtage,edtdob;
    RadioGroup rdgroup;
    RadioButton rbmale,rbfemale;
    TextView txtres;
    String name,state,address,age,dob,gender;
    Button btnsubmit;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        spinner_state = findViewById(R.id.spinner_state);
        edtname = findViewById(R.id.edt_username);
        edtpassword = findViewById(R.id.edt_password);
        edtaddress = findViewById(R.id.edt_address);
        edtage = findViewById(R.id.edt_age);
        edtdob = findViewById(R.id.edt_dob);
        rdgroup = findViewById(R.id.rdgroup);
        rbmale = findViewById(R.id.rb_male);
        rbfemale = findViewById(R.id.rb_female);
        txtres = findViewById(R.id.txt_result);
        btnsubmit = findViewById(R.id.btn_submit);

        ArrayAdapter<String> spinner_adapter = new ArrayAdapter<>(MainActivity.this, android.R.layout.simple_spinner_dropdown_item,states);
        spinner_state.setAdapter(spinner_adapter);

        rdgroup.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(RadioGroup group, int checkedId) {
                if(checkedId == rbmale.getId())
                {
                    gender = "Male";
                }
                else
                {
                    gender = "Female";
                }
            }
        });

        spinner_state.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                state = parent.getItemAtPosition(position).toString();
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) {
            }
        });

        btnsubmit.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                name = edtname.getText().toString();
                address = edtaddress.getText().toString();
                age = edtage.getText().toString();
                dob = edtdob.getText().toString();
                txtres.setText("UserName :"+name+"\n" +"Age :" +age +"\n" + "Date Of Birth :" +dob + "\n" +"Gender :"+gender +"\n" +"Address :"+ address +"\n"+"State:" +state);
            }
        });
    }
}
