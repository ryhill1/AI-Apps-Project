**Power Automate: Curating the Invoice Workflow**

To transform the AI Model into a fully automated process, I designed a Power Automate flow that handles the end-to-end process; from file upload to data extraction and notification. 

The automate is triggered by the user uploading an Invoice to a designated SharePoint folder via Microsoft Teams. This approach was chosen over creating a Power Apps upload form to reduce development time and simplify the user experience, another additional benefit from using Teams was the ability to extract user data. 

Once triggered, the flow:

1 - Calls the AI Builder Model

2 - Routes the data (based on carrier using conditional logic*)

3 - Appends the extracted data to Excel tables

3.1 - Generates a record the first and last dates† 

4 - Generates a summary of key invoice details

5 - Notifies user of process completion

**Design Considerations**
I prioritised low user input, fast execution and clear logic paths
The flow includes error handling and data validation steps to ensure robustness
A summary notification is sent to the Invoice Upload Communications channel to inform the user that the process is complete, allowing them to verify the outcome of the invoice without ever opening it. It also informs them that the BI Report has received the new data and is ready for comparison.

* Although I chose to use standard condition blocks, I later learned that a Switch control would have been more efficient. However, the current setup remains easy to understand and processing speeds which meet requirements.

† This was a particularly complex step, due to the way the AI Builder handles data I was not able to extract the dates in date format. I had to instead filter through blanks (some rows for certain carriers had no dates) and then convert the date to a string format. I then appended this to the newest date in the invoice and separated via "-". This is not a perfect solution as I was unable to use this as a direct filter in the report but again met the requirements. 
