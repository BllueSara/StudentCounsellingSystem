# Student Counselling System
![_مخطط دون اسم_](https://github.com/user-attachments/assets/a1928920-f35e-43a6-a1f5-c3ea6f8be40b)


## Overview
This project is an Admission Counselling system developed using Java Swing. It assists in managing student admissions, collecting preferences, and providing guidance based on available seats and student choices.

## System Requirements
- **NetBeans**: Recommended version with Java 1.8.
- **SQLite Database**: The project includes `studentInfo.sqlite` for storing student information.
- **JAR Files**: Ensure that `rs2xml.jar` and `sqlitejdbc-v056.jar` are included in your project libraries for database connectivity.

## System Architecture
The system is designed using the following architecture:

1. **User Interface (UI)**:
   - Developed using Java Swing to create interactive forms for student registration and admission choices.
   - The UI includes screens for data entry, displaying available seats, and confirming choices.

2. **Database Layer (SQLite)**:
   - The project uses an SQLite database (`studentInfo.sqlite`) to store student information, including personal details and admission choices.

3. **Business Logic Layer**:
   - Handles the core logic, including validating student information, processing admission requests, and generating counseling reports based on available seats.

4. **File System Support**:
   - Some data is managed through file-based storage for certain operations like logging or temporary storage.

## Core Components and Modules

### 1. **Student Registration Module**:
   - Allows students to register their details and preferences for different courses.

### 2. **Admission Choices Processing**:
   - This module calculates student admissions based on available seats and the choices they submitted.

### 3. **Counseling Reports**:
   - After processing, the system generates reports to help guide students on their admission status and possible choices.

## Example Code

### 1. **Audit_details Class**  
   The `Audit_details` class extends `javax.swing.JFrame` and represents a GUI for displaying audit details.

   - **Key Components**:
     - Database Connection: Connects to the database to fetch audit records.
     - Table Display: Uses `JTable` to display the fetched records.
     - Search Functionality: Allows searching through audit records by employee ID.

   - **Code Snippet**:
   ```java
   public class Audit_details extends javax.swing.JFrame {
       Connection conn = null;
       ResultSet rs = null;
       PreparedStatement pst = null;

       public Audit_details() {
           initComponents();
           conn = db.java_db();
           Update_table3();
       }

       private void Update_table3() {
           try {
               String sql = "SELECT * FROM Audit";
               pst = conn.prepareStatement(sql);
               rs = pst.executeQuery();
               tbl_3.setModel(DbUtils.resultSetToTableModel(rs));
           } catch (Exception e) {
               JOptionPane.showMessageDialog(null, e);
           } finally {
               try { rs.close(); pst.close(); } catch (Exception e) {}
           }
       }
   }
   ```

### 2. **Choice Class**  
   The `Choice` class allows users to select their college and branch choices from drop-down menus.

   - **Key Components**:
     - ComboBoxes: Multiple `JComboBox` components for college and branch selections.
     - Action Events: Handles button clicks and combo selections for processing user input.

   - **Code Snippet**:
   ```java
   public class Choice extends javax.swing.JFrame {
       private javax.swing.JComboBox<String> jComboBox1;
       private javax.swing.JButton jButton1;

       public Choice() {
           initComponents();
       }

       private void initComponents() {
           jComboBox1 = new javax.swing.JComboBox<>(new String[] { "Select", "BENNETT", "AMITY" });
           jButton1 = new javax.swing.JButton("OK");
           jButton1.addActionListener(evt -> jButton1ActionPerformed(evt));
       }

       private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {
           String selectedCollege = jComboBox1.getSelectedItem().toString();
       }
   }
   ```

### 3. **ChoicesData Class**  
   The `ChoicesData` class is responsible for storing user choices into a file for future reference.

   - **Key Components**:
     - File Writing: Uses `FileWriter` to append user choices to a text file.
     - Data Handling: Constructs a string representation of choices for storage.

   - **Code Snippet**:
   ```java
   public class ChoicesData {
       public void Store(String txt) throws IOException {
           ChoicesWriter = new FileWriter("choices.txt", true);
           ChoicesWriter.write(txt + " Choice-1: " + cChoice1 + "...");
           ChoicesWriter.flush();
           ChoicesWriter.close();
       }
   }
   ```

### 4. **CounsellingResult Class**  
   The `CounsellingResult` class displays the result of choices made by the user.

   - **Key Components**:
     - File Reading: Reads previously stored data from a file and displays relevant information in text fields.
     - GUI Components: Utilizes `JTextField` to show results based on user input.

   - **Code Snippet**:
   ```java
   public class CounsellingResult extends javax.swing.JFrame {
       public CounsellingResult(String value) throws FileNotFoundException {
           initComponents();
           this.jTextField2.setText(value);
           File f = new File("output.txt");
           Scanner sc = new Scanner(f);
           while (sc.hasNextLine()) {
               String data = sc.nextLine();
           }
       }
   }
   ```

## Instructions to Run the Project

1. **Install Required Software**:
   - Install NetBeans (recommended: version with Java 1.8).

2. **Database Setup**:
   - Ensure that the `studentInfo.sqlite` database file is in the project directory.
   - Include the necessary JAR files (`rs2xml.jar`, `sqlitejdbc-v056.jar`) in your project libraries.

3. **Run the Application**:
   - Clone or download the project.
   - Open the project in NetBeans.
   - Build and run the project from NetBeans.

### Summary of Functionality

- The application is structured to handle user input through GUI elements, store and retrieve data using a database and text files, and present results based on user selections.

### Conclusion
This application showcases standard practices in Java Swing for creating interactive user interfaces, handling database operations, and managing file input/output.


