
# Contact Us Form

Welcome to the Contact Us Form web application! This project provides a user-friendly way for individuals to get in touch with your organization. Users can submit their inquiries and messages through a convenient online form. The submitted data is securely stored in a MySQL database, allowing you to easily manage and respond to inquiries.

This application simplifies the process of collecting and managing user messages, making it a valuable addition to your website or online platform. Whether you run a business, a non-profit organization, or any other entity that needs to engage with its audience, this Contact Us Form can help streamline communication and enhance user experience.


## Table Of Contents

- [Installation](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#installation)
 - [Usage](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#usage)
 - [Acknowledgements](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#acknowledgements)
 - [Technologies Used](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#technologies-used)
 - [Code Description](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#code-description)
 - [Screenshots](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#screenshots)
 - [Future Scope](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#future-scope)
 - [Contributing](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#contributing)
 - [License](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/README.md#license)

## Installation

To set up and run the Contact Us Form web application, follow these steps:

1.Clone the Repository:

Clone this repository to your local development environment using the following command:

```bash
  git clone https://github.com/abhisheksingh-17/Landing-Page-Section.git

```
2.Database Setup:

 - Create a MySQL database (if you haven't already) using a database management tool or the command line.

 - Import the database.sql file included in the repository into your database. This file contains the necessary table structure for storing form data.

 3.Configure Database Connection:

 - Open the form.php file located in the project directory.

 - Replace the following placeholders with your actual database credentials:
```bash
$host = 'localhost';
$db_username = 'your_db_username';
$db_password = 'your_db_password';
$db_name = 'your_db_name';

```

 4.Upload to Web Server:

Upload the entire project to your web server. You can use an FTP client or your hosting provider's file manager for this step.

 5.Access the Application:

Visit the web page where you've deployed the application using a web browser.
## Usage

 1.Access the Contact Form:

Visit the web page where you've deployed the application using a web browser. You will find a user-friendly contact form.

 2.Submit Your Inquiry:

 Fill out the contact form with your details:
 - Name: Enter your full name.
 - Email: Provide your email address.
 - Message: Compose your message or inquiry.

 3.Submit the Form:

Click the "Send" button to submit the form. Your message will be securely sent to the database for storage.

 4.Confirmation Page:

After successful submission, you will be directed to a "Thank You" page (thankyou.html). This page acknowledges that your message has been received and provides a confirmation message.

 5.Data Storage:

The information you submitted, including your name, email address, and message, is securely stored in a MySQL database for future reference.

 6.Managing Inquiries:

To manage and respond to inquiries, you can retrieve the stored data from the database. Consider implementing an administrative interface or script to view and respond to messages.

This application streamlines the communication process between users and your organization, ensuring that user inquiries are promptly recorded and acknowledged. Additionally, it facilitates the management of incoming messages by storing them in a database for your convenience.

Feel free to explore and customize the application to suit your specific needs and preferences.


## Acknowledgements

 I would like to express our gratitude to everyone who has contributed to the development and deployment of this Contact Us Form application. Your support and involvement have been invaluable in making this project a reality.

I extend our thanks to the following individuals and groups:

 - Contributors: To all the contributors who have dedicated their time and expertise to enhance and improve this application.

 - Open Source Community: To the open-source community at large for the wealth of knowledge, tools, and inspiration that have contributed to the development of this project.

 - Users: To the users of this Contact Us Form, whose feedback and engagement help us continually refine and enhance the user experience.

Your contributions and support are deeply appreciated and play a vital role in the success of this project. Thank you for being a part of our journey.

## Technologies Used

This Contact Us Form application is built using the following technologies and tools:

 - HTML: The structure and markup of the web pages are created using HTML.

 - CSS: CSS is used to style and format the web pages, ensuring an appealing and user-friendly design.


 - PHP: PHP is used for server-side scripting to handle form submission, interact with the database, and generate dynamic content.

 - MySQL: MySQL is the relational database management system used to store and manage form data securely.

These technologies work together to provide a robust and efficient solution for managing user inquiries and messages. They ensure a seamless user experience and efficient data storage and retrieval.
## Code Description

```php
<?php
// Check if the form has been submitted
if (isset($_POST['submit'])) {
    // Retrieve user inputs from the form
    $name = $_POST['name'];
    $email = $_POST['email'];
    $message = $_POST['message'];

    // Database connection details
    $host = 'localhost';
    $db_username = 'admin';
    $db_password = '@abhi$17';
    $db_name = 'contact_form';

    // Create a new database connection using mysqli
    $conn = new mysqli($host, $db_username, $db_password, $db_name);

```

 - The code begins by checking if the form has been submitted using isset($_POST['submit']). This condition ensures that the code inside this block runs only when the form is submitted.

 - User inputs, including the name, email, and message, are retrieved from the form using $_POST.

 - Database connection details, such as the host, db_username, db_password, and db_name, are defined to establish a connection to the MySQL database.

 - A new database connection is created using the mysqli extension ($conn = new mysqli($host, $db_username, $db_password, $db_name)). This establishes a connection to the specified database.

 ```php
  // Check if the database connection was successful
    if ($conn->connect_error) {
        die("Connection failed: " . $conn->connect_error);
    }
```
 - The script checks whether the database connection was successful using the connect_error property of the $conn object.

 - If the connection fails, it terminates the script and displays an error message using die().

 ```php
  // Prepare an SQL query to insert data into the database
    $sql = "INSERT INTO contact (name, email, message) VALUES (?, ?, ?)";
    
  // Prepare the SQL statement for execution
    $stmt = $conn->prepare($sql);

  // Bind the user inputs to the prepared statement parameters
    $stmt->bind_param("sss", $name, $email, $message);

  // Execute the prepared statement
    if ($stmt->execute()) {
      // Data insertion was successful

  // Close the statement and database connection
        $stmt->close();
        $conn->close();

  // Redirect to a thank you page after saving the data
        header("Location: thankyou.html");
        exit();
    } else {
  // An error occurred during data insertion
        echo "Error: " . $sql . "<br>" . $conn->error;
    }

  // Close the statement and database connection
    $stmt->close();
    $conn->close();
}
?>

 ```
 - An SQL query to insert data into the contact table is prepared using placeholders ($sql = "INSERT INTO contact (name, email, message) VALUES (?, ?, ?)").

 - The prepared statement is created using $conn->prepare($sql).

 - User inputs ($name, $email, and $message) are bound to the prepared statement parameters using $stmt->bind_param("sss", $name, $email, $message).

 - The prepared statement is executed using $stmt->execute(). If data insertion is successful, it performs the following steps:

 - Closes the prepared statement and the database connection.
 - Redirects the user to a "Thank You" page (thankyou.html) using header().
 - Exits the script to prevent further execution.

 - If an error occurs during data insertion, it displays an error message containing the SQL query and the database error using echo.

 - Finally, it closes the prepared statement and the database connection.

This code snippet handles the submission of the contact form, securely inserts the data into the database, and provides feedback to the user.
## Screenshots

 - Contact Us Page-
![](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/Results/1.png?raw=true)

![](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/Results/2.png?raw=true)

 - Thank You Page-
![](https://github.com/abhisheksingh-17/Contact-Us-Section/blob/main/Results/3.png?raw=true)

## Future Scope

The Contact Us Form project provides a solid foundation for managing user inquiries and messages. While the current version of the project is functional and serves its primary purpose, there are several opportunities for future enhancements and features:

 - User Authentication: Implement user authentication to allow registered users to log in, track their messages, and receive responses.

 - Admin Dashboard: Create an admin dashboard to manage and respond to user messages, providing better support and communication.

 - Email Notifications: Implement email notifications to notify users when their messages are received and when they receive responses.

 - Improved Validation: Enhance input validation and error handling to provide a more user-friendly experience and prevent invalid data submissions.

 - Message Categories: Allow users to categorize their messages, making it easier to route inquiries to the appropriate department.

 - File Uploads: Enable users to attach files or documents when submitting inquiries or feedback.

 - Analytics and Reporting: Add analytics and reporting features to track user interactions and gain insights into user behavior.

 - Localization: Implement multiple languages and localization options to accommodate a broader user base.

 - Integration with CRM: Integrate the system with Customer Relationship Management (CRM) tools to centralize customer interactions.

 - Security Enhancements: Continuously monitor and enhance security measures to protect user data and ensure data privacy compliance.

 - Responsive Design: Ensure the application is fully responsive, providing an optimal experience on various devices, including mobile phones and tablets.

 - Performance Optimization: Optimize code and database queries to improve application performance, especially as the user base grows.

 - Feedback Surveys: Implement feedback surveys or rating systems to gather user feedback on their experience with the contact form.

By considering these future enhancements, you can expand the functionality and usability of your Contact Us Form, making it a more valuable tool for both users and your organization.
## Contributing

I welcome contributions from the community to help improve and enhance the Contact Us Form project. Whether you're a developer, designer, or have valuable insights to share, your contributions can make a difference. Here's how you can get involved:

 - Fork the Repository: Start by forking the project repository on GitHub to create your copy.

 - Clone the Repository: Clone your forked repository to your local development environment using git clone.

 - Create a New Branch: Create a new branch for your contributions to keep your changes separate from the main codebase.

 - Make Changes: Make the necessary changes or improvements in your branch. Please follow coding standards, conventions, and best practices.

 - Test: Test your changes thoroughly to ensure they work as expected and do not introduce any new issues.

 - Commit Changes: Commit your changes with clear and descriptive commit messages.

 - Push to Your Fork: Push your changes to your GitHub fork.

 - Create a Pull Request: Create a Pull Request (PR) from your branch to the main project repository's main or master branch. Be sure to provide a detailed description of your changes.

 - Review and Collaboration: Collaborate with maintainers and other contributors by addressing feedback and making necessary updates to your PR.

 - Merge: Once your PR is approved, it will be merged into the main project.

 - Celebrate: Your contribution is now part of the project! Thank you for your help in making the Contact Us Form better.

Please note that contributions should adhere to the project's code of conduct and respect the guidelines set by the maintainers. Contributors are encouraged to actively participate in discussions, report issues, and help improve the project's documentation.

Together, we can make this Contact Us Form project more robust and valuable to users.

If you have any questions or need assistance, feel free to reach out to the project maintainers.
## License

The Contact Us Form project is open-source software released under the MIT License. This license grants anyone the right to use, modify, distribute, and sublicense the software, provided the following conditions are met:

The original copyright notice and this license notice shall be included in all copies or substantial portions of the software.

The software is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement.

In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

By contributing to or using this project, you agree to comply with the terms and conditions of the MIT License.

For a full copy of the MIT License, please refer to the LICENSE file in this repository.