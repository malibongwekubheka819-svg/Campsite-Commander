# Campsite-Commander
S10523431 Malibongwe Kubheka
Splash Screen code:

import android.content.Intent
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import com.example.caampsitecommander.MainActivity
import com.example.caampsitecommander.R
import java.util.Timer
import kotlin.concurrent.schedule

class Splash : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_splash)

        //  CODE THIS BLOCK TO HANDLE THE 3-SECOND TRANSITION:
        Timer().schedule(3000) {

            // This moves the app from SplashActivity to MainActivity
            val intent = Intent(this@Splash, MainActivity::class.java)
            startActivity(intent)

            // This closes the splash screen so the user can't go back to it
            finish()

        }
        //  END OF TRANSITION CODE
    
    }
}

// Explicit Context Reference (this@Splash): Inside the Timer().schedule lambda block, this refers to the Timer context, not the Activity. Using this@Splash is exactly the correct way to pass the Activity context to the Intent.

Calling finish(): Calling finish() right after startActivity(intent) is best practice for splash screens. It removes the splash activity from the back-stack, ensuring that if the user presses the back button from MainActivity, they exit the app instead of seeing the splash screen again.


Main Screen code: 
package com.example.campsiteapp // ⚠️ LEAVE YOUR OWN ACTUAL PACKAGE NAME HERE!

import android.os.Bundle
import android.widget.Button
import android.widget.TextView
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main) // Loads your dark nature layout

        // 1. Find the elements from your layout XML
        val textTotalCount = findViewById<TextView>(R.id.text_total_count)
        val btnAddGear = findViewById<Button>(R.id.btn_add_gear)

        // 2. Create the list with your 3 specific campsite items
        val gearList = listOf("tent", "marshmallows", "flashlight")

        // 3. THE LOOP: Counts the items in the list one by one
        var totalCount = 0
        for (item in gearList) {
            totalCount = totalCount + 1 // Adds 1 for every item it loops through
        }

        // 4. Push the final calculated number (3) into your TextView display
        textTotalCount.text = totalCount.toString()

        // 5. Setup the "+ Add Gear" button click listener
        btnAddGear.setOnClickListener {
            // This pops up a small notification message at the bottom of the screen
            Toast.makeText(this, "Add Gear Clicked!", Toast.LENGTH_SHORT).show()
        }
    }
}
// The program begins by loading the main layout of the application when the activity is created. It then connects the TextView and Button from the XML layout to the Kotlin code using findViewById().

A list called gearList is created containing three campsite items: a tent, marshmallows, and a flashlight. The program uses a for loop to go through each item in the list and increase the value of a counter variable by one. This allows the application to calculate the total number of items in the list.

Once the loop has finished, the final count is converted to a string and displayed in the TextView on the screen. Since there are three items in the list, the TextView displays the number 3.

The application also includes a button labelled “Add Gear”. When the user taps this button, a Toast message appears at the bottom of the screen displaying the text “Add Gear Clicked!”. This provides feedback to the user that the button has been pressed successfully.

Overall, the code demonstrates how to create a list, use a loop to count items, display results in a TextView, and respond to user interaction through a button click event.

Detailed Screen code:
package com.example.campsiteapp // ⚠️ MAKE SURE THIS MATCHES YOUR ACTUAL PACKAGE NAME

import android.content.Intent
import android.os.Bundle
import android.widget.Button
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity

class DetailActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_detail)

        // Find our layout items
        val btnDisplayList = findViewById<Button>(R.id.btn_display_list)
        val btnBackToBase = findViewById<Button>(R.id.btn_back_to_base)
        val textGearDisplayBox = findViewById<TextView>(R.id.text_gear_display_box)

        // 🔴 FOUR PARALLEL ARRAYS (Indices 0, 1, and 2 match perfectly)
        val arrayItems = arrayOf("Tent", "M-Mallows", "Flashlight")
        val arrayCategories = arrayOf("Shelter", "Food", "Tools")
        val arrayQuantities = arrayOf("1", "2 Bags", "1")
        val arrayNotes = arrayOf("Check pegs", "Keep dry", "Need AA batteries")

        // When "Display Full List" is clicked
        btnDisplayList.setOnClickListener {
            // Set up our table headers inside a string variable
            var tableResult = "ITEM        | CATEGORY   | QTY    | NOTES\n"
            tableResult += "--------------------------------------------------\n"

            // Loop through the arrays using the index (i)
            for (i in arrayItems.indices) {
                // .padEnd() ensures the text columns line up straight like a neat table
                val item = arrayItems[i].padEnd(12)
                val category = arrayCategories[i].padEnd(11)
                val quantity = arrayQuantities[i].padEnd(7)
                val note = arrayNotes[i]

                // Combine them into one row of text
                tableResult += "$item| $category| $quantity| $note\n"
            }

            // Push the final built text table into your TextView layout element
            textGearDisplayBox.text = tableResult
            textGearDisplayBox.setTextColor(0xFFFFFFFF.toInt()) // Turn text white once loaded
        }

        // When "Back to Base" is clicked, navigate back to Main Dashboard
        btnBackToBase.setOnClickListener {
            val intent = Intent(this, MainActivity::class.java)
            startActivity(intent)
            finish() // Close this screen
        }
    }
}
// The DetailActivity class represents the second screen of the campsite application. When the activity is created, the onCreate() method runs and loads the activity_detail.xml layout. The program then connects the buttons and TextView from the layout to the Kotlin code using findViewById().

Four parallel arrays are created to store information about the campsite gear. The first array stores the item names, the second stores the categories, the third stores the quantities, and the fourth stores notes about each item. These arrays are parallel because the information at the same index in each array belongs to the same campsite item. For example, index 0 in all arrays contains information about the tent.

When the Display Full List button is clicked, the program creates a string called tableResult and adds column headings for Item, Category, Quantity, and Notes. A separator line is also added to make the output easier to read.

The program then uses a for loop to move through each index of the arrays. During each loop iteration, it retrieves the item information from the matching positions in all four arrays. The padEnd() function is used to add spaces to the text so that all columns line up neatly in a table format. The information is then combined into a single row and added to the tableResult string.

After the loop finishes, the completed table is displayed in the TextView named textGearDisplayBox. The text colour is also changed to white so that the information is clearly visible against the background.

The screen also contains a Back to Base button. When this button is pressed, an Intent is used to open the MainActivity screen. The finish() method closes the current activity so that the user returns to the main dashboard instead of creating multiple copies of the detail screen.

Overall, this code demonstrates the use of parallel arrays, loops, string formatting, button click events, TextView updates, and navigation between activities in an Android application.

Increase memory for more relevant answers
Upgrade to expand the amount of detail ChatGPT can bring into responses from your saved files and past conversations.
Upgrade to Plus







